# System Information

### First steps

Updated the system on every node, installed `wget` and `epel` repo:
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
The `bcb4` node (i.e. `ip-10-0-1-4`) I use as an edge node to run ansible commands from.
This is my hosts file for running ansible commands:

```
[cm]
bcb4

[mysql]
bcb6 

[others]
bcb12
bcb13
bcb14

```

### Instances

```
Region: eu-central-1b
AMI ID: RHEL-7.2_HVM-20161025-x86_64-1-Hourly2-GP2 - ami-7def1712
OS: Red Hat Enterprise Linux 7.2
```

### Volume space

```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "df -h"
bc7 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.8G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

bc9 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.8G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

bcb4 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.7G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G  172K  7.2G   1% /dev/shm
tmpfs           7.2G   25M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

bc13 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.8G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000

bc11 | SUCCESS | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda2      100G  1.9G   99G   2% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/1000
```

### `yum repolist enabled`
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo yum repolist enabled"
bc9 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

bc7 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

bc13 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

bc11 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

bcb4 | SUCCESS | rc=0 >>
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
repo id                                          repo name                status
epel/x86_64                                      Extra Packages for Enter 11,075
rhui-REGION-client-config-server-7/x86_64        Red Hat Update Infrastru      4
rhui-REGION-rhel-server-releases/7Server/x86_64  Red Hat Enterprise Linux 13,816
rhui-REGION-rhel-server-rh-common/7Server/x86_64 Red Hat Enterprise Linux    209
repolist: 25,104

```

### Add users and groups

Add users `donald` and `vladimir`:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo useradd donald -u 2700"
bc7 | SUCCESS | rc=0 >>


bc9 | SUCCESS | rc=0 >>


bcb4 | SUCCESS | rc=0 >>


bc13 | SUCCESS | rc=0 >>


bc11 | SUCCESS | rc=0 >>


[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo useradd vladimir -u 2800"
bc7 | SUCCESS | rc=0 >>


bc13 | SUCCESS | rc=0 >>


bc11 | SUCCESS | rc=0 >>


bcb4 | SUCCESS | rc=0 >>


bc9 | SUCCESS | rc=0 >>
```

Create the group `hackers` and the group `crackers`:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo groupadd -g 2000 hackers"
bc7 | SUCCESS | rc=0 >>


bcb4 | SUCCESS | rc=0 >>


bc9 | SUCCESS | rc=0 >>


bc13 | SUCCESS | rc=0 >>


bc11 | SUCCESS | rc=0 >>


[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo groupadd -g 2100 crackers"
bc7 | SUCCESS | rc=0 >>


bc13 | SUCCESS | rc=0 >>


bc9 | SUCCESS | rc=0 >>


bcb4 | SUCCESS | rc=0 >>


bc11 | SUCCESS | rc=0 >>
```

Add `vladimir` to `hackers` and `donald` to `crackers`:
```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo usermod -aG hackers vladimir"
bc7 | SUCCESS | rc=0 >>


bc13 | SUCCESS | rc=0 >>


bc9 | SUCCESS | rc=0 >>


bcb4 | SUCCESS | rc=0 >>


bc11 | SUCCESS | rc=0 >>


[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "sudo usermod -aG crackers donald"
bc7 | SUCCESS | rc=0 >>


bc9 | SUCCESS | rc=0 >>


bc13 | SUCCESS | rc=0 >>


bcb4 | SUCCESS | rc=0 >>


bc11 | SUCCESS | rc=0 >>

```

### List `/etc/passwd` entries for users

```
[ec2-user@ip-10-0-1-4 ~]$ [ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "getent passwd vladimir"
bc9 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

bc13 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

bc7 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

bcb4 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

bc11 | SUCCESS | rc=0 >>
vladimir:x:2800:2800::/home/vladimir:/bin/bash

[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "getent passwd donald"
bc7 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

bc9 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

bc13 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

bcb4 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash

bc11 | SUCCESS | rc=0 >>
donald:x:2700:2700::/home/donald:/bin/bash
```

### List `/etc/group` entries for groups

```
[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "getent group hackers"
bc7 | SUCCESS | rc=0 >>
hackers:x:2000:vladimir

bcb4 | SUCCESS | rc=0 >>
hackers:x:2000:vladimir

bc9 | SUCCESS | rc=0 >>
hackers:x:2000:vladimir

bc13 | SUCCESS | rc=0 >>
hackers:x:2000:vladimir

bc11 | SUCCESS | rc=0 >>
hackers:x:2000:vladimir

[ec2-user@ip-10-0-1-4 ~]$ ansible all -i hosts -a "getent group crackers"
bc9 | SUCCESS | rc=0 >>
crackers:x:2100:donald

bc7 | SUCCESS | rc=0 >>
crackers:x:2100:donald

bc13 | SUCCESS | rc=0 >>
crackers:x:2100:donald

bcb4 | SUCCESS | rc=0 >>
crackers:x:2100:donald

bc11 | SUCCESS | rc=0 >>
crackers:x:2100:donald
```