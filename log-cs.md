---
tags: [log/cs]
title: log-cs
created: '2019-04-22T03:42:22.447Z'
modified: '2019-10-07T10:09:07.234Z'
---

# log-cs

## 技术前景与趋势
- realtime/实时
- dynamic/动态
- 3d/三维
- 算法性能优化

## 开发原则
- learn by practice/实用为先/使用为先
- 不要花费过多时间进行工具选择
    - 工具只是解决问题的捷径
    - 在解决业务问题后，可以花更多时间深入工具原理与抽象自己的工具

## pieces
- 监听器的使用    
    - 将业务逻辑系统用事件驱动方式拆分，既能使代码逻辑更清晰，又能自主掌控逻辑的同步和异步执行
    - 在业务中很多场景都可以比喻为事件，比如用户注册，可能要求注册之后发送验证信息，或者创建订单之后需要发送订单详情邮件之类的，还有就是批量处理时，可以拆成一个批量输入命令，然后触发一个事件，事件处理一个任务，这个事件触发也可以在接口或者其它地方触发，但是事件监听是同一套，不用做任何修改，如果一块逻辑已经过时，那直接去掉监听即可，代码上可能只需要修改一行即可
- java network library comparison
    - HttpURLConnection
        - HttpURLConnection是java的标准类，什么都没封装，用起来太原始，不方便，比如重访问的自定义，以及一些高级功能等
        - 从Java 9开始，通过JEP 110, HTTP/2 Client API proposal提供了对HTTP 2.0和WebSocket客户端的编程支持，以HttpClient替换HttpURLConnection/HttpsURLConnection
        - 但是该模块仍然属于沙箱试验，Java 10仍然未能正式发布。从Java 11开始，JEP 110, HTTP/2 Client API终于正式发布，模块名java.net.http
    - Apache HttpClient
        - 在jdk标准库不给力的情况下，Apache HttpComponents HttpClient通常是最佳的HTTP Client library选择。但这个库当前还不支持HTTP/2，支持HTTP/2的版本还处于beta阶段（2018.09.23），因此并不适合用于Android APP中使用，20190722发布的HttpComponents HttpClient 5.0-beta5添加了对http/2协议的支持
        - 在早期版本的Android中，Android SDK中集成了Apache的HttpClient模块，HttpClient就是一个增强版的HttpURLConnection，它只是关注于如何发送请求、接收响应，以及管理HTTP连接
        - 如果做好封装或者使用android-async-http，Afinal，Xutils也能挺简单的完成http请求，但是Android6.0已经放弃了HttpClient，不是系统自带的了
    - OkHttp
        - 由于当前Apache HttpComponents HttpClient版本并不支持 HTTP/2, 而HTTP/2对于移动客户端而言，无论是从握手延迟、响应延迟，还是资源开销看都有相当吸引力。因此这就给了高层次封装且支持HTTP/2 的 http client lib 足够的生存空间，其中最典型的要数OkHttp
        - OKHttp类似于HttpUrlConnection，是基于传输层实现应用层协议的网络框架，而不止是一个Http请求应用的库
        - 默认情况下，OKHttp会自动处理常见的网络问题：像二次连接、SSL的握手问题
        - 从Android4.4开始HttpURLConnection的底层实现采用的是okHttp
        - OkHttp基于NIO 和 Okio，Okio是基于IO和NIO基础上做的一个更简单、高效处理数据流的一个库
    - Volley
        - 是谷歌官方13年I/O大会推出的，volley在设计的时候是将具体的请求客户端做了下封装：HurlStack，也就是说可以支持HttpUrlConnection, HttpClient, OkHttp
        - 也有缺陷，比如不支持post大量数据，所以不适合上传文件。Volley设计的初衷本身也就是为频繁的、数据量小的网络请求而生
        - volley是一个简单的异步http库，仅此而已。缺点是不支持同步，这点会限制开发模式；不能post大数据，所以不适合用来上传文件
    - android-async-http
        - 与volley一样是异步网络库，但volley是封装的httpUrlConnection，它是封装的httpClient，而android平台不推荐用HttpClient了，所以这个库已经不适合android平台了
    - Retrofit
        - 基于OkHttp封装的一套RESTful网络请求框架
        - Retrofit 的封装可以说是很强大，里面涉及到一堆的设计模式，你可以通过注解直接配置请求，你可以使用不同的http客户端，虽然默认是用 Khttp ，可以使用不同Json Converter来序列化数据，同时提供对RxJava的支持
