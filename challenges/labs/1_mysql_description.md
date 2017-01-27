# Install MySQL community server

The first host listed is `bcb6` a.k.a. `ec2-52-59-205-75.eu-central-1.compute.amazonaws.com` (`52.59.205.75`), which I will use for the MySQL server. 
Downloaded and installed the repo RPM from `dev.mysql.com` on all nodes:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm"
```

**By default, the 5.7 repo is enabled. To install 5.5 we have to enable the 5.5 repo and disable the 5.7 repo**:

```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo yum-config-manager --disable mysql57-community"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo yum-config-manager --enable mysql55-community"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo yum update -y"
```

Install `mysql-server` and start the daemon on the selected node:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible mysql -i hosts -a "sudo yum install mysql-server -y"
[ec2-user@ip-10-0-1-4 ~]$ ansible mysql -i hosts -a "sudo service mysqld start"
```

Install the client on all nodes:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo yum install mysql -y"
[ec2-user@ip-10-0-1-4 ~]$ mysql --version
mysql  Ver 14.14 Distrib 5.5.54, for Linux (x86_64) using readline 5.1
```

The final repo config can be seen in the `1_mysql-community.repo.md`.

Installed Oracle JDK 8 on all hosts:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a 'wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F;oraclelicense=accept- securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.rpm"'
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo yum localinstall jdk-8u111-linux-x64.rpm -y"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "java -version"
bcb14 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

bcb12 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

bcb13 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

bcb6 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

bcb4 | SUCCESS | rc=0 >>
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)
```

Installed the latest MySQL Java connector:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "tar -zxvf mysql-connector-java-5.1.40.tar.gz"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -a "sudo bash -c \"echo 'export CLASSPATH=/usr/share/java/mysql-connector-java.jar:\$CLASSPATH' > /etc/profile.d/classpath.sh\""
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "ls /usr/share/java"
bcb12 | SUCCESS | rc=0 >>
mysql-connector-java.jar

bcb13 | SUCCESS | rc=0 >>
mysql-connector-java.jar

bcb6 | SUCCESS | rc=0 >>
mysql-connector-java.jar

bcb14 | SUCCESS | rc=0 >>
mysql-connector-java.jar

bcb4 | SUCCESS | rc=0 >>
mysql-connector-java.jar
```

Created root password on the MySQL node (`cloudera`):
```
[ec2-user@ip-10-0-1-6 ~]$ sudo /usr/bin/mysql_secure_installation
```

Created the databases:
```
[ec2-user@ip-10-0-1-6 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 5.5.54 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on scm.* TO 'cloudera-scm'@'%' IDENTIFIED BY 'cloudera-scm';
Query OK, 0 rows affected (0.00 sec)

mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hive DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hive.* TO 'hive'@'%' IDENTIFIED BY 'hive';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on hue.* to 'hue'@'%' IDENTIFIED BY 'hue';
crQuery OK, 0 rows affected (0.00 sec)

mysql> create database oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on oozie.* to 'oozie'@'%' IDENTIFIED BY 'oozie';
Query OK, 0 rows affected (0.00 sec)

mysql> create database sentry DEFAULT CHARACTER SET utf8;
grant allQuery OK, 1 row affected (0.00 sec)

mysql> grant all on sentry.* to 'sentry'@'%' IDENTIFIED BY 'sentry';
Query OK, 0 rows affected (0.00 sec)

```
