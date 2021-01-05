#############################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh and matthewcmead/docker-cdh
#
# Image with Cloudera CDH 7
# This container running Resource Manager and History Server
#
# Cluster architecture:
# - academysemantix/cdh-namenode: HDFS Namenode and the HDFS Secondary Node
# - academysemantix/cdh-datanode: HDFS Datanode and the Node Manager
# - academysemantix/cdh-yarnmaster: Resource Manager and the History Server
# - academysemantix/cdh-edgenode : Client container to HDFS/Yarn cluster
#############################################################################################
FROM academysemantix/cdh-base

LABEL MAINTAINER Rodrigo Rebouças <rodrigo.a.reboucas@gmail.com>

#setup supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#expose ressourcemanager port
EXPOSE 8032 8088 19888

#start the supervisor
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
