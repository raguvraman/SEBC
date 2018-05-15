    Instance 1 - ClouderaManager and MariaDB Instance, Gateway services for All Hadoop Components.
    Instance 2 - All Master Services - NN,Hiveserever,JHS,Hcatalog
    Instance 3 - All Master Services - RM,SNN,HM,
    Instance 4 -  DN,NM
    Instance 5 -  DN,NM
    Instance 6 -  DN,NM, MariaDB(slave for CM Database HA)

Cluster Installation:
STEP 1 - Preperation #######################################
  
         step a: Update Hostname  for all The hosts
        			hostnamectl set-hostname <Desired hostname for corresponding node> 
                  		ex: hostnamectl set-hostname instance-1.c.trusty-axe-170408.internal
               			Note: I have use the hostnames provided by default by Google.
         step b: Updating Network Config Files
                 b.1) Config File: /etc/sysconfig/network - To update Desired Network config at host level.
           
                      Evidence:
                       [root@instance-1 raguvraman]# cat /etc/sysconfig/network
		                # Created by anaconda
		                NETWORKING=yes
                        HOSTNAME=instance-1.c.trusty-axe-170408.internal  
                        
                           Note: used the default Hostnames and DNS Provided by Google.
                 b.2)  Update /etc/hosts file for hosts look up for Local resolution 
           			[root@instance-1 raguvraman]# cat /etc/hosts
						127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
						::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
						35.231.165.183 metadata.google.internal  # Added by Google
						###### Cloudera Traing Cluster Host Entries#########
						10.142.0.2      instance-1.c.cloudera-204104.internal  instance-1
						10.142.0.3      instance-2.c.cloudera-204104.internal  instance-2
						10.128.0.2      instance-3.c.cloudera-204104.internal  instance-3
						10.128.0.3      instance-4.c.cloudera-204104.internal  instance-4
						10.138.0.2      instance-5.c.cloudera-204104.internal  instance-5
						10.138.0.3      instance-6.c.cloudera-204104.internal  instance-6 
         DNS Lookup Across the cluster:
         			   [root@instance-1 raguvraman]# nslookup instance-6
					    Server:         35.233.232.215
						Address:        35.233.232.215#53
						Non-authoritative answer:
						Name:   instance-6.c.cloudera-204104.internal
						Address: 10.138.0.3
          ntp - Make Sure Time is synchronized to same timezone accross the nodes 
                   
                    Installed NTP and synchronized with UTC Timezone - (took the default timezone provided by google) 
                    [root@instance-1 raguvraman]# ntpq -p
    		         remote           refid      st t when poll reach   delay   offset  jitter
		             ==============================================================================
 		              metadata.google 71.79.79.71      2 u    -   64    1    0.181    0.207   0.108   
          swappiness - Modify the swapness paramters to overcome swapping issues accross the cluster 
                     Swap settings accross the cluster.
                     updated  /etc/sysctl.conf file with vm.swappness=1 
          Hugepage -   disable Transparent Hugepages	
             		 /etc/rc.d/rc.local
             		 echo never > /sys/kernel/mm/transparent_hugepage/enabled
	     			 echo never > /sys/kernel/mm/transparent_hugepage/defrag
    	         	 chmod +x /etc/rc.d/rc.local
    	  selinux - Disable Selinux in all the nodes. 
    	              modified /etc/sysconfig/selinux file with entry selinux=disabled

                        [raguvraman@instance-1 ~]$ cat /etc/sysconfig/selinux 
							# This file controls the state of SELinux on the system.
							# SELINUX= can take one of these three values:
							#     enforcing - SELinux security policy is enforced.
							#     permissive - SELinux prints warnings instead of enforcing.
							#     disabled - No SELinux policy is loaded.
							SELINUX=disabled
							# SELINUXTYPE= can take one of three two values:
							#     targeted - Targeted processes are protected,
							#     minimum - Modification of targeted policy. Only selected processes are protected. 
							#     mls - Multi Level Security protection.
							SELINUXTYPE=targeted 
          firewall - disable Firewall  - later we can enable it and create necessary rules for necesary ports. This is required to avoid known failures during the installation.
                         systemctl stop firewalld 
                         systemctl disable firewalld
          password less - enable Password less authentication between  Cloudera manager host and other hosts in the cluster. 
                 
							## Same thing without a password
							# %wheel        ALL=(ALL)       NOPASSWD: ALL
  							ragu      ALL=(ALL)       NOPASSWD: ALL         


