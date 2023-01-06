---
title: pick-glossary-cs
tags: [cs, glossary, pick]
created: 2020-07-14T11:39:11.610Z
modified: 2020-08-04T11:47:08.669Z
---

# pick-glossary-cs

- kitchen sink approach 厨房水槽法
  - 包含你能想象出的所有特征，然后再检测到底哪个特征起作用

- monkey patching 猴子补丁    
  - 在运行时动态修改模块、类或函数，通常是添加功能或修正缺陷。
  - 猴子补丁在代码运行时（内存中）发挥作用，不会修改源码，因此只对当前运行的程序实例有效。
  - 因为猴子补丁破坏了封装，而且容易导致程序与补丁代码的实现细节紧密耦合，所以被视为临时的变通方案，不是集成代码的推荐方式。
  - Dynamically changing a module, class or function at run time, usually to add features or fix bugs. 
  - Because it is done in memory and not by changing the source code, a monkey patch only affects the currently running instance of the program. 
  - Monkey patches break encapsulation and tend to be tightly coupled to the implementation details of the patched code units, so they are seen as temporary work-arounds and not a recommended technique for code integration.
