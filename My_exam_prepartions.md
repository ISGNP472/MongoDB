/*compound indexes */

db.users.find({dob: {$gte: new Date("1988"), $lte: new Date("1990")}})

mongosh mongodb+srv://hawaii-dba-labls-readonly-user:6Ah4DBF9mEOeU8Ej@instruqttest.3xfvk.mongodb.net \ 
--authenticationDatabase "admin" --quiet \
-- eval 'use dba-labs'
-- eval 'db.books_d1c987ce_3d30_11ef_8ba2_17f063118259.find({"title": "Unlocking Android"})'

--collection
--type
--out
--jsonFormat Modes: Relaxed mode,Cannonical mode
--query - helps to reduced the number of documents. 'single quoted instruciton'


mongoimport mongodb+srv://hawaii-dba-labs-user:nNVAWqNmiz22GV7J@instruqttest.3xfvk.mongodb.net \
--drop --authenticationDatabase "admin" \
--db dba-labs \
--collection books_a88d168e_3d51_11ef_aeea_b7ee57cbee4f \
--file=/sampledata/library.books.json


mongostat
mongotop -- output a list of all the active collections in the datbase with the time spent on reads. 

mongot <options> <connection-string> <polling interval string>.

mongotop options 
    --rowcount -- limits the
    --json 

mongofile Options
 --local
 --db
 --local --put and get options.
 --replace - put to replce GridFS objects with a local file. 
 --writeConcern - 
 --readPreference - Helpful when reading the concern. 
 --v verbosity --
 

db.admin

-- log messages 
 Running log of events that can be used to diagnose issues, tune performance, and monitor the deployments. 

 show log <name>
 Structured JSON format

 Key-value pairs

 Use the File Path to Access the Log File 

    db.serverCmdLineOpts().parsed.systemLog.path
 
Access Logs in mongosh 
    show logs
    show log <type>
    show log global

Which of the following are valid methods to access logs from MongoDB

Run "show log global"  in mongosh
    show log global displays the combined output of all recent log entries
    Open the log file at the log path that's specified in the configuration file 

You can access the system logs 


Unit#13:{"MongoDB Metrics & Monitoring"}
------------------------------------------

{"Query Targeting"}
{"Read Effieciency"}
{"Ideal Ratio is 1"}
{"Very high ration impacts performance"}


{"Query Targeting"}
    Read operations
    Storage : Monitor disk usages
    Writes are refused at capacity. 

Disk Queue Depth
Disk Storage Usages

CPU : Track CPU usages by dev. 
    System cCPU, process CPU, 
    System CPU , Process CPU, 
Memory Metrcis : Amount of system memory available for your workloads. 

Replication lag : this metrics expresss in seconds, expressed in seconds. 
Baseline value : varies depending on workload. 

Burst value : normal to have occascional values. 
Out of Range : query targeting 

{"Core Metrics to monitor"}
    Query Tagering 
    storage
    CPU utilization 
    Memory utilization
    Replication lag

"Which of the following is the ideal value for objects scanned when reviewing the Query Targeting metrics"
    - 1. The ideal ratio of scanned objects to documents returned is about 1:1. 
    
    {"MOre metrcis to monitor"}

    - Opcounters
    - Network 


{"How to return the same metrics with the Atlas CLI"}


atlas alerts settings create --event JOINED_GROUP \
--enabled \
--notificationType USER \
--notificationEmailEnabled \
--notificationIntervalMin 5 \
--notificationUsername nirmaloracleapps@gmail.com \
--output json --projectId 667f36528cc3085eba9978ac



-- Atlas Alerts 

- Configure the alerts
- Respond to the alerts
- Integrations
- Metrics
- Monitoring M10+ 
  view, open, acknowledged

atlas alerts list --output json
atlas alerts ackonwledge <alertID> --comment <comment>
atlas alerts unacknowledge <alertID>



Self managed Monitoring -
-------------------------
    Install Percona MongoDB Exporter on Ubuntu linux
     1. Download of Percona MongoDB exporter
     2. Extract downloaded tarball
     3. Mover exporter binary to /usr/local/bin directory
    Create a new user
     1. Connect to your local mongodb instance
     2. Switch to the admin db within your mongosh shell session. 
     3. Create a new db user with clusermonitor role. 
    Create a service for Percona MongoDB exporter
     1. Create a new service file for mongodb exporter
     2. add following contents to the new service file 
     3. save and exit
     4. restart the system daemon to reload the unit files
     5. start the mongo db exporter service
     6. Enable the exporter service 
     7. confirm the exporter service is running 
     8. Confirm that DB mertics are being collected and available via /metrics endpoint. 
    Configure Percona MongoDB exporter as a Prometheus Target


}

Commandline Metrics

  killOp
  serverStatus  -- 
  db.runCommand(
   {
     serverStatus: 1
   }
  )
  db.runCommand( { serverStatus: 1 } ).connections
  db.adminCommand({currentOp: true, "$all": true})
  db.adminCommand({killop: 1, op: <opid>, comment: <any>})

