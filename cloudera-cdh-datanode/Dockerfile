#######################################################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh and will setup an HDFS datanode
#
# The datanode will expose it's 50020, 50075 and 8042 ports, to use it, you first need to start a namenode
# (using loicmathieu/cloudera-hdfs-namenode) and make sure the netword stack is OK so that the namenode and datanode
# can communicate together
#######################################################################################################################
FROM academysemantix/cdh-base

LABEL MAINTAINER Rodrigo Rebouças <rodrigo.a.reboucas@gmail.com>

#init datanode directory
RUN mkdir -p /hdfs/data

#setup supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#expose port
EXPOSE 9867 9864 9866 8042

#define HDFS volume to enable to persist datanode data (hdfs files) between restart
VOLUME /hdfs

#start the supervisor
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
