FROM tomcat:8.5.82-jdk8-openjdk-slim-buster

MAINTAINER Axiu <itzyx@vip.qq.com>

RUN apt-get update -y && \
	apt-get install -y net-tools && \
	apt-get clean all && \
	rm -rf /var/cache/apt 

ENV TZ PRC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 8080

CMD ["catalina.sh", "run"]