- 阿里飞冰 ice和ant design 区别
    - ice是个项目开发与管理平台，生成的项目的确是没有交互和业务逻辑，这些需要手工编码完成
    - ice前端使用的是阿里内部的fusion库，而不是antd
    - 在ice体系里，组件不受限，既可以用ice提供的组件也可以使用ant的组件，还有更多社区组件
    - 飞冰面向设计师推出iceland，能直接从设计到代码
    - 面向开发者端我们提供了iceworks工具，iceworks是与物料体系打通的关键，所有物料资源，包括iceland上设计师生产的，都会无缝打通


## 开源协议 Open Source License

### 总结
- 修改后可闭源
    - Apache2.0，BSD，MIT
- 修改后必须同样许可
    - GPL

### Apache Licence 2.0
- 允许代码修改、再发布
- 需要给代码的用户一份Apache Licence
- 如果你修改了代码，需要再被修改的文件中说明。
- 在延伸的代码中（修改和有源代码衍生的代码中）需要带有原来代码中的协议，商标，专利声明和其他原来作者规定需要包含的说明。
- 如果再发布的产品中包含一个Notice文件，则在Notice文件中需要带有Apache Licence。你可以在Notice中增加自己的许可，但不可以表现为对Apache Licence构成更改。
- 是对商业应用友好的许可

### GPL (General Public License)
- you have to release source code if you link against and distribute the binary, but don't if you just provide a service
- GPL的出发点是代码的开源/免费使用和引用/修改/衍生代码的开源/免费使用，但不允许修改后和衍生的代码做为闭源的商业软件发布和销售
- GPL规定：只要这种修改文本在整体上或者其某个部分来源于遵循GPL的程序，该修改文本的 整体就必须按照GPL流通，不仅该修改文本的源码必须向社会公开，而且对于这种修改文本的流通不准许附加修改者自己作出的限制。因此，一项遵循GPL流通的程序不能同非自由的软件合并。
- 任何一套软件，只要其中使用了受GPL协议保护的第三方软件的源程序，并向非开发人员发布时，软件本身也就自动成为受GPL保护并且约束的实体。也就是说，此时它必须开放源代码。
- 你可以去掉所有原作的版权信息，只要你保持开源，并且随源代码、二进制版附上GPL的许可证就行
- 无论软件以何种形式发布，都必须同时附上源代码。例如在Web上提供下载，就必须在二进制版本下载的同一个页面提供源码下载，如果以光盘形式发布，就必须同时附上源码
- 开发或维护遵循 GPL 协议开发的软件的公司或个人，可以对使用者收取一定的服务费用
- GPL只是规定用户在获取你的程序的时候必须可以获得源代码，但并没有规定必须免费
- 如果你的确需要发布你的程序，但又不想开源，规避 GPL 的方法是通过 LPC 或者 RPC 间接调用库里的接口。只要库和你的程序不运行在同一进程下，就不需要开源

### LGPL (Lesser GPL)
- you can link against and don't have to release source code as long as you don't modify the library itself
- LGPL是GPL的一个为主要为类库使用设计的开源协议
- LGPL允许商业软件通过类库引用(link)方式使用LGPL类库而不需要开源商业软件的代码。这使得采用LGPL协议的开源代码可以被商业软件作为类库引用并发布和销售。
- 如果修改LGPL协议的代码或者衍生，则所有修改的代码，涉及修改部分的额外代码和衍生的代码都必须采用LGPL协议。因此LGPL协议的开源代码很适合作为第三方类库被商业软件引用，但不适合希望以LGPL协议代码为基础，通过修改和衍生的方式做二次开发的商业软件采用。
- 采用LGPL的代码，一般情况下它本身就是一个第三方库，这时候开发人员仅仅用到了它的功能，而没有对库本身进行任何修改，那么开发人员也不必公布自己的商业源代码。但是如果你修改了这个库的代码，那么你修改的代码必须全部开源，并且协议也是LGPL，但除了库源码之外的商业代码，仍不必公布

