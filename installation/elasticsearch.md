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

{% hint style="info" %}
Elasticsearch can automatically index new document without their mapping having been specified beforehand, but this is a bad practice as you have no control over what is indexed
{% endhint %}

### Pipeline1\_rich\_tweets

```bash
curl -XPUT 'http://localhost:9200/pipeline1_rich_tweets' -d '{
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

### Pipeline2\_rich\_tweets

```bash
curl -XPUT 'http://localhost:9200/pipeline2_rich_tweets' -d '{
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

### Classified users index

```bash
curl -XPUT 'http://localhost:9200/classified_users' -d '{
 "mappings": {
  "doc": {
   "properties": {
    "classification": {
     "properties": {
      "label": {
       "type": "text"
      },
      "weight": {
       "type": "float"
      }
     }
    },
    "confidence": {
     "type": "float"
    },
    "message": {
     "type": "text"
    },
    "user": {
     "properties": {
      "created_at": {
       "type": "text"
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
       "type": "text"
      },
      "screen_name": {
       "type": "text"
      },
      "statuses_count": {
       "type": "long"
      }
     }
    }
   }
  }
 }
}'
```

