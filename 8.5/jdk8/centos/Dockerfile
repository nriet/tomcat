FROM nriet/openjdk:8-jdk-centos7.9.2009

MAINTAINER Axiu <itzyx@vip.qq.com>

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

ENV TOMCAT_MAJOR 8
ENV TOMCAT_VERSION 8.5.78

RUN yum install -y wget && \
                   yum clean all && \
                   rm -rf /var/cache/yum

RUN wget -q http://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz \
   && tar xvzf apache-tomcat-${TOMCAT_VERSION}.tar.gz -C /usr/local/tomcat --strip-components=1 \
   && rm -f apache-tomcat-${TOMCAT_VERSION}.tar.gz


EXPOSE 8080

CMD ["catalina.sh", "run"]
