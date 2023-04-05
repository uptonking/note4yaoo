---
title: lib-fwk-nodejs-stream
tags: [stream]
created: 2023-04-04T07:22:04.919Z
modified: 2023-04-04T07:22:18.609Z
---

# lib-fwk-nodejs-stream

# guide

# blogs

## [[原]dom sax stax解析xml性能分析](https://www.cnblogs.com/hedalixin/archive/2011/12/04/2275453.html)

- StAX是Streaming API for XML的缩写，是一种针对XML的流式拉分析API。关于对XML进行分析（或解析）的技术，大家一定都不陌生了。
  - 在Java 6.0之前，就已经有四种：    
  1. DOM：Document Object Model   
  2. SAX：Simple API for XML   
  3. JDOM：Java-based Document Object Model   
  4. DOM4J：Document Object Model for Java

- StAX采用流模型中的拉模型分析方式。提供基于指针和基于迭代器两种方式的支持。 
  - 优点： 1、接口简单，使用方便。 2、采用流模型分析方式，有较好的性能。
  - 缺点： 1、单向导航，不支持XPath，很难同时访问同一文档的不同部分。

- 由上面的测试结果可以看出，性能表现最好的是SAX，其次是StAX Stream和StAX Event，DOM和DOM4J也有着不错的表现。性能最差的是JDOM。 

- 所以，如果你的应用程序对性能的要求很高，SAX当然是首选。
  - 如果你需要访问和控制任意数据的功能，DOM是个很好的选择，而对Java开发人员来讲，DOM4J是更好的选择。 
  - 如果只需要做XML文档解析的话，综合性能、易用性、面向对象特征等各方面来衡量，StAX Event无疑是最好的选择。
# more
