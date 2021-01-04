---
title: lib-fwk-spring-dev
tags: [docs, spring]
created: '2019-08-01T16:03:46.394Z'
modified: '2020-12-08T13:28:14.387Z'
---

# lib-fwk-spring-dev

# guide

- features

- usecase
  - ioc

- who is using
  - more

- examples
  - libs

- tips

# dev-tips

- WebMvcConfigurationSupport精简了5个方法
  - beanNameHandlerMapping()
  - mvcResourceUrlProvider()
  - mvcValidator()
  - mvcUriComponentsContributor()
  - mvcViewResolver()
- spring处理带有@Configuration注解的类时，先子类再父类，一直上溯到java.lang. Object
  - 但保存bean方法到configurationClasses时，用的是子类，而不是父类
- play-mvc处理带有@Configuration注解的类时，只处理子类，以及子类继承的带有@Bean注解标注的方法
- AnnotationConfigUtils.attributesForRepeatable() 获取注解的所有属性

# faq

- SqlSessionTemplate何时实例化的
- @Bean标注的方法如何注入参数
- properties属性文件何时读取的
- sqlSessionFactory如何autowire到sqlSessionFactoryBean

### spring 常用注解

- @ResponseBody表示该方法的返回结果直接写入HTTP response body中  
  - @ResponseBody and ContentNegotiatingViewResolver are two alternatives for the same thing. 
- @RequestBody

### spring mvc

- ssm实例化时的连续依赖： bookServiceImpl -> bookDao -> sqlSessionFactoryBean -> DaoConfig
- SqlSessionFactory注入的过程中，使用了SqlSessionFactoryBean
- 在实例化bookServiceImpl的过程中，实例化了daoConfig

- `<mvc:default-servlet-handler />` 对应的实现类为DefaultServletHttpRequestHandler，它会像对进入DispatcherServlet的URL进行筛查，

如果发现是静态资源的请求，就将该请求转发给Web应用服务器默认的Servlet处理，如果不是静态资源的请求，才由DispatcherServlet继续处理

- `<mvc:resources />` 则由Spring MVC框架自己处理静态资源，将请求交给SimpleUrlHandlerMapping，
  - 支持将静态的资源映射为classpath中的资源（jar 包中），这样就可以使用dojo等技术对静态资源指定版本。防止服务器端更新了而客户端使用老版本的问题
  - 支持cache-period属性，减少客户端因为获取静态资源而访问服务器的次数

- controller的返回值
  - ModelAndView
  - Model
  - ModelMap
  - Map
  - View
  - String
  - Void

- @ControllerAdvice
  - 一般用作处理系统error，拦截出错信息，返回报错提示界面
  - @ControllerAdvice注解内部使用@ExceptionHandler、@InitBinder、@ModelAttribute注解的方法应用到所有的 @RequestMapping注解的方法

- 非注解的处理器映射器与适配器
  - SimpleUrlHandlerMapping
  - SimpleControllerHandlerAdapter

- spring AnnotatedBeanDefinitionReader 默认注册的beanDefinition
  - org.springframework.context.annotation. CommonAnnotationBeanPostProcessor
  - org.springframework.context.annotation. ConfigurationClassPostProcessor
  - org.springframework.beans.factory.annotation. RequiredAnnotationBeanPostProcessor
  - org.springframework.beans.factory.annotation. AutowiredAnnotationBeanPostProcessor

- ServletContext与ApplicationContext相关概念
  - ServletContext：此接口定义了一系列的方法，可以很方便地与所在的容器进行一些交互，比如通过getMajorVersion与getMinorVersion来获取容器的版本信息等，

    在一个应用中(一个JVM)只有一个ServletContext, 换句话说，容器中所有的servlet都共享同一个ServletContext.

  - ServletConfig: servletConfig是针对servlet而言的，每个servlet都有它独有的serveltConfig信息，相互之间不共享
  - ROOT_WEB_APPLICATION_CONTEXT_ATTRIBUTE

  

- spring mvc 父子上下文/容器
  - Tomcat启动时，监听器ContextLoaderListener创建一个XMLWebApplicationContext上下文容器，

    并加载context-param中的配置文件，完成容器的刷新后将上下文设置到ServletContext。

  - 当DispatcherServlet创建时，先进行初始化操作，从ServletContext中查询出监听器中创建的上下文对象，

    作为父类上下文来创建servlet的上下文容器，并加载Servlet配置中的init-param的配置文件
    (默认加载/WEB-INF/servletName-servlet.xml，servletName为DispatcherServlet配置的servlet-name)，然后完成容器的刷新。

  - 子上下文可以访问父上下文中的bean，反之则不行
  - 通常是将业务操作及数据库相关的bean维护在Listener的父容器中，而在Servlet的子容器中只加载Controller相关的业务实现的bean。
  - 从而将业务实现和业务的具体操作分隔在两个上下文容器中，业务实现bean可以调用业务具体操作的bean。

