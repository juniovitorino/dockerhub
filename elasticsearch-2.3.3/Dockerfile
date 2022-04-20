FROM ubuntu:20.04
SHELL ["/bin/bash", "-c"]
RUN apt update
RUN apt list --upgradable
RUN apt install -y wget
RUN apt install -y systemd
RUN apt install -y openjdk-8-jre

WORKDIR /tmp

ENV LANG=C.UTF-8
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64/jre

RUN wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/deb/elasticsearch/2.3.3/elasticsearch-2.3.3.deb
RUN dpkg -i elasticsearch-2.3.3.deb
RUN systemctl enable elasticsearch.service

RUN echo "network.host: 0.0.0.0" >> /etc/elasticsearch/elasticsearch.yml
RUN echo "transport.host: localhost" >> /etc/elasticsearch/elasticsearch.yml
RUN echo "transport.tcp.port: 9300" >> /etc/elasticsearch/elasticsearch.yml
RUN echo "http.port: 9200" >> /etc/elasticsearch/elasticsearch.yml

EXPOSE 9200/tcp 9300/tcp

VOLUME [/usr/share/elasticsearch/data]

RUN rm -r elasticsearch-2.3.3.deb

WORKDIR /

CMD service elasticsearch start ; tail -F /var/log/elasticsearch/elasticsearch.log
