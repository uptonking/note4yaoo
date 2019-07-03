---
title: log-dev
created: '2019-06-09T15:54:12.063Z'
modified: '2019-07-03T05:37:20.584Z'
tags: [log/dev]
---

# log-dev


- 监听器的使用    
    - 将业务逻辑系统用事件驱动方式拆分，既能使代码逻辑更清晰，又能自主掌控逻辑的同步和异步执行
    - 在业务中很多场景都可以比喻为事件，比如用户注册，可能要求注册之后发送验证信息，或者创建订单之后需要发送订单详情邮件之类的，还有就是批量处理时，可以拆成一个批量输入命令，然后触发一个事件，事件处理一个任务，这个事件触发也可以在接口或者其它地方触发，但是事件监听是同一套，不用做任何修改，如果一块逻辑已经过时，那直接去掉监听即可，代码上可能只需要修改一行即可。

- DNS_PROBE_FINISHED_NXDOMAIN

-  Project 'com.datable:hello-poi:1.0.0' is duplicated in the reactor
原因是父pom.xml指定了多个作为子module，某一个子module 的pom又指定了父 或者 同级 作为自己的子module，导致出现冲突

- 切换jdk版本
   - update-java-alternatives --list
   - update-java-alternatives --set /usr/lib/jvm/java-7-openjdk-amd64

- 删除git commit后不希望版本控制的文件
    - `git rm -r --cached ./datable/.settings`
    
- java 枚举类与switch使用
    - enum switch case label must be the unqualified name of an enumeration constant   
    - switch指定枚举类后，case后只能用枚举类的非限定名，不要再写枚举类了


- junit测试类的方法上使用@Test后，方法名再以test开头会出现问题，如文件无法读取
- junit中方法的执行顺序并不一定按照源码中的书写顺序，如ExcelParserBasicTest类

- app-jcef-example
```
 thread "AWT-EventQueue-0" java.lang.NoSuchMethodError: onScheduleMessagePumpWork
```
maven打包后的main class是 example.simple.CefFrameExample
报错原因可能是cef不同版本的方法不一样

```
java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:target/* example.simple.CefFrameExample
```


- jcef-quickstart

- 运行成功，在任意目录
```
java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:/home/yaoo/Downloads/jcef-quickstart/target/classes  tests.simple.MainFrame
```
- 运行成功，在maven项目根目录
```
java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:lib/jogamp/jar/*:target/classes  tests.simple.MainFrame
```

```
java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:lib/jogamp/jar/*:target/*  tests.simple.MainFrame
```

- 运行失败，core dumped
```
java  -Djava.library.path=lib/native/Release -cp .:lib/jogamp/jar/*:target/classes  tests.simple.MainFrame
```

- jcef自带示例，运行成功，在任意目录均可
```
java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:/home/yaoo/Documents/repo/opensource/java-cef/src/out/linux64 tests.simple.MainFrame
```
 

## jcef build
- error1
    ```
    [ 71%] Linking CXX executable Release/jcef_helper
    /usr/bin/ld: cannot find -lX11
    collect2: error: ld returned 1 exit status
    native/CMakeFiles/jcef_helper.dir/build.make:122: recipe for target 'native/Release/jcef_helper' failed
    make[2]: *** [native/Release/jcef_helper] Error 1
    CMakeFiles/Makefile2:142: recipe for target 'native/CMakeFiles/jcef_helper.dir/all' failed
    make[1]: *** [native/CMakeFiles/jcef_helper.dir/all] Error 2
    Makefile:83: recipe for target 'all' failed
    make: *** [all] Error 2

    ```
    - sudo apt-get install libx11-dev -y

- error2    
    ``` 
    jdk1.8.0_201/include/linux/jawt_md.h:31:10: fatal error: X11/Intrinsic.h: No such file or directory   
    #include <X11/Intrinsic.h>
    ```
-  sudo apt-get install libxt-dev -y
