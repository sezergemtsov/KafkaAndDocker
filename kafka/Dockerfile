FROM amazoncorretto:11-alpine-jdk

# Version of kafka
ENV KAFKA_VERSION=3.5.0
ENV SCALA_VERSION=2.13

# Set up Kafka environment variables
ENV KAFKA_HOME=/kafka_$SCALA_VERSION-$KAFKA_VERSION
ENV PATH=$PATH:$KAFKA_HOME/bin
ENV KAFKA_CLUSTER_ID=-1
ENV BROKER_ID=1
ENV LISTENERS=PLAINTEXT://:9095,CONTROLLER://:9093
ENV ADVERTIZED_LISTENERS=PLAINTEXT://:9095

# Install bash
RUN apk add --no-cache bash

# Install kafka
RUN wget https://downloads.apache.org/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz && \
    tar -xzf kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz && \
    rm kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz

# Set up the data directory for Kafka logs
RUN mkdir /tmp/kraft-combined-logs

# Set up the entrypoint script to format the storage and start the broker
RUN echo '#!/bin/sh' > /entrypoint.sh && \
    echo 'KAFKA_CLUSTER_ID="$($KAFKA_HOME/bin/kafka-storage.sh random-uuid)"' >> /entrypoint.sh && \
    echo 'kafka-storage.sh format -t $KAFKA_CLUSTER_ID -c $KAFKA_HOME/config/kraft/server.properties' >> /entrypoint.sh && \
    echo 'kafka-server-start.sh $KAFKA_HOME/config/kraft/server.properties --override broker.id=$BROKER_ID --override listeners=$LISTENERS --override advertised.listeners=$ADVERTIZED_LISTENERS' >> /entrypoint.sh && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
