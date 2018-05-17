Cloud Provider - Google Cloud

IP address, Host names
[root@ch-1 ~]# nslookup ch-1
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ch-1.c.cloudera-204104.internal
Address: 10.142.0.4

[root@ch-1 ~]# nslookup ch-2
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ch-2.c.cloudera-204104.internal
Address: 10.128.0.4

[root@ch-1 ~]# nslookup ch-3
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ch-3.c.cloudera-204104.internal
Address: 10.138.0.3

[root@ch-1 ~]# nslookup ch-4
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ch-4.c.cloudera-204104.internal
Address: 10.138.0.4

[root@ch-1 ~]# nslookup ch-5
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ch-5.c.cloudera-204104.internal
Address: 10.128.0.3

Filesystem details - 
[root@ch-1 ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G  3.3G   47G   7% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.3G     0  7.3G   0% /dev/shm
tmpfs           7.3G  9.5M  7.3G   1% /run
tmpfs           7.3G     0  7.3G   0% /sys/fs/cgroup
tmpfs           1.5G     0  1.5G   0% /run/user/2901
tmpfs           1.5G     0  1.5G   0% /run/user/1000
tmpfs           1.5G     0  1.5G   0% /run/user/0
[root@ch-1 ~]# ls -lrth /
total 20K
drwxr-xr-x.   2 root root    6 Apr 11 04:59 srv
drwxr-xr-x.   2 root root    6 Apr 11 04:59 opt
drwxr-xr-x.   2 root root    6 Apr 11 04:59 mnt
drwxr-xr-x.   2 root root    6 Apr 11 04:59 media
lrwxrwxrwx.   1 root root    7 May 14 21:06 bin -> usr/bin
lrwxrwxrwx.   1 root root    9 May 14 21:06 lib64 -> usr/lib64
lrwxrwxrwx.   1 root root    7 May 14 21:06 lib -> usr/lib
lrwxrwxrwx.   1 root root    8 May 14 21:06 sbin -> usr/sbin
dr-xr-xr-x.   5 root root 4.0K May 14 21:08 boot
drwxr-xr-x.  18 root root  254 May 17 05:40 var
drwxr-xr-x.   6 root root   66 May 17 05:58 home
dr-xr-xr-x  122 root root    0 May 17 06:08 proc
dr-xr-xr-x   13 root root    0 May 17 06:08 sys
drwxr-xr-x   17 root root 2.8K May 17 06:09 dev
drwxr-xr-x.  14 root root  167 May 17 06:55 usr
drwxr-xr-x   26 root root  740 May 17 07:06 run
drwxr-xr-x.  81 root root 8.0K May 17 07:10 etc
dr-xr-x---.   3 root root  146 May 17 07:30 root
drwxrwxrwt.  13 root root 4.0K May 17 07:32 tmp
drwxr-xr-x    2 root root    6 May 17 07:32 data
[root@ch-1 ~]#

Yum repolist enabled -
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.vcu.edu
 * epel: reflector.westga.edu
 * extras: mirror.mojohost.com
 * updates: mirror.ash.fastserv.com
repo id                 repo name                                         status
base/7/x86_64           CentOS-7 - Base                                    9,911
cloudera-director       Cloudera Director                                      5
epel/x86_64             Extra Packages for Enterprise Linux 7 - x86_64    12,542
extras/7/x86_64         CentOS-7 - Extras                                    258
google-cloud-compute    Google Cloud Compute                                   9
google-cloud-sdk        Google Cloud SDK                                      92
updates/7/x86_64        CentOS-7 - Updates                                   151

jimenez:x:2800:2800::/home/jimenez:/bin/bash
beltran:x:2900:2900::/home/beltran:/bin/bash

astros:x:2900:beltran
rangers:x:2800:jimenez

[root@ch-1 ~]# hostname -f
ch-1.c.cloudera-204104.internal
[root@ch-1 ~]# mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 49
Server version: 5.5.56-MariaDB MariaDB Server

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| hive               |
| hue                |
| mysql              |
| oozie              |
| performance_schema |
| rmandb             |
| scm                |
| sentry             |
+--------------------+
9 rows in set (0.00 sec)




