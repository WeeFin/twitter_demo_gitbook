---
description: >-
  Enrich a user object with classification information depending on his Tweeting history
---

# Classify Users

## Options

* `twitter-source.consumerKey`, `twitter-source.consumerSecret`, `twitter-source.token`, `twitter-source.tokenSecret`: Twitter credentials, can be obtained [here](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens.html)
  * **Required**
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
* `tweetCount`: The number of Tweets to retrieve for each user; cannot exceed 3200
  * _Default_: Maximum \(&lt; 3200\)
  * See [here](https://developer.twitter.com/en/docs/tweets/timelines/api-reference/get-statuses-user_timeline.html) for more information about the limits
* `queryCount`: The maximum number of requests for each user \(a maximum of 200 Tweets can be served for a single request\)
  * _Default_: None \(query while `tweetCount` has not been reached\)


## Usage

```bash
./platform/flink-1.5.0/bin/flink run twitter_demo/processing_examples/classify_users/target/classify_users-0.1.jar  \
    --twitter-source.consumerKey "<key>" \
    --twitter-source.consumerSecret "<secret>" \
    --twitter-source.token "<token>" \
    --twitter-source.tokenSecret "<tokenSecret>" \
    --consumer.bootstrap.servers "<server1[,server2,...]>" \
    --producer.bootstrap.servers "<server1[,server2,...]>" \
    --consumer.group.id "<id>" \
    --consumer.topic.id "<id>" \
    --producer.topic.id "<id>" \
    --classification-file "<path>" \
    --tweet-count "<count>" \
    --query-count "<count>"
```