currentop
killOp
}


SELF BACKUP AND MANAGED BACKUP SERVER:

    Backup plans on a mangodb server 
    Filesystem snapshots on a mongodb server
    Filesystem snapshow volumes on a mongodb serverv



Start the mongod 
Backup and restore a deploy
    mongodump - it's not ideal for the big. It's used for the small deployment. 
    Mongodb cloud manager, Mongodb atlas, and mongodb Ops manager are used for the big backup and production enviornment management. 



mongodump -- to take a small collection and dbs backup. 
    --oplog - to copture the incoming operations. 
    --gzip - to have mongo dump to compress the dump
    --archive - 
    --read preference 
    --db - to take backup of specific database
    --collection -- to take the backup of the specific collections. 


mongodump --db "library" --collection "books" --gzip --archive=/app/library.books.archive "mongodb://dba-admin:dba-pass@localhost:27000,localhost:27001,localhost:27002/?authSource=admin&replicaSet=mongodb-replSet"


Restoring a mongodb deployment :
-------------------------------------
    Same target mongo version to deploy the mongodb version . 
    COnside the performance impact to deploy the target cluster. 
    --drop
    --gzip 
    --oplogReply
    --archive




    mongorestore --drop --gzip --archive=/sampledata/library.books.archive "mongodb://dba-admin:dba-pass@localhost:27000,localhost:27001,localhost:27002/?authSource=admin&replicaSet=mongodb-replSet"


Maitenance with MongoDB Deployments:
---------------------------------------


{"MongoDB Maitenance and Upgrade"}

    Downtime of any kind of be quite costly. 
    Upgrading drivers
    Changing the replica sets. 
    Use an alternate enviornment 
    Primary 
        Secondary {} -- elect as primary 
        Secondary {} 
    
MongoDB minimizes downtime by  leveraging replica sets to perform rolling manitenance. 
    Atlas simplifies the rolling maitenance 

MongoDB Client Driver Upgrades 
    -- NodeJS - before upgrading , check the compatibilty 

Read the compatibility tables in the MongoDB driver documentation. 
How upgrading can impact performance of your application. 
Stable API allows you to upgrade your MongoDB server at will , and ensure that behavior changes between MongoDB versions wont's break your application. 

Check the version of Node.js 
    - node -v 

Confirm the MongoDB Node.js driver version - 
    - grep mongodb package.json

Check Compatibility 
    Upgrade the Node verison 
    Running node -v confirms the node.js version is 16. 
    node -v 

    Upgrade the MongoDB Driver 
    - npm i mongodb

MongoDB Server Upgrade :
  - Upgrade a replica set from version 5.0 to 6.0 on Ubuntu Linux. 
  - Pr-upgrade check list. 
    - Upgrade major release. 
    - db.version() -- it should confirms the current version of the database. 
 - Check the feature compatibility 
   - db.adminCommand( { getParameter: 1, featureCompatibilityVersion: 1}).featureCompatibilityVersion

   Oplog window :

Upgrade process - 
    - Replacing old binaries to new binaries. 
    - Mongod services - import
    - for downgrade - open the support ticket to proper downgrade activity. 
    - value desire version. 


REPLICATION :

  "High Availability"
  MongoDB replica sets :
     - Each replica sets have one primary and two secondary nodes. 
     - The primary 
     - Failover - Intiated automatically when primary  node is unavailable. The primary receives all the writes operations. 
     - Automatic failver - How elections works in mongodb. 
     - Initiating a replica set. 
     - Performing replica set. 
     - Maximum 7 memebers have voting privileges. 
     - It's important to have an odd number 
     - Each replica set have priority number. Higher valu makes more eligible for to become a primary. 

READ AND WRITE CONCERNS WITH MONGODB DEPLOYMENTS
------------------------------------------------
Options for write concerns:
    - Majority - A majority of memebrs are required to acknowledge the write operation before it's complete. 
    - Number - We can provide a write concern that represents the number of memebers needed to acknowledge a write operation. 
    - db.cats.insertOne 

    Read concerns level : 
     Local :
     primary 
     primaryPreferred
     secondary
     secondaryPreferred
     nearest - nearest network ping, which improve the latency. 
     Preference=secondary

    Set read and write concerns globally into the database. 


    Deploy three-member replica set 
    Inititate an election 
    In MongoDB Atlas, replica sets are created



Create a replication set :[
    mongodb keyfile. 
    configurtion process. 
    Mongodb listener - mongod.conf. 
    sudo vim /etc/mongo.conf 
    network settings, security configuration. you do have to multiple file for the same access. 
]

{"Replication in MongoDB"}
 
- Deploying a Replica set in a MongoDB Deployment 

 Deploy a Three-Memeber Replica Set 
   This section demonstrates how to deploy a three- member replica set and is broken into the following steps :
     - Update the mongod configuration files
     - Create security files
     - Initiate an election
     - Create an Admin user

    C