- HttpMessageConverter接口指定了一个可以把Http request信息和Http response信息进行格式转换的转换器。通常实现HttpMessageConverter接口的转换器有以下几种：
  - ByteArrayHttpMessageConverter: 负责读取二进制格式的数据和写出二进制格式的数据；
  - StringHttpMessageConverter： 负责读取字符串格式的数据和写出二进制格式的数据；
  - ResourceHttpMessageConverter：负责读取资源文件和写出资源文件数据；
  - FormHttpMessageConverter： 负责读取form提交的数据（能读取的数据格式为 application/x-www-form-urlencoded，不能读取multipart/form-data格式数据）；负责写入application/x-www-from-urlencoded和multipart/form-data格式的数据；
  - MappingJacksonHttpMessageConverter: 负责读取和写入json格式的数据；
  - SourceHttpMessageConverter： 负责读取和写入 xml 中javax.xml.transform. Source定义的数据；
  - Jaxb2RootElementHttpMessageConverter: 负责读取和写入xml 标签格式的数据；
  - AtomFeedHttpMessageConverter: 负责读取和写入Atom格式的数据；
  - RssChannelHttpMessageConverter: 负责读取和写入RSS格式的数据；

  

- Flash属性
  - flash attributes提供了一个请求为另一个请求存储有用属性的方法。

    这在重定向的时候最常使用，比如常见的 POST/REDIRECT/GET 模式。Flash属性会在重定向前被暂时地保存起来（ 通常是保存在session中） ，
    重定向后会重新被下一个请求取用并立即从原保存地移除。

  - FlashMap 被用来存储flash属性，而用 FlashMapManager 来存储、取回、管理 FlashMap 的实例
  - 控制器通常不需要直接接触 FlashMap 。一般是通过 @RequestMapping 方法去接受一个 RedirectAttributes 类型的参数，

    然后直接地往其中添加flash属性。通过 RedirectAttributes 对象添加进去的flash属性会自动被填充到请求的“输出” FlashMap 对象中去
    

- handlerMapping
  - 一个url路径和一个函数配对，你访问这个url，就会直接调用这个函数，第一步首先要找到是哪个对象，即handler，本工程的handler则是HomeAction对象，

  第二步要找到访问的函数，即HomeAction的handleRequest方法，所以就出现了两个源码接口 HandlerMapping和HandlerAdapter，前者负责第一步，后者负责第二步

  - DefaultServletHttpRequestHandler会对进入DispatcherServlet的URL进行筛查，如果发现是静态资源的请求，

  就将该请求转由Web应用服务器默认的Servlet处理，如果不是静态资源的请求，才由DispatcherServlet继续处理

- 获取DispatcherServlet的映射信息
  - `/` ：拦截所有请求，包括静态资源xx.js, xx.png，但是不包括*.jsp
  - `/*` ：拦截所有请求；连*.jsp页面都拦截，jsp页面是tomcat的jsp引擎解析的
  - `/*` 的优先级大于 `.jsp` 的优先级，.jsp的优先级大于 `/`
- @WebServlet和@WebFilter进行Servlet或Filter配置的情况，两个注解都提供了asyncSupported 属性，默认该属性的取值为false，默认不支持异步处理

- Servlet3.0提供了ServletContainerInitializer接口，支持web应用启动阶段动态注册servlet，filter和listener
  - 必须在对应的jar包的META-INF/services 目录创建一个名为javax.servlet. ServletContainerInitializer的文件，文件内容指定具体的ServletContainerInitializer实现类
  - 一般伴随着ServletContainerInitializer一起使用的还有HandlesTypes注解，可以将感兴趣的一些类注入到ServletContainerInitializerde的onStartup方法作为参数传入
  - Context容器启动时就会分别调用每个ServletContainerInitializer的onStartup方法，并将感兴趣的类作为参数传入

- WebRequest是Spring Web MVC提供的统一请求访问接口，不仅仅可以访问请求相关数据（如参数区数据、请求头数据，但访问不到Cookie区数据），

还可以访问会话和上下文中的数据；

