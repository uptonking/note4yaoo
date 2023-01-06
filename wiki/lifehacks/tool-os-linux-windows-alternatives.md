---
title: tool-os-linux-windows-alternatives
tags: [alternatives, linux, windows]
created: 2020-01-12T12:32:03.096Z
modified: 2021-01-12T18:49:22.746Z
---

# tool-os-linux-windows-alternatives

# guide

# cygwin vs mingw

- Cygwin is:
  - a large collection of GNU and Open Source tools which provide functionality similar to a Linux distribution on Windows.
  - a DLL (cygwin1.dll) which provides substantial POSIX API functionality.
  - Cygwin则是全面模拟了Linux的接口，提供给运行在它上面的的程序使用，并提供了大量现成的软件，更像是一个平台。

- MinGW是Minimalistic GNU for Windows的缩写，也就是Win版的GCC。
  - MingW也有一个叫MSys（Minimal SYStem）的子项目，主要是提供了一个模拟Linux的Shell和一些基本的Linux工具。
  - 因为编译一个大型程序，光靠一个GCC是不够的，还需要有Autoconf等工具来配置项目，所以一般在Windows下编译ffmpeg等Linux下的大型项目都是通过Msys来完成的，
  - 当然Msys只是一个辅助环境，根本的工作还是MingW来做的。

- ## [Cygwin 和MinGW 的区别与联系是怎样的？](https://www.zhihu.com/question/283946185/answers/updated)
- 从目标上说
  - MinGW 是让Windows用户可以用上GNU工具，比如GCC。
  - Cygwin 提供完整的类Unix环境，Windows用户不仅可以使用GNU工具，理论上Linux上的程序只要用Cygwin重新编译，就可以在Windows上运行。
- 从能力上说
  - 如果程序只用到C/C++标准库，可以用MinGW或Cygwin编译。
  - 如果程序还用到了POSIX API，则只能用Cygwin编译。
- 从依赖上说
  - 程序经MinGW编译后可以直接在Windows上面运行。
  - 程序经Cygwin编译后运行，需要依赖安装时附带的 cygwin1.dll。
  - 如果某软件要在Cygwin上编译，发布给别人，则必须要GPL。
    - 不需要。GCC 编译的产物和 GCC 所在的系统（host）都可以不是 GPL 的。
    - 但Cygwin的底层库需要
- cygwin是在windows下模拟了一套类似UNIX的环境；
  - 在cygwin下编译出来的程序需要cygwin.dll才能在windows下运行，源码拿到linux环境下重新编译就可以在linux下跑起来；
- mingw是将一些UNIX/Linux的系统调用映射成windows下的系统调用，从而使得原来在Linux下编译运行的程序可以在windows下编译运行。
  - mingw环境下编译出来的程序，只能在windows下跑，源码在linux环境下编译多半通不过。
  - linux下也可以编译winsdows可执行文件， 比如fastboot。
- 考虑到你的需求是计算数学和深度学习，
  - 无论是cygwin还是mingw性能都会有所损失，难以达到原生Linux应用的性能，比如常用的文件操作API，mingw编译后性能相比于Linux和Mac原生编译非常差。
  - 所以建议你两种都不使用，而使用clang for windows进行开发，从而达到原生平台的性能，同时支持更高级的语法。
  - 但要注意，clang for windows使用的是windows的系统调用api而不是UNIX/Linux的，可能需要一定的工作量。
- 用MinGW和Cygwin编译出来的程序的区别
  - 首先MinGW和Cygwin都不能让Linux下的程序直接运行在Windows上，必需通过源代码重新编译。
  - win和linux的程序不能兼容，主要是它们对这些功能具体实现上的差异
    - 首先是可执行文件的格式，Window使用PE的格式，并且要求以.EXE为后缀名。Linux则使用Elf的格式。
    - 其次操作系统的API也不一样，如Windows用CreateProcess()创建进程，而Linux使用fork()。
  - MingW有专门的W32api头文件，来把代码中Linux方式的系统调用替换为对应的Windows方式。
  - Cygwin则通过cygwin1.dll这个文件来实现这种API的转换，并模拟一个Linux系统调用接口给程序，
    - 程序依然以Linux的方式调用系统API，只不过这个API在cygwin1.dll上，cygwin1.dll再调用Windows对应的实现，来把结果返回给程序。
  - 简单通俗的理解：
    - 修改编译器,让window下的编译器把诸如fork的调用翻译成等价的形式，这就是MingW的做法。
    - 修改库,让Windows提供一个类似Unix提供的库,他们对程序的接口如同Unix一样,而这些库,当然是由Windows的API实现的，这就是Cygwin的做法。
  - 从性能上来看：
    - 用Mingw编译的程序性能会高一点，而且也不用带着那个接近2M的cygwin1.dll文件。
  - 从Linux环境的模拟完整程度来看：
    - Cygwin对Linux的模拟比较完整，甚至有一个Cygwin X的项目，可以直接用Cygwin跑X。
  - 从使用范围关系来看：
    - Cygwin可以设置-mno-cygwin的flag，来使用Mingw编译。
    - 你细心观察的话，你会发现Cygwin的安装工具包的选项里面有minGW工具
    - 而MinGW的MSys上的工具也是通过Cygwin这种模拟的方式来提供的。
  - 总结
    - MinGW和Cygwin这两个工具的关系，用一个不恰当的比方表示：如果MinGW是MFC，那么Cygwin就是.NET了
