FROM java:openjdk-8-jre-alpine

ENV KAFKA_USER=kafka

ADD https://www-us.apache.org/dist/kafka/2.1.0/kafka_2.11-2.1.0.tgz /tmp/

RUN set -ex \ 
    && apk add bash --no-cache \
    && adduser -h /home/${KAFKA_USER} -s /bin/bash -D ${KAFKA_USER} \
    && cd /tmp \
    && tar xvf kafka_2.11-2.1.0.tgz \
    && mv kafka_2.11-2.1.0 /home/${KAFKA_USER}/kafka \
    && mkdir /home/${KAFKA_USER}/kafka/logs \
    && chown -R ${KAFKA_USER} /home/${KAFKA_USER}/kafka/logs \
    && rm -rf /tmp/* 

USER ${KAFKA_USER}
WORKDIR /home/${KAFKA_USER}

EXPOSE 9092

ENTRYPOINT ["kafka/bin/kafka-server-start.sh", "kafka/config/server.properties"]