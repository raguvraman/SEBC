[hdfs@instance-1 ~]$ time yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar teragen -Dmapred.map.tasks=4 -Ddfs.block.size=33554432 1000000 /user/teragentest
18/05/17 04:02:03 INFO client.RMProxy: Connecting to ResourceManager at instance-1.c.cloudera-204104.internal/10.142.0.2:8032
18/05/17 04:02:04 INFO terasort.TeraGen: Generating 1000000 using 4
18/05/17 04:02:05 INFO mapreduce.JobSubmitter: number of splits:4
18/05/17 04:02:05 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
18/05/17 04:02:05 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
18/05/17 04:02:06 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1526523614318_0001
18/05/17 04:02:07 INFO impl.YarnClientImpl: Submitted application application_1526523614318_0001
18/05/17 04:02:07 INFO mapreduce.Job: The url to track the job: http://instance-1.c.cloudera-204104.internal:8088/proxy/application_1526523614318_0001/
18/05/17 04:02:07 INFO mapreduce.Job: Running job: job_1526523614318_0001
18/05/17 04:02:18 INFO mapreduce.Job: Job job_1526523614318_0001 running in uber mode : false
18/05/17 04:02:18 INFO mapreduce.Job:  map 0% reduce 0%
18/05/17 04:02:28 INFO mapreduce.Job:  map 25% reduce 0%
18/05/17 04:02:29 INFO mapreduce.Job:  map 75% reduce 0%
18/05/17 04:02:32 INFO mapreduce.Job:  map 100% reduce 0%
18/05/17 04:02:37 INFO mapreduce.Job: Job job_1526523614318_0001 completed successfully
18/05/17 04:02:37 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=604600
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=337
                HDFS: Number of bytes written=100000000
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=31338
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=31338
                Total vcore-milliseconds taken by all map tasks=31338
                Total megabyte-milliseconds taken by all map tasks=32090112
        Map-Reduce Framework
                Map input records=1000000
                Map output records=1000000
                Input split bytes=337
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=470
                CPU time spent (ms)=7700
                Physical memory (bytes) snapshot=966029312
                Virtual memory (bytes) snapshot=11181240320
                Total committed heap usage (bytes)=1048576000
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=2148987642402270
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=100000000

real    0m36.317s
user    0m6.467s
sys     0m0.341s
Terasort -
[hdfs@instance-1 ~]$ time yarn jar /opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce/hadoop-examples.jar  terasort  /user/teragentest /user/terasorttest
18/05/17 04:06:12 INFO terasort.TeraSort: starting
18/05/17 04:06:13 INFO input.FileInputFormat: Total input paths to process : 4
Spent 151ms computing base-splits.
Spent 2ms computing TeraScheduler splits.
Computing input splits took 154ms
Sampling 4 splits of 4
Making 6 from 100000 sampled records
Computing parititions took 1696ms
Spent 1852ms computing partitions.
18/05/17 04:06:15 INFO client.RMProxy: Connecting to ResourceManager at instance-1.c.cloudera-204104.internal/10.142.0.2:8032
18/05/17 04:06:17 INFO mapreduce.JobSubmitter: number of splits:4
18/05/17 04:06:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1526523614318_0002
18/05/17 04:06:18 INFO impl.YarnClientImpl: Submitted application application_1526523614318_0002
18/05/17 04:06:18 INFO mapreduce.Job: The url to track the job: http://instance-1.c.cloudera-204104.internal:8088/proxy/application_1526523614318_0002/
18/05/17 04:06:18 INFO mapreduce.Job: Running job: job_1526523614318_0002
18/05/17 04:06:27 INFO mapreduce.Job: Job job_1526523614318_0002 running in uber mode : false
18/05/17 04:06:27 INFO mapreduce.Job:  map 0% reduce 0%
18/05/17 04:06:36 INFO mapreduce.Job:  map 50% reduce 0%
18/05/17 04:06:37 INFO mapreduce.Job:  map 100% reduce 0%
18/05/17 04:06:45 INFO mapreduce.Job:  map 100% reduce 17%
18/05/17 04:06:46 INFO mapreduce.Job:  map 100% reduce 50%
18/05/17 04:06:47 INFO mapreduce.Job:  map 100% reduce 100%
18/05/17 04:06:50 INFO mapreduce.Job: Job job_1526523614318_0002 completed successfully
18/05/17 04:06:51 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=43313803
                FILE: Number of bytes written=88188274
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=100000456
                HDFS: Number of bytes written=100000000
                HDFS: Number of read operations=30
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=12
        Job Counters
                Launched map tasks=4
                Launched reduce tasks=6
                Data-local map tasks=1
                Rack-local map tasks=3
                Total time spent by all maps in occupied slots (ms)=27390
                Total time spent by all reduces in occupied slots (ms)=41618
                Total time spent by all map tasks (ms)=27390
                Total time spent by all reduce tasks (ms)=41618
                Total vcore-milliseconds taken by all map tasks=27390
                Total vcore-milliseconds taken by all reduce tasks=41618
                Total megabyte-milliseconds taken by all map tasks=28047360
                Total megabyte-milliseconds taken by all reduce tasks=42616832
        Map-Reduce Framework
                Map input records=1000000
                Map output records=1000000
                Map output bytes=102000000
                Map output materialized bytes=43347671
                Input split bytes=456
                Combine input records=0
                Combine output records=0
                Reduce input groups=1000000
                Reduce shuffle bytes=43347671
                Reduce input records=1000000
                Reduce output records=1000000
                Spilled Records=2000000
                Shuffled Maps =24
                Failed Shuffles=0
                Merged Map outputs=24
                GC time elapsed (ms)=1310
                CPU time spent (ms)=30330
                Physical memory (bytes) snapshot=3551145984
                Virtual memory (bytes) snapshot=28061380608
                Total committed heap usage (bytes)=3682598912
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=100000000
        File Output Format Counters
                Bytes Written=100000000
18/05/17 04:06:51 INFO terasort.TeraSort: done

real    0m39.201s
user    0m7.500s
sys     0m0.369s
