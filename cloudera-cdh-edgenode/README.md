# cloudera-cdh-edgenode

Image with Cloudera CDH 7

This container is a client Hadoop for HDFS and Yarn/Mapreduce.

This container aims to be the edge node so the entry point to send files, launch scripts and jobs, etc. to the cluster.

This container contains the following Hadoop client: hdfs, yarn, mapreduce v2, hive, spark, sqoop.

Depends:
 - Namenode (academysemantix/cdh-namenode)
 - Resource Manager (academysemantix/cdh-yarnmaster)

Cluster architecture:
- academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
- academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
- academysemantix/cdh-yarnmaster: Resource Manager and the History Server
- academysemantix/cdh-edgenode: Edge Node, with Hadoop client : hdfs, yarn, mapreduce v2, hive, spark, sqoop

**Running the container**

```
docker pull academysemantix/cdh-edgenode
docker run -d --net hadoop --net-alias edgenode --link namenode --link yarnmaster
academysemantix/cdh-edgenode
```

**Running the cluster**

1. Firsts, create a directory
```
mkdir big_data
cd big_data
```

2. Setup a network for the cluster
```
docker network create hadoop
```

3. Then start the HDFS and Yarn master containers
```
docker run -d --net hadoop --net-alias namenode \
-p 8020:8020 academysemantix/cdh-namenode
docker run -d --net hadoop --net-alias yarnmaster \
-p 8032:8032 -p 8088:8088 academysemantix/cdh-yarnmaster
```

4. Then start a datanode
```
docker run -d --net hadoop --net-alias datanode1 -h datanode1 --link namenode --link yarnmaster \
-p 50020:50020 -p 50075:50075 -p 8042:8042 academysemantix/cdh-datanode
```

5. Finally launch the edge node and connect to it
```
docker run -d --net hadoop --net-alias edgenode --link namenode --link yarnmaster \
academysemantix/cdh-edgenode
docker run -it big_data-edgenode bash
```

**Access Hadoop Client**

**HDFS & MapReduce :**
```
hdfs dfs -mkdir /teste
```

**Hive :**
```
beeline -u jdbc:hive2://
show databases;
```

**Spark (local) :**
```
spark-shell
val t1 = sc.textFile("hdfs:///teste");
t1.count();
exit;
```

**Spark (yarn) :**
```
spark-shell --master yarn
val t1 = sc.textFile("hdfs:///teste");
t1.count();
exit;
```

**Sqoop :**  
It's installed, use it with scoop from the shell ...
