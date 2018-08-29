# Changelog



## 28.05.18

* Test twitter API
  * Install **twurl** to simplify twitter queries
  * Install **jq** to prettify Json responses
  * Create a twitter account
  * Create a twitter app
  * Configure twurl authentication
  * Test simple queries
    * `twurl /1.1/statuses/home_timeline.json | jq` to get my own timeline
  * Setup the _Application-only authentication_ to query twitter on the behalf of my app
    * Didn't manage to do it
    * Tried `twurl -d 'grant_type=client_credential' /1.1/oauth2/token.json | jq`
  * Query the last status of _@BittnerPierre_'s timeline
    * `twurl "/1.1/statuses/user_timeline.json?screen_name=BittnerPierre&count=1" | jq`
* Configure **zookeeper**, **kafka** & **flink** locally
* Write a Flink job that receive a twitter stream \(from `/statuses/sample` endpoint\)

> * Twitter gives us access to a lot of information in \(very\) limited quantity for free
> * Twitter documentation took me a long time getting used to
> * Flink documentation is pretty lackluster too in my opinion
> * The infrastructure for the simplest local data pipeline is running and the setup process is documented

## 04.06.18

* Modify the Flink job to accept any endpoint and expose configuration to the user
* Create a Kafka topic
* Modify the Flink job to write raw statuses in the newly created topic
* Install an configure **Elasticsearch** & **Kibana** locally
* Write a Flink job that consume messages from this topic and push them into Elasticsearch

> * I tried to setup a simple pipeline with Flink, Kafka & Elasticsearch to discover the tools \(mainly Flink and Kafka for now\)
> * Read some more documentation
> * Encountered some hardware problems \(~1 day lost\)

## 11.06.18

* Refactor project structure to increase reusability
* Add a Flink job to filter some fields from raw twitter statuses and write them in another Kafka topic
* Discover **Vagrant**
* Discover **Ansible**
* Discover **Packer**

> * Started integrating with a development pipeline made by other interns
>   * Had some problems, going to continue later
> * Been told it wasnt my job to package my application into a VM

## 18.06.18

* Install **cerebro** & **Kafka Manager** to have an overview of the cluster
  * Nodes state
  * Indices/topics list
  * …
* Log properly \(in a Kafka topic\)
* documentation
* roadmap
* **Logstash** to the platform
* kafka\_to\_elastic Flink job by Logstash
  * Offers more flexibility
* utility to extract a stream of hashtag from a stream of status

> * Had trouble to log as I wanted to change logging configuration files
>   * Unclear Flink documentation
>   * Nothing about logging inside distributed jobs
>   * Not possible to have one logger config file per job?
>   * Only possible to pass a config file as argument when starting a flink task manager?
>   * Even there, I have to modify Flink's start script because paths are hardcoded
>   * Better when using dataArtisans platform?
>   * One solution is to start one Task Manager per job \(on Yarn\)
> * Started writing my report

## 25.06.18

* Write the report \(draft due by 29.06 & final version due by 05.07\)
  * Structure/plan mostly done
  * writing 10% done
* Extract hashtags occurrences fluctuations out of a statuses stream
  * Reads from a Kafka topic \(passed as argument\) containing statuses
  * Extract hashtags out of each statuses and generate a message per hashtag \(= 0 or more message for each status\)
  * Filter hashtags depending on a whitelist/blacklist passed as argument
  * Count hashtags occurrences during the last X seconds every Y seconds \(X and Y passed as arguments\)
  * Outputs the Z most frequent hashtags in a given Kafka topic \(Z passed as argument\)
  * _One message is generated every Y seconds, composed of the ordered top Z hashtags contained by the messages published in the last X seconds in the input Kafka topic_
  * _Every hashtag is taken into account: tweet, retweet, quoted tweet_

## 02.07.18

* Finish report
* Make a presentation of the project
  * Slides
  * Objectives
  * Work done
* Create graphical representation of these hashtags \(with Kibana\)
  * Visualise trends through curves \(absolute: \# of occurrences for each hashtag\)
  * Or the relative weight of each hashtag

## 09.07.18

* Abstract twitter JSON result to be worked on easily
  * With twitter4s library, create objects that closely match the Twitter API
* Create new use case
  * geographical representation of Tweet origin with Kibana
  * Simple tweet classification from the contained Hashtags and a list of hard-coded keywords

> * Geographical heat-map idea abandoned as it wasn't in line with the overall goal

## 16.07.18

* Create a Simplified Tweet object
  * Reduced complexity
  * Slightly reduced information
* Create a job to query REST endpoints
  * With twitter4s library

> * Had trouble using twitter4s REST client as it makes use of an Akka version that conflicts with Flink's one
>   * Ended up with a dirty "fix"
> * Also had to resolve resource files conflicting with each other

## 23.07.18

* Refactor Parameters classes to be consistent throughout the project
* Create a job that accepts a list of user ids and dumps the timeline of each user into a Kafka topic

## 30.07.18

* Updated Flink to newer minor version \(1.5.2\)
  * Access new API \(AsyncFunction.timeout\)
* Create a job that classify users depending on their tweeting history
  * Find the most used keywords

## 06.08.18

* Refactor several parts of the project
* Write user stories
* Work on keynote speech

## 13.08.18

* 
