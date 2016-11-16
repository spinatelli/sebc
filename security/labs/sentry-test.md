# Sentry test
Installed and configured Sentry service through Cloudera Manager as explained here https://www.cloudera.com/documentation/enterprise/5-6-x/topics/sg_sentry_service_config.html?_ga=1.128676748.1811419797.1479311137#concept_z5b_42s_p4

Configured Sentry to recognize the `spinatelli` account as an administrator, by adding the primary group to the `sentry.service.admin.group` list in CM.

Verified user privileges:
```
[ec2-user@ip-172-0-0-4 ~]$ kinit spinatelli
Password for spinatelli@EU-CENTRAL-1.COMPUTE.INTERNAL:
[ec2-user@ip-172-0-0-4 ~]$ beeline
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
2016-11-16 11:38:04,854 WARN  [main] mapreduce.TableMapReduceUtil: The hbase-prefix-tree module jar containing PrefixTreeCodec is not present.  Continuing without it.
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
Beeline version 1.1.0-cdh5.9.0 by Apache Hive
beeline> !connect jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
scan complete in 2ms
Connecting to jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
Connected to: Apache Hive (version 1.1.0-cdh5.9.0)
Driver: Hive JDBC (version 1.1.0-cdh5.9.0)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116113838_1319ca58-20a1-407c-9470-68afd3999888): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116113838_1319ca58-20a1-407c-9470-68afd3999888); Time taken: 0.089 seconds
INFO  : Executing command(queryId=hive_20161116113838_1319ca58-20a1-407c-9470-68afd3999888): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116113838_1319ca58-20a1-407c-9470-68afd3999888); Time taken: 0.137 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (0.316 seconds)
```

Created a Sentry role with full authorization:
```
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> CREATE ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20161116114040_49b2d2fe-e0db-4337-876a-888479702341): CREATE ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116114040_49b2d2fe-e0db-4337-876a-888479702341); Time taken: 0.055 seconds
INFO  : Executing command(queryId=hive_20161116114040_49b2d2fe-e0db-4337-876a-888479702341): CREATE ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116114040_49b2d2fe-e0db-4337-876a-888479702341); Time taken: 0.463 seconds
INFO  : OK
No rows affected (0.529 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> GRANT ALL ON SERVER server1 TO ROLE sentry_admin;
INFO  : Compiling command(queryId=hive_20161116114040_b6c08dcf-29d2-4bcb-8e5b-48ce674147ac): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116114040_b6c08dcf-29d2-4bcb-8e5b-48ce674147ac); Time taken: 0.094 seconds
INFO  : Executing command(queryId=hive_20161116114040_b6c08dcf-29d2-4bcb-8e5b-48ce674147ac): GRANT ALL ON SERVER server1 TO ROLE sentry_admin
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116114040_b6c08dcf-29d2-4bcb-8e5b-48ce674147ac); Time taken: 0.112 seconds
INFO  : OK
No rows affected (0.219 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> GRANT ROLE sentry_admin TO GROUP spinatelli;
INFO  : Compiling command(queryId=hive_20161116114141_0cdba7df-5607-420d-83cf-840c2a6ff7d9): GRANT ROLE sentry_admin TO GROUP spinatelli
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116114141_0cdba7df-5607-420d-83cf-840c2a6ff7d9); Time taken: 0.059 seconds
INFO  : Executing command(queryId=hive_20161116114141_0cdba7df-5607-420d-83cf-840c2a6ff7d9): GRANT ROLE sentry_admin TO GROUP spinatelli
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116114141_0cdba7df-5607-420d-83cf-840c2a6ff7d9); Time taken: 0.072 seconds
INFO  : OK
No rows affected (0.142 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116114141_867f448e-ecb0-4afc-8f47-fa7ce836bdce): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116114141_867f448e-ecb0-4afc-8f47-fa7ce836bdce); Time taken: 0.049 seconds
INFO  : Executing command(queryId=hive_20161116114141_867f448e-ecb0-4afc-8f47-fa7ce836bdce): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116114141_867f448e-ecb0-4afc-8f47-fa7ce836bdce); Time taken: 0.116 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.225 seconds)
```

