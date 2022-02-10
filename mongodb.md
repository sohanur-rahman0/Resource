## Creating Replica Set

Primary Node
Port: 2717
db path: /mongos/db1

```
mongod --port 2717 --dbpath C:/mongos/db1 --replSet myReplicaSet
```

Secondary Node
Port: 2727
db path: /mongos/db2

```
mongod --port 2727 --dbpath C:/mongos/db2 --replSet myReplicaSet
```

Secondary Node
Port: 2737
db path: /mongos/db3

```
mongod --port 2737 --dbpath C:/mongos/db3 --replSet myReplicaSet
```

```
rs.status() -> tells the status of replica set
rs.initiate() -> initiates a replica set on primary node
rs.add("localhost:2727") ->Adds a member to replica set
rs.remove("localhost:2727") ->removes a member from replica set
rs.slaveOk() -> allows us to read from secondary db
```

mongoDB URI would be:

```
mongodb://localhost:2717,localhost:2727,localhost:2737/?replicaSet=myReplicaSet
```


## Deploying a replicaSet from config file

Node1.conf would look like:
```
storage:
  dbPath: /var/mongodb/db/node1
net:
  bindIp: 192.168.103.100,localhost
  port: 27011
security:
  authorization: enabled
  keyFile: /var/mongodb/pki/m103-keyfile
systemLog:
  destination: file
  path: /var/mongodb/db/node1/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: m103-example
```

Node2.conf would look like:
```
storage:
  dbPath: /var/mongodb/db/node2
net:
  bindIp: 192.168.103.100,localhost
  port: 27012
security:
  authorization: enabled
  keyFile: /var/mongodb/pki/m103-keyfile
systemLog:
  destination: file
  path: /var/mongodb/db/node2/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: m103-example
```

Node3.conf would look like:
```
storage:
  dbPath: /var/mongodb/db/node3
net:
  bindIp: 192.168.103.100,localhost
  port: 27013
security:
  authorization: enabled
  keyFile: /var/mongodb/pki/m103-keyfile
systemLog:
  destination: file
  path: /var/mongodb/db/node3/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: m103-example
```

Creating the keyfile and setting permissions on it:

```
sudo mkdir -p /var/mongodb/pki/
sudo chown vagrant:vagrant /var/mongodb/pki/
openssl rand -base64 741 > /var/mongodb/pki/m103-keyfile
chmod 400 /var/mongodb/pki/m103-keyfile
```
Creating the dbpath for all the nodes:
```
mkdir -p /var/mongodb/db/node1
mkdir /var/mongodb/db/{node2,node3}
```
Starting three nodes with their config files:
```
mongod -f node1.conf
mongod -f node2.conf
mongod -f node3.conf
```
Connect to node1:
```
mongo --port 27011
```
Initiating the replica set:
```
rs.initiate()
```
Creaing a user:
```
use admin
db.createUser({
  user: "m103-admin",
  pwd: "m103-pass",
  roles: [
    {role: "root", db: "admin"}
  ]
})
```
Exiting out of the Mongo shell and connecting to the entire replica set:
```
exit
mongo --host "m103-example/192.168.103.100:27011" -u "m103-admin"
-p "m103-pass" --authenticationDatabase "admin"
```
Getting ReplicaSet status:
```
rs.status()
```
Adding other members to replica set:
```
rs.add("m103:27012")
rs.add("m103:27013")
```
Getting an overview of the replica set topology:
```
res.isMaster()
```
Stepping down as master
```
rs.stepDown()
```
