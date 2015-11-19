FROM ubuntu:14.04

ENV ACLOCAL_PATH "/usr/share/aclocal"

ENV ACLOCAL_FLAGS "-I /usr/share/aclocal"

ENV ACLOCAL "aclocal -I /usr/share/aclocal"

RUN apt-get update && \
apt-get install -y curl python dh-autoreconf software-properties-common python-software-properties ant

RUN apt-add-repository ppa:webupd8team/java

RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections

RUN apt-get update && \
apt-get install -y --force-yes oracle-java7-installer

RUN curl -fL https://github.com/apache/zookeeper/archive/release-3.4.7-rc0.tar.gz | tar xzf - -C /opt && \
cd /opt/zookeeper-release-3.4.7-rc0 && \
ACLOCAL_PATH="/usr/share/aclocal" ACLOCAL_FLAGS="-I /usr/share/aclocal" ACLOCAL="aclocal -I /usr/share/aclocal" \
ant -Djavac.args="-Xlint -Xmaxwarns 1000" tar || ACLOCAL_PATH="/usr/share/aclocal" ACLOCAL_FLAGS="-I /usr/share/aclocal" ACLOCAL="aclocal -I /usr/share/aclocal" \
ant -Djavac.args="-Xlint -Xmaxwarns 1000" tar && \
mv /opt/zookeeper-release-3.4.7-rc0/build/zookeeper-3.4.7 /opt/zookeeper

VOLUME /tmp/zookeeper

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/zookeeper/bin

CMD ["zkServer.sh", "start-foreground"]
