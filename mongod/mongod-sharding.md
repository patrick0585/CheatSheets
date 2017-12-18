MongoDB-Sharding:
-----------------

				|-----------------------|
				|	Client		|
				|-----------------------|
					   |
					   |
					   |
				|-----------------------|
				|	Konfigserver	|
				|    (localhost:27017)
				|-----------------------|
					   |
					   |
					   |
			-----------------------------------------
			|					|
			|					|
		|----------------|			|---------------|
		|    Shard01	 |			|     Shard02	|
		|localhost(27018)|			|localhost(27019|
		|----------------|			|---------------|


0.) (optional) Keyfile erstellen

	openssl rand -base64 741 > mongodb-keyfile
	chmod 600 mongodb-keyfile


1.) Konfigserver erstellen und einrichten

	mongod --fork --configsvr --replSet rs0 --dbpath /data/db/c0 --logpath /data/db/c0/c0.log --port 27017

	mongo --port 27017

	config = {_id: "rs0", members: [{_id:0 ,host: "localhost:27017"}] }

	rs.initiate(config)

	rs.status()


2.) MongoDB Shardingserver erstellen

	mongod --fork --shardsvr --dbpath /data/db/rs0 --logpath /data/db/rs0/rs0.log --port 27018

	mongod --fork --shardsvr --dbpath /data/db/rs1 --logpath /data/db/rs1/rs1.log --port 27019


3.) Mongos-Router erstellen und Sharding-Server hinterlegen

	mongos --fork --configdb rs0/localhost:27017 --logpath=/data/db/mongos.log --port 17017

	mongo --port 17017

	sh.addShard("localhost:27018")

	sh.addShard("localhost:27019")

	sh.enableSharding("testdb")	// Name der Datenbank

	sh.shardCollection("testdb.cities", {"id": 1})	// optional (Definition einer Regel zum Verteilen der Datensätze)
	
	sh.status()	// Informationen

4.) Testen/Hinzufügen von Test-Daten

	mongo --port 17017

	use testdb
	
	for (i=0; i<10000; i++) { db.cities.insert({id: i, name: "Hallo Test", value: Math.random() * 10}); }

	// Pruefen, ob die Datensätze auf den Shardingserver übertagen wurden
