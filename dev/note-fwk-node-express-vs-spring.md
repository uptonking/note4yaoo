---
title: note-fwk-node-express-vs-spring
tags: [comparison, express, framework, spring]
created: '2020-12-09T13:50:52.677Z'
modified: '2021-04-23T18:11:53.294Z'
---

# note-fwk-node-express-vs-spring

# guide

# pieces

- [Why do big companies still write in Java (Spring Boot) when Node.js is faster (and uses less resources) for the job](https://www.quora.com/Why-do-big-companies-still-write-in-Java-Spring-Boot-when-Node-js-is-faster-and-uses-less-resources-for-the-job-that-they-do)
  - Node.js being faster than most other languages is a common misconception. 
    - Node is, however, better at taking in requests because of its non-blocking IO system that processes requests concurrently. 
      - It is better than Java in I/O, but optimizing I/O performance can be done in any other language and other areas of the system should also be taken into account such as load-balancer, database. etc., making it only a small factor in choosing a technology stack.
  - Most companies prefer Java in their tech stack because
    - Java has a mature and thriving ecosystem
      - It has been serving its purpose for more than two decades now
      - Java/Spring are highly matured frameworks. It has stood the test of time. 
      - It offers tons of widely-used libraries
    - Java is statically-typed, unlike most scripting languages
      - You have to explicitly specify the type of an object, promoting type safety and less opportunities to mess up at runtime.
    - When it comes to long-term support and maintainability, Java’s got your back.
      - It is OOP and code modularization is a breeze. 
  - I would think twice before considering Node in my tech stack if I have processes that involves heavy computing.
    - Node.js services runs on a single thread and does not support multi-threading.
    - Javascript itself is a maintenance nightmare. 
    - Node is not faster than Java. 
      - Business logic often needs complex processes and Node is not good in long-running tasks because of its nature. 
      - It’s fine for serving I/O requests but avoid anything that is about to block the event loop. This is why EJB in Java exists.
  - Furthermore, it’s my personal view that 
    - if you are not building something like Facebook or Twitter, does the technology choice really make much difference in terms of performance or scalability? 
    - All these frameworks which we are discussing are quite matured to handle normal traffic within a single organization.

- [Web Development Comparison: Spring Boot vs. Express.js_2019](https://dzone.com/articles/web-development-comparison-springboot-vs-expressjs)
  - The Goal of This Article
    - This is a not so technical comparison
    - I just wanted to outline how it feels to develop web applications in Node.js when you are a Java developer by trade.
    - So please remember, this article is full of personal opinions.
    - I would like to highlight some of the differences that are perceived when developing an application based on the Node/Express stack compared to one based on Spring Boot.
  - I often heard critiques of Java-based web development in favor of Python or Go
    - Java is verbose.
    - Everything is interface-tangled in Java.
    - The memory consumption of Java apps is overwhelming.
    - Disk space consumption can also be overwhelming.
    - Development requires a lot of time.
  - Node.js Is Single-Threaded(the key to Node.js’s speed and low memory consumption)
    - Don’t run CPU-time intensive code or everything will wait for the CPU to be free before executing a new queued function.
    - If something goes wrong and Node.js crashes,then everything crashes
  - Spring Boot indicates a very precise way to organize code into packages (models, services, controllers) 
    - while in an Express.js context there are no such guidelines. 
    - Nevertheless, it is possible to reapply a similar code structure and there are often projects where the code is structured in a similar way to a Spring Boot project.
  - The maturity of Spring Security has yet to be matched by Passport.js, 
    - but the perception I have had is that 80 percent of the features offered by Spring Security are implemented in Passport.js too, in a way that is sometimes simpler.
  - Hibernate is still the most complete, mature, and versatile solution, but at a very high cost! 
    - Sequelize may cover 90% of your use cases.
  - I don’t hate Hibernate, but I surely don’t love it. 
    - It’s over engineered, slow, and complicated
    - Sequelize is small and simple but can’t manage all use cases.
  - Working with JavaScript brings you a greater level of simplicity. 
    - It is ideal for scripting and standard web development, 
    - but I wouldn’t use it for complex projects (except for small dedicated and isolated microservices) 
    - nor would I use it for numeric applications or applications where numbers count 
  - Ultimately, the general feeling I have when developing server-side JavaScript is that everything is a bit simpler and less cumbersome than an equivalent Java-based app, 
    - although I have a strong perception that there is a lack of stability and maturity in respect to the libraries offered in Java
  - Another perception is that the JavaScript development cycle is about 20% faster. 

# ref
