---
title: lib-ag-grid-faq
tags: [ag-grid, faq, lib]
created: '2020-08-05T09:28:52.117Z'
modified: '2020-08-05T09:30:37.370Z'
---

# lib-ag-grid-faq

# todo

- 测试ag-grid行中行嵌套的rowModel

# dev-faq

 

- 通过alert阻塞渲染时观察，此时表格组件内容并没有渲染到页面，但分析源码可知此时已通过appendChild添加页面已有元素

- grid的表头组件是如何渲染的，注意rowModel计算的是rowData，而不是column
  - GridCore中会创建表头最外层的 HeaderRootComp
  - columnController中会创建每个表头行的 HeaderRowComp
  - header和row都是先计算数据模型，再渲染ui

- GridCore的基类Component的setTemplate方法中调用setTemplate/loadTemplate，为什么loadTemplate方法会多次执行
  - 自己分析错了，后面打印的是由其他代码触发调用同一个方法
  - 一个dom元素对象创建时，会递归地创建内部dom元素对应的组件，所有会多次调用setTemplate/loadTemplate

- ClientSideRowModel作为@Bean的类中执行@PostConstruct方法时，添加事件监听器到eventService的映射表后，映射表仍为空
  - console.log(转换后的map对象)，打印出来为空
  - 其实事件监听器的映射表非空，可打印 `Array.from(listenerMap.keys())`
  - 需要修改自定义JSON.stringify()方法来支持打印Map对象
- 进一步分析
  - 上述观点存在部分错误
  - 对于Map类型的对象实例mm
    - 使用 `mm.set('k','v')` 设置值， `console.log(mm)` 能显示该kv， `JSON.stringify(mm)` 序列化为 `{}`
    - 使用 `mm['kk']='vv'` 设置值， `console.log(mm)` 不能显示kkvv， `JSON.stringify(mm)` 序列化为 `{"kk":"vv"}`
  - 对于Set类型的对象实例ss，特别是集合元素为函数时
    - If the `toString()` method is called on built-in function objects or a function created by `Function.prototype.bind` , `toString()` returns a native function string which looks like `function () {\n    [native code]\n` }`
    - Set序列化后的字符串都相同，类似 `[native code]` ，反序列化时元素会减少！！
  - jsonFnClone的部分属性值总是为空，但单独打印size/length确有长度，说明序列化的方法实现存在问题，可以先只调用jsonFnStringify打印字符串而不是对象来分析问题

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
  - 注入属性时，除了从Context的bean映射表容器中查找外，还会从额外指定的映射表providedBeanInstances中查找
