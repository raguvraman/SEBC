Cloud Provider - Google Cloud
Linux - CentOS-7
[root@ex-1 ragu]# yum repolist enabled
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.eecs.wsu.edu
 * epel: mirrors.cat.pdx.edu
 * extras: centos-distro.1gservers.com
 * updates: mirrors.cat.pdx.edu
repo id                                                                        repo name                                                                                               status
!base/7/x86_64                                                                 CentOS-7 - Base                                                                                          9,911
!epel/x86_64                                                                   Extra Packages for Enterprise Linux 7 - x86_64                                                          12,542
!extras/7/x86_64                                                               CentOS-7 - Extras                                                                                          258
!google-cloud-compute                                                          Google Cloud Compute                                                                                         9
!google-cloud-sdk                                                              Google Cloud SDK                                                                                            92
!updates/7/x86_64                                                              CentOS-7 - Updates                                                                                         151

[root@ex-1 ragu]# df -TH
Filesystem     Type      Size  Used Avail Use% Mounted on
/dev/sda1      xfs        54G  2.1G   52G   4% /
devtmpfs       devtmpfs  7.8G     0  7.8G   0% /dev
tmpfs          tmpfs     7.9G     0  7.9G   0% /dev/shm
tmpfs          tmpfs     7.9G   10M  7.8G   1% /run
tmpfs          tmpfs     7.9G     0  7.9G   0% /sys/fs/cgroup
tmpfs          tmpfs     1.6G     0  1.6G   0% /run/user/1000
tmpfs          tmpfs     1.6G     0  1.6G   0% /run/user/1001
tmpfs          tmpfs     1.6G     0  1.6G   0% /run/user/0
[root@ex-1 ragu]#

Uptime-
[root@ex-1 ragu]# uptime
 02:57:36 up 21 min,  2 users,  load average: 0.00, 0.01, 0.02
[root@ex-1 ragu]#
[root@ex-2 ragu]# uptime
 02:58:06 up 22 min,  1 user,  load average: 0.00, 0.01, 0.04
[root@ex-2 ragu]#
[root@ex-3 ragu]# uptime
 02:58:25 up 21 min,  1 user,  load average: 0.00, 0.01, 0.02
[root@ex-3 ragu]#
[root@ex-4 ragu]# uptime
 02:58:42 up 22 min,  1 user,  load average: 0.00, 0.01, 0.01
[root@ex-4 ragu]#
[root@ex-5 ragu]# uptime
 02:58:59 up 22 min,  1 user,  load average: 0.08, 0.03, 0.04
[root@ex-5 ragu]#


[root@ex-1 ragu]# nslookup ex-1
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ex-1.c.cloudera-204104.internal
Address: 10.138.0.2

[root@ex-1 ragu]# nslookup ex-2
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ex-2.c.cloudera-204104.internal
Address: 10.138.0.3

[root@ex-1 ragu]# nslookup ex-3
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ex-3.c.cloudera-204104.internal
Address: 10.128.0.2

[root@ex-1 ragu]# nslookup ex-4
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ex-4.c.cloudera-204104.internal
Address: 10.142.0.3

[root@ex-1 ragu]# nslookup ex-5
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   ex-5.c.cloudera-204104.internal
Address: 10.128.0.3


thanos:x:2500:2701::/home/thanos:/bin/bash
hulk:x:2600:2702::/home/hulk:/bin/bash
groot:x:2700:2702::/home/groot:/bin/bash

thanos:x:2500:
hulk:x:2600:
groot:x:2700:
blackorder:x:2701:
avengers:x:2702:

Mariadb - Setup
[root@ex-1 ragu]# systemctl start mariadb
[root@ex-1 ragu]# systemctl status mariadb
● mariadb.service - MariaDB database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; disabled; vendor preset: disabled)
   Active: active (running) since Fri 2018-05-18 03:08:31 UTC; 14s ago
  Process: 1673 ExecStartPost=/usr/libexec/mariadb-wait-ready $MAINPID (code=exited, status=0/SUCCESS)
  Process: 1588 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir %n (code=exited, status=0/SUCCESS)
 Main PID: 1672 (mysqld_safe)
   CGroup: /system.slice/mariadb.service
           ├─1672 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
           └─2157 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --log-error=/var/log/mariadb/mariadb.log --pid-file=/var/run/mariadb/ma...

May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: MySQL manual for more instructions.
May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: Please report any problems at http://mariadb.org/jira
May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: The latest information about MariaDB is available at http://mariadb.org/.
May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: You can find additional information about the MySQL part at:
May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: http://dev.mysql.com
May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: Consider joining MariaDB's strong and vibrant community:
May 18 03:08:20 ex-1 mariadb-prepare-db-dir[1588]: https://mariadb.org/get-involved/
May 18 03:08:20 ex-1 mysqld_safe[1672]: 180518 03:08:20 mysqld_safe Logging to '/var/log/mariadb/mariadb.log'.
May 18 03:08:20 ex-1 mysqld_safe[1672]: 180518 03:08:20 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql
May 18 03:08:31 ex-1 systemd[1]: Started MariaDB database server.

[root@ex-1 bin]# mysql -u root -p -e "status;"
Enter password:
--------------
mysql  Ver 15.1 Distrib 5.5.56-MariaDB, for Linux (x86_64) using readline 5.1

Connection id:          10
Current database:
Current user:           root@localhost
SSL:                    Not in use
Current pager:          stdout
Using outfile:          ''
Using delimiter:        ;
Server:                 MariaDB
Server version:         5.5.56-MariaDB MariaDB Server
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    utf8
Conn.  characterset:    utf8
UNIX socket:            /var/lib/mysql/mysql.sock
Uptime:                 4 min 36 sec

[root@ex-1 bin]# mysql -u root  -p -e "show databases;"
Enter password:
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

Cloudera Manager Repo -
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
#baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5/
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.11.2/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1