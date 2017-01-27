Using node `bcb4`, a.k.a. `ip-10-0-1-4` as Cloudera Manager node.

Install the yum repo on all nodes:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo"
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo mv cloudera-manager.repo /etc/yum.repos.d/"
```

Install CM packages on node selected for CM:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible cm -i hosts -a "sudo yum install -y cloudera-manager-daemons cloudera-manager-server"
```

Prepare database from CM node:
```
[ec2-user@ip-10-0-1-4 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh -h bc7 mysql scm cloudera-scm
Enter SCM password:
JAVA_HOME=/usr/java/jdk1.8.0_111
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.8.0_111/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```

Start the daemon:
```
[ec2-user@ip-10-0-1-4 ~]$ sudo service cloudera-scm-server start
Starting cloudera-scm-server (via systemctl):              [  OK  ]
```