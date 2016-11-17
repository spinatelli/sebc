# Importing Linux users
```
[root@ip-172-0-0-4 hue]# cd /opt/cloudera/parcels/CDH/lib/hue
[root@ip-172-0-0-4 hue]# export HUE_CONF_DIR="/var/run/cloudera-scm-agent/process/`ls -alrt /var/run/cloudera-scm-agent/process | grep HUE | tail -1 | awk '{print $9}'`"
[root@ip-172-0-0-4 hue]# export HUE_DATABASE_PASSWORD=hue
[root@ip-172-0-0-4 hue]# export HUE_SECRET_KEY=admin
[root@ip-172-0-0-4 hue]# build/env/bin/hue useradmin_sync_with_unix
```