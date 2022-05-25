FROM nriet/tomcat:8.5.78-jdk8-openjdk-slim-buster

MAINTAINER Axiu <itzyx@vip.qq.com>

RUN apt-get update -y && \
	apt-get install python3.7 && \
	apt-get clean all && \
	rm -rf /var/cache/apt 


EXPOSE 8080

CMD ["catalina.sh", "run"]
