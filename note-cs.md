---
title: note-cs
created: '2019-04-22T03:42:22.447Z'
modified: '2019-06-09T06:06:25.310Z'
---

# note-cs

## 开源协议

### GPL
GPL明确规定，任何源码的衍生产品，如果对外发布，都必须保持同样的许可证。这就是说，任何人只要发布MySQL的修改版本，他就必须公开源码，并且同意他人可以自由地复制和分发。



## java中InputStream实例化时，文件是否已经读完了？


## java file

- FileInputStream reads the file byte by byte
  - Abstract class is the superclass of all classes representing an input stream of bytes.
  - 读取字节流，可处理二进制内容
- FileReader reads the file character by character
  - Reader - Abstract class for reading character streams 
  - 读取字符流，一般用于处理文本，不处理视频文件


## 动态链接库 dll
- 大多数操作系统将解析外部引用（比如库）作为加载过程的一部分，可执行文件包含一个叫做import   directory的表，该表的每一项包含一个库的名字。根据表中记录的名字，装载程序在硬盘上搜索需要的库，然后将其加载到内存中预先不确定的位置，之后根据加载库后确定的库的地址更新可执行程序。可执行程序根据更新后的库信息调用库中的函数或引用库中的数据。这种类型的动态加载称为装载时加载，被包括Windows和Linux的大多数系统采用，最复杂的工作之一就是 **加载时链接**。
- 有些操作系统可能在运行时解析引用。在这些系统上，可执行程序调用操作系统API，将库的名字，函数在库中的编号和函数参数一同传递。操作系统负责立即解析然后代表应用调用合适的函数。这种动态链接叫做 **运行时链接** 。因为每个调用都会有系统开销，运行时链接要慢得多，对应用的性能有负面影响。
- 可以动态链接的库，在Windows上是dynamic link library (DLL)，在UNIX或Linux上是Shared  Library。库文件是预先编译链接好的可执行文件，存储在计算机的硬盘上。大多数情况下，同一时间多个应用可以使用一个库的同一份拷贝，操作系统不需要加载这个库的多个实例。  
- Windows和Linux的加载时链接是由操作系统来完成的，格式在不同的系统下有不同的区别，但是原理还是一样的。linux下文件的类型是不依赖于其后缀名的，但一般来讲：
  - .o是目标文件,相当于windows中的.obj文件
  - .so为共享库,是shared object,用于动态连接的,和dll差不多
  - .a为静态库,是好多个.o合在一起,用于静态连接
  - .la为libtool自动生成的一些共享库，主要记录了一些配置信息。
