FROM nriet/tomcat:8.5.78-jdk8-openjdk-slim-buster

MAINTAINER Axiu <itzyx@vip.qq.com>

COPY requirements.txt /tmp

RUN apt-get update -y && \
	apt-get install -y python3.7 python3-pip && \
	apt-get clean all && \
	rm -rf /var/cache/apt 
	
RUN pip3 install --no-cache-dir -r /tmp/requirements.txt

EXPOSE 8080

CMD ["catalina.sh", "run"]
