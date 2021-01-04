# cloudera-cdh-datanode

Image with Cloudera CDH 7

This container running HDFS Datanode and Yarn Node Manager.

Depends:
 - Namenode (academysemantix/cdh-namenode)
 - Resource Manager (academysemantix/cdh-yarnmaster)

Services start with supervisor:
 - Datanode
 - Node Manager

Ports:
 - Datanode: 50020 and 50075
 - Node Manager: 8042

Logs:
 - Datanode: /var/log/hadoop-hdfs
 - NodeManager: /var/log/hadoop-yarn

Cluster architecture:
- academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
- academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
- academysemantix/cdh-yarnmaster: Resource Manager and the History Server
- academysemantix/cdh-edgenode: Edge Node, with Hadoop client : hdfs, yarn, mapreduce v2, hive, spark, sqoop

**Running the container**

```
docker pull academysemantix/cdh-datanode
docker run -d --net hadoop --net-alias datanode1 -h datanode1 --link namenode --link yarnmaster -p 50020:50020 -p 50075:50075 -p 8042:8042 academysemantix/cdh-datanode
```

**Running the cluster**

Documentation: https://hub.docker.com/r/academysemantix/cdh-edgenode/