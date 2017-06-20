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

### update user

### delete user

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
