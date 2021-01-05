#############################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh and matthewcmead/docker-cdh
#
# Image with Cloudera CDH 7
# This container is a client Hadoop for HDFS and Yarn/Mapreduce.
# This container aims to be the edge node so the entry point to send files, launch scripts and jobs, etc. to the cluster.
# This container contains the following Hadoop client: hdfs, yarn, mapreduce v2, hive, spark, sqoop.Image with Cloudera CDH 7
#
# Cluster architecture:
# - academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
# - academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
# - academysemantix/cdh-yarnmaster: Resource Manager and the History Server
# - academysemantix/cdh-edgenode : Client container to HDFS/Yarn cluster
#############################################################################################
FROM academysemantix/cdh-base

LABEL MAINTAINER Rodrigo Rebouças <rodrigo.a.reboucas@gmail.com>

#install hive, spark and scoop 
RUN yum -y install hive sqoop spark-core && rm -rf /var/cache/yum/*

#there is an issue with hive, we need to recrete the db
RUN rm -rf /var/lib/hive/metastore/metastore_db
RUN /usr/lib/hive/bin/schematool -dbType derby -initSchema

#create a staging disk to send/get data to/from the cluster
RUN mkdir /staging

VOLUME /staging

#create directory for a user
USER user
WORKDIR /home/user

CMD ["bash"]