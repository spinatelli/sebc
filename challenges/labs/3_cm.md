# CM API call

```
{
  "items" : [ {
    "hostId" : "i-04d0cebbe06cdfdd9",
    "ipAddress" : "10.0.1.6",
    "hostname" : "ip-10-0-1-6.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-1-4.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-04d0cebbe06cdfdd9",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16389054464
  }, {
    "hostId" : "i-0786c067f81d49d8a",
    "ipAddress" : "10.0.1.4",
    "hostname" : "ip-10-0-1-4.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-1-4.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-0786c067f81d49d8a",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16389316608
  }, {
    "hostId" : "i-07d8db7b772ac209f",
    "ipAddress" : "10.0.1.5",
    "hostname" : "ip-10-0-1-5.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-1-4.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-07d8db7b772ac209f",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16389316608
  }, {
    "hostId" : "i-0c29a952f52986bb5",
    "ipAddress" : "10.0.1.6",
    "hostname" : "ip-10-0-1-6.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-1-4.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-0c29a952f52986bb5",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16389316608
  }, {
    "hostId" : "i-074d50441bf8127f8",
    "ipAddress" : "10.0.1.9",
    "hostname" : "ip-10-0-1-9.eu-central-1.compute.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ip-10-0-1-4.eu-central-1.compute.internal:7180/cmf/hostRedirect/i-074d50441bf8127f8",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "numPhysicalCores" : 2,
    "totalPhysMemBytes" : 16389316608
  } ]
}
```

# List HDFS directories
```
[ec2-user@ip-10-0-1-4 ~]$ hdfs dfs -ls /user
Found 8 items
drwxr-xr-x   - admin    admin               0 2017-01-27 11:36 /user/admin
drwxr-xr-x   - donald   donald              0 2017-01-27 11:36 /user/donald
drwxr-xr-x   - hdfs     supergroup          0 2017-01-27 11:36 /user/hdfs
drwxrwxrwx   - mapred   hadoop              0 2017-01-27 11:32 /user/history
drwxrwxr-t   - hive     hive                0 2017-01-27 11:32 /user/hive
drwxrwxr-x   - hue      hue                 0 2017-01-27 11:33 /user/hue
drwxrwxr-x   - oozie    oozie               0 2017-01-27 11:33 /user/oozie
drwxr-xr-x   - vladimir vladimir            0 2017-01-27 11:36 /user/vladimir
```