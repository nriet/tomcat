FROM tomcat:8.5.82-jdk8-openjdk-slim-buster

MAINTAINER Axiu <itzyx@vip.qq.com>

RUN apt-get update -y && \
	apt-get install -y net-tools curl && \
	apt-get clean all && \
	rm -rf /var/cache/apt 

ENV TZ PRC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 8080

CMD ["catalina.sh", "run"]

#docker buildx build --iidfile /tmp/docker-build-push-7uZURm/iidfile --tag ***/restcloud:3.2-slim-buster --metadata-file /tmp/docker-build-push-7uZURm/metadata-file --push slim-buster/.
