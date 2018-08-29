---
description: Apache Kafka is a distributed message queue
---

# Apache Kafka

## Installation

In your `platform` directory, run:

```bash
wget http://mirror.ibcp.fr/pub/apache/kafka/1.1.0/kafka_2.11-1.1.0.tgz
tar -xzf kafka_2.11-1.1.0.tgz
```

## Setup

In `kafka_2.11-1.1.0/config/server.properties` set:

* `listeners` to `PLAINTEXT://:9092` \(commented by default\)
* `log.dirs` to `/<kafka_home_directory>/kafka-logs`

