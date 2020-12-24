---
title: note-ux-design-theming
tags: [design, theming]
created: '2020-10-27T15:10:11.658Z'
modified: '2020-10-27T15:10:47.179Z'
---

# note-ux-design-theming

## faq

- 切换theme的方案：下载和重渲染 vs 切换类名和重渲染
  - 动态下载css + 解析成CSSOM + 渲染 vs 切换类名 + 渲染
  - 网络io的性能消耗最大
  - 所以推荐使用初始预加载或闲时预加载css的策略，
    - 这样在点击按钮切换theme时，性能消耗较小
  - 也可以尝试使用css variables，利用浏览器作为runtime，无需io

- 使用sass预编译多套主题 vs 使用treat预编译并加载多套主题
  - scss的灵活性不如基于js的treat，因为js可控制编译出类名的逻辑
    - 可控制编译出极短类名、原子类名

- 编译出多套全局主题的css(一套主题包含所有组件) vs 编译出一个组件的多套主题(易拆分代码)
  - theme-ui给出的方案是前者，使用带约束的样式值

## guide

- 实现主流设计系统的theme
  - material-design
  - apple-design
  - facebook-design
  - ant-design

## pieces

- 用js动态生成style节点`document.createElement('style')`
- 一般不都是在最外层加上主题类名，里面的颜色都用颜色变量么

- 实现页面皮肤切换，常见的方案有几种：替换css链接、替换className、改变css原生变量值、使用 less.modifyVars、props参数下发等

- [styled-system Color Modes](https://styled-system.com/guides/color-modes)
  - different color palettes are stored in the `theme.colors` object.
  - By default the base colors are picked up by other components using Styled System.
  - The root layout component uses React state to cycle through the different color modes and creates a new theme object based on state. 

- ### [UI 框架的主题色一般怎么实现的？](https://www.zhihu.com/question/66734943)
  - 要在客户端动态切换主题颜色，要做的无非是两点：
    - 定义所有组件元素的颜色样式和主题色的映射关系；
    - 在客户端主题色切换时触发样式切换。
  - 建立映射
    - 预处理器的色彩变量或函数（编译时），可以灵活定义映射关系
    - 用CSS变量（运行时），可以使用多个变量，不依赖 color，但需要枚举值
    - color-mod() 函数（运行时），可以像预处理器一样灵活定义映射关系
      - 但是这还只存在于CSS Color Module Level 4这份草案中，并没有浏览器实现。
      - 可结合 CSS 变量
    - currentColor（运行时），只能表达直接使用 color 属性值
  - 上面四中方法中只有预处理器、CSS变量是有可能实际使用
  - 如果用预处理器，服务端编译服务肯定是可行的，只是速度可能不会太快。
    - Element UI 2.0 文档右上角加了更换主题色的功能，应该就是通过服务端编译实现的。
    - Less.js 支持在前端动态编译 Less 样式，虽然也是一个选项，但是性能也不怎么样，而且你需要在前端引入 Less.js 的整个运行环境。
    - 这些方法本质上都是在前端动态生成 `<style>` 元素来修改样式。
  - 如果你的目标浏览器支持CSS变量，那么你只要通过 CSSOM 操作样式来修改变量值， `element.style.setProperty()`
  - 又要快（性能高、不依赖网络），又想兼容更多浏览器，还想灵活定义映射、易于切换？暂时应该是做不到的
  - 我感觉更可行的方案，是采取类似前端 Less 编译的方式，自己写一个更轻量级的运行时环境。
    - 但是我们需要的功能只有色彩的动态切换，所以为了减少运行环境的代码，我们可以不提供语法解析、求值等功能，仅仅做做正则匹配和替换。
    - 为此，我们还要对预处理语言的功能做一定的限制，比如，仅使用枚举的颜色，不支持色彩函数
  - 这里我们用 -- 标记变量以方便我们替换
    - 这样我们就得到了一个简单的“CSS 模板”，这个模板作为字符串被前端的JS逻辑引入
    - 这样就用同一份 Less 代码导出了两份 CSS，一份直接插入 DOM，另一份在动态切换时作为模板。
    - 更进一步，我们可以用 Postcss 处理一下“模板”，去除掉不含颜色定义的属性声明，让模板最小化。
    - 我们依然保持在样式文件中建立映射，但将不同颜色的关系定义进行外置，移到客户端进行计算。
    - 使用类似 Less.js 在浏览器动态生成 CSS 的方式进行切换，但将代价最小化，保持整体逻辑的简单、加载时间不会太久。

- ### [HeyUI组件库 | 如何实现在线切换主题](https://zhuanlan.zhihu.com/p/48733695)
  - 吐槽antd，随便切换什么颜色都很卡，因为没有确认按钮，所以随便调一个小颜色，也会重新渲染
  - HEYUI固定4个主题方案，这样就可以免了后端的服务以及前端渲染的卡顿。
    - 由于四套主题都是需要异步加载的，所以需要先编译成css文件
    - 这一点和ant-design以及element不一样，他们都是使用后端实时生成css文件
    - 在首页的方法中添加css的调用方法。

``` JS
dynamicLoadCss(type) {
  let old = document.getElementById('loadcss');
  var head = document.getElementsByTagName('head')[0];
  var link = document.createElement('link');
  link.type = 'text/css';
  link.rel = 'stylesheet';
  link.href = `/themes/${type}/index.css`;
  link.id = 'loadcss';
  head.appendChild(link);
  // delete old link
  if (old) {
    head.removeChild(old);
  }
}
```

  - antd的换主题比较卡，是因为在线编译 less，所以速度很慢很卡，而且 antd 是不要服务端的
