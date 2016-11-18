# Install CM

Installing CM on host `ip-172-30-1-6`.

Installed Cloudera repo on all hosts
```
[ec2-user@ip-172-30-1-6 ~]$ ansible all -i hosts -a "wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo"
[ec2-user@ip-172-30-1-6 ~]$ ansible all -i hosts -a "sudo mv cloudera-manager.repo /etc/yum.repos.d/"
[ec2-user@ip-172-30-1-6 ~]$ ansible all -i hosts -a "sudo yum update -y"
```

Installed CM on the host:
```
[ec2-user@ip-172-30-1-6 ~]$ sudo yum install -y cloudera-manager-daemons cloudera-manager-server
```

Installed Agents on all nodes:
```
[ec2-user@ip-172-30-1-6 ~]$ ansible all -i hosts -a "sudo yum install -y cloudera-manager-daemons cloudera-manager-agent"
```

Configured `server_host` for the Agents:
```
[ec2-user@ip-172-30-1-6 ~]$ ansible all -i hosts -a "sudo sed -i 's/server\_host=localhost/server_host=ip-172-30-1-6.eu-central-1.compute.internal/' /etc/cloudera-scm-agent/config.ini"
```

Prepare database for SCM
```
[ec2-user@ip-172-30-1-6 ~]$ sudo /usr/share/cmf/schema/scm_prepare_database.sh -h ip-172-30-1-5.eu-central-1.compute.internal mysql scm cloudera-scm
Enter SCM password:
JAVA_HOME=/usr/java/jdk1.8.0_111
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.8.0_111/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!

```

Start CM Server:
```
[ec2-user@ip-172-30-1-6 ~]$ sudo service cloudera-scm-server start
```

Start Agents
```
[ec2-user@ip-172-30-1-6 ~]$ ansible all -i hosts -a "sudo service cloudera-scm-agent start"
```

From the Web UI Installed CDH 5.7.4 by changing the Cloudera parcel repo.