2_MariaDB repication 


1.b) modify /etc/my.cnf.d/server.cnf  file in both the machines with respective configs.

            Master 10.142.0.3 :

            [mysqld]
              log-bin
              server_id=1
              replicate-do-db=scm
              bind-address=10.142.0.3

            slave 10.138.0.2 :

            [mysqld]
            log-bin
            server_id=2
            replicate-do-db=scm
            bind-address=10.138.0.2 
     
 1.c ) Restart MariaDB server on both the hosts to run the server with updated configs:

2. DB configuration at Master server         

step 2.a ) Login with root account and verify the respective database. 

[root@instance-4 tmp]# mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 16
Server version: 10.1.33-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use scm;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [scm]> show tables;
+--------------------------------+
| Tables_in_scm                  |
+--------------------------------+
| AUDITS                         |
| CLIENT_CONFIGS                 |
| CLIENT_CONFIGS_TO_HOSTS        |
| CLUSTERS                       |
| CLUSTERS_AUD                   |
| CLUSTER_ACTIVATED_RELEASES     |
| CLUSTER_ACTIVATED_RELEASES_AUD |
| CLUSTER_MANAGED_RELEASES       |
| CLUSTER_UNDISTRIBUTED_RELEASES |
#
| CM_PEERS                       |
| CM_VERSION                     |
| COMMANDS                       |
| COMMANDS_DETAIL                |
| COMMAND_SCHEDULES              |
| CONFIGS                        |
| CONFIGS_AUD                    |
| CONFIG_CONTAINERS              |
| CREDENTIALS                    |
| DIAGNOSTICS_EVENTS             |
| EXTERNAL_ACCOUNTS              |
| EXTERNAL_ACCOUNTS_AUD          |
| GLOBAL_SETTINGS                |
| HOSTS                          |
| HOSTS_AUD                      |
| HOST_TEMPLATES                 |
| HOST_TEMPLATE_TO_ROLE_CONF_GRP |
| METRICS                        |
| PARCELS                        |
| PARCEL_COMPONENTS              |
| PROCESSES                      |
| PROCESSES_DETAIL               |
| PROCESS_ACTIVE_RELEASES        |
| RELEASES                       |
| RELEASES_AUD                   |
| REVISIONS                      |
| ROLES                          |
| ROLES_AUD                      |
| ROLE_CONFIG_GROUPS             |
| ROLE_CONFIG_GROUPS_AUD         |
| ROLE_STALENESS_STATUS          |
| SCHEMA_VERSION                 |
| SERVICES                       |
| SERVICES_AUD                   |
| SNAPSHOT_POLICIES              |
| USERS                          |
| USER_ROLES                     |
| USER_SETTINGS                  |
+--------------------------------+
47 rows in set (0.00 sec)

MariaDB [scm]> Bye
[root@instance-4 tmp]# vi /etc/my.cnf
[root@instance-4 tmp]# cd /etc/my.cnf
my.cnf    my.cnf.d/ 
[root@instance-4 tmp]# cd /etc/my.cnf.d/
client.cnf                enable_encryption.preset  mysql-clients.cnf         server.cnf                tokudb.cnf                
[root@instance-4 tmp]# cd /etc/my.cnf.d/
client.cnf                enable_encryption.preset  mysql-clients.cnf         server.cnf                tokudb.cnf                
[root@instance-4 tmp]# cd /etc/my.cnf.d/server.cnf 
bash: cd: /etc/my.cnf.d/server.cnf: Not a directory
[root@instance-4 tmp]# vi  /etc/my.cnf.d/server.cnf 
[root@instance-4 tmp]# systemctl restart mariadb
[root@instance-4 tmp]# netstat -tulpn | grep 3306
tcp        0      0 10.142.0.3:3306         0.0.0.0:*               LISTEN      3115/mysqld         

step 2.b) Log on to the MariaDB server as root, create the user slave and assign the necessary grants:

