---
title: lib-editor-textbus-community
tags: [community, textbus]
created: 2023-02-21T00:08:57.962Z
modified: 2023-02-21T00:09:17.475Z
---

# lib-editor-textbus-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 兜兜转转又弄回 contenteditable 了_20230225
- 为了兼容移动端是吧
  - pc 可以随便，移动只能原生
  - 能力不够，暂时没找到很好的在移动端画光标，而没有问题的路径


- ## 我甚至在想，要不要把组件再改回 class
  - 改回 class 干嘛， 函数组件不好写吗
  - class 有类型推断的优势
  - 函数组件有 hook 的优势
  - 一个类型更友好，一个组合更方便
- 为什么函数组件 类型推断有问题呀
  - 比如你要判断一个组件，用 class 直接 instanceof
  - 现在只能 typeof xxx && comp.name === 'xxx'
  - 并且下面这个还不能完全，扩展的方法无法推断，用类的话，就没有这个问题
  - 其实 class 里也可以用 hook，不过，这样就不能直接 new 了
- 你是要它能够自动推断，而不是用ts 告诉编译器类型信息是吧
  - 是的
  - 要通过特定的工厂去实例化 class，比如 context.createInstance(ClassComponent)，这样才能在 class 里使用 hook
  - 现在这种方式，也不方便做 component.createInstance(这里的参数）
和组件的 setup(这里接收){}
  - 这样也增加了一点点心智理解负担
- 所以没有两全的方法
  - 或者可以new，但是要约定一个比如 init 方法，在这个方法里可以使用 hook
  - 这个 init 必须是 textbus 来调用，方便创建 hook 上下文信息
- 1.0 就是用过class

- ## const [state, setState] = useState() 用这种模式，就必须要走 react的那种设计
- 对长文档有很大的性能问题要处理
  - 弄到最后，就造了个 react出来

- ## textbus 的性能瓶颈不在文档长度和大小上
- 在组件复杂度上
  - 如表格这种，如果单元格过多，textbus 类似把每个组件和插槽都调用了 react memo
  - 但组件本身很大的话，这个通用算法就解决不了了
