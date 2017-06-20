## [mongod](https://de.wikipedia.org/wiki/MongoDB) Cheat Sheet

### Create Root User

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
### Set authorization inside mongod.conf
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
