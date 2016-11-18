# System Information

### First steps

Updated system, installed `wget` and `epel` repo:
```
sudo yum update -y
sudo yum install wget bind-utils
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo rpm -Uvh epel-release-latest-7*.rpm
sudo yum update -y
```

Installed `ansible` for easier execution of commands on multiple hosts:
```
sudo yum install -y ansible
```

### Instances

```
Region: eu-central-1
AMI ID: RHEL-7.1_HVM-20150803-x86_64-1-Hourly2-GP2 (ami-38d2d625)
OS: Red Hat Enterprise Linux 7.1
```

### Volume space

```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "df -h"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.6G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G  172K  7.2G   1% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.5G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.5G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.5G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.5G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   33M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

```

### `yum repolist enabled`
```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo yum repolist enabled"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!epel/x86_64                                      Extra Packages for Ente 10,829
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 24,432

ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                           repo name               status
!rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastr      4
!rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linu 13,390
!rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linu    209
repolist: 13,603

```

### Add users and groups

Add users `bavaria` and `saxony`:
```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo useradd bavaria -u 2700"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>


[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo useradd saxony -u 2800"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
```

Create the group `democratic` and the group `social`:
```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo groupadd -g 2000 democratic"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>


[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo groupadd -g 2100 social"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
```

Add `bavaria` to `social` and `saxony` to `democratic`:
```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo usermod -aG social bavaria"
ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>


[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "sudo usermod -aG democratic saxony"
ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>


ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>

```

### List `/etc/passwd` entries for users

```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "getent passwd bavaria"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
bavaria:x:2700:2700::/home/bavaria:/bin/bash

[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "getent passwd saxony"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash

ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
saxony:x:2800:2800::/home/saxony:/bin/bash
```

### List `/etc/group` entries for groups

```
[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "getent group democratic"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>
democratic:x:2000:saxony

ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>
democratic:x:2000:saxony

ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>
democratic:x:2000:saxony

ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
democratic:x:2000:saxony

ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
democratic:x:2000:saxony

[ec2-user@ip-172-30-1-5 ~]$ ansible all -i hosts -a "getent group social"
ip-172-30-1-5.eu-central-1.compute.internal | SUCCESS | rc=0 >>
social:x:2100:bavaria

ip-172-30-1-7.eu-central-1.compute.internal | SUCCESS | rc=0 >>
social:x:2100:bavaria

ip-172-30-1-9.eu-central-1.compute.internal | SUCCESS | rc=0 >>
social:x:2100:bavaria

ip-172-30-1-6.eu-central-1.compute.internal | SUCCESS | rc=0 >>
social:x:2100:bavaria

ip-172-30-1-8.eu-central-1.compute.internal | SUCCESS | rc=0 >>
social:x:2100:bavaria
```