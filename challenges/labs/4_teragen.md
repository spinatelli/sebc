# Teragen

```
[donald@ip-10-0-1-4 ec2-user]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Dmapreduce.job.maps=6 -Ddfs.block.size=33554432 51200000 tgen51 2m
17/01/27 11:39:28 INFO client.RMProxy: Connecting to ResourceManager at ip-10-0-1-4.eu-central-1.compute.internal/10.0.1.4:8032
17/01/27 11:39:29 INFO terasort.TeraSort: Generating 51200000 using 6
17/01/27 11:39:29 INFO mapreduce.JobSubmitter: number of splits:6
17/01/27 11:39:29 INFO Configuration.deprecation: dfs.block.size is deprecated. Instead, use dfs.blocksize
17/01/27 11:39:29 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1485534725513_0001
17/01/27 11:39:29 INFO impl.YarnClientImpl: Submitted application application_1485534725513_0001
17/01/27 11:39:29 INFO mapreduce.Job: The url to track the job: http://ip-10-0-1-4.eu-central-1.compute.internal:8088/proxy/application_1485534725513_0001/
17/01/27 11:39:29 INFO mapreduce.Job: Running job: job_1485534725513_0001
17/01/27 11:39:35 INFO mapreduce.Job: Job job_1485534725513_0001 running in uber mode : false
17/01/27 11:39:35 INFO mapreduce.Job:  map 0% reduce 0%
17/01/27 11:39:46 INFO mapreduce.Job:  map 5% reduce 0%
17/01/27 11:39:48 INFO mapreduce.Job:  map 15% reduce 0%
17/01/27 11:39:49 INFO mapreduce.Job:  map 16% reduce 0%
17/01/27 11:39:50 INFO mapreduce.Job:  map 25% reduce 0%
17/01/27 11:39:51 INFO mapreduce.Job:  map 27% reduce 0%
17/01/27 11:39:52 INFO mapreduce.Job:  map 28% reduce 0%
17/01/27 11:39:53 INFO mapreduce.Job:  map 32% reduce 0%
17/01/27 11:39:54 INFO mapreduce.Job:  map 34% reduce 0%
17/01/27 11:39:55 INFO mapreduce.Job:  map 35% reduce 0%
17/01/27 11:39:56 INFO mapreduce.Job:  map 38% reduce 0%
17/01/27 11:39:57 INFO mapreduce.Job:  map 40% reduce 0%
17/01/27 11:39:58 INFO mapreduce.Job:  map 41% reduce 0%
17/01/27 11:39:59 INFO mapreduce.Job:  map 44% reduce 0%
17/01/27 11:40:00 INFO mapreduce.Job:  map 46% reduce 0%
17/01/27 11:40:01 INFO mapreduce.Job:  map 48% reduce 0%
17/01/27 11:40:02 INFO mapreduce.Job:  map 51% reduce 0%
17/01/27 11:40:03 INFO mapreduce.Job:  map 53% reduce 0%
17/01/27 11:40:04 INFO mapreduce.Job:  map 55% reduce 0%
17/01/27 11:40:05 INFO mapreduce.Job:  map 58% reduce 0%
17/01/27 11:40:06 INFO mapreduce.Job:  map 60% reduce 0%
17/01/27 11:40:07 INFO mapreduce.Job:  map 61% reduce 0%
17/01/27 11:40:08 INFO mapreduce.Job:  map 64% reduce 0%
17/01/27 11:40:09 INFO mapreduce.Job:  map 67% reduce 0%
17/01/27 11:40:10 INFO mapreduce.Job:  map 68% reduce 0%
17/01/27 11:40:11 INFO mapreduce.Job:  map 71% reduce 0%
17/01/27 11:40:12 INFO mapreduce.Job:  map 73% reduce 0%
17/01/27 11:40:13 INFO mapreduce.Job:  map 75% reduce 0%
17/01/27 11:40:14 INFO mapreduce.Job:  map 78% reduce 0%
17/01/27 11:40:15 INFO mapreduce.Job:  map 80% reduce 0%
17/01/27 11:40:16 INFO mapreduce.Job:  map 82% reduce 0%
17/01/27 11:40:17 INFO mapreduce.Job:  map 84% reduce 0%
17/01/27 11:40:18 INFO mapreduce.Job:  map 87% reduce 0%
17/01/27 11:40:19 INFO mapreduce.Job:  map 88% reduce 0%
17/01/27 11:40:20 INFO mapreduce.Job:  map 91% reduce 0%
17/01/27 11:40:22 INFO mapreduce.Job:  map 93% reduce 0%
17/01/27 11:40:23 INFO mapreduce.Job:  map 96% reduce 0%
17/01/27 11:40:24 INFO mapreduce.Job:  map 97% reduce 0%
17/01/27 11:40:26 INFO mapreduce.Job:  map 100% reduce 0%
17/01/27 11:40:34 INFO mapreduce.Job: Job job_1485534725513_0001 completed successfully
17/01/27 11:40:34 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=737328
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=511
                HDFS: Number of bytes written=5120000000
                HDFS: Number of read operations=24
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=12
        Job Counters
                Launched map tasks=6
                Other local map tasks=6
                Total time spent by all maps in occupied slots (ms)=279307
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=279307
                Total vcore-seconds taken by all map tasks=279307
                Total megabyte-seconds taken by all map tasks=286010368
        Map-Reduce Framework
                Map input records=51200000
                Map output records=51200000
                Input split bytes=511
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=1187
                CPU time spent (ms)=90680
                Physical memory (bytes) snapshot=2337861632
                Virtual memory (bytes) snapshot=16735174656
                Total committed heap usage (bytes)=2189950976
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=109963291816450258
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=5120000000

real    1m8.180s
user    0m6.399s
sys     0m0.251s
```

# `hdfs dfs -ls /user/donald/tgen512m`
```
[donald@ip-10-0-1-4 ec2-user]$ hdfs dfs -ls /user/donald/tgen512m
Found 7 items
-rw-r--r--   3 donald donald          0 2017-01-27 11:40 /user/donald/tgen512m/_SUCCESS
-rw-r--r--   3 donald donald  853333400 2017-01-27 11:40 /user/donald/tgen512m/part-m-00000
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:40 /user/donald/tgen512m/part-m-00001
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:40 /user/donald/tgen512m/part-m-00002
-rw-r--r--   3 donald donald  853333400 2017-01-27 11:40 /user/donald/tgen512m/part-m-00003
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:40 /user/donald/tgen512m/part-m-00004
-rw-r--r--   3 donald donald  853333300 2017-01-27 11:40 /user/donald/tgen512m/part-m-00005
```

# Number of blocks
```
[donald@ip-10-0-1-4 ec2-user]$ hadoop fsck /user/donald/tgen512m
DEPRECATED: Use of this script to execute hdfs command is deprecated.
Instead use the hdfs command for it.

Connecting to namenode via http://ip-10-0-1-4.eu-central-1.compute.internal:50070
FSCK started by donald (auth:SIMPLE) from /10.0.1.4 for path /user/donald/tgen512m at Fri Jan 27 11:41:40 EST 2017
.......Status: HEALTHY
 Total size:    5120000000 B
 Total dirs:    1
 Total files:   7
 Total symlinks:                0
 Total blocks (validated):      156 (avg. block size 32820512 B)
 Minimally replicated blocks:   156 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Fri Jan 27 11:41:40 EST 2017 in 4 milliseconds


The filesystem under path '/user/donald/tgen512m' is HEALTHY
```