[root@instance-4 tmp]# mysql -u root -p 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 10.1.33-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE USER 'slave'@'localhost' IDENTIFIED BY 'bigdata';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> GRANT REPLICATION SLAVE ON *.* TO slave IDENTIFIED BY 'bigdata' WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH TABLES WITH READ LOCK;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> SHOW MASTER STATUS;
+-----------------------+----------+--------------+------------------+
| File                  | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+-----------------------+----------+--------------+------------------+
| instance-4-bin.000001 |      777 |              |                  |
+-----------------------+----------+--------------+------------------+
1 row in set (0.00 sec)

MariaDB [(none)]> SHOW MASTER STATUS;
+-----------------------+----------+--------------+------------------+
| File                  | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+-----------------------+----------+--------------+------------------+
| instance-4-bin.000001 |      777 |              |                  |
+-----------------------+----------+--------------+------------------+
1 row in set (0.00 sec)

MariaDB [(none)]> exit;
Bye
[root@instance-4 tmp]# mysql -u root -p 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 5
Server version: 10.1.33-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> UNLOCK TABLES;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> exit;
Bye

step 2.c) Run the mysql_upgrade procedure to upgrade the system tables
[root@instance-4 tmp]# mysql_upgrade -u root -p
Enter password: 
Phase 1/7: Checking and upgrading mysql database
Processing databases
mysql
mysql.column_stats                                 OK
mysql.columns_priv                                 OK
mysql.db                                           OK
mysql.event                                        OK
mysql.func                                         OK
mysql.gtid_slave_pos                               OK
mysql.help_category                                OK
mysql.help_keyword                                 OK
mysql.help_relation                                OK
mysql.help_topic                                   OK
mysql.host                                         OK
mysql.index_stats                                  OK
mysql.innodb_index_stats                           OK
mysql.innodb_table_stats                           OK
mysql.plugin                                       OK
mysql.proc                                         OK
mysql.procs_priv                                   OK
mysql.proxies_priv                                 OK
mysql.roles_mapping                                OK
mysql.servers                                      OK
mysql.table_stats                                  OK
mysql.tables_priv                                  OK
mysql.time_zone                                    OK
mysql.time_zone_leap_second                        OK
mysql.time_zone_name                               OK
mysql.time_zone_transition                         OK
mysql.time_zone_transition_type                    OK
mysql.user                                         OK
Phase 2/7: Installing used storage engines... Skipped
Phase 3/7: Fixing views
Phase 4/7: Running 'mysql_fix_privilege_tables'
Phase 5/7: Fixing table and database names
Phase 6/7: Checking and upgrading tables
Processing databases
information_schema
performance_schema
scm
scm.AUDITS                                         OK
scm.CLIENT_CONFIGS                                 OK
scm.CLIENT_CONFIGS_TO_HOSTS                        OK
scm.CLUSTERS                                       OK
scm.CLUSTERS_AUD                                   OK
scm.CLUSTER_ACTIVATED_RELEASES                     OK
scm.CLUSTER_ACTIVATED_RELEASES_AUD                 OK
scm.CLUSTER_MANAGED_RELEASES                       OK
scm.CLUSTER_UNDISTRIBUTED_RELEASES                 OK
scm.CM_PEERS                                       OK
scm.CM_VERSION                                     OK
scm.COMMANDS                                       OK
scm.COMMANDS_DETAIL                                OK
scm.COMMAND_SCHEDULES                              OK
scm.CONFIGS                                        OK
scm.CONFIGS_AUD                                    OK
scm.CONFIG_CONTAINERS                              OK
scm.CREDENTIALS                                    OK
scm.DIAGNOSTICS_EVENTS                             OK
scm.EXTERNAL_ACCOUNTS                              OK
scm.EXTERNAL_ACCOUNTS_AUD                          OK
scm.GLOBAL_SETTINGS                                OK
scm.HOSTS                                          OK
scm.HOSTS_AUD                                      OK
scm.HOST_TEMPLATES                                 OK
scm.HOST_TEMPLATE_TO_ROLE_CONF_GRP                 OK
scm.METRICS                                        OK
scm.PARCELS                                        OK
scm.PARCEL_COMPONENTS                              OK
scm.PROCESSES                                      OK
scm.PROCESSES_DETAIL                               OK
scm.PROCESS_ACTIVE_RELEASES                        OK
scm.RELEASES                                       OK
scm.RELEASES_AUD                                   OK
scm.REVISIONS                                      OK
scm.ROLES                                          OK
scm.ROLES_AUD                                      OK
scm.ROLE_CONFIG_GROUPS                             OK
scm.ROLE_CONFIG_GROUPS_AUD                         OK
scm.ROLE_STALENESS_STATUS                          OK
scm.SCHEMA_VERSION                                 OK
scm.SERVICES                                       OK
scm.SERVICES_AUD                                   OK
scm.SNAPSHOT_POLICIES                              OK
scm.USERS                                          OK
scm.USER_ROLES                                     OK
scm.USER_SETTINGS                                  OK
Phase 7/7: Running 'FLUSH PRIVILEGES'
OK
[root@instance-4 tmp]# 