- 通常把一些公用函数制作成函数库,供其它程序使用，函数库分为静态库和共享库
- 程序函数库简单的说就是一个文件包含了一些编译好的代码和数据，这些编译好的代码和数据可以供其他的程序使用。程序函数库可以使整个程序更加模块化，更容易重新编译，而且更方便升级。程序函数库可分为3种类型：静态函数库（static libraries）、共享函数库（shared libraries）和动态加载函数库（dynamically loaded libraries）。
- 静态函数库是在程序执行前就加入到目标程序中去了；而共享函数库则是在程序启动的时候加载到程序中，它可以被不同的程序共享；动态加载函数库则可以在程序运行的任何时候动态的加载
- 静态函数库实际上就是简单的一个普通的目标文件的集合，一般来说习惯用“.a”作为文件的后缀,静态库函数允许程序员把程序link起来而不用重新编译代码，节省了重新编译代码的时间。
- 共享函数库中的函数是在当一个可执行程序在启动的时候被加载。每个共享函数库都有个特殊的名字，称作“soname”。Soname名字命名必须以“lib”作为前缀，然后是函数库的名字，然后是“.so”，最后是版本号信息。不过有个特例，就是非常底层的C库函数都不是以lib开头这样命名的。当可执行程序需要在自己的程序中列出这些他们需要的共享库函数的时候，它只要用soname就可以了
- 动态加载的函数库Dynamically loaded (DL) libraries是一类函数库，它可以在程序运行过程中的任何时间加载，们特别适合在函数中加载一些模块和plugin扩展模块的场合。Linux系统下，DL函数库与其他函数库在格式上没有特殊的区别，创建的时候是标准的object格式。主要的区别就是 这些函数库不是在程序链接的时候或者启动的时候加载，而是通过一个API来打开一个函数库，寻找符号表，处理错误和关闭函数库。通常C语言环境下，需要包含这个头文件。
- 动态链接库在unix下，习惯以 .so 为文件名结尾（通常还以 lib 开头）。而Windows下是以 .DLL 为文件后缀。如果需要运行时主动加载一个动态链接库，windows下可以使用 LoadLibrary 这个 kernel API (在 kernel32.dll 中)；unix 下是用 dlopen 。Windows 下找到 dll 中导出符号的地址，可以用 GetProcAddress ，而 unix 也有对应的 api。这些相互对应的api，似乎预示着对等的功能，但事实上是有区别的。
- DLL 事实上和 EXE 文件一样，同属 PE 格式的执行文件。对于隐式的引用外部符号，需要把外部符号所在的位置写在 PE 头上。PE 加载器将从 PE 头上找到依赖的符号表，并加载依赖的其它 DLL 文件。
- so 文件大多为 elf 执行文件格式。当它们需要的外部符号，可以不写明这些符号所在的位置。也就是说，通常 so 文件本身并不知道它依赖的那些符号在哪些 so 里面。这些符号是由调用 dlopen 的进程运行时提供的。而 unix 下的执行文件本身会暴露自己静态链接的符号，（可以是自己本身实现的，或者是从静态库 .a 文件里链入的）。dlopen 将把这些符号通报给 dlopen 加载的 .so 文件，最终完成动态链接。


## java jdk webview js engine

- The full Oracle Java Runtime 8 ships with two JavaScript engines
- Nashorn: "Nashorn's goal is to implement a lightweight high-performance JavaScript runtime in Java with a native JVM. This Project intends to enable Java developers embedding of JavaScript in Java applications via JSR-223 and to develop free standing JavaScript applications using the jrunscript command-line tool."
- JavaScriptCore: The JavaScript engine built into the WebKit implementation wrapped by WebView component the JavaFX system.
JavaScript Runtime Used by WebView and JavaFX applications
- JavaFX Webkit does not use Nashorn, it uses JavaScriptCore.

## JavaFX 框架 前景 观点

- https://www.zhihu.com/question/305434657
- https://www.zhihu.com/question/266195521

- 优点
  - 跨平台
  - 支持通过 fxml 和 css 来编写界面
  - 提供WebView组件
  - 借助 ExcelsiorJET 能够将 JavaFX 的应用 aot
- 缺点
  - 跨平台时可能出现一些行为不一致
  - 样式过度依赖css，很多东西都无法依赖代码来指定
  - 原生组件不算丰富
  - 对于系统原生功能支持不够，譬如没有提供支持触控板手势的API
  - 没有热加载，所以不够直观，而且api不是那么直观
- wps office 2019 addons文件夹包含软件各个组件，几乎都是html实现的，.kuip文件包含主题样式
  - wps未使用qml
