FROM ubuntu:17.04
MAINTAINER admin<admin@xyz.com>

COPY logstash-forwarder.crt /etc/pki/tls/certs/

RUN apt-get update && apt-get -y install wget

RUN cd / && wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-5.5.2-linux-x86_64.tar.gz && \
	tar xvzf filebeat-5.5.2-linux-x86_64.tar.gz && mv filebeat-5.5.2-linux-x86_64 filebeat

COPY filebeat.yml /filebeat/

CMD ["/filebeat/filebeat", "-e", "-c", "/filebeat/filebeat.yml"]

#docker run --link elasticsearch --link logstash -d --name filebeat  devendhar/ubuntufilebeat:17.04
