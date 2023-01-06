---
title: lang-java
tags: [java, lang]
created: 2019-06-09T05:35:12.366Z
modified: 2020-07-14T09:26:35.281Z
---

# lang-java

# 开发通用问题

- 搜索
- 缓存
- 消息
- 日志

# tips

- all in java as backend 
- 若要专注于提高渲染、存储、计算等方面的性能，请参考cpp
- java的优势是既简单又高性能(相对于其他语言)

# java-next

- java panama
  - 项目的目的是让java更加方便滴集成native的类库，比如各种用c/c++提供的api，以前都是使用jni，有一定的局限性，比如需要用户同时了解java和c/c++，巴拿马项目可以根据c的头文件自动生成java的interface，并接入jit，这样用户就可以完全不碰c/c++代码而使用native类库了，应用的经典例子就是opengl

# dev

- 枚举类以后增加枚举值的方式
  - 枚举类只适合做数量确定的元素的事情, 不确定的还是另外设计方法来做吧
  - 既然要动态添加，就不适合用枚举。用xml配置文件，然后解析，是适合这种动态的做法
- java枚举类可以被继承吗
  - Java字节码格式并不禁止继承java.lang. Enum，但javac编译器硬性不让你继承java.lang. Enum
  - 若继承了java.lang. Enum类，则不能继承其他父类；Enum类实现了java.lang. Serializable/Comparable接口；
  - 枚举类与普通类的不同在于，它的构造器私有，这也决定了它如果需要被继承时的特殊性。若其它的外部类A继承它，由于在构造类A的对象时，需要调用父类的构造方法，由于枚举类的构造器私有，所有无法调用，导致枚举类不可以被其它的外部类继承。
  - 但是有没有办法去继承它愣？答案是有的，那就需要用到内部类了(内部类能访问外部类的任何成员，当然能访问已被私有的构造器了)
- 如何获取list中对象的类型
  - 若非空，则list.get(0).getClass()
  - 若为空，则手动传入BeanClass.class
- 使用java反射的 Class.newInstance()创建对象，要求
  - 模型类无构造方法（会使用自动生成的无参构造方法）
  - 或可以显式写出模型类的无参构造方法，若还存在其他构造方法则必须写出无参构造方法
- 使用java命令执行jar包时，不能同时使用 -cp 和 -jar
  - `-jar` the JAR file is the source of all user classes, and other user class path settings are ignored.