- viewpoint
- 旧的swing项目当然不会轻易更换框架，而新的项目没人再选择Java了。FXML、硬件加速、MVVM思想都很好，但是这些别人也有，而且成熟得比Java早，何必要换成Java？Java要是真想在GUI翻身，还得像electron那样拿出点顺应潮流的东西、别人还没做好的东西。我觉得在WebAssembly是个方向。
- 我很看好JAVAFX，我看好一切跨平台GUI方案，包括Qt（QML），这才是应该长期发展的技术。很多人扯H5的跨平台GUI方案，你要真的纯粹用H5，不跟本地软硬件资源有任何交互，只跟服务器端增删改查，我感觉也折腾不出什么激动人心的产品，还不如人家用Chrome直接访问呢。
- 我这里只说PC端跨平台GUI，移动端我估计会在微信小程序上实现UI的大统一，毕竟小程序为Android和IOS提供了统一的软硬件资源框架（包括摄像头，蓝牙等硬件资源），同时又为用户提供了即用即走的便利性（免安装），还为开发者节省了大量的登陆逻辑和安全风险。
- Electron的本质是一套用NodeJS控制的Chrominum，单纯用Electron估计也就只能做一个披着应用程序边框和标题栏的网页，跟Chrome建立桌面图标有点类似。真正开发一套商业或者工业级的企业程序，不调用个把dll/so估计是不现实的，而NodeJS调用dll或者so的开发体验和运行效率，要远远低于JNI，就更别提Qt这种原生态C++了。
- 我理想中的跨平台GUI项目选型：移动端无一例外微信小程序解决；PC端，工程师熟悉JS就用Electron，不过要做好在NodeJS平台调用dll/so的基础功课。三种框架的开发体验Electron>JAVAFX>Qt，客户体验Qt>JAVAFX>Electron，平衡下来我觉得JAVAFX还算较好的选择
- 如今的JavaFX也不过是袭人故技，用FXML布局，Java实现业务逻辑。性能上不如duilib，开发速度上又不如Web。虽然jdk11 已经能把javafx 独立出来了，但仍无可避免jre带来的臃肿体积。重点是由于不流行 **学的人少** ，根本没公司愿意用。而且由于浏览器性能越来越强，Web单页应用如火如荼，React, Vue都妇孺皆知了，重点是效果完全不输原生应用
- Oracle的JDK在中文输入的场景一直做得很烂。特别是用搜狗输入法的时候，有很多意料之外的行为。包括JavaFX和Swing都有问题。目前基于Java的成熟的商业应用，都会包含自己魔改过的JRE。典型例子就是Jetbrains加的产品。之前是直接借助系统JDK运行的，但后来发生了滚动条失灵、中文输入法无法输入等问题后，就捆绑了基于OpenJDK的自家的Jetbreans JRE。

## jackson-core 源码结构

- JsonParser、JsonGenerator提供顶层读写抽象类、JsonFactory提供工厂方法
- io包提供输入输出方法：跳过特殊字符、encode/decode、mergedStream、utf8->utf32
- json包提供读写具体实现
  - async提供非阻塞的异步读写方法
- format包提供数据格式匹配方法
- filter提供数据过滤方法
- sym包提供特殊符号的处理方法
- type包提供泛型处理方法
- util包提供各种工具类

## easyexcel 源码结构

- ExcelReader、ExcelWriter、ExcelFactory提供顶层读写具体类
- analysis包提供解析03、07格式excel的方法
- write包提供生成excel的方法
- annotation提供注解
- context包提供读写相关上下文
- event提供事件监听器
- metadata包提供spreadsheet模型抽象
- modelbuild提供将字符串转换成bean的方法
- parameter提供生成excel所需参数
- support提供枚举类
- util提供各种工具类
- constant提供常量

## java string 

- StringReader
- String Pool是一个固定大小的Hashtable，默认大小是1009，如果放入常量池的字符串过多，就会造成hash冲突，导致链表很长，而链表长了后直接会造成的影响就是当调用String.intern时性能会大幅下降
- 直接使用双引号声明出来的String对象会直接存储在常量池中
- intern 方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中
- 在Jdk6以及以前的版本中，字符串的常量池是放在堆的Perm区的，Perm区是一个类静态的区域，主要存储一些加载类的信息，常量池，方法片段等内容，默认大小只有4m，一旦常量池中大量使用 intern 是会直接产生java.lang.OutOfMemoryError: PermGen space错误的。 所以在jdk7的版本中，字符串常量池已经从Perm区移到Java Heap区。jdk8已经直接取消了Perm区，而新建立了一个元区。

