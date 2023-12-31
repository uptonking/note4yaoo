---
title: lang-java-aot
tags: [aot, compiler, java]
created: 2023-12-31T15:08:21.416Z
modified: 2023-12-31T15:08:38.616Z
---

# lang-java-aot

# guide

# dev

# blogs

## [Diving Deep into the Latest on Project Leyden, Valhalla & Hermes - JVM Weekly vol. 146_202308](https://www.linkedin.com/pulse/diving-deep-latest-project-leyden-valhalla-hermes-jvm-skowro%C5%84ski)

- Leyden moves some of the required optimization processes to earlier stages (like Ahead-of-Time compilation, Application Class Data Sharing time, or Linking), based on the specific program and runtime environment needs.
  - Leyden doesn't solely depend on static transformation. Java currently employs the so-called Tiered Compilation strategy to reach optimal performance. It starts from Level 0, where the JVM starts interpreting bytecode, and applications gradually advance to Level 4, which already utilizes optimized code. 
# discuss
- ## 

- ## 

- ## 

- ## [Static Java (Leyden), GraalVM Native and OpenJDK - Andrew Dinn : java_202112](https://www.reddit.com/r/java/comments/rbarej/static_java_leyden_graalvm_native_and_openjdk/)
- It feels like Leyden is turning into "let's try and reimplement Graal native-image in C++" which is probably not the most useful way to spend time, given that native-image already exists, is years ahead, is open source, by the same company even, and there are plenty of other high priority projects OpenJDK could work on.

- Does someone know how GraalVM JNI (and panama foreign) overhead compare to the JIT version? Is it also possible to more tightly control compiled code like inline asm and better constant folding? I remember annotations for inlining but not much else.
  - There is a sepparate graalvm native image c api, if you want to limit your program to graalvm native image you could use that