- NativeWebRequest继承了WebRequest，并提供访问本地Servlet API的方法。

- Servlet生命周期的三个阶段，就是所谓的init-service-destroy
- Servlet生命周期的service阶段中，每一次Http请求到来，容器都会启动一个请求线程，通过service()方法，委派到doGet()或者doPost()这些方法，完成Http请求的处理
- 在初始化流程中，SpringMVC巧妙的运用依赖注入读取参数，并最终建立一个与容器上下文相关联的Spring子上下文。

- DispatcherServlet类的初始化入口方法init()定义在HttpServletBean这个父类中
- ContextLoaderListener所初始化的这个Spring容器上下文，被称为根上下文
- 在DispatcherServlet的初始化过程中，同样会初始化一个WebApplicationContext的实现类，作为自己独有的上下文，会将上面的根上下文作为自己的父上下文

- RedirectView跳转时会将跳转之前的请求中的参数保存到FlashMap中，然后通过FlashManager保存起来

- SpringServletContainerInitializer
  - 实现了Servlet3.0的ServletContainerInitializer接口，且优先级会高于xml中配置的listener
  - 用户可以选择是否提供WebApplicationInitializer实现，如果未检测到WebApplicationInitializer类型，则此SpringServletContainerInitializer将不起作用
  - 如果在类路径下找不到WebApplicationInitializer实现，则此方法不会有任何操作。将发出INFO级别的日志消息，通知用户ServletContainerInitializer确实已被调用，但没有找到WebApplicationInitializer实现。
  - 假设检测到一个或多个WebApplicationInitializer类型，它们将被实例化（如果存在@Order注释或实现Ordered接口，则对其进行排序）。然后，将调用每个实例WebApplicationInitializer.onStartup(ServletContext)方法，并委派ServletContext，以便每个实例都可以注册和配置Servlet，例如Spring的DispatcherServlet，listeners（如Spring的ContextLoaderListener），或者其他Servlet API组件（如filters）

    

- HttpServletBean 以依赖注入的方式来读取Servlet类的<init-param>配置信息
- FrameworkServlet完成的是容器上下文的建立
- DispatcherServlet完成的是SpringMVC具体编程元素的初始化策略

- DispatcherServlet
  - 是一个标准的Servlet，它的作用是接收和转发web请求到内部框架处理单元
  - 作为前端控制器，处理流程：
      - 一个http请求到达服务器，被DispatcherServlet接收。DispatcherServlet将请求委派给合适的处理器Controller，此时处理控制权到达Controller对象。
      - Controller内部完成请求的数据模型的创建和业务逻辑的处理，然后再将填充了数据后的模型即model和控制权一并交还给DispatcherServlet，委派DispatcherServlet来渲染响应。
      - DispatcherServlet再将这些数据和适当的数据模版视图结合，向Response输出响应。
  - HandlerAdapter是扩展点，可以提供自己的实现类来处理handler对象

- HandlerMapping接口
  - 扩展点
  - `HandlerExecutionChain getHandler(HttpServletRequest request)`
  - HandlerMapping的实现类可以利用HttpServletRequest中的 所有信息来做出这个HandlerExecutionChain对象的生成
  - 可以编写任意的HandlerMapping实现类，依据任何策略来决定一个web请求到HandlerExecutionChain对象的生成

- HandlerExecutionChain
  - 有属性 `HandlerInterceptor[] interceptors`
  - 在真正调用其handler对象前，HandlerInterceptor接口实现类组成的数组将会被遍历，其 `preHandle()` 方法会被依次调用，然后真正的handler对象将被调用
  - 在将处理结果写到HttpServletResponse对象之前（SpringMVC称为渲染视图），其 `postHandle()` 方法会被依次调用
  - 视图渲染完成后，最后 `afterCompletion()` 方法会被依次调用，整个web请求的处理过程就结束了
  - 在一个处理对象执行之前，之后利用拦截器做文章，这已经成为一种经典的框架设计套路

  

- HandlerInterceptor
  - 扩展点3位置
  - 通过自定义拦截器，可以在一个请求被真正处理之前、请求被处理但还没输出到响应中、请求已经被输出到响应中之后这三个时间点去做任何事情

- HandlerAdapter  

  

- ModelAndView是SpringMVC中对视图和数据的一个聚合类
  - 所有的数据，最后会作为一个Map对象传递到View实现类中的render方法，调用这个render方法，就完成了视图到响应的渲染
  - 这个View实现类，就是来自HandlerAdapter中的handle方法的返回结果
  - 从ModelAndView到真正的View实现类有一个解析的过程，ModelAndView中可以有真正的视图对象，也可以只是有一个视图的名字

  

