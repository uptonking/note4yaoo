---
title: lib-ag-grid-faq
tags: [ag-grid, faq, lib]
created: '2020-08-05T09:28:52.117Z'
modified: '2020-08-05T09:30:37.370Z'
---

# lib-ag-grid-faq

## todo

- 测试ag-grid行中行嵌套的rowModel

## dev-faq

- ClientSideRowModel作为@Bean的类中执行@PostConstruct方法时，添加事件监听器到eventService的映射表后，映射表仍为空
  - console.log(转换后的map对象)，打印出来为空
  - 其实事件监听器的映射表非空，可打印 `Array.from(listenerMap.keys())`
  - 需要修改console.log方法，或JSON.stringify()方法来支持打印Map对象

- EventService的dispatchEvent()方法为什么要调用2次dispatchToListeners，第1次异步，第2次同步

``` JS
public dispatchEvent(event: AgEvent): void {
  this.dispatchToListeners(event, true);
  this.dispatchToListeners(event, false);

  this.firedEvents[event.type] = true;
}
```

  - 跟踪分析源码可得，第1次调用eventType对应的所有异步事件处理函数，第2次调用eventType对应的所有同步事件处理函数
  - 因为addEventListener可以对同一事件添加多个事件处理函数

- GridCore中 `@Autowired('eGridDiv') private eGridDiv;` 是如何注入属性进行初始化的，因为EGridDiv类不存在
  - 注入属性时，除了从bean对象容器映射表中查找外，还会从额外指定的映射表providedBeanInstances中查找
