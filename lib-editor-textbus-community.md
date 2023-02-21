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

- ## 

- ## const [state, setState] = useState() 用这种模式，就必须要走 react的那种设计
- 对长文档有很大的性能问题要处理
  - 弄到最后，就造了个 react出来

- ## textbus 的性能瓶颈不在文档长度和大小上
- 在组件复杂度上
  - 如表格这种，如果单元格过多，textbus 类似把每个组件和插槽都调用了 react memo
  - 但组件本身很大的话，这个通用算法就解决不了了