### AGPL (Affero General Public License)
-  you have to allow the source to be downloaded even if you never distribute the binary but do provide a service
- GPL（2.x ~ 3.x） 协议还有一个非常大的“漏洞”，就是软件“发布” 才必须开源。如果软件不发布，即使使用 GPL (2.x ~ 3.x) 也可以不用开源。随着以Google为代表的软件作为服务的互联网公司的兴起，它们的“不分发软件，为客户提供网络服务”的商业模式就不受GPL协议的约束
- AGPL = GPL + 一条限制
- 一条限制：如果使用AGPL许可的软件与用户通过网络进行交互，也需要提供源代码给用户，所有的修改也要给用户

### BSD
- 可以自由的使用，修改源代码，也可以将修改后的代码作为开源或者专有软件再发布
- 如果再发布的产品中包含源代码，则在源代码中必须带有原来代码中的BSD协议。
- 如果再发布的只是二进制类库/软件，则需要在类库/软件的文档和版权声明中包含原来代码中的BSD协议。
- 不可以用开源代码的作者/机构名字和原来产品的名字做市场推广

### MIT
- 和BSD一样宽范的许可协议,你必须在你的发行版里包含原许可协议的声明，无论你是以二进制发布的还是以源代码发布的
- 被授权人有权利使用、复制、修改、合并、出版发行、散布、再授权及贩售软体及软体的副本。
- 被授权人可根据程式的需要修改授权条款为适当的内容。
- 在软件和软件的所有副本中都必须包含版权声明和许可声明
- 甚至可以用原作者名字来推广

### MPL (Mozilla Public License)
- MPL虽然要求对于经MPL许可证发布的源代码的修改也要以MPL许可证的方式再许可出来，以保证其他人可以在MPL的条款下共享源代码。但是，在MPL 许可证中对“发布”的定义是“以源代码方式发布的文件”，这就意味着MPL允许一个企业在自己已有的源代码库上加一个接口，除了接口程序的源代码以MPL许可证的形式对外许可外，源代码库中的源代码就可以不用MPL许可证的方式强制对外许可。这些，就为借鉴别人的源代码用做自己商业软件开发的行为留了一个方式
- MPL许可证第三条第7款中允许被许可人将经过MPL许可证获得的源代码同自己其他类型的代码混合得到自己的软件程序。
- 要求源代码的提供者不能提供已经受专利保护的源代码
- 要求所有再发布者都得有一个专门的文件就对源代码程序修改的时间和修改的方式有描述
- MPL第二版与Apache许可证以及GPL第二版或更新、LGPL2.1版或更新，及AGPL第三版或更新兼容。而1.1版因为有“一些复杂的限制”造成与GPL的不兼容（从而阻止升级到MPL 2.0）

### EPL
- Eclipse Public License 1.0
    - 允许Recipients任意使用、复制、分发、传播、展示、修改以及改后闭源的二次商业发布
    - 当一个Contributors将源码的整体或部分再次开源发布的时候,必须继续遵循EPL开源协议来发布,而不能改用其他协议发布
    - 商业软件可以使用，也可以修改EPL协议的代码，但要承担代码产生的侵权责任


## 动态链接库 dll
- 大多数操作系统将解析外部引用（比如库）作为加载过程的一部分，可执行文件包含一个叫做import directory的表，该表的每一项包含一个库的名字。根据表中记录的名字，装载程序在硬盘上搜索需要的库，然后将其加载到内存中预先不确定的位置，之后根据加载库后确定的库的地址更新可执行程序。可执行程序根据更新后的库信息调用库中的函数或引用库中的数据。这种类型的动态加载称为装载时加载，被包括Windows和Linux的大多数系统采用，最复杂的工作之一就是 **加载时链接**。
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


