---
title: latest-java-jvm
tags: [java, latest]
created: 2019-10-15T12:20:54.755Z
modified: 2020-09-26T12:52:47.994Z
---

# latest-java-jvm

# latest-jvm

- [JetBrains 将 Skia 接入 Java 的 Skija 项目](https://www.zhihu.com/question/430884791/answers/updated)
# openjdk
- 201909-jdk 13 is released
  - ZGC：Uncommit Unused Memory
  - Reimplement the Legacy Socket API
  - Switch Expressions 
  - Text Blocks
  - Dynamic CDS Archives
# js-jvm
- http://git.javadeploy.net/jimsproch/JavaPoly
  - /15Star/MIT/2017
  - JavaPoly.js is a library that polyfills native JVM support in the browser. 
  - It allows you to import your existing Java code, and invoke the code directly from Javascript.

```html
<html>
<!-- Include the Polyfill -->
<script src="https://www.javapoly.com/javapoly.js"></script>

<!-- Write your Java code -->
<script type="text/java">
  package com.demo;
  import com.javapoly.dom.Window;

  public class Greeter
  {
    public static void sayHello(String name)
    {
      Window.alert("Hello " + name + ", from Java!");
    }
  }
</script>

<!-- Invoke your Java code from Javascript -->
<script type="text/javascript">
  com.demo.Greeter.sayHello("world");
</script>

</html>
```

# JVM alternatives to JS
- [JVM alternatives to JS](https://github.com/renatoathaydes/jvm-alternatives-to-js)
  - CheerpJ
  - GWT
  - JSweet
  - TeaVM
  - Vaadin Flow
# discuss
- trending
  - [发现现在流行的Java项目都是中文only了, Java只有中国人在搞了吗？ - 知乎](https://www.zhihu.com/question/360671800/answers/updated)

- ## 

- ## 

- ## 

- ## [Java Native有哪些优缺点？ 哪些公司已经用到生产环境了？ - 知乎](https://www.zhihu.com/question/589712237/answers/updated)
- tomcat这个烂大街的java web服务器已经实现了native化_202307
  - [Apache Tomcat 9 (9.0.78) - Ahead of Time compilation support](https://tomcat.apache.org/tomcat-9.0-doc/graal.html)
  - Tomcat supports using the GraalVM/Mandrel Native Image tool to produce a native binary including the container. 