JAVA Installation ###################################################################	         	 
  

 Download the JDK 1.8  rpm from Oracle downloads and did the rpm based installation in all the nodes. 
  rpm -ivh jdk-8u171-linux-x64.rpm and set the JAVA HOME Directory in its default location 
  [root@instance-1 raguvraman]# echo $JAVA_HOME
   /usr/java/jdk1.8.0_161/
    
Clouderamanager  setup ############################################################## 
     
a:  configure the repository for clouderamanager for selected version and Install and setup its database:

         Downloaded https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo and placed it into /etc/yum.repos.d   and install  clouderamanager with below steps.
                a.1 : yum install cloudera-manager-daemons cloudera-manager-server
b: Configure External Database MariaDB as backend database for CM

        				Note: Server version: 5.5.56-MariaDB MariaDB Server
                    
                       Below are the sequence of steps that i have followed.
                 1)  yum install mariadb-server
                 2)  updated /etc/my.cnf file with cloudera recommended configs.
                 3)  Configure mysql_secure_installation and set root password and configure it accroding to cloudera recommendation
                        
                       [root@instance-1 raguvraman]# cat /etc/my.cnf
									[mysqld]
									datadir=/var/lib/mysql
									socket=/var/lib/mysql/mysql.sock
									# Disabling symbolic-links is recommended to prevent assorted security risks
									symbolic-links=0
									# Settings user and group are ignored when systemd is used.
									# If you need to run mysqld under a different user or group,
									# customize your systemd unit file for mariadb according to the
									# instructions in http://fedoraproject.org/wiki/Systemd
									key_buffer = 16M
									key_buffer_size = 32M
									max_allowed_packet = 32M
									thread_stack = 256K
									thread_cache_size = 64
									query_cache_limit = 8M
									query_cache_size = 64M
									query_cache_type = 1
									binlog_format = mixed
									read_buffer_size = 2M
									read_rnd_buffer_size = 16M
									sort_buffer_size = 8M
									join_buffer_size = 8M
									## Updated below Parameters for MariaDB HA####
									log-bin
									server_id=1
									replicate-do-db=scm
									bind-address=10.142.0.2
									# InnoDB settings
									innodb_file_per_table = 1
									innodb_flush_log_at_trx_commit  = 2
									innodb_log_buffer_size = 64M
									innodb_buffer_pool_size = 4G
									innodb_thread_concurrency = 8
									innodb_flush_method = O_DIRECT
									innodb_log_file_size = 512M
									[mysqld_safe]
									log-error=/var/log/mariadb/mariadb.log
									pid-file=/var/run/mariadb/mariadb.pid
									#
									# include all files from the config directory
									#
									!includedir /etc/my.cnf.d
		
            
		 			 b.3.1) Install mysql-connector 
		 			  				 yum install mysql-connector* -y 
		 			  			 Note: This insallation will configure mysql connector and places a respective jar file in /usr/share/java/ directory. this will help All JAVA API to connect with underlying mysql database. 

		 			 b 3.2) Start the MariaDB server:   
                      				 systemctl start mariadb
									 Check - netstat -tulpn | grep 3306
                     b.3.3) Configure mysql_secure_installation using command /usr/bin/mysql_secure_installation as below.
			 						[...]
			 						Enter current password for root (enter for none):
			 						OK, successfully used password, moving on...
			 						[...]
			 						Set root password? [Y/n] y
			 						New password:
			 						Re-enter new password:
			 						[...]
			 						Remove anonymous users? [Y/n] y
									[...]
			 						Disallow root login remotely? [Y/n] n
			 						[...]
			 						Remove test database and access to it [Y/n] y
			 						[...]
			 						Reload privilege tables now? [Y/n] y
 			 						... Success!
                 					

