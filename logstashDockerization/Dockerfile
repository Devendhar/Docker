FROM ubuntu:17.04
MAINTAINER admin <admin@xyz.com>

#oracle 8 installation
RUN apt-get update && \
	apt-get install -y --no-install-recommends software-properties-common && \
 	add-apt-repository -y ppa:webupd8team/java && \
	apt-get update && \
	(echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) && \
	apt-get install --no-install-recommends -y oracle-java8-installer


ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

ENV LT_PKG_NAME logstash-5.5.2
RUN cd / && wget https://artifacts.elastic.co/downloads/logstash/logstash-5.5.2.tar.gz && tar -xvzf $LT_PKG_NAME.tar.gz && mv /$LT_PKG_NAME /logstash

COPY config/openssl.cnf /etc/ssl/ 
COPY config/jvm.options /logstash/config/ 
COPY config/logstash-filter.conf  /logstash/config/

RUN mkdir -p /etc/pki/tls/certs && mkdir /etc/pki/tls/private && cd /etc/pki/tls && \
	openssl req -config /etc/ssl/openssl.cnf -x509 -days 3650 -batch -nodes -newkey rsa:2048 -keyout private/logstash-forwarder.key -out certs/logstash-forwarder.crt


CMD ["/logstash/bin/logstash", "-f", "/logstash/config/logstash-filter.conf"]

EXPOSE 5044

