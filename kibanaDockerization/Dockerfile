FROM ubuntu:17.04
MAINTAINER admin <admin@xyz.com>

#ENV kibana_pkg kibana-5.5.2
ADD kibana-5.5.2-amd64.deb /

RUN  apt-get update && apt-get install /kibana-5.5.2-amd64.deb


copy kibana.yml /etc/kibana/

ENV PATH /usr/share/kibana/bin:$PATH

CMD ["kibana"]

EXPOSE 5601
