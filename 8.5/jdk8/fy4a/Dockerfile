FROM nriet/tomcat:8.5.82-jdk8-openjdk-slim-buster-python3

MAINTAINER Axiu <itzyx@vip.qq.com>
 
COPY app /app

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		gfortran \
	; \
	rm -rf /var/cache/apt 

COPY requirements.txt ./

RUN pip install --no-cache-dir -r requirements.txt

RUN cd /app/fy4a/; \
	f2py -m index2data -c index2data.f90

EXPOSE 8080

CMD ["catalina.sh", "run"]