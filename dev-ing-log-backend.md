---
title: dev-ing-log-backend
tags: [backend, dev]
created: 2020-02-20T10:56:13.810Z
modified: 2023-06-14T00:52:52.145Z
---

# dev-ing-log-backend
- about crud, rpc, database
# logging

 

## [The Dhall configuration language](https://dhall-lang.org/)

- Dhall is a programmable configuration language that you can think of as: 
  - JSON + functions + types + imports

## CQRS系统

- 简单的说，CQRS(Command Query Responsibility Segregation)就是一个系统，从架构上把CRUD系统拆分为两部分：命令（Command）处理和查询（Query）处理。
  - CQRS即读与写的职责分离。CQRS将读取和写入分离到不同的模型中，使用命令更新数据，查询用于读取数据。
  - 读写分离是物理层面的分离，CQRS是数据模型层面的分离
- 其中命令处理包括增、删、改。
- 然后命令与查询两边可以用不同的架构实现，以实现CQ两端（即Command Side，简称C端；Query Side，简称Q端）的分别优化
- CQRS作为一个读写分离思想的架构，在数据存储方面也没有做过多的约束。所以 CQRS可以有不同层次的实现。
- CQRS可以有两种实现方式
- CQ两端数据库共享，只是在上层代码上分离。
  - 这样做的好处是可以让我们的代码读写分离，更容易维护，
  - 而且不存在 CQ 两端的数据一致性问题，因为是共享一个数据库的。这种架构是非常实用的。
- CQ两端不仅代码分离，数据库也分离，然后Q端数据由C端同步过来。
  - 同步方式有两种：同步或异步，
  - 如果需要 CQ 两端的强一致性，则需要用同步；
  - 如果能接受 CQ 两端数据的最终一致性，则可以使用异步。
  - C端可以采用Event Sourcing（简称ES）模式，所有C端的最新数据全部用 Domain Event 表达即可；
  - 而要查询显示用的数据，则从Q端的 ReadDB（关系型数据库）查询即可。

## 文本编码

- ANSI
  - 泛指最早每种国家语言各自实现的扩展编码方式，各个编码互相之间不兼容，比较省空间。
- Unicode
  - 一套抽象的兼容所有常用语言的编码方式，但是不适合计算机系统直接存储。
- UTF-8
  - 一种将unicode转换成适合计算机存储的方式，相对其他的UTF-xx省空间，同时又可以和ASCII混用，结构相对复杂，底层处理相对慢。
- UTF-16，UTF-32
  - 另外的unicode存储编码，结构简单，不能和ASCII混用。
- BOM
  - 一种为了跨平台设计的文件起始标记，但很多程序没去处理这个，用了BOM反而常造成问题。
- 在Windows记事本的语境中
  - 所谓的「ANSI」指的是对应当前系统 locale 的遗留（legacy）编码
  - 所谓的「Unicode」指的是带有 BOM 的小端序 UTF-16
  - 所谓的「UTF-8」指的是带 BOM 的 UTF-8

## java maven

- maven-config
  -  maven会根据模块的版本号(pom文件中的version)中是否带有-SNAPSHOT来判断是快照版本还是正式版本
    - 如果是快照版本，那么在mvn deploy时会自动发布到快照版本库中，而使用快照版本的模块，在不更改版本号的情况下，直接编译打包时，maven会自动从镜像服务器上下载最新的快照版本
    - 如果是正式发布版本，那么在mvn deploy时会自动发布到正式版本库中，而使用正式版本的模块，在不更改版本号的情况下，编译打包时如果本地已经存在该版本的模块则不会主动去镜像服务器上下载
  -  在distributionManagement段中配置的是snapshot快照库和release发布库的地址
  - 依赖搜索顺序： local_repo > settings_profile_repo > pom_profile_repo > pom_repositories > settings_mirror > central
  - mirror vs repository
    - 镜像是一个特殊的配置，其实镜像等同与远程仓库，没有匹配远程仓库的镜像就毫无作用 
    - 在mirrorOf与repositoryId相同的时候优先是使用mirror的地址
      - 当一个 repository 存在 mirror 时，Maven 查找 jar 时永远使用的是 mirror 配置的地址
      - 当一个 repository 不存在 mirror 时，按照在 repositories 节点中定义的先后顺序。先定义，先查找。
    - mirrorOf等于*的时候覆盖所有repository配置
    - 存在多个mirror配置的时候mirrorOf应该*放到最后
    - 从超级父pom里继承来的中央repository在effective-pom里总是为最后一个repository
- maven-cli
  - `mvn install`
    - mvn install 会将项目生成的构件安装到本地Maven仓库，mvn deploy 用来将项目生成的构件分发到远程Maven仓库
- JPMS  
  - Java Platform Module System (JSR 376)，也就是Jigsaw项目   
- java枚举类与switch使用
  - enum switch case label must be the unqualified name of an enumeration constant   
  - switch指定枚举类后，case后只能用枚举类的非限定名，不要再写枚举类了

## java string 

- StringReader
- String Pool是一个固定大小的Hashtable，默认大小是1009，如果放入常量池的字符串过多，就会造成hash冲突，导致链表很长，而链表长了后直接会造成的影响就是当调用String.intern时性能会大幅下降
- 直接使用双引号声明出来的String对象会直接存储在常量池中
- intern方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中
  - 在Jdk6以及以前的版本中，字符串的常量池是放在堆的Perm区的，Perm区是一个类静态的区域，主要存储一些加载类的信息，常量池，方法片段等内容，默认大小只有4m，一旦常量池中大量使用intern是会直接产生java.lang. OutOfMemoryError: PermGen space错误的。
  - 所以在jdk7的版本中，字符串常量池已经从Perm区移到Java Heap区。
  - jdk8已经直接取消了Perm区，而新建立了一个元区

## maven的packaging为bundle

- bundle是OSGI中的依赖单元，是一种特殊格式的jar
- `<dependency>` 的type也可以为bundle

## jdk webview js engine

- The full Oracle Java Runtime 8 ships with two JavaScript engines
- Nashorn: "Nashorn's goal is to implement a lightweight high-performance JavaScript runtime in Java with a native JVM. This Project intends to enable Java developers embedding of JavaScript in Java applications via JSR-223 and to develop free standing JavaScript applications using the jrunscript command-line tool."
- JavaScriptCore: The JavaScript engine built into the WebKit implementation wrapped by WebView component the JavaFX system. JavaScript Runtime Used by WebView and JavaFX applications
- JavaFX Webkit does not use Nashorn, it uses JavaScriptCore.

## build tools: bazel; buck

- bazel：由google开发维护，支持Java/C++，支持Android，存在版本之间不兼容的问题
- buck：由facebook开发，支持Android/iOS，移动端支持更好

## Java File

- FileInputStream reads the file byte by byte
  - Abstract class is the superclass of all classes representing an input stream of bytes.
  - 读取字节流，可处理二进制内容
- FileReader reads the file character by character
  - Reader - Abstract class for reading character streams 
  - 读取字符流，一般用于处理文本，不处理视频文件
  - java中InputStream实例化时，文件是否已经读完了？ no
