#########################################################################################
# This dockerfile is derived from loicmathieu/cloudera-cdh and will setup an edge node to
# works with the other cloudera containers.
# It also contains some pig/hive script and CSV test files to start with
#
#########################################################################################
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

CMD ["bash"]