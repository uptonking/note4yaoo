---
title: algs-usecase
tags: [algorithms, usecase]
created: '2020-09-12T13:41:54.393Z'
modified: '2020-12-20T15:24:16.216Z'
---

# algs-usecase

# sort

# search

- 将arr创建成set时，数组中重复元素会被清理掉，但有时需要数组与set长度相等，如何查找数组中的重复元素并合理处理

# dev

- 递归 vs 循环
  - 如果是用c/c++/java这一类的常规的语言来开发的话，递归很难调试。
    - 设了断点也不知道到底到了哪一层；检查个变量也不知道是哪一层的；
    - 系统帮你维护了一个堆栈，但是这个堆栈是代码和数据共用的，无法直观的查看。
    - 对于这种情况，能用循环的就尽量用循环，好调试、好维护。
  - 对于LISP/erlang/prolog这种鼓励递归的语言，当然要用递归
  - 某些比较难懂的算法，不管你是用循环还是递归，可能都很难懂，难读，难调试! 
    - 所以，尽可能封装起来，独立起来，不要暴露到外面，可以单独测试、单独调试。
    - 上层调用的时候，才不要关心底层用的是循环还是递归呢。
  - 有很多程序员确实比较依赖断点来调试，也确实很快解决问题了。
    - 对于他们来说，那么能采用循环来代替递归的话确实是更好的选择。
    - 断点是一种很不好，很偷懒的调试方法。比较好的做法是只凭看，头脑里面推理找到错误。如果觉得复杂到了光凭推理不能解决的话，首先想到是该不该拆分逻辑，使用测试用例。全部招都用完了，最后才到断点，不过这种情况基本上极难遇见。
    - 就C++来说，我觉得用递归的时候查看整个栈上的数值还是很麻烦的。从现有工具来说，我觉得用循环的话断点调试的难度小很多。
  - ref
    - https://www.zhihu.com/question/20418254

- ## Voronoi polygons for hover interactivity of points are popular and make sense to dataviz practitioners but maybe we should have been teaching people how to use quadtrees instead? 
- https://twitter.com/Elijah_Meeks/status/1378880759713333252

# ref

- [世界上有哪些代码量很少，但很牛逼很经典的算法或项目案例？](https://www.zhihu.com/question/358255792)
