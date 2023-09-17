---
title: lib-db-app-community-streaming
tags: [community, database, streaming]
created: 2023-09-17T17:58:24.440Z
modified: 2023-09-17T18:00:17.315Z
---

# lib-db-app-community-streaming

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

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
