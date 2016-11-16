# API requests

## Stop Hive
```
$ curl -u spinatelli:cloudera -X POST http://54.93.36.100:7180/api/v2/clusters/Spinatelli/services/hive/commands/stop
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   180    0   180    0     0   1276      0 --:--:-- --:--:-- --:--:--  1276{
  "id" : 979,
  "name" : "Stop",
  "startTime" : "2016-11-16T10:04:32.286Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```

## Start Hive
```
$ curl -u spinatelli:cloudera -X POST http://54.93.36.100:7180/api/v2/clusters/Spinatelli/services/hive/commands/start
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   181    0   181    0     0    578      0 --:--:-- --:--:-- --:--:--   609{
  "id" : 983,
  "name" : "Start",
  "startTime" : "2016-11-16T10:05:27.853Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```

## Check Hive status
```
$ curl -u spinatelli:cloudera http://bc1:7180/api/v2/clusters/Spinatelli/services/hive/
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   530    0   530    0     0   5638      0 --:--:-- --:--:-- --:--:--  5638{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-0-0-4.eu-central-1.compute.internal:7180/cmf/serviceRedirect/hive",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD"
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD"
  } ],
  "configStale" : false,
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive"
}
```