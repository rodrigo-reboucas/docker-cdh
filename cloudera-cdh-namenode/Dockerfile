#############################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh
#
# Image with Cloudera CDH 7
# This container running HDFS Namenode and HDFS Secondary Node
#
# Cluster architecture:
# - academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
# - academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
# - academysemantix/cdh-yarnmaster: Resource Manager and the History Server
# - academysemantix/cdh-edgenode : Client container to HDFS/Yarn cluster
#############################################################################################
FROM academysemantix/cdh-base

LABEL MAINTAINER Rodrigo Rebouças <rodrigo.a.reboucas@gmail.com>

#init namenode directory
RUN mkdir -p /hdfs/nm

#install the namenode stuff
RUN yum -y install hadoop-hdfs-namenode && rm -rf /var/cache/yum/*

#format the namenode
RUN hdfs namenode -format

#setup supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#expose namenode port
EXPOSE 8020 9870

#define HDFS volume to enable to persist namenode fsimage between restart
VOLUME /hdfs

#start the supervisor
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