## JavaFX 框架 前景 观点
- 参考
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
- 参考
    - 旧的swing项目当然不会轻易更换框架，而新的项目没人再选择Java了。FXML、硬件加速、MVVM思想都很好，但是这些别人也有，而且成熟得比Java早，何必要换成Java？Java要是真想在GUI翻身，还得像electron那样拿出点顺应潮流的东西、别人还没做好的东西。我觉得在WebAssembly是个方向。
    - 我很看好JAVAFX，我看好一切跨平台GUI方案，包括Qt（QML），这才是应该长期发展的技术。很多人扯H5的跨平台GUI方案，你要真的纯粹用H5，不跟本地软硬件资源有任何交互，只跟服务器端增删改查，我感觉也折腾不出什么激动人心的产品，还不如人家用Chrome直接访问呢。
    - 我这里只说PC端跨平台GUI，移动端我估计会在微信小程序上实现UI的大统一，毕竟小程序为Android和IOS提供了统一的软硬件资源框架（包括摄像头，蓝牙等硬件资源），同时又为用户提供了即用即走的便利性（免安装），还为开发者节省了大量的登陆逻辑和安全风险。
    - Electron的本质是一套用NodeJS控制的Chrominum，单纯用Electron估计也就只能做一个披着应用程序边框和标题栏的网页，跟Chrome建立桌面图标有点类似。真正开发一套商业或者工业级的企业程序，不调用个把dll/so估计是不现实的，而NodeJS调用dll或者so的开发体验和运行效率，要远远低于JNI，就更别提Qt这种原生态C++了。
    - 我理想中的跨平台GUI项目选型：移动端无一例外微信小程序解决；PC端，工程师熟悉JS就用Electron，不过要做好在NodeJS平台调用dll/so的基础功课。三种框架的开发体验Electron>JAVAFX>Qt，客户体验Qt>JAVAFX>Electron，平衡下来我觉得JAVAFX还算较好的选择
    - 如今的JavaFX也不过是袭人故技，用FXML布局，Java实现业务逻辑。性能上不如duilib，开发速度上又不如Web。虽然jdk11 已经能把javafx 独立出来了，但仍无可避免jre带来的臃肿体积。重点是由于不流行 **学的人少** ，根本没公司愿意用。而且由于浏览器性能越来越强，Web单页应用如火如荼，React, Vue都妇孺皆知了，重点是效果完全不输原生应用
    - Oracle的JDK在中文输入的场景一直做得很烂。特别是用搜狗输入法的时候，有很多意料之外的行为。包括JavaFX和Swing都有问题。目前基于Java的成熟的商业应用，都会包含自己魔改过的JRE。典型例子就是Jetbrains加的产品。之前是直接借助系统JDK运行的，但后来发生了滚动条失灵、中文输入法无法输入等问题后，就捆绑了基于OpenJDK的自家的Jetbreans JRE。
    - wps office 2019 addons文件夹包含软件各个组件，几乎都是html实现的，.kuip文件包含主题样式
    - wps未使用qml

## jackson-core源码结构
- JsonParser、JsonGenerator提供顶层读写抽象类、JsonFactory提供工厂方法
- io包提供输入输出方法：跳过特殊字符、encode/decode、mergedStream、utf8->utf32
- json包提供读写具体实现
  - async提供非阻塞的异步读写方法
- format包提供数据格式匹配方法
- filter提供数据过滤方法
- sym包提供特殊符号的处理方法
- type包提供泛型处理方法
- util包提供各种工具类

### jackson-core处理json
- ObjectMapper提供解析器和生成器的入口
- JsonParser提供底层json解析器
- JsonGenerator提供底层json生成器
- JsonParser的工作原理
  - 将JSON分解成一系列的token，然后迭代token解析，token类型由JsonToken中一系列的常量来表示
  - 如果token指向的是字段名称，JsonParser的getCurrentName()方法返回当前字段的名称。
  - 如果token指向的是字符串字段值，getValueAsString()方法以字符串的形式返回当前token的值，JsonParser还有更多相似的方法，如getText()

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

