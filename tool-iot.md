---
title: tool-iot
tags: [iot, tool]
created: '2019-08-11T07:36:17.519Z'
modified: '2020-07-14T11:19:07.949Z'
---

# tool-iot

## 设备使用问题

- 强制全家桶
- 乱推送
- 手机管家/安全管家
- 同行和消费者的角度不同

## cross

- 科学上网解决方案
  - 自用vps
    - 太容易被wall
  - 可更换ip的shadowsocks服务
    - 网速不稳定
    - ios商店无法下载proxy

## mobile

- 小米mix alpha环绕屏的使用场景(官方未给出)
  - 应用演示
  - 背面歌词/封面
  - 背部笔记
  - ios widgets

## Ubuntu

- ubuntu的软件生态较为丰富
- 根据UnitsPolicy，文件管理器显示文件的大小基于1KB=1000bytes(SI standard)，而终端ls -lh显示大小基于1KiB=1024bytes(IEC standard), 

## Android

- Android确实是Linux的一个发行版，不同的是，Android基于Linux而非GNU/Linux
- Debian、Ubuntu基于GNU/Linux，它的应用层用的是 GNU（glibc，libstdc++、GNU CoreUtils 等等），内核用的是Linux。而Android的应用层是自己的一套。
- 安卓基于Linux，在改版的Linux kernel上运行了一个改版的JAVA虚拟机，即ART（以前是Dalvik）。安卓也没有用GNU/Linux的套件，甚至这个kernel都是变种的。
- GNU计划始于1984年，它的最终的目标是完成一套完全自由的操作系统。
  - 到1991年，Linux内核的第一个版本公开发行时，GNU计划已经完成了除操作系统内核之外的大部分软件，
  - 其中包括了Shell程序（Bash），C语言程序库（Glibc）以及一个C语言编译器（GCC）等等。
  - 1992年Linus Torvalds开发了Linux - 一个免费的内核, 将Linux与几乎完成的GNU系统的结合诞生了一个完全的操作系统：一个基于Linux的GNU系统

## Fuchsia OS

## 阿里YunOS/AliOS

- 2011年7月28日，阿里巴巴正式推出YunOS，基于linux kernel，设计借鉴了Android
- YunOS兼容Android应用，YunOS的虚拟机还是Dalvik虚拟机修改版
- 魅族支持过YunOS，但坚持使用魅族UI，在一个商业化的操作系统中，核心层并不核心
- YunOS应用在电视盒子上后私自删除用户软件，强迫使用YunOS自带软件
- 改名为AliOS后专注于汽车，与android区别越来越大，linux内核+运行库

## 华为HarmonyOS鸿蒙系统

- 特点：分布架构、高性能、内核安全、生态共享、开源
