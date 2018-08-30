# TODO

* Write unit tests
* Switch to Flink 1.6
  * This would remove the need for Logstash
    * used because of outdated Flink-&gt;ES connector
  * Add a lot of flexibility to index new data that Logstash lacks
* Improve Tweet classification
  * Apply stemming algorithm to keywords
  * Parse links?
* Improve User classification
  * Parse user description
  * Let the user decide how many Tweets are needed to achieve max confidence
* Filter "delete" status updates from twitter\_to\_kafka job
  * Add a flag "--only-posts" to activate this behavior?
* In count\_hashtags job, instead of removing hashtags not in "displayOnly" range, aggregate them in a "\_other" category
  * add a flag --no-other to disable this behavior
