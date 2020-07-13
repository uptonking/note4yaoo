---
title: lang-python
tags: [lang/python]
created: '2019-06-09T05:36:34.221Z'
modified: '2020-07-07T08:10:42.079Z'
---

# lang-python

## python3

## python2

## python并发

- Python是通过一个全局解释器锁GIL（Global Interpreter Lock）来实现线程同步的。当Python程序只有单线程时，并不会启用GIL，而当用户创建了一个thread时，表示要使用多线程，Python解释器就会自动激活GIL，并创建所需要的上下文环境和数据结构
- 线程调度机制将会为线程分配GIL，获取到GIL的线程就能开始执行，而其他线程则必须等待。由于GIL的存在，Python的多线程性能十分低下，无法发挥多核CPU的优势，性能甚至不如单线程。因此如果你想用到多核CPU，一个建议是使用多进程
- 操作系统里面最重要的两个概念是进程和线程，Python中使用的是PyInterpreterState和PyThreadState来表示的

## python解释器

- Python程序运行的原理
  - 执行 `python demo.py` 后，将会启动Python解释器
  - python.exe解释器会将源码中的demo.py编译成一个字节码对象PyCodeObject
    - 将编译结果保存到了pyc文件中，这样下次就不用编译，直接加载到内存
    - .pyc文件是字节码对象(PyCodeObject)在本地磁盘上的表现形式
    - PyCodeObject对象包含了源码中的字符串、常量值以及通过语法解析后编译生成的字节码指令
  - demo.py被编译后，接下来就由Python解释器来执行字节码指令了
  - Python解释器会从编译得到的PyCodeObject对象中依次读入每一条字节码指令，并在当前的上下文环境中执行这条字节码指令

- 解释器
- gc
  - python虚拟机的垃圾回收使用的是引用计数法
    - 频繁更新引用计数会降低运行效率
    - 引用计数无法解决循环引用问题
