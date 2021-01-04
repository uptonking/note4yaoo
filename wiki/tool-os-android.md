---
title: tool-os-android
tags: [android, iot, operating-system]
created: '2020-11-25T08:18:17.409Z'
modified: '2020-12-22T12:42:09.830Z'
---

# tool-os-android

# pieces

# Android OS

- Android确实是Linux的一个发行版，Android基于Linux而非GNU/Linux
  - Debian、Ubuntu基于GNU/Linux，它的应用层用的是GNU（glibc，libstdc++、GNU CoreUtils 等等），内核用的是Linux。
  - 而Android的应用层是自己的一套。
- 安卓基于Linux，在改版的Linux kernel上运行了一个改版的JAVA虚拟机，即ART（以前是Dalvik）。
  - 安卓也没有用GNU/Linux的套件，甚至这个kernel都是变种的。
- GNU计划始于1984年，它的最终的目标是完成一套完全自由的操作系统。
  - 到1991年，Linux内核的第一个版本公开发行时，GNU计划已经完成了除操作系统内核之外的大部分软件，
  - 其中包括了Shell程序（Bash），C语言程序库（Glibc）以及一个C语言编译器（GCC）等等。
  - 1992年Linus Torvalds开发了Linux - 一个免费的内核, 将Linux与几乎完成的GNU系统的结合诞生了一个完全的操作系统：一个基于Linux的GNU系统
