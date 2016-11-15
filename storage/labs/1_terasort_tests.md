# Performance tests

Generated 10G of data in `/user/spinatelli/teragen_data_10g`:

```
[spinatelli@ip-172-0-0-4 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.0-1.cdh5.9.0.p0.23/jars/hadoop-examples.jar teragen -Dmapred.map.tasks=4 -Ddfs.block.size=33554432 107374182 /user/spinatelli/teragen_data_10g
16/11/15 06:00:17 INFO Configuration.deprecation: session.id is deprecated. Instead, use dfs.metrics.session-id
16/11/15 06:00:17 INFO jvm.JvmMetrics: Initializing JVM Metrics with processName=JobTracker, sessionId=
16/11/15 06:00:18 INFO terasort.TeraSort: Generating 107374182 using 1
16/11/15 06:00:18 INFO mapreduce.JobSubmitter: number of splits:1
16/11/15 06:00:18 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
16/11/15 06:00:18 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
16/11/15 06:00:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_local2144542687_0001
16/11/15 06:00:18 INFO mapreduce.Job: The url to track the job: http://localhost:8080/
16/11/15 06:00:18 INFO mapreduce.Job: Running job: job_local2144542687_0001
16/11/15 06:00:18 INFO mapred.LocalJobRunner: OutputCommitter set in config null
16/11/15 06:00:18 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 06:00:18 INFO mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter
16/11/15 06:00:18 INFO mapred.LocalJobRunner: Waiting for map tasks
16/11/15 06:00:18 INFO mapred.LocalJobRunner: Starting task: attempt_local2144542687_0001_m_000000_0
16/11/15 06:00:18 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 06:00:18 INFO mapred.Task:  Using ResourceCalculatorProcessTree : [ ]
16/11/15 06:00:18 INFO mapred.MapTask: Processing split: org.apache.hadoop.examples.terasort.TeraGen$RangeInputFormat$RangeInputSplit@4d74a156
16/11/15 06:00:19 INFO mapreduce.Job: Job job_local2144542687_0001 running in uber mode : false
16/11/15 06:00:19 INFO mapreduce.Job:  map 0% reduce 0%
16/11/15 06:00:24 INFO mapred.LocalJobRunner: map > map

<...more output...>

16/11/15 06:02:52 INFO mapreduce.Job:  map 98% reduce 0%
16/11/15 06:02:54 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:54 INFO mapred.Task: Task:attempt_local2144542687_0001_m_000000_0 is done. And is in the process of committing
16/11/15 06:02:54 INFO mapred.LocalJobRunner: map > map
16/11/15 06:02:54 INFO mapred.Task: Task attempt_local2144542687_0001_m_000000_0 is allowed to commit now
16/11/15 06:02:54 INFO output.FileOutputCommitter: Saved output of task 'attempt_local2144542687_0001_m_000000_0' to hdfs://ip-172-0-0-4.eu-central-1.compute.internal:8020/user/spinatelli/teragen_data_10g/_temporary/0/task_local2144542687_0001_m_000000
16/11/15 06:02:54 INFO mapred.LocalJobRunner: map
16/11/15 06:02:54 INFO mapred.Task: Task 'attempt_local2144542687_0001_m_000000_0' done.
16/11/15 06:02:54 INFO mapred.LocalJobRunner: Finishing task: attempt_local2144542687_0001_m_000000_0
16/11/15 06:02:54 INFO mapred.LocalJobRunner: map task executor complete.
16/11/15 06:02:54 INFO mapreduce.Job:  map 100% reduce 0%
16/11/15 06:02:54 INFO mapreduce.Job: Job job_local2144542687_0001 completed successfully
16/11/15 06:02:54 INFO mapreduce.Job: Counters: 21
        File System Counters
                FILE: Number of bytes read=276326
                FILE: Number of bytes written=573007
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=0
                HDFS: Number of bytes written=10737418200
                HDFS: Number of read operations=4
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
        Map-Reduce Framework
                Map input records=107374182
                Map output records=107374182
                Input split bytes=83
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=911
                Total committed heap usage (bytes)=163053568
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=230593859918397906
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=10737418200

real    2m38.893s
user    2m16.977s
sys     0m4.068s
```

Ran `terasort` on that set of data:

```
[spinatelli@ip-172-0-0-4 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.0-1.cdh5.9.0.p0.23/jars/hadoop-examples.jar terasort /user/spinatelli/teradata_data_10g /user/spinatelli/terasort_data_10g
16/11/15 07:24:57 INFO terasort.TeraSort: starting
16/11/15 07:24:58 INFO input.FileInputFormat: Total input paths to process : 1
Spent 197ms computing base-splits.
Spent 7ms computing TeraScheduler splits.
Computing input splits took 205ms
Sampling 10 splits of 320
Making 1 from 100000 sampled records
Computing parititions took 629ms
Spent 836ms computing partitions.
16/11/15 07:24:59 INFO Configuration.deprecation: session.id is deprecated. Instead, use dfs.metrics.session-id
16/11/15 07:24:59 INFO jvm.JvmMetrics: Initializing JVM Metrics with processName=JobTracker, sessionId=
16/11/15 07:24:59 INFO mapreduce.JobSubmitter: number of splits:320
16/11/15 07:24:59 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_local1547391313_0001
16/11/15 07:24:59 INFO mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-spinatelli/mapred/local/14ion.lst
16/11/15 07:24:59 INFO mapred.LocalDistributedCacheManager: Localized hdfs://ip-172-0-0-4.eu-central-1.compute.interlst as file:/tmp/hadoop-spinatelli/mapred/local/1479212699636/_partition.lst
16/11/15 07:24:59 INFO mapreduce.Job: The url to track the job: http://localhost:8080/
16/11/15 07:24:59 INFO mapreduce.Job: Running job: job_local1547391313_0001
16/11/15 07:24:59 INFO mapred.LocalJobRunner: OutputCommitter set in config null
16/11/15 07:24:59 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 07:24:59 INFO mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.mapreduce.lib.output.FileOutputCo
16/11/15 07:24:59 INFO mapred.LocalJobRunner: Starting task: attempt_local1547391313_0001_m_000000_0
16/11/15 07:24:59 INFO mapred.LocalJobRunner: Waiting for map tasks
16/11/15 07:25:00 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 07:25:00 INFO mapred.Task:  Using ResourceCalculatorProcessTree : [ ]
16/11/15 07:25:00 INFO mapred.MapTask: Processing split: hdfs://ip-172-0-0-4.eu-central-1.compute.internal:8020/user
16/11/15 07:25:00 INFO mapred.MapTask: (EQUATOR) 0 kvi 26214396(104857584)
16/11/15 07:25:00 INFO mapred.MapTask: mapreduce.task.io.sort.mb: 100
16/11/15 07:25:00 INFO mapred.MapTask: soft limit at 83886080
16/11/15 07:25:00 INFO mapred.MapTask: bufstart = 0; bufvoid = 104857600
16/11/15 07:25:00 INFO mapred.MapTask: kvstart = 26214396; length = 6553600
16/11/15 07:25:00 INFO mapred.MapTask: Map output collector class = org.apache.hadoop.mapred.MapTask$MapOutputBuffer
16/11/15 07:25:00 INFO mapred.LocalJobRunner:
16/11/15 07:25:00 INFO mapred.MapTask: Starting flush of map output
16/11/15 07:25:00 INFO mapred.MapTask: Spilling map output
16/11/15 07:25:00 INFO mapred.MapTask: bufstart = 0; bufend = 34225590; bufvoid = 104857600
16/11/15 07:25:00 INFO mapred.MapTask: kvstart = 26214396(104857584); kvend = 24872220(99488880); length = 1342177/6
16/11/15 07:25:00 INFO mapreduce.Job: Job job_local1547391313_0001 running in uber mode : false
16/11/15 07:25:00 INFO mapreduce.Job:  map 0% reduce 0%

<.. bunch of output ..>

16/11/15 07:50:42 INFO mapreduce.Job:  map 100% reduce 100%
16/11/15 07:50:45 INFO mapred.LocalJobRunner: reduce > reduce
16/11/15 07:50:45 INFO mapred.Task: Task:attempt_local1537187461_0001_r_000000_0 is done. And is in the process of committing
16/11/15 07:50:45 INFO mapred.LocalJobRunner: reduce > reduce
16/11/15 07:50:45 INFO mapred.Task: Task attempt_local1537187461_0001_r_000000_0 is allowed to commit now
16/11/15 07:50:45 INFO output.FileOutputCommitter: Saved output of task 'attempt_local1537187461_0001_r_000000_0' to hdfs://ip-172-0-0-4.eu-central-1.compute.internal:8020/user/spinatelli/terasort_data_10g/_temporary/0/task_local1537187461_0001_r_000000
16/11/15 07:50:45 INFO mapred.LocalJobRunner: reduce > reduce
16/11/15 07:50:45 INFO mapred.Task: Task 'attempt_local1537187461_0001_r_000000_0' done.
16/11/15 07:50:45 INFO mapred.LocalJobRunner: Finishing task: attempt_local1537187461_0001_r_000000_0
16/11/15 07:50:45 INFO mapred.LocalJobRunner: reduce task executor complete.
16/11/15 07:50:45 INFO mapreduce.Job: Job job_local1537187461_0001 completed successfully
16/11/15 07:50:46 INFO mapreduce.Job: Counters: 35
        File System Counters
                FILE: Number of bytes read=33557881789
                FILE: Number of bytes written=1825729904451
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1737303062200
                HDFS: Number of bytes written=10737418200
                HDFS: Number of read operations=111388
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=644
        Map-Reduce Framework
                Map input records=107374182
                Map output records=107374182
                Map output bytes=10952166564
                Map output materialized bytes=11166916848
                Input split bytes=52800
                Combine input records=0
                Combine output records=0
                Reduce input groups=107374182
                Reduce shuffle bytes=11166916848
                Reduce input records=107374182
                Reduce output records=107374182
                Spilled Records=319438188
                Shuffled Maps =320
                Failed Shuffles=0
                Merged Map outputs=320
                GC time elapsed (ms)=39031
                Total committed heap usage (bytes)=85605220352
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10737418200
        File Output Format Counters
                Bytes Written=10737418200
16/11/15 07:50:46 INFO terasort.TeraSort: done

real    12m41.384s
user    11m54.367s
sys     1m10.719s
```

