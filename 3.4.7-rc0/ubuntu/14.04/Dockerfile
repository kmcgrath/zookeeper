FROM ubuntu:14.04

RUN apt-get update && \
apt-get install -y curl openjdk-7-jre-headless python

# https://www.apache.org/mirrors/dist.html
RUN curl -fL https://github.com/apache/zookeeper/archive/release-3.4.7-rc0.tar.gz | tar xzf - -C /opt && \
mv /opt/zookeeper-release-3.4.7-rc0 /opt/zookeeper

VOLUME /tmp/zookeeper

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/zookeeper/bin

CMD ["zkServer.sh", "start-foreground"]
