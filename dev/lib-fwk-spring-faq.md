---
title: lib-fwk-spring-faq
tags: [faq, framework, spring]
created: '2021-09-18T13:13:46.487Z'
modified: '2021-09-18T13:15:34.236Z'
---

# lib-fwk-spring-faq

# not-yet

# [spring为什么使用三级缓存而不是两级？](https://www.zhihu.com/question/445446018)
- 一级缓存：存储单例bean，
  - 即 `Map<String, Object> singletonObjects`（bean name to bean instance）
- 二级缓存：存储提前暴露的bean，真正的解决循环依赖是靠二级缓存的。
  - `Map<String, Object> earlySingletonObjects` （Cache of early singleton objects: bean name to bean instance）
- 三级缓存：存储bean和其要加强的aop处理，如果需要aop增强的bean遇到了循环依赖，则使用该缓存中的aop处理代理增强bean（Cache of singleton factories: bean name to ObjectFactory.）  
- 实际上不用三级缓存也可以解决循环依赖，但是如果有需要aop增强的bean时，就要在初始化bean的时候对bean做增强了，这违背了Spring在结合AOP跟Bean的生命周期的设计！
  - Spring结合AOP跟Bean的生命周期本身就是通过AnnotationAwareAspectJAutoProxyCreator这个后置处理器来完成的，在这个后置处理的postProcessAfterInitialization方法中对初始化后的Bean完成AOP代理。
  - 如果出现了循环依赖，那没有办法，只有给Bean先创建代理，但是没有出现循环依赖的情况下，设计之初就是让Bean在生命周期的最后一步完成代理而不是在实例化后就立马完成代理。
