# Install MySQL community server

I chose the host `ip-172-30-1-5` for the MySQL server.
Downloaded the repo RPM from `dev.mysql.com`:
```
[ec2-user@ip-172-30-1-5 ~]$ wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
--2016-11-18 03:09:26--  http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
Resolving dev.mysql.com (dev.mysql.com)... 137.254.60.11
Connecting to dev.mysql.com (dev.mysql.com)|137.254.60.11|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: http://repo.mysql.com//mysql57-community-release-el7-9.noarch.rpm [following]
--2016-11-18 03:09:26--  http://repo.mysql.com//mysql57-community-release-el7-9.noarch.rpm
Resolving repo.mysql.com (repo.mysql.com)... 104.108.47.193
Connecting to repo.mysql.com (repo.mysql.com)|104.108.47.193|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9224 (9.0K) [application/x-redhat-package-manager]
Saving to: ‘mysql57-community-release-el7-9.noarch.rpm.1’

100%[===========================================================================================>] 9,224       --.-K/s   in 0s

2016-11-18 03:09:26 (54.8 MB/s) - ‘mysql57-community-release-el7-9.noarch.rpm.1’ saved [9224/9224]

[ec2-user@ip-172-30-1-5 ~]$ sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm
warning: mysql57-community-release-el7-9.noarch.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
Preparing...                          ################################# [100%]
Updating / installing...
   1:mysql57-community-release-el7-9  ################################# [100%]
```

**By default, the 5.7 repo is enabled. To install 5.6 we have to enable the 5.6 repo and disable the 5.7 repo**:

```
[ec2-user@ip-172-30-1-5 ~]$ sudo yum-config-manager --disable mysql57-community
[ec2-user@ip-172-30-1-5 ~]$ sudo yum-config-manager --enable mysql56-community
[ec2-user@ip-172-30-1-5 ~]$ sudo yum update -y
```

The final repo config can be seen in the `1_mysql-community.repo.md`.

Installed the MySQL client packages on all nodes (to be sure, used same repo on all other nodes as well to have the same version everywhere):
```
[ec2-user@ip-172-30-1-5 ~]$ ansible not_mysql_server -i hosts -a "wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm"
[ec2-user@ip-172-30-1-5 ~]$ ansible not_mysql_server -i hosts -a "sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm"
[ec2-user@ip-172-30-1-5 ~]$ ansible not_mysql_server -i hosts -a "sudo yum-config-manager --disable mysql57-community"
[ec2-user@ip-172-30-1-5 ~]$ ansible not_mysql_server -i hosts -a "sudo yum-config-manager --enable mysql56-community"
[ec2-user@ip-172-30-1-5 ~]$ ansible not_mysql_server -i hosts -a "sudo yum update -y"
[ec2-user@ip-172-30-1-5 ~]$ ansible not_mysql_server -i hosts -a "sudo yum install -y mysql"
```

Installed Oracle JDK 8 on all hosts:
```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a 'wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F;oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.rpm"'
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo yum localinstall jdk-8u111-linux-x64.rpm -y"
```

Installed the latest MySQL Java connector:
```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz"
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "tar -zxvf mysql-connector-java-5.1.40.tar.gz"
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar"
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a 'sudo echo "export CLASSPATH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH" > profile.d/classpath.sh'
```

Created root password:
```
[ec2-user@ip-172-30-1-5 ~]$ sudo /usr/bin/mysql_secure_installation
```

Databse `test` was not created so no need to delete it.
Created the databases:
```
[ec2-user@ip-172-30-1-5 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 15
Server version: 5.6.34 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql>  grant all on scm.* TO 'cloudera-scm'@'%' IDENTIFIED BY 'cloudera-scm';
Query OK, 0 rows affected (0.00 sec)

mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hive DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.01 sec)

mysql> grant all on hive.* TO 'hive'@'%' IDENTIFIED BY 'hive';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hue.* to 'hue'@'%' IDENTIFIED BY 'hue';
Query OK, 0 rows affected (0.01 sec)

mysql> create database oozie DEFAULT CHARACTER SET utf8;
grant all on oozie.* to 'oozie'@'%' IDENTIFIED BY 'oozie';
Query OK, 1 row affected (0.00 sec)

mysql> grant all on oozie.* to 'oozie'@'%' IDENTIFIED BY 'oozie';
Query OK, 0 rows affected (0.00 sec)

mysql> create database sentry DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on sentry.* to 'sentry'@'%' IDENTIFIED BY 'sentry';
Query OK, 0 rows affected (0.00 sec)

```

# List of grants

```
[ec2-user@ip-172-30-1-5 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 17
Server version: 5.6.34 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show grants for 'cloudera-scm';
+-------------------------------------------------------------------------------------------------------------+
| Grants for cloudera-scm@%                                                                                   |
+-------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'cloudera-scm'@'%' IDENTIFIED BY PASSWORD '*97E42E92255EBA4D1B96085222961540CD97F908' |
| GRANT ALL PRIVILEGES ON `scm`.* TO 'cloudera-scm'@'%'                                                       |
+-------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for hive;
+-----------------------------------------------------------------------------------------------------+
| Grants for hive@%                                                                                   |
+-----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'hive'@'%' IDENTIFIED BY PASSWORD '*4DF1D66463C18D44E3B001A8FB1BBFBEA13E27FC' |
| GRANT ALL PRIVILEGES ON `hive`.* TO 'hive'@'%'                                                      |
+-----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for hue;
+----------------------------------------------------------------------------------------------------+
| Grants for hue@%                                                                                   |
+----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'hue'@'%' IDENTIFIED BY PASSWORD '*15221DE9A04689C4D312DEAC3B87DDF542AF439E' |
| GRANT ALL PRIVILEGES ON `hue`.* TO 'hue'@'%'                                                       |
+----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for oozie;
+------------------------------------------------------------------------------------------------------+
| Grants for oozie@%                                                                                   |
+------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'oozie'@'%' IDENTIFIED BY PASSWORD '*2B03FE0359FAD3B80620490CE614F8622E0828CD' |
| GRANT ALL PRIVILEGES ON `oozie`.* TO 'oozie'@'%'                                                     |
+------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for sentry;
+-------------------------------------------------------------------------------------------------------+
| Grants for sentry@%                                                                                   |
+-------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'sentry'@'%' IDENTIFIED BY PASSWORD '*78CD2A8CB7403E99F97588EDF05B3EEAC6494302' |
| GRANT ALL PRIVILEGES ON `sentry`.* TO 'sentry'@'%'                                                    |
+-------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for rman;
+-----------------------------------------------------------------------------------------------------+
| Grants for rman@%                                                                                   |
+-----------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'rman'@'%' IDENTIFIED BY PASSWORD '*819397F8B454D58DA4E9F42A88A4873756B8C96D' |
| GRANT ALL PRIVILEGES ON `rman`.* TO 'rman'@'%'                                                      |
+-----------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)
```