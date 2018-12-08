FROM java:openjdk-8-jre-alpine

ENV ZOO_USER=zookeeper

ADD https://www-us.apache.org/dist/zookeeper/stable/zookeeper-3.4.12.tar.gz ./zoo.cfg /tmp/

RUN set -ex \ 
    && apk add bash --no-cache \
    && adduser -h /home/${ZOO_USER} -s /bin/bash -D ${ZOO_USER} \
    && cd /tmp \
    && tar xvf zookeeper-3.4.12.tar.gz \
    && mv zookeeper-3.4.12 /home/${ZOO_USER}/zookeeper \
    && mv zoo.cfg /home/${ZOO_USER}/zookeeper/conf/zoo.cfg \
    && rm -rf /tmp/* \
    && mkdir -p /var/zookeeper-data \
    && chown -R ${ZOO_USER} /var/zookeeper-data

USER ${ZOO_USER}
WORKDIR /home/${ZOO_USER}

EXPOSE 2181

ENTRYPOINT ["zookeeper/bin/zkServer.sh", "start-foreground"]