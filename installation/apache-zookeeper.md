---
description: >-
  Apache ZooKeeper is a centralized service for maintaining configuration
  information, naming, providing distributed synchronization, and providing
  group services
---

# Apache ZooKeeper

## Installation

In your `platform` directory, run:

```bash
wget http://mirrors.standaloneinstaller.com/apache/zookeeper/zookeeper-3.4.12/zookeeper-3.4.12.tar.gz
tar -xzf zookeeper-3.4.12.tar.gz
```

## Setup

```bash
mv zookeeper-3.4.12/conf/zoo_sample.cfg zookeeper-3.4.12/conf/zoo.cfg
mkdir zookeeper-3.4.12/data
```

In `zookeeper-3.4.12/conf/zoo.cfg`, set `dataDir` to `/<zookeeper_home_directory>/data`

