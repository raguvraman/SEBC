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

Preparing the Database-
[root@ex-2 yum.repos.d]# cat /etc/cloudera-scm-server/db.properties
# Auto-generated by scm_prepare_database.sh on Fri May 18 03:38:00 UTC 2018
#
# For information describing how to configure the Cloudera Manager Server
# to connect to databases, see the "Cloudera Manager Installation Guide."
#
com.cloudera.cmf.db.type=mysql
com.cloudera.cmf.db.host=ex-1.c.cloudera-204104.internal
com.cloudera.cmf.db.name=scm1
com.cloudera.cmf.db.user=scm1
com.cloudera.cmf.db.setupType=EXTERNAL
com.cloudera.cmf.db.password=scm1
[root@ex-2 yum.repos.d]#

Cloudera Manager Server Started -
[root@ex-2 yum.repos.d]# tail -4 /var/log/cloudera-scm-server/cloudera-scm-server.log
2018-05-18 03:40:54,492 INFO WebServerImpl:org.mortbay.log: jetty-6.1.26.cloudera.4
2018-05-18 03:40:54,496 INFO WebServerImpl:org.mortbay.log: Started SelectChannelConnector@0.0.0.0:7180
2018-05-18 03:40:54,496 INFO WebServerImpl:com.cloudera.server.cmf.WebServerImpl: Started Jetty server.
2018-05-18 03:40:56,667 INFO ScmActive-0:com.cloudera.server.cmf.components.ScmActive: ScmActive completed successfully.
[root@ex-2 yum.repos.d]#

Users -
drwxr-xr-x   - hdfs   supergroup          0 2018-05-18 04:38 /user/groot
drwxrwxrwx   - mapred hadoop              0 2018-05-18 04:12 /user/history
drwxrwxr-t   - hive   hive                0 2018-05-18 04:15 /user/hive
drwxrwxr-x   - hue    hue                 0 2018-05-18 04:15 /user/hue
drwxr-xr-x   - hdfs   supergroup          0 2018-05-18 04:38 /user/hulk
drwxrwxr-x   - oozie  oozie               0 2018-05-18 04:21 /user/oozie
drwxr-xr-x   - hdfs   supergroup          0 2018-05-18 04:38 /user/thanos
[root@ex-1 ~]#

