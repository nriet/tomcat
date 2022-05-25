FROM nriet/tomcat:8.5.78-jdk8-openjdk-slim-buster

MAINTAINER Axiu <itzyx@vip.qq.com>

COPY requirements.txt /tmp

RUN apt-get update -y && \
	apt-get install -y python3.7 python3-pip && \
	apt-get clean all && \
	pip3 install -r /tmp/requirements.txt && \
	rm -rf /var/cache/apt 


EXPOSE 8080

CMD ["catalina.sh", "run"]
