# cloudera-cdh

Base image with Cloudera CDH 7, porpose to make specific CDH containers.

This container setup a Yarn ResourceManager and a HDFS  MaprReduce 2 HistoryServer.

Cluster architecture:
- academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
- academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
- academysemantix/cdh-yarnmaster: Resource Manager and the History Server
- academysemantix/cdh-edgenode: Edge Node, with Hadoop client : hdfs, yarn, mapreduce v2, hive, spark, sqoop

**Running the container**
```
docker pull academysemantix/cdh-base
docker run -ti academysemantix/cdh-base
```

**Running the cluster**

Documentation: https://hub.docker.com/r/academysemantix/cdh-edgenode/