- java version manager
  - [jabba](https://github.com/shyiko/jabba) /1.7kStar
    - Java Version Manager inspired by nvm (Node.js). Written in Go.
    - The goal is to provide unified pain-free experience of installing (and switching between different versions of) JDK regardless of the OS
  - [jenv](https://github.com/jenv/jenv) /3.5kStar
    - It lets you switch between java versions.
    - It sets JAVA_HOME inside your shell, in a way that can be set globally, local to the current working directory or per shell.
    - However, this project does not install java for you.
  - [sdkman](https://github.com/sdkman/sdkman-cli) /3.8kStar
    - Formerly known as GVM the Groovy enVironment Manager, it was inspired by the very useful RVM and rbenv tools

# java basics

## oop

- java创建对象的方式
  - new ClassConstructor()
  - Class.newInstance()
  - constructor.newInstance()
  - obj.clone()
  - Deserialization: objectInputStream.readObject()

## java 集合

## java 并发

## jvm

## java 反射

- java反射作用
  - 在运行时检测或修改程序行为
  - 增加了程序的灵活性

- java反射缺点
  - 反射包括了一些动态类型，所以JVM无法对这些代码进行优化。因此，反射操作的效率要比那些非反射操作低得多。我们应该避免在经常被执行的代码或对性能要求很高的程序中使用反射
  - 使用反射技术要求程序必须在一个没有安全限制的环境中运行
  - 反射增加了程序的复杂性，反射允许执行在正常情况下不被允许的操作，可能导致功能上的错误，降低可移植性
  - 在使用反射修改某个对象的成员变量会造成一定程度的性能开销，因为在反射时这样的操作需要引发许多额外操作，比如验证访问权限
  - 反射也会导致一些运行时的计算优化失效，如重复设置一个变量多次值
  - 使用 `setAccessible(true)` 可能会导致意想不到的后果，比如： 在运行时虽然你通过反射修改了变量的值，但其他部分可能还在使用原来的值

- 在使用反射获取或者修改一个变量的值时，编译器不会进行自动装/拆箱。
  - 因此我们无法给一个 Integer 类型的变量赋整型值，必须给它赋一个 Integer 对象才可以。
  - 应该使用 `f.set(obj, new Integer(43));`

## java 泛型

- `List<?>` 和 `List<T>` 的区别
  - 类型参数“<T>”主要用于声明泛型类或泛型方法
  - 无界通配符“<?>”主要用于使用泛型类或泛型方法
  - https://www.zhihu.com/question/31429113
  - https://blog.csdn.net/margin_0px/article/details/82906596

  

## java 注解

## java 网络

## java io

# maven

- jar包MANIFEST. MF文件内容与maven坐标GAV的队友关系
  - Implementation-Vendor-Id = groupId
  - Implementation-Title = artifactId，这个不一定对应，artifactId也可能就是jar包名
  - Implementation-Version = version
- maven提供6个内置属性，用户可直接使用
  - ${basedir}表示项目根目录, 即包含pom.xml文件的目录; 
  - ${version}表示项目版本; 
  - ${project.basedir}同${basedir}; 
  - ${project.baseUri}表示项目文件地址; 
  - ${maven.build.timestamp}表示项目构件开始时间; 
  - ${maven.build.timestamp.format}表示属性${maven.build.timestamp}的展示格式, 默认值为yyyyMMdd-HHmm

## maven plugins

- maven-compiler-plugin
  - 编译java源码，可指定javac参数
- maven-jar-plugin
  - maven默认使用的打包插件，可指定启动的mainClass，但此jar不包含所依赖的其他jar中的class
  - 可在maven生成的jar中的MANIFEST. MF文件中定义一个 main 来指定启动类
- maven-shade-plugin
  - 打包生成一个可执行的uber-jar，它包含所有的依赖jar，可解决jar包冲突的问题
- maven-assembly-plugin	
  - 打包成jar包含所有依赖和资源，可定制和重新组装目录
  - 不仅会将 Dependency 中的 Class 文件打入最终的 Jar 包，还会将 Dependency 中的资源文件，诸如 properties 文件打入最终的 Jar 包，同名资源会冲突
- maven-dependency-plugin 

# Java Specification

## JVM

## Java Language

# Java Ecosystem

## web

- 过滤器和拦截器的执行顺序  

先执行过滤器，然后执行拦截器  

- 拦截器和AOP是什么关系  

AOP也是拦截器的一种，通常用在维护数据操作层，拦截器多用于验证登陆状态之类的

- 什么时候用过滤器，什么时候用监听器，什么时候用拦截器？在什么场景要使用？  

过滤器通常用在设定字符编码之类的，设置请求的默认值，监听器用来监听控制器情况

## spring framework

### filter, interceptor & listener

- https://my.oschina.net/zdtdtel/blog/3025880
- filter 过滤器(实现 javax.servlet. Filter 接口)
  - 过滤器应用场景：对请求的URL进行过滤, 对敏感词过滤
  - Filter是Servlet规范的一部分
  - 过滤器是在web应用启动的时候初始化一次, 在web应用停止的时候销毁
  - 挡在拦截器的外层
- interceptor 拦截器(实现 org.springframework.web.servlet. HandlerInterceptor 接口)
  - 拦截器应用场景：性能分析, 权限检查, 日志记录
  - 不依赖Spring容器, 可以使用Spring容器管理的Bean
  - 拦截器通过动态代理进行
- listener 监听器(实现 javax.servlet. ServletRequestListener/ServletContextListener, javax.servlet.http. HttpSessionListener等接口)
  - 监听器应用场景：监听对象的创建与销毁, 比如session, request, ServletContext
  - Listener是Servlet规范的一部分

## objenesis 可以不使用构造方法创建Java对象

- https://blog.csdn.net/codershamo/article/details/52015206
- Objenesis是一个Java类库，用来实例化一个特定class的对象
- Java已经支持使用Class.newInstance()动态实例化类的实例。但是类必须拥有一个合适的构造器。有很多场景下不能使用这种方式实例化类，如：构造器需要参数、构造器有side effects、构造器会抛异常
- 在类库中经常会有类必须拥有一个默认构造器的限制。Objenesis通过绕开对象实例构造器来克服这个限制。
- 实例化一个对象而不调用构造器是一个特殊的任务，然而在一些特定的场合是有用的，如：序列化，远程调用和持久化、代理，AOP库和Mock对象、容器框架

## game

- java游戏开发依赖于图形库
- common
  - https://jogamp.org/
- 2D
  - https://github.com/libgdx/libgdx
- 3D
  - https://github.com/jMonkeyEngine/jmonkeyengine
  - https://github.com/benoit-dumas/OpenRTS
- fxgl
  - https://github.com/AlmasB/FXGL
  - 支持2D，支持Java和Kotlin，MIT
  - 提供示例 Win/Mac/Linux/Android 5.0+(Sample)/iOS(alpha)/Web(Sample)
  - 0.5.4版本支持java8-10, 11.3版本支持java11，之后作者只会开发维护11+的版本，目前11版功能不如0.5.4全面
- misc
  - https://github.com/LWJGL/lwjgl3
  - xmage 万智牌，类似 magic duels

## 图形开发

- JFC（全称为Java Foundation Classes，中文译为Java基础类）是一个图形框架
- JFC主要是由Abstract Window Toolkit（AWT）、Swing以及Java 2D三者所构成，若将这些一同搭配运用，则用Java程式语言撰写开发成的使用者介面，无论转移到Windows、Mac OS X或Linux等各种不同的作业平台上，都能保有一致性的图像呈现。

# JDK

## New Features Of JDK 

### JDK 1.0 - 19960123

### JDK 1.1 - 19970219

### J2SE 1.2 - 19981208

### J2SE 1.3 - 20000508

### J2SE 1.4 - 20020206

### J2SE 5.0 - 20040930

### Java SE 6 - 20061211

### Java SE 7 - 20110728

### Java SE 8 - 20140318

### Java SE 9 - 20170921

### Java SE 10 - 20180320

### Java SE 11 - 20180925

### Java SE 12 - 20190319

## Alibaba Dragonwell JDK

- Dragonwell是阿里巴巴公司发布并长期支持的一款JDK发行版，它基于OpenJDK项目，通过Java TCK测试，并包含了一些在阿里内部广泛使用的附加特性
- 目前Dragonwell仅支持Linux x86-64操作系统(201907)
- 目前Dragonwell仅支持JDK8版本

### 定制特性

- JWarmup
  - 根据前一次程序运行的情况，记录下热点方法、类编译顺序等信息，在应用下一次启动的时候积极加载相关的类，并积极编译相关的方法，进而应用启动后可以直接运行编译好的Java代码(C2编译）。
  - 典型用法
      - 在Beta灰度环境，进行应用压测，记录下热点方法、类编译顺序等信息
      - 在Production环境，使用提前记录的profiling data提前编译热点方法
- Java Flight Recorder (JFR) 
  - 收集Java应用运行过程中的诊断及性能数据的工具
  - 在使用默认配置的情况下，JFR带来的额外开销将小于2%
  - JMC可以用于分析JFR产生的事件记录
- Serviceability
  - 迷你Heapdump支持 
      - Alibaba Dragonwell允许您在使用jmap工具生成heapdump的时候忽略掉所有原始类型数组的内容，只dump出对象引用等信息，从而缩小生成的Heapdump文件大小。使用时，只需要给-dump子命令添加mini参数即可。
  - `-XX:+PrintYoungGenHistoAfterParNewGC` 这个参数会打印在一次ParNew GC之后的young区对象的histogram。
  - `-XX:+PrintGCRootsTraceTime` 这个参数会打印一次ParNew GC的具体耗时，类似于G1的gclog显示，这个参数主要用于用户排查时间较长的gc暂停时间

## OpenJDK

### Download

- [Archived OpenJDK Releases 9-12](http://jdk.java.net/archive/)

## Oracle JDK

### Download

- Oracle Java Archive 1-12
- https://www.oracle.com/technetwork/java/archive-139210.html
- **Last BCL JDK**
  - 8u201/8u202 
      - https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html
  - 7u80
      - https://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html
  - 6u45
      - https://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase6-419409.html

### JDK Release Notes 

- [Java version history](https://en.wikipedia.org/wiki/Java_version_history)
- https://www.oracle.com/technetwork/java/javase/jdk-relnotes-index-2162236.html
- https://www.oracle.com/technetwork/java/javase/cpu-psu-explained-2331472.html

### Oracle Java SE Support Roadmap

- java 11 is a LTS version. 2018-2026.
- https://www.oracle.com/technetwork/java/java-se-support-roadmap.html

- OpenJDK vs Oracle JDK
  - 授权协议不同 GPLv2+CPE vs BCL
  - 代码完整性不同
    - 从Oracle JDK7/OpenJDK7开始，闭源和开源版的实质差异实在是非常小
    - Oracle JDK7在OpenJDK7的基础上带了一些value-add，其中很多还没啥用（例如browser plugin）
    - Rhino没有包含在OpenJDK里纯粹是因为license不兼容
    - OpenJDK8有新JS引擎Nashorn

## License  

- The Oracle JDK License has changed for releases starting April 16, 2019.
- The previous Oracle Java SE license - Binary Code License (**BCL**)
- Oracle as of Java 9 provides two distinct Java release
  - Oracle OpenJDK releases under the open source GNU General Public License v2, with the Classpath Exception (**GPLv2+CPE**) (since Java 9)
  - Oracle Java SE product releases, which includes the Oracle JDK for Java 8 and later, and Oracle JRE with Java Web Start in Java 8, under the **OTN** License Agreement for Java SE
- Oracle Java SE Licensing FAQ
  - https://www.oracle.com/technetwork/java/javase/overview/oracle-jdk-faqs.html
  - https://www.oracle.com/downloads/licenses/javase-license1.html
  - http://openjdk.java.net/faq/
  - http://aleung.github.io/blog/2017/01/06/Use-OpenJDK-in-proprietary-software/

## 其他JDK

- IBM J9 JDK, for AIX, Linux, Windows, MVS, OS/400, Pocket PC, z/OS
  - IBM于201709开源OpenJ9并托管给Eclipse基金会
  - https://www.infoq.cn/article/2017/09/IBM-JVM-OpenJ9-Eclipse
- Azul Zing JVM，since 2010, 实现类C4(Continuously Concurrent Compacting Collector)GC算法
  - Azul distributes and supports Zulu and Zulu Enterprise, a certified binary build of OpenJDK since 201309.
- Apache Harmony
  - 一个兼容Java5的JDK实现，始于2005，于2011年终止研发
  - Harmony类库于2007年底被Google Android采用为其类库
  - Android平台所使用的虚拟机Dalvik(<=4.4)和ART(>4.4)使用了Harmony部份的子集
  - Android 7.0 Nougat replaced Harmony with OpenJDK in 2016
- jdk讨论参考
  - https://www.zhihu.com/question/275665265
