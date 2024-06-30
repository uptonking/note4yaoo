---
title: lib-notb-observablehq-pm-xp
tags: [notebook, observablehq, pm, xp]
created: 2021-05-25T17:52:27.247Z
modified: 2024-06-30T03:20:48.202Z
---

# lib-notb-observablehq-pm-xp

# observablehq-xp

- tips
  - observable-notebook的使用体验，感觉像是为内置d3语法的文档而专门设计的ide
# general-xp-pros
- 可以修改和探索任何发布的notebook
- 动态交互的reactive document，适合用来做展示文档或仪表板
# general-xp-cons
- 不支持edit in place 原地编辑，对于文本而言，类似word的编辑体验最好
  - 当cell的文本过多时，想要编辑需要下滑很久到编辑区；
- 不支持 search: in issues, forum, notebooks

- 代码太多会影响文档的可读性
  - 参考方案0：代码或公式放在appendix，appendix显示在文档右侧toc的位置
  - 参考方案1：一个单独的代码编辑器，里面的定义的export都可以在文档里面使用
  - 参考方案2：单独的文档浏览器，浏览体验最好，因为不可编辑
# text-editor-pros
- cell的执行顺序不按照书写顺序，而按照依赖顺序
- import named cells from other notebooks
  - `import` cell `with` data `from` other-notebook
# text-editor-cons
- 代码编辑类
  - rename cell时，不支持自动更新引用
  - inspector对象的属性值时，字符串蓝色，数字青色，类型颜色的标记不明显

- 文本编辑类

- 导航浏览类
  - 文档不支持自动生成目录toc
  - 快捷键冲突
  - 跳转到声明处，未实现

- 文本内容布局类
  - 不支持图文混排，如水平分栏，只能上下堆叠单元格

- 内容渲染类
  - 数组转换成字符串时，输出的元素间无逗号，所有元素连在一起，与js的arr.toString()行为不一致
  - 浏览渲染的内容时，中文和英文间无空格，显得很挤

## syntax

- import的不一致
  - cell、`require(npm-amd)`、`import(npm-esm)`

- 不支持解构赋值 destructuring
  - [Destructuring Objects At Top Level](https://github.com/observablehq/feedback/issues/48)

### done

<!-- #region /folded syntax -->
- [x] import的来源无法区分来自npm，还是来自其他observable notebook
  - observablehq对于导入npm包使用`require()`，默认基于cdn.jsdelivr.net，需要AMD
  - `import()`需要手动指定cdn.skypack.dev，需要es6
<!-- #endregion /folded syntax -->

## markdown

- markdown的code block的样式与observablehq的代码样式相同，易混淆文档和实际执行的代码

## wontfix

- 若作为标题的文字中包含@用户名，则该行文字很快就会换行
  - 多观察几篇文章，文本区块的宽度比代码区块的宽度要短很多，加上标题行字体大，所以标题行很容易换行，视觉上不友好
# data-pros

# data-cons

# viz-pros

# viz-cons

# draft
- 自动在末尾生成appendix
# proposals
- [Making Your Code Citable](https://guides.github.com/activities/citable-code/)
  - 提出了一种基于zenodo发布与引用代码或网页的方法
  - 类似arxiv、biorxiv、figshare、peerage of science、peerj preprints