## jackson 处理 json

- ObjectMapper提供解析器和生成器的入口
- JsonParser提供底层json解析器
- JsonGenerator提供底层json生成器

- JsonParser的工作原理
  - 将JSON分解成一系列的token，然后迭代token解析，token类型由JsonToken中一系列的常量来表示
  - 如果token指向的是字段名称，JsonParser的getCurrentName()方法返回当前字段的名称。
  - 如果token指向的是字符串字段值，getValueAsString()方法以字符串的形式返回当前token的值。   JsonParser还有更多相似的方法，如getText()。


## maven的packaging为bundle
- bundle是OSGI中的依赖单元，是一种特殊格式的jar
- `<dependency>`的type也可以为bundle

## JPMS  
- Java Platform Module System (JSR 376)，也就是Jigsaw 项目   

## xml的生成

- SAX parsing is for reading documents, not writing them. You can write XML with the XMLStreamWriter.
- Generating XML via Java (https://www.techrepublic.com/article/generating-xml-via-java/)
  - Using the StringBuffer class
  - Using DOM
  - Using SAX
  - Using a custom XmlWriter class

## jdk xml解析 sax方式 方法顺序

- sax中DefaultHandler解析XML的总体过程   
startDocument --> 具体读到某个node（非根node和根node）的解析过程 --> endDocument  

- 解析XML非根node的顺序  
 startElement --> characters --> endElement --> characters    
(endElement后会再调用一次characters方法)    

- 解析XML根node的顺序
 startElement --> characters --> endElement  

## xlsx Excel2007 常见标签

- sheet1.xml 
    - worksheet
        - dimension： ref=A1:D9，存放的是sheet的行列数
        - sheetViews：
        - sheetFormatPr:
        - cols：子元素col存放各列宽度
        - sheetData：存放所有单元格数据
            - row： 存放行信息，r="1" s="1" customFormat="1" ht="29" customHeight="1" spans="1:4"
                - c：存放列信息，r="A1" s="1" t="s"
                    - v：存放单元格数据， `<v>0</v>` ，文本字符串用的是sharedStrings.xml中的索引
        - pageMargins
        - headerFooter

## xlsx Excel2007 格式解析 
- Excel2007是使用XML格式来存储的，把一个excel文件(test.xlsx)后缀改为.zip，解压后的结构
- [Content_Types].xml：列出Excel解压后各个XML文件名及其类型
- xl文件夹
    - workbook.xml：列出Workbook包含的所有sheets，sheet用索引标识
    - sharedStrings.xml：Excel将各个sheet中字符型单元格的值存放在sharedStrings.xml中用于共享
    - styles.xml：存放每个单元格的样式
    - worksheets文件夹
        - sheet1.xml：存放单张sheet中所有单元格数据，其中文本型单元格数据用索引值表示
    - _rels文件夹
        - workbook.xml.rels.xml：定义了workbook中sheet1索引、styles索引、sharedStrings索引
    - theme文件夹
        - theme1.xml：定义workbook的样式
- _rels文件夹
    - .rels：描述workbook与docProps中文件的关系
- docProps文件夹：整个excel文档的元信息
    - core.xml：描述文件的创建时间、修改时间、创建者、修改者、主题
    - app.xml ：描述文档的其他属性如文档类型、版本、是否只读、是否共享、安全属性，还包括创建该文档的软件

## poi Class SharedStringsTable

- Table of strings shared across all sheets in a workbook.
- When displaying text in the spreadsheet, the cell table will just contain an index into the string table as the value of a cell, instead of the full string.

## poi各jar包作用
- poi-version.jar：用于操作.xls文件；依赖于commons-logging, commons-codec, log4j；
- poi-scratchpad-version.jar：用于操作.ppt、.doc、.vsd、.pub、.msg文件；依赖于poi；
- poi-ooxml-version.jar、poi-ooxml-schemas-version.jar：用于操作.xlsx、.pptx、docx文件；依赖于poi, dom4j，xmlbeans, stax-api-1.0.1；
- 操作Excel主要是指ss包、xssf包；

## xml的解析方式
- 基于dom
    - 将整个xml加载到内存中，形成文档对象，所有对xml操作都对内存中文档对象进行，几乎所有开发语言都支持
    - Tree model parser (Object based) (Tree of nodes).
    - DOM is read and write (can insert or delete nodes).
    - Backward and forward search is possible for searching the tags, making it easy to navigate 
    - 优点
        - 允许应用程序对数据和结构做出更改
        - 方便在树结构中导航，获取和操作任意部分的数据
    - 缺点
        - 需要加载整个XML文档来构造层次结构，内存消耗大，容易溢出

- 基于sax
    - 基于事件/流的方式，在解析XML文档时触发一系列的事件，当发现给定tag时激活一个回调方法，边解析边处理，边释放内存资源
    - push模式，由解析器调用事件处理器，一旦解析器开始执行，就会迭代每个xml元素直到结束，无法控制何时如何解析    
    - Event based parser (Sequence of events).
    - SAX is read only i.e. can’t insert or delete the node.
    - SAX reads the XML file from top to bottom and backward navigation is not possible.
    - 优点
        - 只在读取数据时检查数据，不需要保存在内存中，内存消耗小
        - 效率和性能较高，能解析大于系统内存的文档。
        - 不需要等待所有数据都被处理，分析就能立即开始。
        - 可以在某个条件得到满足时停止解析，不必解析整个文档。
    - 缺点
        - 需要应用程序自己负责TAG的处理逻辑（例如维护父/子关系等），文档越复杂程序就越复杂
        - 单向导航，无法定位文档层次，很难同时访问同一文档的不同部分数据，不支持XPath


- 基于stax
    - 基于事件/流的方式
    - pull模式，由事件处理器控制解析器何时解析下一个元素

- 其他
    - SAX解析器当接收到XML文件内容，服务器端解析器SAXParser自动开始解析，自动解析过程中调用处理器相应方法处理所有元素，这是推模式
    - StAX解析器需要手动通过next触发文档解析事件，在客户端代码中获取当前事件，从而调用相应事件处理方法
    - StAX方式解析xml的效率好于SAX 
        - SAX无选择性的，所有事件都会处理的解析方式，解析器控制事件的调用；StAX由用户自主控制需要处理事件类型以及事件的调用
        - 使用Stax进行数据解析时，随时终止解析
        - StAX has NO Support for Schema Validation
        - StAX Allows Subparsing / Delegation
        - StAX has Support for XML Writing, SAX does not have support for writing XML
        - http://tutorials.jenkov.com/java-xml/sax-vs-stax.html
    - JAXP是sun官方推出的解析xml的api，同时支持 DOM SAX StAX
    - JDOM与DOM有一些不同，JDOM仅使用具体类而不使用接口，这在某些方面简化了API，但是也限制了灵活性，还大量使用了Collections类
    - DOM4j最初是JDOM的一个分支，后来开发了许多超出基本XML文档表示的功能，包括集成的XPath支持、XML Schema支持以及用于大文档或流化文档的基于事件的处理，还提供了构建文档表示的选项
    - XML PULL是Android内置的xml解析技术，采用StAX方式解析xml，需要客户端程序手动完成解析，XmlPullParser存放解析方法next()，用于解析器解析下一事件
    - https://www.cnblogs.com/lanxuezaipiao/archive/2013/05/17/3082949.html 四种生成和解析XML文档的方法详解
    - https://blog.csdn.net/zhongkelee/article/details/51737710  XML文档DOM、SAX、STAX解析方式详解  

## 如何遍历文件夹下上亿文件而不栈溢出   
- 考虑层序遍历   
- https://www.cnblogs.com/intsmaze/p/6031894.html    
   