- web开发主要任务
  - url映射
  - http请求参数绑定
  - http响应输出

### spring

- EventListenerMethodProcessor这个beanPostProcessor较特殊
  - 初始化了AspectJExpressionPointcut类的shadowMatchCache

- singletonObjects里面的对象可以比beanDefinitionMaps的多

- 创建代理对象时，aspect切面对象可以不存在

- Advice接口是AOP联盟定义的一个空的标记接口，Advice有几个子接口：
  - BeforeAdvice，前置增强，意思是在我们的目标类之前调用的增强。这个接口也没有定义任何方法。
      - MethodBeforeAdvice接口，是BeforeAdvice的子接口，表示在方法前调用的增强，方法前置增强不能阻止方法的调用，但是能抛异常来使目标方法不继续执行。
  - AfterReturningAdvice，方法正常返回前的增强，该增强可以看到方法的返回值，但是不能更改返回值，该接口有一个方法afterReturning
  - ThrowsAdvice，抛出异常时候的增强，也是一个标志接口，没有定义任何方法。
  - Interceptor，拦截器，也没有定义任何方法，表示一个通用的拦截器，不属于Spring，是AOP联盟定义的接口
      - MethodInterceptor不属于Spring，是AOP联盟定义的接口，是Interceptor的子接口，我们通常叫做环绕增强，抽象方法是 `Object invoke(MethodInvocation invocation) throws Throwable;`
      - MethodInterceptor用来在目标方法调用前后做一些事情，参数MethodInvocation是一个方法调用的连接点，返回的是invocation.proceed()方法的返回值
      - JointPoint接口，是一个通用的运行时连接点，运行时连接点是在一个静态连接点发生的事件
      - Invocation接口是Joinpoint的子接口，表示程序的调用，一个Invocation就是一个连接点，可以被拦截器拦截
      - MethodInvocation接口是Invocation的子接口，用来描述一个方法的调用。
      - ConstructorInvocation接口是Invocation的子接口，描述的是构造器的调用
  - DynamicIntroductionAdvice，动态引介增强，有一个方法implementsInterface。

- 经常使用的内部Bean名称
  - org.springframework.context.annotation.internalConfigurationAnnotationProcessor
      - class org.springframework.context.annotation.ConfigurationClassPostProcessor
  - org.springframework.context.annotation.internalAutowiredAnnotationProcessor
      - class org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor
  - org.springframework.context.annotation.internalCommonAnnotationProcessor
      - class org.springframework.context.annotation.CommonAnnotationBeanPostProcessor
  - org.springframework.context.annotation.internalRequiredAnnotationProcessor
      - class org.springframework.beans.factory.annotation.RequiredAnnotationBeanPostProcessor

- BeanPostProcessor
  - postProcessBeforeInitialization 初始化前扩展(执行init-method前)
  - postProcessAfterInitialization 初始化后扩展(执行init-method后)
- InstantiationAwareBeanPostProcessor
  - postProcessBeforeInstantiation 对象实例化前扩展
  - postProcessAfterInstantiation 对象实例化后扩展
  - postProcessPropertyValues 属性依赖注入前扩展
- SmartInstantiationAwareBeanPostProcessor
  - predictBeanType 预测bean的类型，在beanFactory的getType时被调用
  - determineCandidateConstructors 对象实例化时决定要使用的构造函数时被调用
  - getEarlyBeanReference 循环依赖处理时获取Early对象引用时被调用

- aop相关
  - aspect：包含advice和point cut
  - advice：增强处理
  - advisor：将目标对象、增强行为和切入点三者结合起来，即通过Advisor可以定义那些目标对象的那些方法在什么地方使用这些增加的行为
  - join point：要匹配的方法调用处
  - point cut：公共可重用的匹配表达式
  - 创建代理对象
      - JdkDynamicAopProxy
          - getProxy()
      - CglibAopProxy
          - getProxy()
  - 获取匹配advice AnnotationAwareAspectAutoProxyCreator
      - findCandidateAdvisors()
      - findAdvisorsThatCanApply()

- @Bean和@Component区别
  - @Component是lite-mode，bean：class -> 1:1
  - @Bean是显式声明bean定义，bean：class -> N:1
  - @Component用于type，@Bean用于方法

- `@Order` 注解可以控制配置类的加载顺序，数值越小，优先级越高

