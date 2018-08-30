---
description: 'Elasticsearch is a distributed, RESTful search and analytics engine'
---

# Elasticsearch

## Installation

In your `platform` directory, run:

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.0.tar.gz
tar -xzf elasticsearch-6.3.0.tar.gz
```

## Create indices

Indices creation is documented in their respective pipeline/module section

{% hint style="info" %}
Elasticsearch can automatically index new document without their mapping having been specified beforehand, but this is a bad practice as you have no control over what is indexed
{% endhint %}
