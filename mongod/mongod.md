# [mongod](https://de.wikipedia.org/wiki/MongoDB) Cheat Sheet

- [user administration](#user-administration)
  * [create root user](#create-root-user)
  * [create user](#create-user)
  * [update user](#update-user)
  * [delete user](#delete-user)
- [user role administration](#user-role-administration)
  * [create user role](#create-user-role)
  * [update user role](#update-user-role)
  * [delete user role](#delete-user-role)
- [configuration options](#configuration-options)
  * [set authorization inside mongod.conf](#set-authorization-inside-mongodconf)


## user administration

### create root user

use admin database
```
use admin
```
create root user in admin database
```
db.createUser( { user: "<username>",
          pwd: "<password>",
          roles: [ "userAdminAnyDatabase",
                   "dbAdminAnyDatabase",
                   "readWriteAnyDatabase"

] } )

```

### create user

select database the user will be authorized for
```
use test
```
create a user with **readWrite** role for the database **test**

mongodb built-in-roles can be found [here](https://docs.mongodb.com/manual/reference/built-in-roles/#database-user-roles)
```
db.createUser({user: "testUser", pwd: "123456", roles: [{role: "readWrite", db: "test"}]})
```
check if user was successfully created
```
db.getUser("testUser")
{
	"_id" : "test.testUser",
	"user" : "testUser",
	"db" : "test",
	"roles" : [
		{
			"role" : "readWrite",
			"db" : "test"
		}
	]
}
```

### update user

select database the user is authorized for
```
use test
```
get user information
```
db.getUser("testUser")
{
	"_id" : "test.testUser",
	"user" : "testUser",
	"db" : "test",
	"roles" : [
		{
			"role" : "readWrite",
			"db" : "test"
		}
	]
}
```
update customData for user
```
db.updateUser("testUser", { "customData": {city: "Münster", zip: "48165"}})
```
get user information after update
```
db.getUser("testUser")
{
	"_id" : "test.testUser",
	"user" : "testUser",
	"db" : "test",
	"roles" : [
		{
			"role" : "readWrite",
			"db" : "test"
		}
	],
	"customData" : {
		"city" : "Münster",
		"zip" : "48165"
	}
}
```
update user role
```
db.updateUser("testUser", { "roles": [{ "role": "read", "db": "test"}] })
```
### delete user
```
db.dropUser("testUser")
```
check if user was successfully deleted
```
db.getUser("testUser")
null
```

## user role administration

### create user role

### update user role

### delete user role

## configuration options

### set authorization inside mongod.conf
add the following entry inside mongod.conf
```
security:
    authorization: "enabled"
```

Connect to mongod with authentication
```
mongo -u "root" -p "<password>" --authenticationDatabase "admin"
```

## Authors

* **Patrick Kowalik** - *Initial work* - [Mongod CheatSheet](https://github.com/patrick0585/CheatSheets)