- 常用的后处理器
  - BeanFactoryPostProcessor
      - 在容器注册了BeanDefinition之后，实例化之前执行，通过这个接口可以获取Bean定义的元数据并且修改它们，如Bean的scope属性、property值等，也可以操作beanFactory
      - ConfigurationClassPostProcessor
  - BeanPostProcessor
      - 在Bean实例化完毕后执行，所以任何BeanPostProcessor都是在BeanFactoryPostProcessor之后执行的，可以实现自动注入、各种代理(AOP)等

- BeanDefinition
  - 对于GenericBD和ChildBD，parentName可以有
  - 对于RootBD，parentName不存在，getParentName()始终返回空

  

- spring扩展点
  - 用BeanPostProcessor定制bean实例化后的初始化逻辑，发生在 `doCreateBean()` -> `initializeBean()`
      - 实现该接口可提供自定义（或默认地来覆盖容器）的实例化逻辑、依赖解析逻辑等
      - 如果配置了多个BeanPostProcessor，那么可以通过设置 `order` 属性来控制执行次序
      - BeanPostProcessor仅对所在容器中的bean进行后置处理，将不会对定义在另一个容器中的bean进行后置处理
      - AOP自动代理实现了BeanPostProcessor，所以BeanPostProcessors或bean的直接引用不会被自动代理
  - 用BeanFactoryPostProcessor定制BeanDefinition元数据，发生在 `refresh()` -> `invokeBeanFactoryPostProcessors()`
      - BeanFactoryPostProcessor在容器实际实例化任何其它的bean之前读取配置元数据，并有可能修改它
  - FactoryBean接口是插入到Spring IoC容器用来定制实例化逻辑的一个接口点

  

- spring createBean()顺序
  - doCreateBean()之前， `resolveBeforeInstantiation()` 可提前返回 beanPostProcessor处理过得bean
  - beanFactoryAware和beanNameAware的处理是在 `doCreateBean() -> initializeBean()`
  - `initializeBean()` 方法中先执行 xxAware，再执行 afterPropertiesSet()

  

- - spring注解扫描解析
    - @ComponentScan: ConfigurationClassParser.doProcessConfigurationClass()
    - @Component: ClassPathScanningCandidateComponentProvider.findCandidateComponents()
    - @Configuration: ConfigurationClassPostProcessor.processConfigBeanDefinitions()
    - @Bean: ConfigurationClassParser.doProcessConfigurationClass()

    

- AbstractApplicationContext类 refresh() 

  1) prepareRefresh(); 

      - 初始化前的准备工作，如对系统属性或者环境进行准备及验证

  2) ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory(); 

      - 初始化BeanFactory，并进行XML文件读取

  3) prepareBeanFactory(beanFactory); 

      - 对BeanFactory进行各种功能填充

  4) postProcessBeanFactory(beanFactory); 

      - 初始化前的准备工作，如对系统属性或者环境进行准备及验证

  5) invokeBeanFactoryPostProcessors(beanFactory); 

      - 激活各种BeanFactory处理器
      - 扫描 `@Configuration` 和 `@Bean`

  6) registerBeanPostProcessors(beanFactory); 

      - 拦截bean创建的bean处理器，这里只是注册，真正的调用是在getBean时候
      - 将各种BeanDefnition转换成RootBeanDefinition，如Annotated, Scanned
      - 扫描 `@Bean` ，将各种BeanDefnition转换成RootBeanDefinition，包括 `ConfigurationClassBeanDefinition`

  7) initMessageSource(); 

      - 为上下文初始化Message源，即对不同语言的消息体进行国际化处理

  8) initApplicationEventMulticaster(); 

      - 初始化应用消息广播器，并放入 `applicationEventMulticaster` bean中

  9) onRefresh(); 

      - 留给子类来初始化其他的bean

  10) registerListeners(); 

      - 在所有注册的bean中查找listenerbean，注册到消息广播器中

  11) finishBeanFactoryInitialization(beanFactory); 

      - 初始化剩下的单例(非懒加载)

  12) finishRefresh(); 

      - 完成刷新过程，通知生命周期处理器lifecycleProcessor刷新过程，同时发出ContextRefreshEvent通知别人

  

- spring aop概念
  - aspect：切面
  - advice：增强处理的通知
  - pointcut：切入点，通过切入点表达式定义，添加了增强处理通知的方法调用处
  - joinpoint：连接点，所有方法调用处

  