Created new users on all cluster nodes:
```
[ec2-user@ip-172-0-0-4 ~]$ ansible all -i hosts -a "sudo groupadd selector"
bc5 | SUCCESS | rc=0 >>


bc3 | SUCCESS | rc=0 >>


bc4 | SUCCESS | rc=0 >>


bc2 | SUCCESS | rc=0 >>


bc1 | SUCCESS | rc=0 >>


[ec2-user@ip-172-0-0-4 ~]$ ansible all -i hosts -a "sudo groupadd inserters"
bc4 | SUCCESS | rc=0 >>


bc1 | SUCCESS | rc=0 >>


bc3 | SUCCESS | rc=0 >>


bc2 | SUCCESS | rc=0 >>


bc5 | SUCCESS | rc=0 >>


[ec2-user@ip-172-0-0-4 ~]$ ansible all -i hosts -a "sudo useradd -u 1100 -g selector george"
bc4 | SUCCESS | rc=0 >>


bc1 | SUCCESS | rc=0 >>


bc2 | SUCCESS | rc=0 >>


bc3 | SUCCESS | rc=0 >>


bc5 | SUCCESS | rc=0 >>


[ec2-user@ip-172-0-0-4 ~]$ ansible all -i hosts -a "sudo useradd -u 1200 -g inserters ferdinand"
bc1 | SUCCESS | rc=0 >>


bc4 | SUCCESS | rc=0 >>


bc3 | SUCCESS | rc=0 >>


bc2 | SUCCESS | rc=0 >>


bc5 | SUCCESS | rc=0 >>

[ec2-user@ip-172-0-0-4 ~]$ kadmin -p cloudera-scm@EU-CENTRAL-1.COMPUTE.INTERNAL
Authenticating as principal cloudera-scm@EU-CENTRAL-1.COMPUTE.INTERNAL with password.
Password for cloudera-scm@EU-CENTRAL-1.COMPUTE.INTERNAL:
kadmin:  addprinc george
WARNING: no policy specified for george@EU-CENTRAL-1.COMPUTE.INTERNAL; defaulting to no policy
Enter password for principal "george@EU-CENTRAL-1.COMPUTE.INTERNAL":
Re-enter password for principal "george@EU-CENTRAL-1.COMPUTE.INTERNAL":
Principal "george@EU-CENTRAL-1.COMPUTE.INTERNAL" created.
kadmin:  addprinc ferdinand
WARNING: no policy specified for ferdinand@EU-CENTRAL-1.COMPUTE.INTERNAL; defaulting to no policy
Enter password for principal "ferdinand@EU-CENTRAL-1.COMPUTE.INTERNAL":
Re-enter password for principal "ferdinand@EU-CENTRAL-1.COMPUTE.INTERNAL":
Principal "ferdinand@EU-CENTRAL-1.COMPUTE.INTERNAL" created.
kadmin:  exit
```

Created test roles:
```
beeline> !connect jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
scan complete in 2ms
Connecting to jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
Connected to: Apache Hive (version 1.1.0-cdh5.9.0)
Driver: Hive JDBC (version 1.1.0-cdh5.9.0)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> CREATE ROLE reads;
INFO  : Compiling command(queryId=hive_20161116115050_9a76c39d-21ec-4bfb-bec4-f0b1a9d78541): CREATE ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115050_9a76c39d-21ec-4bfb-bec4-f0b1a9d78541); Time taken: 0.056 seconds
INFO  : Executing command(queryId=hive_20161116115050_9a76c39d-21ec-4bfb-bec4-f0b1a9d78541): CREATE ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115050_9a76c39d-21ec-4bfb-bec4-f0b1a9d78541); Time taken: 0.049 seconds
INFO  : OK
No rows affected (0.159 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> CREATE ROLE writes;
INFO  : Compiling command(queryId=hive_20161116115050_50fbac61-281b-499f-86c5-5680b88727e3): CREATE ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115050_50fbac61-281b-499f-86c5-5680b88727e3); Time taken: 0.066 seconds
INFO  : Executing command(queryId=hive_20161116115050_50fbac61-281b-499f-86c5-5680b88727e3): CREATE ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115050_50fbac61-281b-499f-86c5-5680b88727e3); Time taken: 0.025 seconds
INFO  : OK
No rows affected (0.102 seconds)
```

Granted read privilege for all tables to `reads`:
```
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> GRANT SELECT ON DATABASE default TO ROLE reads;
INFO  : Compiling command(queryId=hive_20161116115151_fc7b5983-5ea1-4544-8387-8a916a8432b0): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115151_fc7b5983-5ea1-4544-8387-8a916a8432b0); Time taken: 0.055 seconds
INFO  : Executing command(queryId=hive_20161116115151_fc7b5983-5ea1-4544-8387-8a916a8432b0): GRANT SELECT ON DATABASE default TO ROLE reads
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115151_fc7b5983-5ea1-4544-8387-8a916a8432b0); Time taken: 0.04 seconds
INFO  : OK
No rows affected (0.105 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> GRANT ROLE reads TO GROUP selector;
INFO  : Compiling command(queryId=hive_20161116115151_cc32964c-2e07-4cc5-8df3-7b841411ef01): GRANT ROLE reads TO GROUP selector
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115151_cc32964c-2e07-4cc5-8df3-7b841411ef01); Time taken: 0.05 seconds
INFO  : Executing command(queryId=hive_20161116115151_cc32964c-2e07-4cc5-8df3-7b841411ef01): GRANT ROLE reads TO GROUP selector
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115151_cc32964c-2e07-4cc5-8df3-7b841411ef01); Time taken: 0.034 seconds
INFO  : OK
No rows affected (0.094 seconds)
```