Validated the output:
```
[spinatelli@ip-172-0-0-4 ~]$ time hadoop jar /opt/cloudera/parcels/CDH-5.9.0-1.cdh5.9.0.p0.23/jars/hadoop-examples.jar teravalidate /user/spinatelli/terasort_data_10g /user/spinatelli/teravalidate_data_10g
16/11/15 07:51:44 INFO Configuration.deprecation: session.id is deprecated. Instead, use dfs.metrics.session-id
16/11/15 07:51:44 INFO jvm.JvmMetrics: Initializing JVM Metrics with processName=JobTracker, sessionId=
16/11/15 07:51:44 INFO input.FileInputFormat: Total input paths to process : 1
Spent 133ms computing base-splits.
Spent 3ms computing TeraScheduler splits.
16/11/15 07:51:44 INFO mapreduce.JobSubmitter: number of splits:1
16/11/15 07:51:44 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_local295849706_0001
16/11/15 07:51:45 INFO mapreduce.Job: The url to track the job: http://localhost:8080/
16/11/15 07:51:45 INFO mapreduce.Job: Running job: job_local295849706_0001
16/11/15 07:51:45 INFO mapred.LocalJobRunner: OutputCommitter set in config null
16/11/15 07:51:45 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 07:51:45 INFO mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.mapreduce.lib.output.FileOutputCommitter
16/11/15 07:51:45 INFO mapred.LocalJobRunner: Waiting for map tasks
16/11/15 07:51:45 INFO mapred.LocalJobRunner: Starting task: attempt_local295849706_0001_m_000000_0
16/11/15 07:51:45 INFO output.FileOutputCommitter: File Output Committer Algorithm version is 1
16/11/15 07:51:45 INFO mapred.Task:  Using ResourceCalculatorProcessTree : [ ]
16/11/15 07:51:45 INFO mapred.MapTask: Processing split: hdfs://ip-172-0-0-4.eu-central-1.compute.internal:8020/user/spinatelli/terasort_data_10g/part-r-00000:0+10737418200
16/11/15 07:51:45 INFO mapred.MapTask: (EQUATOR) 0 kvi 26214396(104857584)
16/11/15 07:51:45 INFO mapred.MapTask: mapreduce.task.io.sort.mb: 100
16/11/15 07:51:45 INFO mapred.MapTask: soft limit at 83886080
16/11/15 07:51:45 INFO mapred.MapTask: bufstart = 0; bufvoid = 104857600
16/11/15 07:51:45 INFO mapred.MapTask: kvstart = 26214396; length = 6553600
16/11/15 07:51:45 INFO mapred.MapTask: Map output collector class = org.apache.hadoop.mapred.MapTask$MapOutputBuffer
16/11/15 07:51:46 INFO mapreduce.Job: Job job_local295849706_0001 running in uber mode : false
16/11/15 07:51:46 INFO mapreduce.Job:  map 0% reduce 0%

<..bunch of output..>

16/11/15 07:53:12 INFO mapred.LocalJobRunner: reduce task executor complete.
16/11/15 07:53:13 INFO mapreduce.Job:  map 100% reduce 100%
16/11/15 07:53:13 INFO mapreduce.Job: Job job_local295849706_0001 completed successfully
16/11/15 07:53:13 INFO mapreduce.Job: Counters: 35
        File System Counters
                FILE: Number of bytes read=553138
                FILE: Number of bytes written=1146065
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=21474836400
                HDFS: Number of bytes written=25
                HDFS: Number of read operations=13
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=4
        Map-Reduce Framework
                Map input records=107374182
                Map output records=3
                Map output bytes=83
                Map output materialized bytes=95
                Input split bytes=166
                Combine input records=0
                Combine output records=0
                Reduce input groups=3
                Reduce shuffle bytes=95
                Reduce input records=3
                Reduce output records=1
                Spilled Records=6
                Shuffled Maps =1
                Failed Shuffles=0
                Merged Map outputs=1
                GC time elapsed (ms)=681
                Total committed heap usage (bytes)=535822336
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10737418200
        File Output Format Counters
                Bytes Written=25

real    1m31.941s
user    1m15.030s
sys     0m9.912s
```