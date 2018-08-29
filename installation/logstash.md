---
description: >-
  Logstash is a data processing pipeline that ingests data from a multitude of
  sources simultaneously, transforms it, and then sends it to a "stash".
---

# Logstash

## Installation

In your `platform` directory, run:

```bash
wget https://artifacts.elastic.co/downloads/logstash/logstash-6.3.0.tar.gz
tar -xzf logstash-6.3.0.tar.gz
```

## Setup

To run multiple Logstash pipelines in the same process, change the content of `platform/logstash-6.3.0/config/pipelines.yml` to:

```yaml
- pipeline.id: pipeline1_rich_tweets
  path.config: "<PATH_TO_YOUR_PROJECT>/config/pipeline1_rich_tweets.conf"
- pipeline.id: pipeline2_rich_tweets
  path.config: "<PATH_TO_YOUR_PROJECT>/config/pipeline2_rich_tweets.conf"
```

{% hint style="info" %}
When Logstash is run without -f argument, it will look in `pipelines.yml` by default to find the pipelines' configuration files
{% endhint %}

## Add new pipelines

To add a new pipeline, simply create a `.conf` file and set its path in `platform/logstash-6.3.0/config/pipelines.yml`

