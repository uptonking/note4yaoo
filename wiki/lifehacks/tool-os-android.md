---
title: tool-os-android
tags: [android, iot, operating-system]
created: 2020-11-25T08:18:17.409Z
modified: 2020-12-22T12:42:09.830Z
---

# tool-os-android

# guide

# android-app-store

## [F-Droid](https://f-droid.org/)

- F-Droid is an installable catalogue of FOSS (Free and Open Source Software) applications for the Android platform. 
- [安卓哥：关于F-Droid , 你需要知道的一切](https://zhuanlan.zhihu.com/p/112633800)
  - F-Droid最大的特点在与其与Linux软件包管理高度吻合，采用的是源安装，即有源有软件，无源无软件，和linux必须添加软件源是一个道理。
  - F-Droid已经有了国内的源，就是[清华大学的开源镜像站点](https://mirrors.tuna.tsinghua.edu.cn/help/fdroid/)。
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
