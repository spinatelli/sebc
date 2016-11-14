# System Configuration Checks

1. Check `vm.swappiness` on all your nodes
    * Set the value to `1` if necessary

    ```
    [ec2-user@ip-172-0-0-4 ~]$ sysctl vm.swappiness
    vm.swappiness = 30
    [ec2-user@ip-172-0-0-4 ~]$ sudo sysctl vm.swappiness=1
    vm.swappiness = 1
    ```

2. Show the mount attributes of all volumes

    ```
    [ec2-user@ip-172-0-0-4 ~]$ mount | column -t
    sysfs       on  /sys                             type  sysfs       (rw,nosuid,nodev,noexec,relatime,seclabel)
    proc        on  /proc                            type  proc        (rw,nosuid,nodev,noexec,relatime)
    devtmpfs    on  /dev                             type  devtmpfs    (rw,nosuid,seclabel,size=7598116k,nr_inodes=1899529,mode=755)
    securityfs  on  /sys/kernel/security             type  securityfs  (rw,nosuid,nodev,noexec,relatime)
    tmpfs       on  /dev/shm                         type  tmpfs       (rw,nosuid,nodev,seclabel)
    devpts      on  /dev/pts                         type  devpts      (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
    tmpfs       on  /run                             type  tmpfs       (rw,nosuid,nodev,seclabel,mode=755)
    tmpfs       on  /sys/fs/cgroup                   type  tmpfs       (ro,nosuid,nodev,noexec,seclabel,mode=755)
    cgroup      on  /sys/fs/cgroup/systemd           type  cgroup      (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
    pstore      on  /sys/fs/pstore                   type  pstore      (rw,nosuid,nodev,noexec,relatime)
    cgroup      on  /sys/fs/cgroup/hugetlb           type  cgroup      (rw,nosuid,nodev,noexec,relatime,hugetlb)
    cgroup      on  /sys/fs/cgroup/net_cls,net_prio  type  cgroup      (rw,nosuid,nodev,noexec,relatime,net_prio,net_cls)
    cgroup      on  /sys/fs/cgroup/freezer           type  cgroup      (rw,nosuid,nodev,noexec,relatime,freezer)
    cgroup      on  /sys/fs/cgroup/cpu,cpuacct       type  cgroup      (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
    cgroup      on  /sys/fs/cgroup/cpuset            type  cgroup      (rw,nosuid,nodev,noexec,relatime,cpuset)
    cgroup      on  /sys/fs/cgroup/pids              type  cgroup      (rw,nosuid,nodev,noexec,relatime,pids)
    cgroup      on  /sys/fs/cgroup/memory            type  cgroup      (rw,nosuid,nodev,noexec,relatime,memory)
    cgroup      on  /sys/fs/cgroup/devices           type  cgroup      (rw,nosuid,nodev,noexec,relatime,devices)
    cgroup      on  /sys/fs/cgroup/perf_event        type  cgroup      (rw,nosuid,nodev,noexec,relatime,perf_event)
    cgroup      on  /sys/fs/cgroup/blkio             type  cgroup      (rw,nosuid,nodev,noexec,relatime,blkio)
    configfs    on  /sys/kernel/config               type  configfs    (rw,relatime)
    /dev/xvda2  on  /                                type  xfs         (rw,relatime,seclabel,attr2,inode64,noquota)
    selinuxfs   on  /sys/fs/selinux                  type  selinuxfs   (rw,relatime)
    systemd-1   on  /proc/sys/fs/binfmt_misc         type  autofs      (rw,relatime,fd=29,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
    hugetlbfs   on  /dev/hugepages                   type  hugetlbfs   (rw,relatime,seclabel)
    debugfs     on  /sys/kernel/debug                type  debugfs     (rw,relatime)
    mqueue      on  /dev/mqueue                      type  mqueue      (rw,relatime,seclabel)
    tmpfs       on  /run/user/1000                   type  tmpfs       (rw,nosuid,nodev,relatime,seclabel,size=1497260k,mode=700,uid=1000,gid=1000)

    ```

3. Show the reserve space of any non-root, ext-based volumes

    ```
    [ec2-user@ip-172-0-0-4 ~]$ df -H
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/xvda2       11G  1.4G  9.5G  13% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.7G     0  7.7G   0% /dev/shm
    tmpfs           7.7G   18M  7.7G   1% /run
    tmpfs           7.7G     0  7.7G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/1000
    [ec2-user@ip-172-0-0-4 ~]$ sudo fdisk -l /dev/xvda2

    Disk /dev/xvda2: 10.7 GB, 10735304192 bytes, 20967391 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes

    ```

4. Show that transparent hugepages is disabled

    ```
    [ec2-user@ip-172-0-0-4 ~]$ cat /sys/kernel/mm/transparent_hugepage/enabled
    [always] madvise never
    [ec2-user@ip-172-0-0-4 ~]$ cat /sys/kernel/mm/transparent_hugepage/defrag
    [always] madvise never
    ```

