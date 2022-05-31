FROM tomcat:8.5.78-jdk8-openjdk-slim-buster

MAINTAINER Axiu <itzyx@vip.qq.com>

RUN apt-get update -y && \
	apt-get install -y net-tools locales && \
	apt-get clean all && \
	rm -rf /var/cache/apt 

ENV LANG zh_CN.utf8 
ENV TZ PRC
ENV LC_ALL zh_CN.UTF-8

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 8080

CMD ["catalina.sh", "run"]
