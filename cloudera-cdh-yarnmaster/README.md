# cloudera-cdh-yarnmaster

Image with Cloudera CDH 7

This container running Resource Manager and History Server

Services start with supervisor:
 - Resource Manager
 - History Server

Ports:
 - Resource Manager: 8032
 - History Server: 8080

Logs:
 - Resource Manager: /var/log/hadoop-yarn
 - History Server: /var/log/hadoop-mapreduce

Cluster architecture:
- academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
- academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
- academysemantix/cdh-yarnmaster: Resource Manager and the History Server
- academysemantix/cdh-edgenode: Edge Node, with Hadoop client : hdfs, yarn, mapreduce v2, hive, spark, sqoop

**Running the container**
```
docker pull academysemantix/cdh-yarnmaster
docker run -d -p 8032:8032 -p 8088:8088 academysemantix/cdh-yarnmaster
```

**Running the cluster**

Documentation: https://hub.docker.com/r/academysemantix/cdh-edgenode/