## SAX解析XML方法执行顺序
1. startDocument()：开始处理文档；
2. startElement(String uri, String localName, String qName, Attributes attributes)：处理元素的开始；
3. characters(char[] ch, int start, int length)：用来读取文本内容；
4. endElement(String uri, String localName, String qName)：元素处理结束；
5. endDocument()：文档处理结束
- 参考 
    - 在开始处理标签后，如`<books>`或`</title>`后，会立即调用一次characters()方法，并且在ide里面debug时无法直接追踪  
    - 若两个xml标签之间无间隔，则不会调用characters()方法，如`<title>aa</title><author>bb</author>`

### jdk xml解析 sax方式 方法顺序
- sax中DefaultHandler解析XML的总体过程   
startDocument --> 具体读到某个node（非根node和根node）的解析过程 --> endDocument  

- 解析XML非根node的顺序  
 startElement --> characters --> endElement --> characters    
(endElement后会再调用一次characters方法)    

- 解析XML根node的顺序
 startElement --> characters --> endElement  


## XML的生成
- SAX parsing is for reading documents, not writing them. You can write XML with the XMLStreamWriter.
- Generating XML via Java (https://www.techrepublic.com/article/generating-xml-via-java/)
  - Using the StringBuffer class
  - Using DOM
  - Using SAX
  - Using a custom XmlWriter class

## xlsx Excel2007 常用标签结构
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

## apache poi
- poi Class SharedStringsTable
    - Table of strings shared across all sheets in a workbook.
    - When displaying text in the spreadsheet, the cell table will just contain an index into the string table as the value of a cell, instead of the full string.
- poi各jar包作用
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

    
## cs-summary
- npm list -g -depth=0
  - 列出本地已安装的包
- npx
  - npm从5.2版开始，增加了 npx 命令
  - npx 想要解决的主要问题，就是调用项目内部安装的模块
  - 若要调用Mocha，一般只能在项目脚本和package.json的scripts字段里面，如果想在命令行下调用，必须 `node-modules/.bin/mocha --version`
  - npx让项目内部安装的模块用起来更方便 `npx mocha --version`
  - npx的原理就是运行的时候，会到node_modules/.bin路径和环境变量$PATH里面，检查命令是否存在
  - 由于npx会检查环境变量$PATH，所以系统命令也可以调用 `npx ls -ll`
- build tool
    - bazel：由google开发维护，支持Java/C++，支持Android
    - buck：由facebook开发，支持Android/iOS，移动端支持更好
- java中InputStream实例化时，文件是否已经读完了？
    - no???
- Java File
    - FileInputStream reads the file byte by byte
      - Abstract class is the superclass of all classes representing an input stream of bytes.
      - 读取字节流，可处理二进制内容
    - FileReader reads the file character by character
      - Reader - Abstract class for reading character streams 
      - 读取字符流，一般用于处理文本，不处理视频文件
- jdk webview js engine
    - The full Oracle Java Runtime 8 ships with two JavaScript engines
    - Nashorn: "Nashorn's goal is to implement a lightweight high-performance JavaScript runtime in Java with a native JVM. This Project intends to enable Java developers embedding of JavaScript in Java applications via JSR-223 and to develop free standing JavaScript applications using the jrunscript command-line tool."
    - JavaScriptCore: The JavaScript engine built into the WebKit implementation wrapped by WebView component the JavaFX system.
    JavaScript Runtime Used by WebView and JavaFX applications
    - JavaFX Webkit does not use Nashorn, it uses JavaScriptCore.
- 如何遍历文件夹下上亿文件而不栈溢出   
    - 考虑层序遍历   
    - https://www.cnblogs.com/intsmaze/p/6031894.html
- java string 
    - StringReader
    - String Pool是一个固定大小的Hashtable，默认大小是1009，如果放入常量池的字符串过多，就会造成hash冲突，导致链表很长，而链表长了后直接会造成的影响就是当调用String.intern时性能会大幅下降
    - 直接使用双引号声明出来的String对象会直接存储在常量池中
    - intern 方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中
    - 在Jdk6以及以前的版本中，字符串的常量池是放在堆的Perm区的，Perm区是一个类静态的区域，主要存储一些加载类的信息，常量池，方法片段等内容，默认大小只有4m，一旦常量池中大量使用 intern 是会直接产生java.lang.OutOfMemoryError: PermGen space错误的。 所以在jdk7的版本中，字符串常量池已经从Perm区移到Java Heap区。jdk8已经直接取消了Perm区，而新建立了一个元区
- maven的packaging为bundle
    - bundle是OSGI中的依赖单元，是一种特殊格式的jar
    - `<dependency>`的type也可以为bundle
- JPMS  
    - Java Platform Module System (JSR 376)，也就是Jigsaw项目   
- java枚举类与switch使用
    - enum switch case label must be the unqualified name of an enumeration constant   
    - switch指定枚举类后，case后只能用枚举类的非限定名，不要再写枚举类了
- REPL 交互式编程环境 (Read-Eval-Print-Loop) 
    - jShell
    - python 
    - babel-node(有babel-cli提供)
- targe=_blank
    - 当一个外部链接使用了target=_blank的方式，这个外部链接会打开一个新的浏览器tab。此时，新页面会打开，并且和原始页面占用**同一个进程**(UI进程)。
    - 这也意味着，如果这个新页面有任何性能上的问题，比如有一个很高的加载时间，这也将会影响到原始页面的表现。
    - 如果你打开的是一个同域的页面，那么你将可以在新页面访问到原始页面的所有内容，包括document对象(window.opener.document)。
    - 如果你打开的是一个跨域的页面，你虽然无法访问到document，但是你依然可以访问到location对象。
- node依赖
    - dependencies
        - 是最常用普通业务依赖
    - devDependencies
        - 开发环境依赖，常用来指定打包、测试工具
    - peerDependencies
        - 比较适合插件库来声明所依赖的核心库，将依赖提升到根目录避免重复下载
        - 指定当前包（也就是你写的包）兼容的宿主版本
        - 可以避免类依赖库被重复下载
            - 如果用户显式依赖了核心库，则可以忽略各插件的peerDependency声明
            - 如果用户没有显式依赖核心库，则按照插件peerDependencies中声明的版本将库安装到项目根目录中
            - 当用户依赖的版本、各插件依赖的版本之间不相互兼容，貌似会报错让用户自行修复
    - optionalDependencies
        - 可选依赖，它们即使安装失败，npm仍然继续运行
    - bundleDependencies
        - 在发布时会将指定的包打包到最终的发布包里
        - undleDependencies节点的功能跟dependencies节点是一样的，区别在于，当需要构建项目并发布版本时，bundleDependencies节点下的依赖会被包含在构建结果中，不需要另外npm install来安装了
    - 参考
        - https://github.com/SamHwang1990/blog/issues/7
- node-path
    - `path.join(path1，path2，path3.......)`
        - 先解析相对路径..，再拼接返回，path片段/docs,./docs,docs三种方式处理无差别
        - 用平台特定的分隔符把全部给定的path片段连接到一起，并规范化生成的路径
        - path片段前的`./`可有可无，只进行路径拼接
        - `path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');`
            - 返回: '/foo/bar/baz/asdf'
    - `path.resolve([from...],to)`
        - 先解析路径，再生成绝对路径返回，./docs,docs相同，/docs会作为绝对路径起点
        - 按参数从左向右，把路径片段的序列解析为一个**绝对路径**，一定生成绝对路径
        - path.resolve('/foo', '/bar', 'baz') 会返回 /bar/baz
    - `__dirname`
        - Node.js中的文件路径大概有 __dirname, __filename, process.cwd(), ./ 或者 ../
            - 前3者都是绝对路径
        - `__dirname`：    当前执行文件所在目录的绝对路径
        - `__filename`：   当前执行文件的带有完整绝对路径文件名的绝对路径
        - `process.cwd()`：当前执行node命令时候的文件夹目录名 
        - `./`：跟process.cwd()一样，返回node命令时所在的文件夹的绝对路径
        - `require(./a.js)`：当node遇到require时，会相对当前执行文件查找
        - 建议：只在require()中才使用相对路径(./, ../)的写法，其他地方一律绝对路径
- html a标签属性 rel='nofollow'
    - 告诉搜索引擎不要此网页上的链接或不要追踪此特定链接
    - 使用场景
        - 屏蔽广告/付费链接的权重
        - 屏蔽恶意用户
        - 划分优先级
    - rel="noopener noreferrer"可以取消传递相关信息
- The main difference between Cyan and Teal is that the Cyan is a color visible between blue and green; subtractive (CMY) primary color and Teal is a low-saturated color, a bluish-green to dark medium, similar to medium blue-green and dark cyan.
- 语言地区代码的构成，如en-US, zh-CN
    - The syntax and registry of HTTP language tags is the same as that defined by RFC 1766 
    - a language tag is composed of 1 or more parts: A primary language tag and a possibly empty series of subtags
    - any two-letter primary-tag is an ISO-639 language abbreviation and any two-letter initial subtag is an ISO-3166 country code.
    - 参考 https://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html
- 渐进式图片  
    - JPEG、GIF和PNG这三种图像格式都提供了一种功能，让图像能够更快地显示图像可以以一种特殊方式存储，显示时先大概显示图像的草图，当文件全部下载后再填充细
- file-loader will copy files to the build folder and insert links to them where they are included. 
- url-loader will encode entire file bytes content as base64 and insert base64-encoded content where they are included. So there is no separate file.
- The url-loader works like the file-loader, but can return a DataURL if the file is smaller than a byte limit.
- 获取数组中随机元素
    - ` arr[Math.floor(Math.random()*(arr.length))]`
- `performance.now()` vs `date.now()`
    - performance.now() returns the number of milliseconds, with microseconds in the fractional part and is more precise in orders of magnitude. 精度更高，不依赖系统时间，但在大型循环中使用会明显感觉慢，输出的是相对于performance.timing.navigationStart(页面初始化)的时间
        - Use cases include benchmarking and other cases where a high-resolution time is required such as media (gaming, audio, video, etc.)
        - performance.now() is only available in newer browsers (including IE10+).可能会有兼容性问题
    - Date.now() returns the number of milliseconds elapsed since Unix epoch(1 January 1970 00:00:00 UTC) and is dependent on system clock.会因为系统时间的变化而改变，准确性有时不能保证
        - Use cases include same old date manipulation ever since the beginning of JavaScript.
- typescript typeof
```
let bar = {a: 0};
let TypeofBar = typeof bar;  // the value "object"
type TypeofBar = typeof bar; // the type {a: number}
```
- Object.prototype.hasOwnProperty.call(obj, attrName);
    - obj.hasOwnProperty(prop)判断一个属性是定义在对象本身而不是继承自原型链
        - 调用的是js中Object对象原型上的hasOwnProperty()方法
    - js没有将hasOwnProperty作为一个敏感词，所以我们很有可能将对象的一个属性命名为hasOwnProperty，这样一来就无法再使用对象原型的hasOwnProperty 方法来判断属性是否是来自原型链，解决方法有几种
        - ({}).hasOwnProperty.call(foo, 'bar'); // true
        - Object.prototype.hasOwnProperty.call(foo, 'bar');
- TypeScript 3.0在JSX命名空间中引入了一个新的类型别名`LibraryManagedAttributes`
    - 这是一个辅助类型，用于告诉TypeScript某个JSX标记可以接受哪些属性
    - TypeScript 3.0 adds support for a new type alias in the JSX namespace called LibraryManagedAttributes. 
    - This helper type defines a transformation on the component’s Props type, before using to check a JSX expression targeting it; thus allowing customization like: how conflicts between provided props and inferred props are handled, how inferences are mapped, how optionality is handled, and how inferences from differing places should be combined.
    - The default-ed properties are inferred from the defaultProps property type. If an explicit type annotation is added, e.g. static defaultProps: `Partial<Props>`; the compiler will not be able to identify which properties have defaults
    - Use static defaultProps: `Pick<Props, "name">` as an explicit type annotation instead


