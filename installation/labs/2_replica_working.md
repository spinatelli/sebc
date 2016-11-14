### MySQL Installation

Following steps were performed to install the MySQL database (taken from [http://www.cloudera.com/documentation/enterprise/latest/topics/cm_ig_mysql.html])

Installed JDK on all nodes:
```
[ec2-user@ip-172-0-0-4 ~]$ wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
"http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.rpm"
[ec2-user@ip-172-0-0-4 ~]$ sudo yum localinstall jdk-8u111-linux-x64.rpm
```

Installed the `mysql` package on all nodes (e.g. on `bc1`):
```
[ec2-user@ip-172-0-0-4 ~]$ sudo yum install mysql
```

Installed the `mysql-server` package on `bc1` and `bc4` (a.k.a `ip-172-0-0-4` and `ip-172-0-0-5`):

```
[ec2-user@ip-172-0-0-4 ~]$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
[ec2-user@ip-172-0-0-4 ~]$ sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
[ec2-user@ip-172-0-0-4 ~]$ sudo yum update
[ec2-user@ip-172-0-0-4 ~]$ sudo yum install mysql-server
[ec2-user@ip-172-0-0-4 ~]$ sudo systemctl start mysqld
```

Moved InnoDB logfiles to home directory (just as an example, can be backed up elsewhere):

```
[ec2-user@ip-172-0-0-4 ~]$ sudo mv /var/lib/mysql/ib_logfile* ~
```

Located the option file in `/etc/my.cnf` and used Cloudera's recommended settings, but with `max_connections` to 2*100+50=250 (as recommended):

```
[mysqld]
transaction-isolation = READ-COMMITTED
sql_mode=STRICT_ALL_TABLES
key_buffer    = 32M
key_buffer_size = 64M
max_allowed_packet = 32M
thread_stack    = 256K
thread_cache_size  = 64
query_cache_limit  = 16M
query_cache_size   = 64M
query_cache_type   = 1
max_connections = 700
table_open_cache = 256
sort_buffer_size = 8M
join_buffer_size = 8M
net_buffer_length = 8K
read_buffer_size = 2M
read_rnd_buffer_size = 16M
thread_concurrency = 8
binlog_format=row
 
log-bin=mysql-bin   #Added for MySQL Replication
server-id   = 1     #Note: this should be 2 on the slave node
 
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 1 #Changed from 2 to 1 for Replication
innodb_log_buffer_size          = 64M
innodb_buffer_pool_size         = 6G
innodb_thread_concurrency       = 16
innodb_flush_method             = O_DIRECT
innodb_log_file_size = 1024M
sync_binlog=1       #Added for MySQL Replication
 
[mysqldump]
quick
max_allowed_packet = 16M
 
[mysql]
no-auto-rehash
 
[mysqlhotcopy]
interactive-timeout
 
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
```
`server-id` has been set to 2 on the slave node (`bc4`).

Ensured MySQL server starts at boot:
```
[ec2-user@ip-172-0-0-4 ~]$ sudo chkconfig mysqld on
```

Started the MySQL server:

```
[ec2-user@ip-172-0-0-4 ~]$ sudo service mysqld start
```

Set up the MySQL root password to `cloudera`:

```
[ec2-user@ip-172-0-0-4 ~]$ sudo /usr/bin/mysql_secure_installation
<output here>
All done!
```

Installed the MySQL JDBC Driver on all nodes
```
[ec2-user@ip-172-0-0-4 ~]$ wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
[ec2-user@ip-172-0-0-4 ~]$ tar -zxvf mysql-connector-java-5.1.40.tar.gz
[ec2-user@ip-172-0-0-4 ~]$ sudo cp mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar
```

Ran following commands on MySQL to setup the replication.
On Master (`bc1`):
```
[ec2-user@ip-172-0-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> GRANT REPLICATION SLAVE ON *.* TO 'slave_user'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> SET GLOBAL binlog_format = 'ROW';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

mysql> flush tables with read lock;
Query OK, 0 rows affected (0.00 sec)

mysql> show master status;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000001 |      403 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
1 row in set (0.00 sec)

mysql> unlock tables;
Query OK, 0 rows affected (0.00 sec)

```

On Slave (`bc4`):

```
[ec2-user@ip-172-0-0-5 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CHANGE MASTER TO MASTER_HOST='ip-172-0-0-4',MASTER_USER='slave_user', MASTER_PASSWORD='password', MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=403;
Query OK, 0 rows affected, 2 warnings (0.02 sec)

mysql> start slave;
Query OK, 0 rows affected (0.00 sec)

mysql> exit;
Bye
```

On Master we create the databases:

```
[ec2-user@ip-172-0-0-4 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.6.34-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on scm.* TO 'cloudera-scm'@'%' IDENTIFIED BY 'cloudera-scm';
Query OK, 0 rows affected (0.00 sec)

mysql> create database amon DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.01 sec)

mysql> grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'amon';
Query OK, 0 rows affected (0.00 sec)

mysql> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';
Query OK, 0 rows affected (0.00 sec)

mysql> create database nav DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'nav';
Query OK, 0 rows affected (0.00 sec)

mysql> create database metastore DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on metastore.* TO 'hive'@'%' IDENTIFIED BY 'hive';
Query OK, 0 rows affected (0.00 sec)

mysql> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.01 sec)

mysql> grant all on hue.* to 'hue'@'%' IDENTIFIED BY 'hue';
Query OK, 0 rows affected (0.00 sec)

mysql> create database oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on oozie.* to 'oozie'@'%' IDENTIFIED BY 'oozie';
Query OK, 0 rows affected (0.00 sec)

mysql> create database sentry DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on sentry.* to 'sentry'@'%' IDENTIFIED BY 'sentry';
Query OK, 0 rows affected (0.00 sec)

mysql> create database navms DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'navms';
Query OK, 0 rows affected (0.00 sec)

```

On Slave we can see the replication:
```
[ec2-user@ip-172-0-0-5 ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 7
Server version: 5.6.34-log MySQL Community Server (GPL)

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
| amon               |
| hue                |
| metastore          |
| mysql              |
| nav                |
| oozie              |
| performance_schema |
| rman               |
| scm                |
+--------------------+
10 rows in set (0.00 sec)

```
