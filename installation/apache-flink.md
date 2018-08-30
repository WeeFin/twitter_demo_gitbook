---
description: Apache Flink is a stream processing framework
---

# Apache Flink

## Installation

In your `platform` directory, run:

```bash
wget https://archive.apache.org/dist/flink/flink-1.5.3/flink-1.5.3-bin-scala_2.11.tgz
tar -xzf flink-1.5.3-bin-scala_2.11.tgz
```

## Setup

To be able to run multiple jobs on a local \(one taskmanager\) cluster, set `taskmanager.numberOfTaskSlots: 10` in `flink-1.5.3/conf/fliink-conf.yaml`.

## Log in Kafka

We need to modify some Flink internals to output our logs in a Kafka topic:

First, Change these files:

{% code-tabs %}
{% code-tabs-item title="flink-1.5.3/conf/log4j.properties" %}
```text
log4j.rootLogger=INFO, console

log4j.logger.akka=WARN
log4j.logger.org.apache.kafka=WARN
log4j.logger.org.apache.hadoop=WARN
log4j.logger.org.apache.zookeeper=WARN
log4j.logger.com.weefin=TRACE, kafka
# suppress the warning that hadoop native libraries are not loaded (irrelevant for the client)
log4j.logger.org.apache.hadoop.util.NativeCodeLoader=OFF
# suppress the irrelevant (wrong) warnings from the netty channel handler
log4j.logger.org.apache.flink.shaded.akka.org.jboss.netty.channel.DefaultChannelPipeline=ERROR

log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Target=System.out
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p %-60c %x - %m%n

log4j.appender.kafka=org.apache.kafka.log4jappender.KafkaLog4jAppender
log4j.appender.kafka.brokerList=localhost:9092
log4j.appender.kafka.topic=logs.flink
log4j.appender.kafka.layout=org.apache.log4j.PatternLayout
log4j.appender.kafka.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p %c{1}:%L - %m%n
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="flink-1.5.3/conf/log4j-cli.properties" %}
```text
log4j.rootLogger=INFO, console
log4j.logger.com.weefin=TRACE, kafka
# suppress the warning that hadoop native libraries are not loaded (irrelevant for the client)
log4j.logger.org.apache.hadoop.util.NativeCodeLoader=OFF
# suppress the irrelevant (wrong) warnings from the netty channel handler
log4j.logger.org.apache.flink.shaded.akka.org.jboss.netty.channel.DefaultChannelPipeline=ERROR

log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Target=System.out
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p %-60c %x - %m%n

log4j.appender.kafka=org.apache.kafka.log4jappender.KafkaLog4jAppender
log4j.appender.kafka.brokerList=localhost:9092
log4j.appender.kafka.topic=logs.flink
log4j.appender.kafka.layout=org.apache.log4j.PatternLayout
log4j.appender.kafka.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Then, add the needed dependencies in `flink-1.5.3/lib`:

```bash
cd flink-1.5.3/lib
wget http://central.maven.org/maven2/org/apache/kafka/kafka-log4j-appender/1.1.0/kafka-log4j-appender-1.1.0.jar
wget http://central.maven.org/maven2/org/apache/kafka/kafka-clients/1.1.0/kafka-clients-1.1.0.jar
cd ../..
```