[root@ex-1 ~]# curl -u admin:admin 'http://10.138.0.3:7180/api/v5/hosts'
{
  "items" : [ {
    "hostId" : "60baae6f-003a-49a7-8786-9923230b9928",
    "ipAddress" : "10.138.0.2",
    "hostname" : "ex-1.c.cloudera-204104.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/hostRedirect/60baae6f-003a-49a7-8786-9923230b9928",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "totalPhysMemBytes" : 15600513024
  }, {
    "hostId" : "613a93d8-a9e8-4f56-b031-a39d6e591436",
    "ipAddress" : "10.138.0.3",
    "hostname" : "ex-2.c.cloudera-204104.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/hostRedirect/613a93d8-a9e8-4f56-b031-a39d6e591436",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "totalPhysMemBytes" : 15600513024
  }, {
    "hostId" : "093cf09f-4576-4d74-a640-67de0c4148b4",
    "ipAddress" : "10.128.0.2",
    "hostname" : "ex-3.c.cloudera-204104.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/hostRedirect/093cf09f-4576-4d74-a640-67de0c4148b4",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "totalPhysMemBytes" : 15600513024
  }, {
    "hostId" : "4c56f25b-d162-4b94-952e-80e5782f740d",
    "ipAddress" : "10.142.0.3",
    "hostname" : "ex-4.c.cloudera-204104.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/hostRedirect/4c56f25b-d162-4b94-952e-80e5782f740d",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "totalPhysMemBytes" : 15600513024
  }, {
    "hostId" : "90312363-b140-49b5-9999-4a84d33cb422",
    "ipAddress" : "10.128.0.3",
    "hostname" : "ex-5.c.cloudera-204104.internal",
    "rackId" : "/default",
    "hostUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/hostRedirect/90312363-b140-49b5-9999-4a84d33cb422",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 4,
    "totalPhysMemBytes" : 15600504832
  } ]

Services Stat -
[root@ex-1 ~]# curl -u admin:admin 'http://10.138.0.3:7180/api/v11/clusters/raguvraman/services'
{
  "items" : [ {
    "name" : "zookeeper",
    "type" : "ZOOKEEPER",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/zookeeper",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/zookeeper/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "ZOOKEEPER_CANARY_HEALTH",
      "summary" : "GOOD",
      "suppressed" : true
    }, {
      "name" : "ZOOKEEPER_SERVERS_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "ZooKeeper",
    "entityStatus" : "GOOD_HEALTH"
  }, {
    "name" : "hdfs",
    "type" : "HDFS",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hdfs",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hdfs/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HDFS_BLOCKS_WITH_CORRUPT_REPLICAS",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HDFS_CANARY_HEALTH",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HDFS_DATA_NODES_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HDFS_FREE_SPACE_REMAINING",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HDFS_HA_NAMENODE_HEALTH",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HDFS_MISSING_BLOCKS",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HDFS_UNDER_REPLICATED_BLOCKS",
      "summary" : "GOOD",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "HDFS",
    "entityStatus" : "GOOD_HEALTH"
  }, {
    "name" : "yarn",
    "type" : "YARN",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/yarn",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/yarn/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "YARN_JOBHISTORY_HEALTH",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "YARN_NODE_MANAGERS_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "YARN_RESOURCEMANAGERS_HEALTH",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "YARN_USAGE_AGGREGATION_HEALTH",
      "summary" : "DISABLED",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "YARN (MR2 Included)",
    "entityStatus" : "GOOD_HEALTH"
  }, {
    "name" : "hive",
    "type" : "HIVE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hive",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hive/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HIVE_HIVEMETASTORES_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HIVE_HIVESERVER2S_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HIVE_WEBHCATS_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Hive",
    "entityStatus" : "GOOD_HEALTH"
  }, {
    "name" : "hbase",
    "type" : "HBASE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hbase",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hbase/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HBASE_MASTER_HEALTH",
      "summary" : "GOOD",
      "suppressed" : false
    }, {
      "name" : "HBASE_REGION_SERVERS_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "HBase",
    "entityStatus" : "GOOD_HEALTH"
  }, {
    "name" : "oozie",
    "type" : "OOZIE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/oozie",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/oozie/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "OOZIE_OOZIE_SERVERS_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Oozie",
    "entityStatus" : "GOOD_HEALTH"
  }, {
    "name" : "hue",
    "type" : "HUE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hue",
    "roleInstancesUrl" : "http://ex-2.c.cloudera-204104.internal:7180/cmf/serviceRedirect/hue/instances",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HUE_HUE_SERVERS_HEALTHY",
      "summary" : "GOOD",
      "suppressed" : false
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Hue",
    "entityStatus" : "GOOD_HEALTH"
  } ]

Teragen-
time yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapred.map.tasks=40 -Ddfs.block.size=67108864 5242880 /user/groot/tgen
O/P-
[groot@ex-1 root]$ time yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapred.map.tasks=40 -Ddfs.block.size=67108864 5242880 /user/groot/tgen
18/05/18 05:34:42 INFO client.RMProxy: Connecting to ResourceManager at ex-1.c.cloudera-204104.internal/10.138.0.2:8032
18/05/18 05:34:43 INFO terasort.TeraGen: Generating 5242880 using 40
18/05/18 05:34:44 INFO mapreduce.JobSubmitter: number of splits:40
18/05/18 05:34:44 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
18/05/18 05:34:44 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
18/05/18 05:34:45 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1526620461077_0001
18/05/18 05:34:45 INFO impl.YarnClientImpl: Submitted application application_1526620461077_0001
18/05/18 05:34:45 INFO mapreduce.Job: The url to track the job: http://ex-1.c.cloudera-204104.internal:8088/proxy/application_1526620461077_0001/
18/05/18 05:34:45 INFO mapreduce.Job: Running job: job_1526620461077_0001
18/05/18 05:34:56 INFO mapreduce.Job: Job job_1526620461077_0001 running in uber mode : false
18/05/18 05:34:56 INFO mapreduce.Job:  map 0% reduce 0%
18/05/18 05:35:09 INFO mapreduce.Job:  map 8% reduce 0%
18/05/18 05:35:10 INFO mapreduce.Job:  map 15% reduce 0%
18/05/18 05:35:12 INFO mapreduce.Job:  map 20% reduce 0%
18/05/18 05:35:14 INFO mapreduce.Job:  map 25% reduce 0%
18/05/18 05:35:20 INFO mapreduce.Job:  map 30% reduce 0%
18/05/18 05:35:21 INFO mapreduce.Job:  map 40% reduce 0%
18/05/18 05:35:25 INFO mapreduce.Job:  map 43% reduce 0%
18/05/18 05:35:26 INFO mapreduce.Job:  map 47% reduce 0%
18/05/18 05:35:27 INFO mapreduce.Job:  map 50% reduce 0%
18/05/18 05:35:31 INFO mapreduce.Job:  map 55% reduce 0%
18/05/18 05:35:32 INFO mapreduce.Job:  map 65% reduce 0%
18/05/18 05:35:35 INFO mapreduce.Job:  map 68% reduce 0%
18/05/18 05:35:38 INFO mapreduce.Job:  map 70% reduce 0%
18/05/18 05:35:40 INFO mapreduce.Job:  map 75% reduce 0%
18/05/18 05:35:41 INFO mapreduce.Job:  map 77% reduce 0%
18/05/18 05:35:42 INFO mapreduce.Job:  map 82% reduce 0%
18/05/18 05:35:43 INFO mapreduce.Job:  map 90% reduce 0%
18/05/18 05:35:45 INFO mapreduce.Job:  map 93% reduce 0%
18/05/18 05:35:48 INFO mapreduce.Job:  map 95% reduce 0%
18/05/18 05:35:51 INFO mapreduce.Job:  map 100% reduce 0%
18/05/18 05:36:08 INFO mapreduce.Job: Job job_1526620461077_0001 completed successfully
18/05/18 05:36:08 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=5108910
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=3397
                HDFS: Number of bytes written=524288000
                HDFS: Number of read operations=160
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=80
        Job Counters
                Launched map tasks=40
                Other local map tasks=40
                Total time spent by all maps in occupied slots (ms)=415270
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=415270
                Total vcore-milliseconds taken by all map tasks=415270
                Total megabyte-milliseconds taken by all map tasks=425236480
        Map-Reduce Framework
                Map input records=5242880
                Map output records=5242880
                Input split bytes=3397
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=6803
                CPU time spent (ms)=67490
                Physical memory (bytes) snapshot=9944899584
                Virtual memory (bytes) snapshot=111340642304
                Total committed heap usage (bytes)=11152654336
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=11257830824958050
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=524288000

real    1m27.788s
user    0m7.526s
sys     0m0.344s

hdfs dfs -ls /user/groot/tgen -
[groot@ex-1 root]$ hdfs dfs -ls /user/groot/tgen
Found 41 items
-rw-r--r--   3 hdfs supergroup          0 2018-05-18 05:36 /user/groot/tgen/_SUCCESS
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00000
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00001
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00002
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00003
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00004
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00005
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00006
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00007
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00008
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00009
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00010
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00011
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00012
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00013
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00014
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00015
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00016
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00017
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00018
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00019
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00020
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00021
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00022
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00023
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00024
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00025
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00026
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00027
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00028
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00029
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00030
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00031
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00032
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00033
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00034
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00035
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00036
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00037
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00038
-rw-r--r--   3 hdfs supergroup   13107200 2018-05-18 05:35 /user/groot/tgen/part-m-00039

[groot@ex-1 root]$ hadoop fsck -blocks /user/groot
DEPRECATED: Use of this script to execute hdfs command is deprecated.
Instead use the hdfs command for it.

Connecting to namenode via http://ex-1.c.cloudera-204104.internal:50070
FSCK started by hdfs (auth:SIMPLE) from /10.138.0.2 for path /user/groot at Fri May 18 05:41:48 UTC 2018
.........................................Status: HEALTHY
 Total size:    524288000 B
 Total dirs:    2
 Total files:   41
 Total symlinks:                0
 Total blocks (validated):      40 (avg. block size 13107200 B)
 Minimally replicated blocks:   40 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Fri May 18 05:41:48 UTC 2018 in 3 milliseconds


The filesystem under path '/user/groot' is HEALTHY



