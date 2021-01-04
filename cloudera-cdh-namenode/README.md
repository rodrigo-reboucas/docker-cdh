# cloudera-cdh-namenode

Image with Cloudera CDH 7

This container running HDFS Namenode and HDFS Secondary Node

Services start with supervisor:
 - Namenode
 - Secondary Node

Ports:
 - Both: 8020

Logs:
 - Both: /var/log/hadoop-hdfs 

Cluster architecture:
- academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
- academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
- academysemantix/cdh-yarnmaster: Resource Manager and the History Server
- academysemantix/cdh-edgenode: Edge Node, with Hadoop client : hdfs, yarn, mapreduce v2, hive, spark, sqoop

**Running the container**

```
docker pull academysemantix/cdh-namenode
docker run -d -p 8020:8020 academysemantix/cdh-namenode
```

**Running the cluster**

Documentation: https://hub.docker.com/r/academysemantix/cdh-edgenode/