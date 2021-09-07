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