##### 3. Configuring MySQL Server on Slave ###############

   step 3.a )  Take mysql dump from master node. 

          [root@instance-5 tmp]# mysqldump -h 10.142.0.3 -u root -p scm > scm.sql
   step 3.b) Once connected to the database server, create the user and an empty database, and grant permissions:

          MariaDB [(none)]> GRANT ALL PRIVILEGES ON scm.* TO 'slave'@'localhost' IDENTIFIED BY 'bigdata' WITH GRANT OPTION;
          Query OK, 0 rows affected (0.01 sec)

          MariaDB [(none)]> FLUSH PRIVILEGES;
          Query OK, 0 rows affected (0.01 sec)

          MariaDB [(none)]> exit;
          Bye
    [root@instance-5 tmp]# systemctl restart mariadb;
step 3.c) Run the mysql_upgrade procedure to upgrade the system tables
    [root@instance-5 tmp]# mysql_upgrade -u root -p
Enter password: 
Phase 1/7: Checking and upgrading mysql database
Processing databases
mysql
mysql.column_stats                                 OK
mysql.columns_priv                                 OK
mysql.db                                           OK
mysql.event                                        OK
mysql.func                                         OK
mysql.gtid_slave_pos                               OK
mysql.help_category                                OK
mysql.help_keyword                                 OK
mysql.help_relation                                OK
mysql.help_topic                                   OK
mysql.host                                         OK
mysql.index_stats                                  OK
mysql.innodb_index_stats                           OK
mysql.innodb_table_stats                           OK
mysql.plugin                                       OK
mysql.proc                                         OK
mysql.procs_priv                                   OK
mysql.proxies_priv                                 OK
mysql.roles_mapping                                OK
mysql.servers                                      OK
mysql.table_stats                                  OK
mysql.tables_priv                                  OK
mysql.time_zone                                    OK
mysql.time_zone_leap_second                        OK
mysql.time_zone_name                               OK
mysql.time_zone_transition                         OK
mysql.time_zone_transition_type                    OK
mysql.user                                         OK
Phase 2/7: Installing used storage engines... Skipped
Phase 3/7: Fixing views
Phase 4/7: Running 'mysql_fix_privilege_tables'
Phase 5/7: Fixing table and database names
Phase 6/7: Checking and upgrading tables
Processing databases
information_schema
performance_schema
scm
scm.AUDITS                                         OK
scm.CLIENT_CONFIGS                                 OK
scm.CLIENT_CONFIGS_TO_HOSTS                        OK
scm.CLUSTERS                                       OK
scm.CLUSTERS_AUD                                   OK
scm.CLUSTER_ACTIVATED_RELEASES                     OK
scm.CLUSTER_ACTIVATED_RELEASES_AUD                 OK
scm.CLUSTER_MANAGED_RELEASES                       OK
scm.CLUSTER_UNDISTRIBUTED_RELEASES                 OK
scm.CM_PEERS                                       OK
scm.CM_VERSION                                     OK
scm.COMMANDS                                       OK
scm.COMMANDS_DETAIL                                OK
scm.COMMAND_SCHEDULES                              OK
scm.CONFIGS                                        OK
scm.CONFIGS_AUD                                    OK
scm.CONFIG_CONTAINERS                              OK
scm.CREDENTIALS                                    OK
scm.DIAGNOSTICS_EVENTS                             OK
scm.EXTERNAL_ACCOUNTS                              OK
scm.EXTERNAL_ACCOUNTS_AUD                          OK
scm.GLOBAL_SETTINGS                                OK
scm.HOSTS                                          OK
scm.HOSTS_AUD                                      OK
scm.HOST_TEMPLATES                                 OK
scm.HOST_TEMPLATE_TO_ROLE_CONF_GRP                 OK
scm.METRICS                                        OK
scm.PARCELS                                        OK
scm.PARCEL_COMPONENTS                              OK
scm.PROCESSES                                      OK
scm.PROCESSES_DETAIL                               OK
scm.PROCESS_ACTIVE_RELEASES                        OK
scm.RELEASES                                       OK
scm.RELEASES_AUD                                   OK
scm.REVISIONS                                      OK
scm.ROLES                                          OK
scm.ROLES_AUD                                      OK
scm.ROLE_CONFIG_GROUPS                             OK
scm.ROLE_CONFIG_GROUPS_AUD                         OK
scm.ROLE_STALENESS_STATUS                          OK
scm.SCHEMA_VERSION                                 OK
scm.SERVICES                                       OK
scm.SERVICES_AUD                                   OK
scm.SNAPSHOT_POLICIES                              OK
scm.USERS                                          OK
scm.USER_ROLES                                     OK
scm.USER_SETTINGS                                  OK
Phase 7/7: Running 'FLUSH PRIVILEGES'
OK

