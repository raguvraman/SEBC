[ragu@instance-1 ~]$ sudo su - hdfs
Last failed login: Thu May 17 03:21:15 UTC 2018 on pts/0
There was 1 failed login attempt since the last successful login.
[hdfs@instance-1 ~]$ hdfs dfs -mkdir /user/precious
[hdfs@instance-1 ~]$ hdfs dfs -put snapshot.txt /user/precious
put: `snapshot.txt': No such file or directory
[hdfs@instance-1 ~]$ ls -lrt
total 0
[hdfs@instance-1 ~]$ vi snapshot.txt
[hdfs@instance-1 ~]$ hdfs dfs -put snapshot.txt /user/precious
[hdfs@instance-1 ~]$ hdfs dfsadmin -allowSnapshot /user/precious
Allowing snaphot on /user/precious succeeded
[hdfs@instance-1 ~]$ hdfs dfs -createSnapshot /user/precious
Created snapshot /user/precious/.snapshot/s20180517-035116.416
[hdfs@instance-1 ~]$ hdfs dfs -ls /user/precious/.snapshot/s20180517-035116.416
Found 1 items
-rw-r--r--   3 hdfs supergroup         17 2018-05-17 03:46 /user/precious/.snapshot/s20180517-035116.416/snapshot.txt
[hdfs@instance-1 ~]$ hdfs dfs -rm -r /user/precious/snapshot.txt
18/05/17 03:55:08 INFO fs.TrashPolicyDefault: Moved: 'hdfs://nameservice1/user/precious/snapshot.txt' to trash at: hdfs://nameservice1/user/hdfs/.Trash/Current/user/precious/snapshot.txt
[hdfs@instance-1 ~]$ hdfs dfs -cp /user/precious/.snapshot/s20180517-035116.416/snapshot.txt /user/precious
[hdfs@instance-1 ~]$ hdfs dfs -ls /user/precious
Found 1 items
-rw-r--r--   3 hdfs supergroup         17 2018-05-17 03:57 /user/precious/snapshot.txt