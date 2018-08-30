---
description: >-
  Output an ordered list of hashtags associated with their respective number of
  occurrences in a given time-window
---

# Count Hashtags

## Options

* `consumer.bootstrap.servers` A comma separated list of Kafka brokers
  * _Default:_ `localhost:9092`
* `consumer.group.id` The consumer group this process is consuming on behalf of
  * **Required**
* `consumer.topic.id` The name of the Kafka topic to read from
  * **Required**
* `producer.bootstrap.servers` A comma separated list of Kafka brokers
  * _Default:_ `localhost:9092`
* `producer.topic.id` The name of the Kafka topic to write to
  * **Required**
* `black-list` A comma separated list of hashtags to ignore \(case insensitive\)
  * _Default:_ `""`
* `white-list` A comma separated list of hashtags to count \(case insensitive, has no effect if empty\)
  * _Takes priority over_ `black-list` _if both are non-empty_
  * _Default:_ `""`
* `window-size` The size of the window in seconds
  * _Default:_ `60`
* `window-slide` The frequency of output in seconds
  * _Default:_ `5`
* `display-only` The maximum number of hashtags in a single output
  * _Default:_ `10`
* `min-occurrences` The number of occurrence\(s\) needed in the current time-window for a hashtag to be part of the output
  * _Default:_ `1`

{% hint style="info" %}

* All outputs are lowercase. As Hashtags are case-insensitive, original case cannot be preserved when grouping them together
* In case of equal Hashtags count, the order is undefined as well which ones are retained when `display-only` value is reached
* When the window is empty, no output is generated
* Windows consider processing time when grouping Hashtags together
* The output is not timestamped

{% endhint %}

## Usage

```bash
./platform/flink-1.5.0/bin/flink run twitter_demo/count_hashtags/target/count_hashtags-0.1.jar \
    --consumer.bootstrap.servers "<server1[,server2,...]>" \
    --consumer.group.id "<id>" \
    --consumer.topic.id "<id>" \
    --producer.bootstrap.servers "<server1[,server2,...]>" \
    --producer.topic.id "<id>" \
    --black-list "<word1[,word2,...]>" \
    --white-list "<word1[,word2,...]>" \
    --window-size "<seconds>" \
    --window-slide "<seconds>" \
    --display-only "<count>" \
    --min-occurrences "<count>"
```

### **Example**

Every 5 seconds, display the 5 most used Hashtags withing the last 5 minutes, excluding "yes", "no", "Yes", "NO", …

```bash
./platform/flink-1.5.0/bin/flink run twitter_demo/count_hashtags/target/count_hashtags-0.1.jar \
    --consumer.group.id "group1" \
    --consumer.topic.id "raw_statuses" \
    --producer.topic.id "hashtags_count" \
    --black-list "yes, no" \
    --window-size "300" \
    --display-only "5"
```

## O**utput**

The output is in the form of a JSON array containing one object per counted Hashtag. Each Hashtag object contains two entries:

* `text`, the hashtag text
* `count`, its number of occurrence\(s\) within the current time-window

### Example

```javascript
[{"text":"the","count":12},{"text":"quick","count":4},{"text":"brown","count":3},{"text":"fox","count":2},{"text":"jumps","count":2}]
```
