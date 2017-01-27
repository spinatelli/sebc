
# Information

Hostname of MySQL node: `bc7`, a.k.a. `ip-10-0-0-7`, or **publicly** `ec2-52-59-249-254.eu-central-1.compute.amazonaws.com` (`52.59.249.254`)

MySQL version on all nodes:
```
[ec2-user@ip-10-0-0-4 ~]$ ansible all -i hosts -a "mysql --version"
bc7 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

bc9 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

bc4 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

bc13 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1

bc11 | SUCCESS | rc=0 >>
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1
```

List of databases:
```
[ec2-user@ip-10-0-0-7 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 5.5.54 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
9 rows in set (0.00 sec)
```