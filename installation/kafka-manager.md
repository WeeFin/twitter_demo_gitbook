---
description: Kafka Manager is a browser-based Kafka cluster manager
---

# Kafka Manager

## Installation

In your `platform` directory, run:

```bash
wget https://github.com/yahoo/kafka-manager/archive/1.3.3.17.tar.gz
tar -xzf 1.3.3.17.tar.gz
cd kafka-manager-1.3.3.17
./sbt clean dist
cd ..
unzip -a kafka-manager-1.3.3.17/target/universal/kafka-manager-1.3.3.17.zip
```

## Setup

In `kafka-manager-1.3.3.17/conf/application.conf`, set `kafka-manager.zkhosts` to `"localhost:2181"`

