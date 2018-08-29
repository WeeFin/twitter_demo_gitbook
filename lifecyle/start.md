# Platform

## Start script

The `start_platform.sh` script should be all you have to run to \(dirtily\) start everything.

## Stop script

If the platform was started with the previous script it can be stopped by running the `stop_platform.sh` one.

You may still need to throw some `kill -9` here and there…

## Dashboards

With the platform up and running, you have access to:

* Flink dashboard at `http://localhost:8081`
* Kibana dashboard at `http://localhost:5601`
* Cerebro dashboard at `http://localhost:9000`
  * Connect to `http://localhost:9200`
* Kafka Manager dashboard at `http://localhost:9001`
  * The first time, select add cluster and set:
    * A Cluster Name
    * Cluster Zookeeper Hosts to `localhost:2181`
    * Kafka Version to `1.0.0`

