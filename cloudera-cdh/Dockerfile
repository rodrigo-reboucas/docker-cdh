#############################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh and matthewcmead/docker-cdh
#
# Base image with Cloudera CDH 7, porpose to make specific CDH containers.
# This container setup a Yarn ResourceManager and a HDFS  MaprReduce 2 HistoryServer.
#
# Cluster architecture:
# - academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
# - academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
# - academysemantix/cdh-yarnmaster: Resource Manager and the History Server
# - academysemantix/cdh-edgenode : Client container to HDFS/Yarn cluster
#############################################################################################
FROM academysemantix/java

LABEL MAINTAINER Rodrigo Rebouças <rodrigo.a.reboucas@gmail.com>

ENV CDH_VER 6.3.2

#copy cloudera CDH repo
COPY cloudera-cdh.repo /etc/yum.repos.d

#Install epel repo because supervisor isn't in the base repo
RUN yum -y install epel-release && rm -rf /var/cache/yum/*

#Install hadoop and supervisor so that the derived images will not be too fat
RUN yum -y install hadoop supervisor &&  rm -rf /var/cache/yum/*

#Add user
RUN yum -y install sudo && rm -rf /var/cache/yum/*
RUN adduser user
RUN mkdir /home/user/bin && chown user:user /home/user/bin
RUN echo 'export PATH=${HOME}/bin:${PATH}' >>/home/user/.bashrc
RUN echo "user ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/user

#copy hadoop conf
COPY config/* /usr/lib/hadoop/etc/hadoop/

#set HADOOP_* environement variables
ENV HADOOP_HOME /usr/lib/hadoop
ENV HADOOP_CONF_DIR /etc/hadoop/conf
ENV HADOOP_COMMON_HOME /usr/lib/hadoop
ENV HADOOP_HDFS_HOME /usr/lib/hadoop-hdfs
ENV HADOOP_YARN_HOME /usr/lib/hadoop-yarn
ENV HADOOP_MAPRED_HOME /usr/lib/hadoop-mapreduce

CMD ["hadoop", "version"]