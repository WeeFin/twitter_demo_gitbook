---
description: All-in-one (data extraction to visualization) pipeline starting routine
---

# Pipelines

{% hint style="info" %}
The platform must be up and running before starting any pipeline
{% endhint %}

## Pipeline 1

![Pipeline 1](../.gitbook/assets/story1.png)

### Configuration

All fields in `config/pipeline1.cfg` must be set:

* `trackedKeywords`: A comma-separated list of keywords to track which will be used to determine what Tweets will be delivered on the stream. See [track](https://developer.twitter.com/en/docs/tweets/filter-realtime/guides/basic-stream-parameters) for more informations
* `classificationFile`: The absolute path to a `.csv` file used to append a Label to each Tweet. The file must have the following structure: _term, label, weight._
  * _term_: the term to track \(case-insensitive\)
  * _label_: the label to associate with the tracked term
  * _weight_: the relative weight of the term. Used when determining the main label of a Tweet; Defaults to 1.

### Index creation

Simply run the following command in a terminal to create the index.

```bash
curl -XPUT 'http://localhost:9200/pipeline1_rich_tweets' -H'Content-Type: application/json' -d '{
 "mappings": {
  "doc": {
   "properties": {
    "confidence": {
     "type": "float"
    },
    "classification": {
     "type": "keyword"
    },
    "entity": {
     "properties": {
      "created_at": {
       "type": "date",
       "format": "EEE MMM dd HH:mm:ss Z yyyy"
      },
      "favorite_count": {
       "type": "long"
      },
      "hashtags": {
       "type": "keyword"
      },
      "id": {
       "type": "long"
      },
      "lang": {
       "type": "keyword"
      },
      "message": {
       "type": "text"
      },
      "quoted_status": {
       "properties": {
        "created_at": {
         "type": "date",
         "format": "EEE MMM dd HH:mm:ss Z yyyy"
        },
        "favorite_count": {
         "type": "long"
        },
        "hashtags": {
         "type": "keyword"
        },
        "id": {
         "type": "long"
        },
        "lang": {
         "type": "keyword"
        },
        "retweet_count": {
         "type": "long"
        },
        "text": {
         "type": "text"
        },
        "user": {
         "properties": {
          "created_at": {
           "type": "date",
           "format": "EEE MMM dd HH:mm:ss Z yyyy"
          },
          "description": {
           "type": "text"
          },
          "followers_count": {
           "type": "long"
          },
          "id": {
           "type": "long"
          },
          "name": {
           "type": "keyword"
          },
          "screen_name": {
           "type": "keyword"
          },
          "statuses_count": {
           "type": "long"
          }
         }
        }
       }
      },
      "retweet_count": {
       "type": "long"
      },
      "retweeted_status": {
       "properties": {
        "created_at": {
         "type": "date",
         "format": "EEE MMM dd HH:mm:ss Z yyyy"
        },
        "favorite_count": {
         "type": "long"
        },
        "hashtags": {
         "type": "keyword"
        },
        "id": {
         "type": "long"
        },
        "lang": {
         "type": "keyword"
        },
        "quoted_status": {
         "properties": {
          "created_at": {
           "type": "date",
           "format": "EEE MMM dd HH:mm:ss Z yyyy"
          },
          "favorite_count": {
           "type": "long"
          },
          "hashtags": {
           "type": "keyword"
          },
          "id": {
           "type": "long"
          },
          "lang": {
           "type": "keyword"
          },
          "retweet_count": {
           "type": "long"
          },
          "text": {
           "type": "text"
          },
          "user": {
           "properties": {
            "created_at": {
             "type": "date",
             "format": "EEE MMM dd HH:mm:ss Z yyyy"
            },
            "description": {
             "type": "text"
            },
            "followers_count": {
             "type": "long"
            },
            "id": {
             "type": "long"
            },
            "name": {
             "type": "keyword"
            },
            "screen_name": {
             "type": "keyword"
            },
            "statuses_count": {
             "type": "long"
            }
           }
          }
         }
        },
        "retweet_count": {
         "type": "long"
        },
        "text": {
         "type": "text"
        },
        "user": {
         "properties": {
          "created_at": {
           "type": "date",
           "format": "EEE MMM dd HH:mm:ss Z yyyy"
          },
          "description": {
           "type": "text"
          },
          "followers_count": {
           "type": "long"
          },
          "id": {
           "type": "long"
          },
          "name": {
           "type": "keyword"
          },
          "screen_name": {
           "type": "keyword"
          },
          "statuses_count": {
           "type": "long"
          }
         }
        }
       }
      },
      "text": {
       "type": "text"
      },
      "user": {
       "properties": {
        "created_at": {
         "type": "date",
         "format": "EEE MMM dd HH:mm:ss Z yyyy"
        },
        "description": {
         "type": "text"
        },
        "followers_count": {
         "type": "long"
        },
        "id": {
         "type": "long"
        },
        "name": {
         "type": "keyword"
        },
        "screen_name": {
         "type": "keyword"
        },
        "statuses_count": {
         "type": "long"
        }
       }
      }
     }
    }
   }
  }
 }
}'
```

### Dashboard creation

In Kibana front-end (`http://localhost:5601`), navigate to Management > Saved Objects and click Import.
Then select `config/pipeline1.json` file to import.
This should give you access to a new graph in the visualize tab (named `Pipeline 1 - Stream classification repartition`) that will populate as data arrives.

## Pipeline 2

![Pipeline 2](../.gitbook/assets/story3.png)

### Configuration

All fields in `config/pipeline2.cfg` must be set:

* `userIds`: A comma-separated list of user IDs to retrieve historical Tweets from
* `tweetCount`: The number of Tweets to retrieve for each user; cannot exceed 3200
  * See [here](https://developer.twitter.com/en/docs/tweets/timelines/api-reference/get-statuses-user_timeline.html) for more information about the limits
* `queryCount`: The maximum number of requests for each user \(a maximum of 200 Tweets can be served for a single request\)
* `classificationFile`: The absolute path to a `.csv` file used to append a Label to each user. The file must have the following structure: _term, label, weight._
  * _term_: the term to track \(case-insensitive\)
  * _label_: the label to associate with the tracked term
  * _weight_: the relative weight of the term. Used when determining the main label of a Tweet; Defaults to 1.

### Index creation

Simply run the following command in a terminal to create the index.

```bash
curl -XPUT 'http://localhost:9200/pipeline2_rich_tweets' -H'Content-Type: application/json' -d '{
 "mappings": {
  "doc": {
   "properties": {
    "confidence": {
     "type": "float"
    },
    "classification": {
     "type": "keyword"
    },
    "entity": {
     "properties": {
      "created_at": {
       "type": "date",
       "format": "EEE MMM dd HH:mm:ss Z yyyy"
      },
      "favorite_count": {
       "type": "long"
      },
      "hashtags": {
       "type": "keyword"
      },
      "id": {
       "type": "long"
      },
      "lang": {
       "type": "keyword"
      },
      "message": {
       "type": "text"
      },
      "quoted_status": {
       "properties": {
        "created_at": {
         "type": "date",
         "format": "EEE MMM dd HH:mm:ss Z yyyy"
        },
        "favorite_count": {
         "type": "long"
        },
        "hashtags": {
         "type": "keyword"
        },
        "id": {
         "type": "long"
        },
        "lang": {
         "type": "keyword"
        },
        "retweet_count": {
         "type": "long"
        },
        "text": {
         "type": "text"
        },
        "user": {
         "properties": {
          "created_at": {
           "type": "date",
           "format": "EEE MMM dd HH:mm:ss Z yyyy"
          },
          "description": {
           "type": "text"
          },
          "followers_count": {
           "type": "long"
          },
          "id": {
           "type": "long"
          },
          "name": {
           "type": "keyword"
          },
          "screen_name": {
           "type": "keyword"
          },
          "statuses_count": {
           "type": "long"
          }
         }
        }
       }
      },
      "retweet_count": {
       "type": "long"
      },
      "retweeted_status": {
       "properties": {
        "created_at": {
         "type": "date",
         "format": "EEE MMM dd HH:mm:ss Z yyyy"
        },
        "favorite_count": {
         "type": "long"
        },
        "hashtags": {
         "type": "keyword"
        },
        "id": {
         "type": "long"
        },
        "lang": {
         "type": "keyword"
        },
        "quoted_status": {
         "properties": {
          "created_at": {
           "type": "date",
           "format": "EEE MMM dd HH:mm:ss Z yyyy"
          },
          "favorite_count": {
           "type": "long"
          },
          "hashtags": {
           "type": "keyword"
          },
          "id": {
           "type": "long"
          },
          "lang": {
           "type": "keyword"
          },
          "retweet_count": {
           "type": "long"
          },
          "text": {
           "type": "text"
          },
          "user": {
           "properties": {
            "created_at": {
             "type": "date",
             "format": "EEE MMM dd HH:mm:ss Z yyyy"
            },
            "description": {
             "type": "text"
            },
            "followers_count": {
             "type": "long"
            },
            "id": {
             "type": "long"
            },
            "name": {
             "type": "keyword"
            },
            "screen_name": {
             "type": "keyword"
            },
            "statuses_count": {
             "type": "long"
            }
           }
          }
         }
        },
        "retweet_count": {
         "type": "long"
        },
        "text": {
         "type": "text"
        },
        "user": {
         "properties": {
          "created_at": {
           "type": "date",
           "format": "EEE MMM dd HH:mm:ss Z yyyy"
          },
          "description": {
           "type": "text"
          },
          "followers_count": {
           "type": "long"
          },
          "id": {
           "type": "long"
          },
          "name": {
           "type": "keyword"
          },
          "screen_name": {
           "type": "keyword"
          },
          "statuses_count": {
           "type": "long"
          }
         }
        }
       }
      },
      "text": {
       "type": "text"
      },
      "user": {
       "properties": {
        "created_at": {
         "type": "date",
         "format": "EEE MMM dd HH:mm:ss Z yyyy"
        },
        "description": {
         "type": "text"
        },
        "followers_count": {
         "type": "long"
        },
        "id": {
         "type": "long"
        },
        "name": {
         "type": "keyword"
        },
        "screen_name": {
         "type": "keyword"
        },
        "statuses_count": {
         "type": "long"
        }
       }
      }
     }
    }
   }
  }
 }
}'
```

### Dashboard creation

In Kibana front-end (`http://localhost:5601`), navigate to Management > Saved Objects and click Import.
Then select `config/pipeline2.json` file to import.
This should give you access to a new graph in the visualize tab (named `Pipeline 2 - User timeline classification evolution`) that will populate as data arrives.