c)  Configure Database for Cloudera manager and start clouderamanager service :

                        1)  configure a temp user in MariaDB  and execute the prepare DB script as below
                                   mysql -u root -p <use root password > and create temp user as below.
                                   mysql> grant all on *.* to 'temp'@'%' identified by 'temp' with grant option;
				  			       Query OK, 0 rows affected (0.00 sec) 
                        2)   use database preparation script to prepare cloudera manager database    
                                   /usr/share/cmf/schema/scm_prepare_database.sh mysql -h instance-1.c.cloudera-204104.internal -utemp -ptemp 
                                                                           --scm-host instance-1.c.cloudera-204104.internal  scm scm scm
                           Output :
		 						Looking for MySQL binary
		 						Looking for schema files in /usr/share/cmf/schema
		 						Verifying that we can write to /etc/cloudera-scm-server
		 						Creating SCM configuration file in /etc/cloudera-scm-server
		 						Executing: /usr/java/jdk1.8.161/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
								[ main] DbCommandExecutor INFO Successfully connected to database.
								All done, your SCM database is configured correctly!
                        
                          Cross validation:
                 				[root@instance-1 raguvraman]# cat /etc/cloudera-scm-server/db.properties
								# Auto-generated by scm_prepare_database.sh on Sat May 12 02:34:37 UTC 2018
								#
								# For information describing how to configure the Cloudera Manager Server
								# to connect to databases, see the "Cloudera Manager Installation Guide."
								#
								com.cloudera.cmf.db.type=mysql
								com.cloudera.cmf.db.host=instance-1.c.trusty-axe-170408.internal
								com.cloudera.cmf.db.name=scm
								com.cloudera.cmf.db.user=scm
								com.cloudera.cmf.db.setupType=EXTERNAL
								com.cloudera.cmf.db.password=scm
                     
d) start clouderamanger server :
                            	systemctl start cloudera-scm-server 
                            	
                           [root@instance-1 opt]# netstat -tulpn| grep 71
							tcp        0      0 0.0.0.0:9996            0.0.0.0:*               LISTEN      4716/java           
							tcp        0      0 0.0.0.0:7180            0.0.0.0:*               LISTEN      6947/java           
							tcp        0      0 10.142.0.2:9997         0.0.0.0:*               LISTEN      4716/java           
							tcp        0      0 0.0.0.0:5678            0.0.0.0:*               LISTEN      4713/java           
							tcp        0      0 0.0.0.0:7182            0.0.0.0:*               LISTEN      6947/java           
							tcp        0      0 0.0.0.0:7184            0.0.0.0:*               LISTEN      4826/java           
							tcp        0      0 0.0.0.0:4433            0.0.0.0:*               LISTEN      11717/python2.7     
							tcp        0      0 0.0.0.0:7185            0.0.0.0:*               LISTEN      4826/java           
							tcp        0      0 0.0.0.0:7186            0.0.0.0:*               LISTEN      4938/java           
							tcp        0      0 0.0.0.0:7187            0.0.0.0:*               LISTEN      4869/java           
							tcp        0      0 10.142.0.2:8083         0.0.0.0:*               LISTEN      4713/java           
							tcp        0      0 127.0.0.1:7190          0.0.0.0:*               LISTEN      11717/python2.7     
							tcp        0      0 10.142.0.2:8086         0.0.0.0:*               LISTEN      4716/java           
							tcp        0      0 0.0.0.0:7191            0.0.0.0:*               LISTEN      11717/python2.7     
							tcp6       0      0 :::4434                 :::*                    LISTEN      11717/python2.7     
							tcp6       0      0 :::7191                 :::*                    LISTEN      11717/python2.7     
							udp        0      0 0.0.0.0:7191            0.0.0.0:*                           11717/python2.7     
							udp6       0      0 :::7191                 :::*                                11717/python2.7

                      e) Login into CLouderamanger web console using the below URL
                              http://<hostname/IP>:7180

                              http://35.231.165.183:7180/cmf/home   userID/PSW : admin/admin
 

                        
4. Installing CLoudera Management service  ########################################################
      
        a ) create database for all respected services:

       Clouderamanagent service includes below list of serivces which are required to access to database to store cluster metrics and other necessary metadata. 
         List of clouderamanagent services:
                    Connect with mysql database with root account. 
                    Command mysql -u root -p 
                        execute the below commands. 
                    Activity Monitor
                         create database amondb DEFAULT CHARACTER SET utf8;
					     grant all on amondb.* TO 'amon'@'%' IDENTIFIED BY 'bigdata';
		    		Reports Manager
                         create database rmandb DEFAULT CHARACTER SET utf8;
                         grant all on rmandb.* TO 'rman'@'%' IDENTIFIED BY 'bigdata';
		            Cloudera Navigator Audit Server
			             create database navdb DEFAULT CHARACTER SET utf8;
			             grant all on navdb.* TO 'nav'@'%' IDENTIFIED BY 'bigdata';
		            Cloudera Navigator Metadata Server 
                         create database navmsdb DEFAULT CHARACTER SET utf8;
		                 grant all on navmsdb.* TO 'navms'@'%' IDENTIFIED BY 'bigdata';

         b ) Login into clouderamanager and Install clouderamanagement service 