step 3.d) Log on to the database and run the following commands in the MariaDB prompt
          [root@instance-5 tmp]# mysql -u root -p 
          Enter password: 
          Welcome to the MariaDB monitor.  Commands end with ; or \g.
          Your MariaDB connection id is 15
          Server version: 10.1.33-MariaDB MariaDB Server

          Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

          Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.  

  
MariaDB [(none)]> CHANGE MASTER TO MASTER_HOST='10.142.0.3', MASTER_USER='slave', MASTER_PASSWORD='bigdata', MASTER_PORT=3306, MASTER_LOG_FILE='instance-4-bin.000001', MASTER_LOG_POS=777, MASTER_CONNECT_RETRY=10;
Query OK, 0 rows affected (0.15 sec)

MariaDB [(none)]> START SLAVE;
Query OK, 0 rows affected (0.03 sec)

MariaDB [(none)]> SHOW SLAVE STATUS\G;
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 10.142.0.3
                  Master_User: slave
                  Master_Port: 3306
                Connect_Retry: 10
              Master_Log_File: instance-4-bin.000001
          Read_Master_Log_Pos: 777
               Relay_Log_File: instance-5-relay-bin.000002
                Relay_Log_Pos: 542
        Relay_Master_Log_File: instance-4-bin.000001
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB: scm
          Replicate_Ignore_DB: 
           Replicate_Do_Table: 
       Replicate_Ignore_Table: 
      Replicate_Wild_Do_Table: 
  Replicate_Wild_Ignore_Table: 
                   Last_Errno: 0
                   Last_Error: 
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 777
              Relay_Log_Space: 845
              Until_Condition: None
               Until_Log_File: 
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File: 
           Master_SSL_CA_Path: 
              Master_SSL_Cert: 
            Master_SSL_Cipher: 
               Master_SSL_Key: 
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error: 
               Last_SQL_Errno: 0
               Last_SQL_Error: 
  Replicate_Ignore_Server_Ids: 
             Master_Server_Id: 1
               Master_SSL_Crl: 
           Master_SSL_Crlpath: 
                   Using_Gtid: No
                  Gtid_IO_Pos: 
      Replicate_Do_Domain_Ids: 
  Replicate_Ignore_Domain_Ids: 
                Parallel_Mode: conservative
1 row in set (0.02 sec)
ERROR: No query specified
MariaDB [(none)]> 

we can see in above o/p the paramter "Slave_IO_State: Waiting for master to send event"
