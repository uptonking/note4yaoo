---
title: lang-java-community-servlet
tags: [java, servlet]
created: 2024-02-19T05:23:47.730Z
modified: 2024-02-19T05:24:00.064Z
---

# lang-java-community-servlet

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [servlet的本质是什么，它是如何工作的？ - 知乎](https://www.zhihu.com/question/21416727)
- 作用就是为java程序提供一个统一的web应用的规范，方便程序员统一的使用这种规范来编写程序，应用容器可以使用提供的规范来实现自己的特性。
  - 其他内部实现由厂商自己实现，tomcat jetty jboss等等应运而生。面向接口编程
- 一个http请求到来，容器将请求封装成servlet中的request对象，在request中你可以得到所有的http信息，然后你可以取出来操作，最后你再把数据封装成servlet的response对象，应用容器将respose对象解析之后封装成一个http response

- 浏览器发送一个HTTP请求，HTTP请求由Web容器分配给特定的Servlet进行处理，Servlet的本质是一个Java对象，这个对象拥有一系列的方法来处理HTTP请求。常见的方法有doGet()，doPost()等。Web容器中包含了多个Servlet，特定的HTTP请求该由哪一个Servlet来处理是由Web容器中的web.xml来决定的。