5. Report the network interface attributes

    ```
    [ec2-user@ip-172-0-0-4 ~]$ ifconfig
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
            inet 172.0.0.4  netmask 255.255.255.240  broadcast 172.0.0.15
            inet6 fe80::7b:faff:fee2:a145  prefixlen 64  scopeid 0x20<link>
            ether 02:7b:fa:e2:a1:45  txqueuelen 1000  (Ethernet)
            RX packets 59238  bytes 71092600 (67.7 MiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 20320  bytes 2841187 (2.7 MiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1  (Local Loopback)
            RX packets 284  bytes 194232 (189.6 KiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 284  bytes 194232 (189.6 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    ```

6. Show forward and reverse host lookups using `getent` and `nslookup`

    ```
    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.4
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    4.0.0.172.in-addr.arpa  name = ip-172-0-0-4.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.5
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    5.0.0.172.in-addr.arpa  name = ip-172-0-0-5.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.6
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    6.0.0.172.in-addr.arpa  name = ip-172-0-0-6.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.7
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    7.0.0.172.in-addr.arpa  name = ip-172-0-0-7.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.8
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    8.0.0.172.in-addr.arpa  name = ip-172-0-0-8.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ getent hosts 172.0.0.4
    172.0.0.4       bc1 ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts ip-172-0-0-4
    172.0.0.4       ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts bc1
    172.0.0.4       bc1 ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts ip-172-0-0-4.eu-central-1.compute.internal
    fe80::7b:faff:fee2:a145 ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts 172.0.0.5
    172.0.0.5       bc2 ip-172-0-0-5.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts 172.0.0.6
    172.0.0.6       bc3 ip-172-0-0-6.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts 172.0.0.7
    172.0.0.7       bc4 ip-172-0-0-7.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts 172.0.0.8
    172.0.0.8       bc5 ip-172-0-0-8.eu-central-1.compute.internal

    ```

7. Verify the <code>nscd</code> service is running
    `nscd` was not installed on the nodes. Installed package `nscd` on all nodes and started service.
    ```
    [ec2-user@ip-172-0-0-4 ~]$ sudo yum install nscd
    <yum output here>
    [ec2-user@ip-172-0-0-4 ~]$ sudo service nscd start
    Redirecting to /bin/systemctl start  nscd.service
    [ec2-user@ip-172-0-0-4 ~]$ sudo service nscd status
    Redirecting to /bin/systemctl status  nscd.service
    ● nscd.service - Name Service Cache Daemon
       Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
       Active: active (running) since Mon 2016-11-14 09:26:47 EST; 35s ago
      Process: 18556 ExecStop=/usr/sbin/nscd --shutdown (code=exited, status=0/SUCCESS)
      Process: 18559 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
     Main PID: 18560 (nscd)
       CGroup: /system.slice/nscd.service
               └─18560 /usr/sbin/nscd

    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 monitoring directory `/etc` (2)
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 monitoring file `/etc/resolv.conf` (5)
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 monitoring directory `/etc` (2)
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 monitoring file `/etc/services` (6)
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 monitoring directory `/etc` (2)
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 disabled inotify-based monitoring for file `/etc/netgroup': No such file or directory
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 stat failed for file `/etc/netgroup'; will try again later: No such file or directory
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 Access Vector Cache (AVC) started
    Nov 14 09:26:47 ip-172-0-0-4.eu-central-1.compute.internal systemd[1]: Started Name Service Cache Daemon.
    Nov 14 09:27:06 ip-172-0-0-4.eu-central-1.compute.internal nscd[18560]: 18560 checking for monitored file `/etc/netgroup': No such file or directory

    ```

8. Verify the <code>ntpd</code> service is running
    `ntpd` was not installed on the nodes. Installed package `ntp` on all nodes and started service.
    ```
    [ec2-user@ip-172-0-0-4 ~]$ sudo yum install ntp
    <yum output here>
    [ec2-user@ip-172-0-0-4 ~]$ sudo service ntpd start
    Redirecting to /bin/systemctl start  ntpd.service
    [ec2-user@ip-172-0-0-4 ~]$ sudo service ntpd status
    Redirecting to /bin/systemctl status  ntpd.service
    ● ntpd.service - Network Time Service
       Loaded: loaded (/usr/lib/systemd/system/ntpd.service; disabled; vendor preset: disabled)
       Active: active (running) since Mon 2016-11-14 09:29:24 EST; 2s ago
      Process: 18846 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
     Main PID: 18847 (ntpd)
       CGroup: /system.slice/ntpd.service
               └─18847 /usr/sbin/ntpd -u ntp:ntp -g

    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: Listen normally on 2 lo 127.0.0.1 UDP 123
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: Listen normally on 3 eth0 172.0.0.4 UDP 123
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: Listen normally on 4 lo ::1 UDP 123
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: Listen normally on 5 eth0 fe80::7b:faff:fee2:a145 UDP 123
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: Listening on routing socket on fd #22 for interface updates
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal systemd[1]: Started Network Time Service.
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: 0.0.0.0 c016 06 restart
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
    Nov 14 09:29:24 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: 0.0.0.0 c011 01 freq_not_set
    Nov 14 09:29:25 ip-172-0-0-4.eu-central-1.compute.internal ntpd[18847]: 0.0.0.0 c614 04 freq_mode
    [ec2-user@ip-172-0-0-4 ~]$
    ```
