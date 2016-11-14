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
    proc        on  /proc                       type  proc        (rw,nosuid,nodev,noexec,relatime)
    sysfs       on  /sys                        type  sysfs       (rw,nosuid,nodev,noexec,relatime,seclabel)
    devtmpfs    on  /dev                        type  devtmpfs    (rw,nosuid,seclabel,size=7600900k,nr_inodes=1900225,mode=755)
    securityfs  on  /sys/kernel/security        type  securityfs  (rw,nosuid,nodev,noexec,relatime)
    tmpfs       on  /dev/shm                    type  tmpfs       (rw,nosuid,nodev,seclabel)
    devpts      on  /dev/pts                    type  devpts      (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
    tmpfs       on  /run                        type  tmpfs       (rw,nosuid,nodev,seclabel,mode=755)
    tmpfs       on  /sys/fs/cgroup              type  tmpfs       (rw,nosuid,nodev,noexec,seclabel,mode=755)
    cgroup      on  /sys/fs/cgroup/systemd      type  cgroup      (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
    pstore      on  /sys/fs/pstore              type  pstore      (rw,nosuid,nodev,noexec,relatime)
    cgroup      on  /sys/fs/cgroup/cpuset       type  cgroup      (rw,nosuid,nodev,noexec,relatime,cpuset)
    cgroup      on  /sys/fs/cgroup/cpu,cpuacct  type  cgroup      (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
    cgroup      on  /sys/fs/cgroup/memory       type  cgroup      (rw,nosuid,nodev,noexec,relatime,memory)
    cgroup      on  /sys/fs/cgroup/devices      type  cgroup      (rw,nosuid,nodev,noexec,relatime,devices)
    cgroup      on  /sys/fs/cgroup/freezer      type  cgroup      (rw,nosuid,nodev,noexec,relatime,freezer)
    cgroup      on  /sys/fs/cgroup/net_cls      type  cgroup      (rw,nosuid,nodev,noexec,relatime,net_cls)
    cgroup      on  /sys/fs/cgroup/blkio        type  cgroup      (rw,nosuid,nodev,noexec,relatime,blkio)
    cgroup      on  /sys/fs/cgroup/perf_event   type  cgroup      (rw,nosuid,nodev,noexec,relatime,perf_event)
    cgroup      on  /sys/fs/cgroup/hugetlb      type  cgroup      (rw,nosuid,nodev,noexec,relatime,hugetlb)
    configfs    on  /sys/kernel/config          type  configfs    (rw,relatime)
    /dev/xvda2  on  /                           type  xfs         (rw,relatime,seclabel,attr2,inode64,noquota)
    selinuxfs   on  /sys/fs/selinux             type  selinuxfs   (rw,relatime)
    systemd-1   on  /proc/sys/fs/binfmt_misc    type  autofs      (rw,relatime,fd=32,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
    debugfs     on  /sys/kernel/debug           type  debugfs     (rw,relatime)
    mqueue      on  /dev/mqueue                 type  mqueue      (rw,relatime,seclabel)
    hugetlbfs   on  /dev/hugepages              type  hugetlbfs   (rw,relatime,seclabel)

    ```

3. Show the reserve space of any non-root, ext-based volumes

    ```
    [ec2-user@ip-172-0-0-4 ~]$ df -H
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/xvda2      108G  1.7G  106G   2% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.7G     0  7.7G   0% /dev/shm
    tmpfs           7.7G   18M  7.7G   1% /run
    tmpfs           7.7G     0  7.7G   0% /sys/fs/cgroup

    [ec2-user@ip-172-0-0-4 ~]$ sudo fdisk -l /dev/xvda2

    Disk /dev/xvda2: 107.4 GB, 107372068352 bytes, 209711071 sectors
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
            inet6 fe80::dd:dcff:febb:cb55  prefixlen 64  scopeid 0x20<link>
            ether 02:dd:dc:bb:cb:55  txqueuelen 1000  (Ethernet)
            RX packets 211354  bytes 286895735 (273.6 MiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 70785  bytes 13529360 (12.9 MiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 0  (Local Loopback)
            RX packets 147  bytes 97490 (95.2 KiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 147  bytes 97490 (95.2 KiB)
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

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.12
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    12.0.0.172.in-addr.arpa  name = ip-172-0-0-12.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.14
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    14.0.0.172.in-addr.arpa  name = ip-172-0-0-14.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.13
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    13.0.0.172.in-addr.arpa  name = ip-172-0-0-13.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ nslookup 172.0.0.5
    Server:         172.0.0.2
    Address:        172.0.0.2#53

    Non-authoritative answer:
    5.0.0.172.in-addr.arpa  name = ip-172-0-0-5.eu-central-1.compute.internal.

    Authoritative answers can be found from:

    [ec2-user@ip-172-0-0-4 ~]$ getent hosts 172.0.0.4
    172.0.0.4       bc1 ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts ip-172-0-0-4
    172.0.0.4       ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts bc1
    172.0.0.4       bc1 ip-172-0-0-4.eu-central-1.compute.internal
    [ec2-user@ip-172-0-0-4 ~]$ getent hosts ip-172-0-0-4.eu-central-1.compute.internal
    fe80::dd:dcff:febb:cb55 ip-172-0-0-4.eu-central-1.compute.internal

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
