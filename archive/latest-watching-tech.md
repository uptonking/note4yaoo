---
title: latest-watching-tech
tags: [latest, watching]
created: 2020-12-31T16:57:15.944Z
modified: 2021-01-04T16:26:14.832Z
---

# latest-watching-tech

# app

# infrastructure

- 202101-平头哥基于安卓开源项目 (AOSP) 实现了对RISC-V架构的支持。
  - 安卓软件栈主要包括系统内核、硬件抽象、运行时、框架层、应用五个层次的近千个软件包，而且其中涉及到处理器架构相关移植工作：本地库支持、ART支持、Linux内核支持、build系统支持四大部分
  - 本地库 
    - 完成 bionic、ART、Clang/LLVM、NDK、VNDK、OpenGL、V8 等软件包的 RISC-V 架构的支持：
    - 为 bionic 添加动态链接、系统调用、浮点数学库支持；
  - ART
    - 基于 ART 实现了 RISC-V 架构的 DEX 实时解释执行、dex2oat、JNI 调用以及 JIT 编译优化，
    - 并且提高 了JAVA程序在 RISC-V 平台上执行的效率。
  - Linux 内核
    - 完善了Clang/LLVM对 Linux 内核的编译支持，修复了 Clang/LLVM 的问题，
    - 将RISC-V 架构的 Linux 内核与安卓系统进行了适配。
  - Build系统
    - 安卓的编译框架主要由 blueprint 和 soong 构成，平头哥整合编译框架、本地方法库、模拟器，应用和服务等一些模块，
    - 实现了 RISC-V 架构对安卓 build 系统的支持。
