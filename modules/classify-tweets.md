---
description: >-
  Enrich a Tweet object with classification information depending on its content
---

# Classify Tweets

## Options

* `consumer.bootstrap.servers`: A comma separated list of Kafka brokers
  * _Default:_ `localhost:9092`
* `consumer.group.id`: The consumer group this process is consuming on behalf of
  * **Required**
* `consumer.topic.id`: The name of the Kafka topic to read from
  * **Required**
* `producer.bootstrap.servers`: A comma separated list of Kafka brokers
  * _Default:_ `localhost:9092`
* `producer.topic.id`: The name of the Kafka topic to write to
  * **Required**
* `classificationFile`: The absolute path to a `.csv` file used to append a Label to each Tweet. The file must have the following structure: _term, label, weight._
  * **Required**

## Usage

```bash
./platform/flink-1.5.0/bin/flink run twitter_demo/processing_examples/classify_tweets/target/classify_tweets-0.1.jar  \
    --consumer.bootstrap.servers "<server1[,server2,...]>" \
    --producer.bootstrap.servers "<server1[,server2,...]>" \
    --consumer.group.id "<id>" \
    --consumer.topic.id "<id>" \
    --producer.topic.id "<id>" \
    --classification-file "<path>"
```
