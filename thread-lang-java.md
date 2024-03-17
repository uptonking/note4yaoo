---
title: thread-lang-java
tags: [java, jvm, lang]
created: 2023-12-14T04:25:01.370Z
modified: 2023-12-15T19:40:39.912Z
---

# thread-lang-java

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-jvm
- ## 

- ## 

- ## JVM Performance Comparison for JDK 21
- https://twitter.com/ionutbalosin/status/1754737482422181973
  - A deep dive into JVM performance comparison where @gigiblender and I explore different optimizations in OpenJDK C2, Oracle GraalVM, and Graal CE JITs
  - TL; DR: Check out the @GraalVM JDK distribution and its JIT compiler if you want some extra performance for your @Java applications
- ### 🆚️⚡️ [JVM Performance Comparison for JDK 21 – Ionut Balosin _202402](https://ionutbalosin.com/2024/02/jvm-performance-comparison-for-jdk-21/)

# discuss-news-java
- ## 

- ## 🐛🍎 An issue introduced by macOS 14.4, which causes Java process to terminate unexpectedly, is affecting all Java versions from Java 8 to the early access builds of JDK 22. _202403
- https://twitter.com/tison1096/status/1769297687046951179
  - [Java users on macOS 14 running on Apple silicon systems should consider delaying the macOS 14.4 update](https://blogs.oracle.com/java/post/java-on-macos-14-4)
- 这个其实不算是java问题，虚拟机的异常处理最后必然要结合宿主机的软硬件中断或系统信号，问题在于苹果系统并不是一个unix完全兼容系统，在发信号这方面完全可以不按标准来。
- 感觉还是因为之前的不合理，但 bug 变 feature 然后有人依赖于这个 feature 了
- 我记得有说法说 Chromium 也在 macOS 上用了不少非公开 API。
- jvm的safe point 也是用保护页实现的

- ## "JEP 467: Markdown Documentation Comments"
- https://twitter.com/gunnarmorling/status/1762719948709806338
  - Yes, finally! Being able to use Markdown in #JavaDoc should make live a bit easier. Can't wait!

# discuss
- ## 

- ## 

- ## 

- ## Why people constantly complain that they don't understand pointers? Pointer is just an index in a global array of bytes that we call "memory". What's the problem?
- https://twitter.com/tsoding/status/1759191261129343058
- I think many people are missing background about computer architecture and more importantly the difference between stack and heap memory areas. 

- ## Hibernate and Debezium both came out of @RedHat
- https://twitter.com/nandini__bagga/status/1756283118632222759
- Hibernate was created externally originally. Then the team joined JBoss who got acquired by Red Hat. 
  - Debezium indeed was kicked off by RHT engineers.
- I've been recently going through Debezium postgres CDC, the fact that it's built on top of Kafka is very interesting to me.

- ## 我对技术的追求就是打死也不用 Java。
- https://twitter.com/syeerzy/status/1748545447919018119
  - 曾经我也这么想，直到遇见一个土豪甲方说必须用Java…
- 甲方说的对，好多场景，成本和应用要求限定了只能用java。
  - 不是，因为对Java他们已经构建了一套完整的自动化发布部署安全审核等的工具和流程，其他技术栈并不方便接进去

- ## Is there any multi-threaded #Java compiler? 
- https://twitter.com/gunnarmorling/status/1747000299447848964
  - `javac` is single-threaded AFAIK, what about others? 
  - Or is parallelization at the module level generally considered good enough?
- Maven seems to be parallel at the module level, as you said. (After some quick googling)
- I believe Eclipse `ecj` has support for it.
  - Been years since I had to care as it "just works" so not sure how much it utilizes/benefits from multiple corese.
- actually -  it might just be thats done at the IDE level not the compiler itself.
- Interesting, after a quick look at that issue it seems ecj itself can use multiple threads. That would be nice.

- ## Tracking Java Native Memory With JDK Flight Recorder
- https://twitter.com/gunnarmorling/status/1736455915627233293
  - JFR has added a few new event types for tracking memory allocations in Java 20/21
- I hope the proposition of @tstuefe of tracking any native allocation via an "preloaded interceptor" lib will be accepted.

- There are no stack traces to find the problematic code if it allocates too much?
  - For on-heap allocations, you can do so using the jdk. ObjectAllocationSample event. E.g. like so with a simple SQL query via JFR Analytics
  - I don't think for off-heap, there's an equivalent. You could instrument the relevant APIs using JMC Agent, though.
