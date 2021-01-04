#############################################################################################
# Base container of Cloudera CDH 6, so don't use it directly.
# - academysemantix/cdh-namenode : HDFS namenode and a secondarynamenode
# - academysemantix/cdh-yarnmaster : Yarn ResourceManager 
#	and a MapReduce HistoryServer
# - academysemantix/cdh-datanode : HDFS datanode and a Yarn NodeManager
# - academysemantix/cdh-edgenode : Client container to HDFS/Yarn cluster
############################################################################################
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