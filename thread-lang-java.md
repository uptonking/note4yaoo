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

# discuss
- ## 

- ## 

- ## 

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
