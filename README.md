# Twitter Data Ingestion with Apache Nifi

This project includes building a data pipeline for ingesting data from Twitter with Apache Nifi

## Simplified Architecture

![Social Media Data Ingestion Pipeline High Level Architecture](.gitbook/assets/image%20%281%29.png)

## Step 1 - Connect to Twitter

To be able to connect to Twitter API, you need to have API keys that are provided by Twitter. If you are a student and will use this API for educational purposes, you can apply for a free API to Twitter. For more information please check [https://developer.twitter.com/en/docs/twitter-api](https://developer.twitter.com/en/docs/twitter-api).

* [x] We will use GetTwitter processor to connect to Twitter via API.

![](.gitbook/assets/image%20%282%29.png)

![](.gitbook/assets/image%20%283%29.png)

## Step 2 - Clean & Transform Data

To clean tweet data and extract the desired infoırmation, we will use JoltTransformJson processor.

* [x] Please select JoltTransformJson processor and connect this processor with GetTwitter.

![](.gitbook/assets/image%20%284%29.png)

* [x] Enter the jolt spesification written to extract some fields which are "created\_at" , " id", "text", "source", "user.id", "user.name".

![](.gitbook/assets/image%20%285%29.png)

```text
#Jolt Spesification
[
  {
    "operation": "shift",
    "spec": {
      "created_at": "created_at",
      "id": "tweet_id",
      "text": "text",
      "source": "source",
      "user": {
        "id": "user_id",
        "name": "name"
      }
    }
  }
  ]
```

## Step 3 - Save Data on Filesystem

We will save outputs into a directory on our host.

* [x] Create a directory to save twitter data

```text
mkdir /home/ubuntu/twitter-data
```

* [x] Be sure that the file has proper permissions. \(Nifi should be able to write into this file\)!!
* [x] Select PutFile processor and connect this with JoltTransformJson

![](.gitbook/assets/image%20%286%29.png)



![](.gitbook/assets/image%20%287%29.png)



