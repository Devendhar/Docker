FROM ubuntu:14.04
MAINTAINER admin <admin@xyz.com>

#oracle 8 installation
RUN apt-get update && \
	apt-get install -y --no-install-recommends software-properties-common && \
 	add-apt-repository -y ppa:webupd8team/java && \
	apt-get update && \
	(echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) && \
	apt-get install --no-install-recommends -y oracle-java8-installer
#	apt-get install vi

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle 


#ElasticSearch Installation
#wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.5.2.tar.gz
ENV ES_PKG_NAME elasticsearch-5.5.2
RUN	cd / && \
	wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.5.2.tar.gz && \
	tar -xvzf $ES_PKG_NAME.tar.gz && \
	mv /$ES_PKG_NAME /elasticsearch

COPY config/elasticsearch.yml /elasticsearch/config/
COPY config/jvm.options /elasticsearch/config/

RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000 && \
	chown -R elasticsearch:elasticsearch /elasticsearch

USER elasticsearch


CMD ["/elasticsearch/bin/elasticsearch"]

EXPOSE 9200
EXPOSE 9300
