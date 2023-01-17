FROM nriet/tomcat:8.5.78-jdk8-openjdk-slim-buster-python3

MAINTAINER Axiu <itzyx@vip.qq.com>
 
COPY requirements.txt ./

COPY app /app

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		gfortran \
	; \
	pip install --no-cache-dir -r requirements.txt \
	rm -rf /var/cache/apt 

EXPOSE 8080

CMD ["catalina.sh", "run"]