- 扫描basePackage  
  - ComponentScanBeanDefinitionParser解析xml中配置的 `<context:component-scan base-package="a.b" />`
  - ClassPathBeanDefinitionScanner解析直接传入的包名

  

- dependenciesForBeanMap记录bean之间的依赖关系有两方面的作用：  
  - 在单例情况下，可以指定相互依赖bean之间的销毁顺序
  - 避免循环依赖

  

- spring doGetBean()方法执行顺序  
  - getSingleton()
  - new ObjectFactory(){}
  - createBean()

  

- spring bean配置不同类型方法的执行顺序，从先到后：
  - postProcessBeforeInitialization
  - afterPropertiesSet
  - init-method
  - postProcessAfterInitialization

  

- spring doCreateBean()方法中3个重要的任务
  - 创建实例：createBeanInstance(beanName, mbd, args); -> BeanWrapper
  - 注入属性：populateBean(beanName, mbd, instanceWrapper); -> void
  - 执行初始化方法：initializeBean(beanName, exposedObject, mbd); -> Object(bean instance)    
      - 先执行实现了InitializingBean接口的afterPropertiesSet()，再执行配置的init-method名称的方法

- spring autowired 注入方式

  -@Autowired默认通过byType注入，若存在多个实现类，byType有歧义，则需通过byName的方式来注入，name默认就是根据变量名来的

  - @Autowired只有required属性可以设置，默认为true
  - 如果想通过指定具体的bean的名称，可以使用@Qualifier
  - @Autowired的解析器是AutowiredAnnotationBeanPostProcessor

  

- PropertyEditor  
  - 由于Bean属性通过配置文档以字符串了方式为属性赋值，属性编辑器负责将这个字符串转换为属性的直接对象，如属性的类型为int，那编辑器的工作就是 `int i = Integer.parseInt("1");`
  - Spring为一般的属性类型提供了默认的编辑器，BeanWrapperImpl负责对注入的Bean进行包装化的管理，常见属性类型对应的编辑器即在该类中定义

  

- spring对于没有无参构造器的bean就利用CGLIB生成实例，否则就直接反射成实例

- spring xml中id和name区别  
  - name可配置多个别名  
  - The id attribute allows you to specify exactly one id. Conventionally these names are alphanumeric ('myBean', 'fooService', etc), but may special characters as well. If you want to introduce other aliases to the bean, you can also specify them in the name attribute, separated by a comma (, ), semicolon (; ), or white space. 

  

- 重要实现模块
  - BeanDefinition
  - BeanDefinitionReader
  - Resource
  - BeanFactory
  - ApplicationContext

  

- BeanDefinitionReader
  - BeanDefinitionRegistry接口一次只能注册一个BeanDefinition，而且只能自己构造BeanDefinition类来注册。   
  - BeanDefinitionReader解决了这些问题，它一般可以使用一个BeanDefinitionRegistry构造，然后通过#loadBeanDefinitions（..）等方法，把“配置源”转化为多个BeanDefinition并注册到BeanDefinitionRegistry中  
  - 可以说BeanDefinitionReader帮助BeanDefinitionRegistry实现了高效、方便的注册BeanDefinition。

  

- spring3个核心组件
  - core：工具包
  - context：运行环境，读取bean配置、管理bean关系
  - beans：bean定义、解析、创建

  

- BeanFactory
  - BeanFactory 有三个子类：ListableBeanFactory、HierarchicalBeanFactory 和 AutowireCapableBeanFactory。      
  - 最终的默认实现类是 DefaultListableBeanFactory，实现了所有的接口  

- objenesis
  - objenesis是一个小型java类库用来实例化一个特定class的对象。
  - 使用场合：Java已经支持使用Class.newInstance()动态实例化类的实例。但是类必须拥有一个合适的构造器。有很多场景下不能使用这种方式实例化类，比如：
      - 构造器需要参数
      - 构造器有side effects
      - 构造器会抛异常
      - 因此，在类库中经常会有类必须拥有一个默认构造器的限制。Objenesis通过绕开对象实例构造器来克服这个限制。
  - 典型使用: 实例化一个对象而不调用构造器是一个特殊的任务，然而在一些特定的场合是有用的：
      - 序列化，远程调用和持久化 -对象需要实例化并存储为到一个特殊的状态，而没有调用代码。
      - 代理，AOP库和Mock对象 -类可以被子类继承而子类不用担心父类的构造器
      - 容器框架 -对象可以以非标准的方式被动态实例化。

# spring boot

- 常用特有注解
  - @SpringBootApplication
  - @EnableAutoConfiguration
