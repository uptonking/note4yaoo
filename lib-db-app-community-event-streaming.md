---
title: lib-db-app-community-event-streaming
tags: [community, database, events, streaming]
created: 2023-09-17T17:58:24.440Z
modified: 2023-10-27T07:02:42.391Z
---

# lib-db-app-community-event-streaming

# guide

# discuss-stars
- ## 

- ## 

- ## ➿ Any unexpected downsides to offering streaming HTTP API endpoints that serve up eg 100, 000 JSON objects in a go rather than asking users to paginate 100 at a time over 1, 000 requests, assuming efficient implementation of that streaming endpoint? _202106
- https://twitter.com/simonw/status/1405554676993433605
  - [Notes on streaming large API responses](https://simonwillison.net/2021/Jun/25/streaming-large-api-responses/)

- ## Parquet + HTTP range headers = efficient retrieval of just the required columns
- https://twitter.com/gunnarmorling/status/1725414843119710524
  - Nice write-up by @markhneedham (inspired by similar write-up on #DuckDB by @simonw ).
  - [Summing columns in remote Parquet files using ClickHouse | Mark Needham](https://www.markhneedham.com/blog/2023/11/15/clickhouse-summing-columns-remote-files/)

# discuss-stream-db
- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## At WarpStream, we’re betting on the future of data streaming being completely object storage based.
- https://twitter.com/richardartoul/status/1729566466305913166
  - [S3 Express is All You Need - WarpStream](https://www.warpstream.com/blog/s3-express-is-all-you-need)

- ## I think there's a massive opportunity for a standardized cross-platform/language connectors API: 
- https://twitter.com/gunnarmorling/status/1729519342008533238
  - kinda like Kafka Connect, but in a separate process (side car, if you will), with #gRPC API. 
  - Implement each connector once, then use bindings for Kafka, Pulsar, Flink, etc.
- Thinking on this more.. I think KC just needs to be torn apart. Between the in-memory data model and the language-agnostic API you’re talking about. ‘tis the season to disaggregate.
  - Yepp, 💯. Touched on this a while ago. But by now I think things should be taken a step further and such a connector runtime should be not tied to Kafka, or any other specific transport.
- that is kinda like what we have been doing in @ApacheCamel and in particular with #camelk with the KameletBinding/Pipe API
  - Ha, yeah. My memory on Camel details are fading; does it help with splitting up "partitions" across compute nodes? Say, I want to read from a Kafka cluster with 100 topics. Can I set up one Camel connector to split this into tasks running on ten machines, reading ten topics each?
- Ha, yeah. My memory on Camel details are fading; does it help with splitting up "partitions" across compute nodes? Say, I want to read from a Kafka cluster with 100 topics. Can I set up one Camel connector to split this into tasks running on ten machines, reading ten topics each?

- Why gRPC?
  - Just an example, could be anything efficient cross-process really. What others would you have in mind?
- I don't have any preference but I have been thinking a lot about this recently for cross-process or even cross-JVM communication. I see people using Kafka for that use case sometimes but it's super expensive.
- rsocket seems also a great option, in particular the backpressure built-in capabilities

- This is what @daprdev aims at

- ## Extremely annoying fact: Kafka transactional producers and consumers do not offer read-your-writes consistency.
- https://twitter.com/nikhilbenesch/status/1728874132161564986
- The “original sin” is the fact that uncommitted transactions produce real records into the partition, so uncommitted transactions can block future transactional consumers indefinitely in order to preserve read committed isolation.
  - 💯 this. I wish the records would be staged elsewhere and then get stitched into the topic with contiguous offsets at the time of commit. But I guess that would have strained the produce API (i.e., every produced message gets an offset immediately).
- How do you define “read your write” consistency in this context? A read_committed consumer only returns committed records. So you should always read only the committed writes.
  - As Jepsen does! If I produce a message to a topic transactionally, get an ack, then in the same process fetch and read to the high water mark using a read_committed consumer, I’m not guaranteed to see the message I *know* exists.
- You can do it (we have system tests for RYOW in our entirely Kafka-Stream based system), but you need an RPC layer which allows the producer and the consumer to communicate with each other. It only makes sense if you expose an API and use kafka as an implementation detail

- ## Schema drift is inevitable in streaming data. Consciously designed data contracts can encapsulate stream consumers from schema changes.
- https://twitter.com/dunithd/status/1727941660053504454
  - 📝 [“Change Data Capture Breaks Encapsulation”. Does it, though?_202311](https://www.decodable.co/blog/change-data-capture-breaks-encapsulation-does-it-though)

- ## IBM MQ -> RabbitMQ -> Kafka ->Pulsar, How do message queue architectures evolve? 
- https://twitter.com/bytebytego/status/1726861680880304638
- IBM MQ was launched in 1993. It was originally called MQSeries and was renamed WebSphere MQ in 2002. It was renamed to IBM MQ in 2014. 
  - IBM MQ is a very successful product widely used in the financial sector. 
- RabbitMQ architecture differs from IBM MQ and is more similar to Kafka concepts. 
  - The producer publishes a message to an exchange with a specified exchange type. It can be direct, topic, or fanout. The exchange then routes the message into the queues based on different message attributes and the exchange type. The consumers pick up the message accordingly. 
- LinkedIn open sourced Kafka in 2011. Kafka is optimized for writing. 
  - It offers a high-throughput, low-latency platform for handling real-time data feeds. 
  - It provides a unified event log to enable event streaming and is widely used in internet companies. 
- Pulsar, developed originally by Yahoo, is an all-in-one messaging and streaming platform. 
  - Compared with Kafka, Pulsar incorporates many useful features from other products. 
  - Pulsar architecture is more cloud-native, providing better support for cluster scaling and partition migration, etc.
  - There are two layers in Pulsar architecture: the serving layer and the persistent layer. Pulsar natively supports tiered storage, where we can leverage cheaper object storage like AWS S3 to persist messages for a longer term. 

- ## [Yelp rebuilds corrupted Cassandra cluster using its data streaming architecture | Hacker News_202307](https://news.ycombinator.com/item?id=36771331)
- 
- 
- 

- ## 🔥 [Streaming Databases in Real-Time with Kafka, Debezium, and MySQL | Hacker News_201703](https://news.ycombinator.com/item?id=13995648)
- 
- 
- 

- ## Understanding the Differences between Lambda and Kappa Data Processing Architectures for Big Data_202303
- https://twitter.com/moderndatastack/status/1637808211565891584
  - [Data processing architectures — Lambda vs Kappa for Big Data_202303](https://medium.com/towards-data-engineering/data-processing-architectures-lambda-vs-kappa-for-big-data-8cc9a7edeffd)
  - [Modern Data Architecture: An Overview of Lambda and Kappa Architectures_202003](https://www.credera.com/insights/modern-data-architecture-an-overview-of-lambda-and-kappa-architectures)

- Lambda and Kappa are two data processing architectures used to analyze large volumes of data in real time
- Lambda Architecture has three layers  
  - the batch layer, which processes historical data in batches, 
  - the speed layer, which processes real-time data streams in a distributed manner, 
  - and the serving layer, which provides queryable views of the data.
- Kappa Architecture, on the other hand, eliminates the batch layer and processes real-time data using a stream processing system, which stores the data in a database.
- Lambda is ideal for scenarios where historical data analysis is important, while Kappa is perfect for situations where real-time insights are critical.

- ## 🔥 [Queues are Databases (1995) | Hacker News202007](https://news.ycombinator.com/item?id=23727877)
- 
- 
- 
