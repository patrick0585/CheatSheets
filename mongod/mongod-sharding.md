# MongoDB-Sharding Tutorial

- [MongoDB-Sharding Tutorial](#mongodb-sharding-tutorial)
  * [Tutorial Steps](#mongodb-sharding-tutorial)
    + [1.) Create Keyfile (optional)](#1--create-keyfile--optional-)
    + [2.) Create and configure Configserver](#2--create-and-configure-configserver)
    + [3.) Create Shardingserver (mongod)](#3--create-shardingserver--mongod-)
    + [3.) Create mongos-Router and add Sharding-Server](#3--create-mongos-router-and-add-sharding-server)
    + [4.) Test Sharding with test-data](#4--test-sharding-with-test-data)
  * [Authors](#authors)

				|-----------------------|
				|	Client		|
				|-----------------------|
					   |
					   |
					   |
				|-----------------------|
				|	Konfigserver	|
				|    (localhost:27017)  |
				|-----------------------|
					   |
					   |
					   |
			-----------------------------------------
			|					|
			|					|
	       |-----------------|			|-----------------|
	       |    Shard01      |			|     Shard02	  |
	       |(localhost:27018)|			|(localhost:27019)|
	       |-----------------|			|-----------------|

## MongoDB-Sharding-Tutorial

### 1.) Create Keyfile (optional)
```
openssl rand -base64 741 > mongodb-keyfile
chmod 600 mongodb-keyfile
```

### 2.) Create and configure Configserver
```
mongod --fork --configsvr --replSet rs0 --dbpath /data/db/c0 --logpath /data/db/c0/c0.log --port 27017

mongo --port 27017

config = {_id: "rs0", members: [{_id:0 ,host: "localhost:27017"}] }

rs.initiate(config)

rs.status()
```

### 3.) Create Shardingserver (mongod)
```
mongod --fork --shardsvr --dbpath /data/db/rs0 --logpath /data/db/rs0/rs0.log --port 27018

mongod --fork --shardsvr --dbpath /data/db/rs1 --logpath /data/db/rs1/rs1.log --port 27019
```

### 3.) Create mongos-Router and add Sharding-Server
```
mongos --fork --configdb rs0/localhost:27017 --logpath=/data/db/mongos.log --port 17017

mongo --port 17017

sh.addShard("localhost:27018")

sh.addShard("localhost:27019")

sh.enableSharding("testdb")	// Name der Datenbank

sh.shardCollection("testdb.cities", {"id": 1})	// optional (Definition einer Regel zum Verteilen der Datensätze)
	
sh.status()	// Informationen
```

### 4.) Test Sharding with test-data
```
mongo --port 17017

use testdb
	
for (i=0; i<10000; i++) { db.cities.insert({id: i, name: "Hallo Test", value: Math.random() * 10}); }

// check if data was sent through Sharding-Server
```

## Authors

* **Patrick Kowalik** - *Initial work* - [Mongod CheatSheet](https://github.com/patrick0585/CheatSheets/mongod-sharding.md)
