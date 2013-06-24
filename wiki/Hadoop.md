---
title: Hadoop
permalink: wiki/Hadoop/
layout: wiki
---

MapReduce v2 (YARN)
-------------------

MapReduce has undergone a complete overhaul and CDH4 now includes
MapReduce 2.0 (MRv2). The fundamental idea of MRv2's YARN architecture
is to split up the two primary responsibilities of the JobTracker —
resource management and job scheduling/monitoring — into separate
daemons: a global ResourceManager (RM) and per-application
ApplicationMasters (AM). With MRv2, the ResourceManager (RM) and
per-node NodeManagers (NM), form the data-computation framework. The
ResourceManager service effectively replaces the functions of the
JobTracker, and NodeManagers run on slave nodes instead of TaskTracker
daemons. The per-application ApplicationMaster is, in effect, a
framework specific library and is tasked with negotiating resources from
the ResourceManager and working with the NodeManager(s) to execute and
monitor the tasks.

### Running a bundled example

$ hadoop jar /usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar pi
-Dmapreduce.clientfactory.class.name=org.apache.hadoop.mapred.YarnClientFactory
-libjars /usr/lib/hadoop-mapreduce/hadoop-mapreduce-client-jobclient.jar
16 10000

HDFS
----

### Create your home directory

$ hdfs hadoop fs -mkdir /user/<user>
