FROM registry.access.redhat.com/ubi8/openjdk-8:1.14-14.1675788284
MAINTAINER pader "huangmnlove@163.com"

USER root
# set environment
ENV MODE="cluster" \
    PREFER_HOST_MODE="ip"\
    BASE_DIR="/home/nacos" \
    CLASSPATH=".:/home/nacos/conf:$CLASSPATH" \
    CLUSTER_CONF="/home/nacos/conf/cluster.conf" \
    FUNCTION_MODE="all" \
    JAVA_HOME="/usr/lib/jvm/java-1.8.0" \
    NACOS_USER="nacos" \
    JAVA="/usr/lib/jvm/java-1.8.0/bin/java" \
    JVM_XMS="1g" \
    JVM_XMX="1g" \
    JVM_XMN="512m" \
    JVM_MS="128m" \
    JVM_MMS="320m" \
    NACOS_DEBUG="n" \
    TOMCAT_ACCESSLOG_ENABLED="false" \
    TIME_ZONE="Asia/Shanghai"

ARG NACOS_VERSION=2.2.0
ARG HOT_FIX_FLAG=""

WORKDIR $BASE_DIR

#yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel wget iputils nc vim libcurl
ADD nacos-server-2.2.0.tar.gz /home
RUN rm -rf /home/nacos-server-2.2.0.tar.gz /home/nacos/bin/* /home/nacos/conf/*.properties /home/nacos/conf/*.example /home/nacos/conf/nacos-mysql.sql

#RUN rm -rf /home/nacos/bin/* /home/nacos/conf/*.properties /home/nacos/conf/*.example /home/nacos/conf/nacos-mysql.sql
RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone 

ADD bin/docker-startup.sh bin/docker-startup.sh
ADD conf/application.properties conf/application.properties

# set startup log dir
RUN mkdir -p logs \
	&& cd logs \
	&& touch start.out \
	&& ln -sf /dev/stdout start.out \
	&& ln -sf /dev/stderr start.out
RUN chmod +x bin/docker-startup.sh

EXPOSE 8848
ENTRYPOINT ["bin/docker-startup.sh"]
#ENTRYPOINT ["/bin/bash"]
