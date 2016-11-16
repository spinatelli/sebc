# Upgrade Cloudera Manager

## Report latest available API version
```
$ curl -u spinatelli:cloudera http://54.93.36.100:7180/api/version
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100     3  100     3    0     0     48      0 --:--:-- --:--:-- --:--:--    48
v14
```


## Report CM Version
```
$ curl -u spinatelli:cloudera http://54.93.36.100:7180/api/v14/cm/version
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   170    0   170    0     0   1808      0 --:--:-- --:--:-- --:--:--  2151{
  "version" : "5.9.0",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20161006-1801",
  "gitHash" : "898a5e032c080e18833dfc58180761f6ef2ea351",
  "snapshot" : false
}

```

## List all CM users
```
$ curl -u spinatelli:cloudera http://54.93.36.100:7180/api/v14/users
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   215    0   215    0     0   2756      0 --:--:-- --:--:-- --:--:--  2756{
  "items" : [ {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  }, {
    "name" : "spinatelli",
    "roles" : [ "ROLE_ADMIN" ]
  } ]
}
```

## Report the DB server in use by CM
```
$ curl -u spinatelli:cloudera http://54.93.36.100:7180/api/v14/cm/scmDbInfo
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    55    0    55    0     0    696      0 --:--:-- --:--:-- --:--:--   873{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```