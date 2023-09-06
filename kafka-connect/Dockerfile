FROM confluentinc/cp-kafka-connect:6.2.0

USER root

RUN yum install unzip -y

ARG DEBEZIUM_VERSION=1.5.0
RUN confluent-hub install --no-prompt debezium/debezium-connector-mysql:$DEBEZIUM_VERSION

ARG KAFKA_JDBC_VERSION=10.0.0
ARG MYSQL_VERSION=8.0.26

# Deploy MySQL JDBC Driver | MySQL Connector
RUN cd /usr/share/java/kafka && \
curl -sO https://repo1.maven.org/maven2/mysql/mysql-connector-java/$MYSQL_VERSION/mysql-connector-java-$MYSQL_VERSION.jar

# Deploy Kafka Connect JDBC | JDBC Sink
RUN mkdir /usr/share/confluent-hub-components/kafka-connect-jdbc && \ 
cd /usr/share/confluent-hub-components/kafka-connect-jdbc && \
curl -sO https://packages.confluent.io/maven/io/confluent/kafka-connect-jdbc/$KAFKA_JDBC_VERSION/kafka-connect-jdbc-$KAFKA_JDBC_VERSION.jar

# Install datetime converter
RUN cd /usr/share/confluent-hub-components && \ 
wget https://github.com/holmofy/debezium-datetime-converter/archive/refs/tags/v1.4.0.Final.zip

RUN cd /usr/share/confluent-hub-components && unzip v1.4.0.Final.zip