Granted read privilege for `default.sample07` only to `writes`:
```
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> REVOKE ALL ON DATABASE default FROM ROLE writes;
INFO  : Compiling command(queryId=hive_20161116115151_7798e19b-fb31-42ac-a61e-3f699c9404ef): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115151_7798e19b-fb31-42ac-a61e-3f699c9404ef); Time taken: 0.058 seconds
INFO  : Executing command(queryId=hive_20161116115151_7798e19b-fb31-42ac-a61e-3f699c9404ef): REVOKE ALL ON DATABASE default FROM ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115151_7798e19b-fb31-42ac-a61e-3f699c9404ef); Time taken: 0.079 seconds
INFO  : OK
No rows affected (0.145 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> GRANT SELECT ON default.sample_07 TO ROLE writes;
INFO  : Compiling command(queryId=hive_20161116115252_d332475c-225c-4a9e-9138-67595c896d36): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115252_d332475c-225c-4a9e-9138-67595c896d36); Time taken: 0.051 seconds
INFO  : Executing command(queryId=hive_20161116115252_d332475c-225c-4a9e-9138-67595c896d36): GRANT SELECT ON default.sample_07 TO ROLE writes
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115252_d332475c-225c-4a9e-9138-67595c896d36); Time taken: 0.034 seconds
INFO  : OK
No rows affected (0.096 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> GRANT ROLE writes TO GROUP inserters;
INFO  : Compiling command(queryId=hive_20161116115252_c0920ea1-ed52-4b97-b9b3-83af86c7ff6f): GRANT ROLE writes TO GROUP inserters
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115252_c0920ea1-ed52-4b97-b9b3-83af86c7ff6f); Time taken: 0.052 seconds
INFO  : Executing command(queryId=hive_20161116115252_c0920ea1-ed52-4b97-b9b3-83af86c7ff6f): GRANT ROLE writes TO GROUP inserters
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115252_c0920ea1-ed52-4b97-b9b3-83af86c7ff6f); Time taken: 0.023 seconds
INFO  : OK
No rows affected (0.087 seconds)
```

`kinit` as `george` then logged into beeline:

```
[ec2-user@ip-172-0-0-4 ~]$ kinit george
Password for george@EU-CENTRAL-1.COMPUTE.INTERNAL:
[ec2-user@ip-172-0-0-4 ~]$ beeline
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
2016-11-16 11:53:46,755 WARN  [main] mapreduce.TableMapReduceUtil: The hbase-prefix-tree module jar containing PrefixTreeCodec is not present.  Continuing without it.
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
Beeline version 1.1.0-cdh5.9.0 by Apache Hive
beeline> !connect jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
scan complete in 2ms
Connecting to jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
Connected to: Apache Hive (version 1.1.0-cdh5.9.0)
Driver: Hive JDBC (version 1.1.0-cdh5.9.0)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116115454_d93ff371-f234-4da9-8cbc-4a2727244e4b): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115454_d93ff371-f234-4da9-8cbc-4a2727244e4b); Time taken: 0.065 seconds
INFO  : Executing command(queryId=hive_20161116115454_d93ff371-f234-4da9-8cbc-4a2727244e4b): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115454_d93ff371-f234-4da9-8cbc-4a2727244e4b); Time taken: 0.12 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
4 rows selected (0.268 seconds)
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> [ec2-user@ip-172-0-0-4 ~]$ kinit ferdinand
Password for ferdinand@EU-CENTRAL-1.COMPUTE.INTERNAL:
[ec2-user@ip-172-0-0-4 ~]$ beeline
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
2016-11-16 11:54:23,315 WARN  [main] mapreduce.TableMapReduceUtil: The hbase-prefix-tree module jar containing PrefixTreeCodec is not present.  Continuing without it.
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=512M; support was removed in 8.0
Beeline version 1.1.0-cdh5.9.0 by Apache Hive
beeline> !connect jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
scan complete in 1ms
Connecting to jdbc:hive2://ip-172-0-0-14.eu-central-1.compute.internal:10000/default;principal=hive/ip-172-0-0-14.eu-central-1.compute.internal@EU-CENTRAL-1.COMPUTE.INTERNAL
Connected to: Apache Hive (version 1.1.0-cdh5.9.0)
Driver: Hive JDBC (version 1.1.0-cdh5.9.0)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://ip-172-0-0-14.eu-central-1.co> show tables;
INFO  : Compiling command(queryId=hive_20161116115454_ade9a912-36c8-4e9a-bc6d-a4b1f023a1cc): show tables
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20161116115454_ade9a912-36c8-4e9a-bc6d-a4b1f023a1cc); Time taken: 0.054 seconds
INFO  : Executing command(queryId=hive_20161116115454_ade9a912-36c8-4e9a-bc6d-a4b1f023a1cc): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20161116115454_ade9a912-36c8-4e9a-bc6d-a4b1f023a1cc); Time taken: 0.14 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| sample_07  |
+------------+--+
1 row selected (0.272 seconds)
```

We can see everything worked as expected. Yay!