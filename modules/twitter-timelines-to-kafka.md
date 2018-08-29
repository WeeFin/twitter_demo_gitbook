---
description: >-
  Retrieve timelines (historical Tweets) from specified users and push the
  received content to a Kafka topic
---

# Twitter timelines to Kafka

## Options

* `userIds`: A comma-separated list of user IDs to retrieve Tweets from
  * **Required**
* `twitter-source.consumerKey`, `twitter-source.consumerSecret`, `twitter-source.token`, `twitter-source.tokenSecret`: Twitter credentials, can be obtained [here](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens.html)
  * **Required**
* `bootstrap.servers`: A comma separated list of Kafka brokers
  * _Default:_ `localhost:9092`
* `topic.id`: The name of the Kafka topic to write to
  * **Required**
* `tweetCount`: The number of Tweets to retrieve for each user; cannot exceed 3200
  * _Default_: maximum \(&lt; 3200\)
  * See [here](https://developer.twitter.com/en/docs/tweets/timelines/api-reference/get-statuses-user_timeline.html) for more information about the limits
* `queryCount`: The maximum number of requests for each user \(a maximum of 200 Tweets can be served for a single request\)
  * _Default_: None \(query while `tweetCount` has not been reached\)

## Usage

```bash
./platform/flink-1.5.0/bin/flink run twitter_demo/twitter_stream_to_kafka/target/twitter_stream_to_kafka-0.1.jar \
    --uri "<uri>" \
    --http-method "<method>" \
    --twitter-source.consumerKey "<key>" \
    --twitter-source.consumerSecret "<secret>" \
    --twitter-source.token "<token>" \
    --twitter-source.tokenSecret "<tokenSecret>" \
    --bootstrap.servers "<server1[,server2,...]>" \
    --topic.id "<id>"
```

{% hint style="info" %}
This could be achieved with Logstash twitter input plugin too, but would limit configuration options greatly.
{% endhint %}

