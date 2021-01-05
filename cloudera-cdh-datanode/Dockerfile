#######################################################################################################################
#############################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh and matthewcmead/docker-cdh
#
# Image with Cloudera CDH 7
# This container running HDFS Datanode and Yarn Node Manager.
#
# Cluster architecture:
# - academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
# - academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
# - academysemantix/cdh-yarnmaster: Resource Manager and the History Server
# - academysemantix/cdh-edgenode : Client container to HDFS/Yarn cluster
############################################################################################
FROM academysemantix/cdh-base

LABEL MAINTAINER Rodrigo Rebouças <rodrigo.a.reboucas@gmail.com>

#init datanode directory
RUN mkdir -p /hdfs/data

#setup supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#expose port
EXPOSE 9867 9864 9866 8042

#chown hdfs the datanode data
RUN chown -R hdfs:hadoop /hdfs

#define HDFS volume to enable to persist datanode data (hdfs files) between restart
VOLUME /hdfs

#start the supervisor
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
