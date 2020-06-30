---
tags: [dev, faq]
title: log-faq-dev-repeat
created: '2019-08-01T16:03:46.394Z'
modified: '2020-06-30T05:21:55.764Z'
---

# log-faq-dev-repeat


- js function declaration vs function expression(named/anonymous)
  - 匿名函数表达式无法递归调用自身(arguments.callee无法在严格模式)，具名可以
  - 调试时的可读性
  - Availability (scope) of the function，函数或变量会自动提升hoist
    - one difference that concerns me is when the machine creates the function object. Which in the case of declarations is before any statement is executed but after a statement body is invoked (be that the global code body or a sub-function's), and in the case of expressions is when the statement it is in gets executed. 
  - (function(){}).name === ""，匿名函数表达式会返回true
    - Both have a name property
  - In Google's V8 and Firefox's Spidermonkey there might be a few microsecond JIST compilation difference, but ultimately the result is the exact same.
  - If we declare the variable as function funcName(){}, then the immutability of the variable is the same as declaring it with var。
    - function expression can be const
    - function declaration name can be reassigned, too
  - Function Declarations are only allowed to appear in Program or FunctionBody. Syntactically, they can not appear in Block (`{ ... }`) — such as that of if, while or for statements. This is because Blocks can only contain Statements, not SourceElements, which Function Declaration is. 
    - The only way Expression is allowed directly within Block is when it is part of ExpressionStatement. 
    - However, ExpressionStatement is explicitly defined to not begin with "function" keyword, and this is exactly why Function Declaration cannot appear directly within a Statement or Block (note that Block is merely a list of Statements).
  - ref
    - http://kangax.github.io/nfe/
    - https://stackoverflow.com/questions/336859/var-functionname-function-vs-function-functionname
- `var arr=[1,2,3]; arr.count=3;` 
  - console.log(arr)得到`[1, 2, 3, b: 33]`
  - arr.length得到3
  - 可以借助此方法对数组插值，参考styled-system的responsive array prop value
- Is it possible to have a comment inside a es6 template string?
  - comment in expression interpolation  
  ```
  const fields = `
    id, ${ /* post id */'' }
    message, ${ /* post status/message */'' }
    created_time
  `;
  ```
  - parse comment in tag function  
  ```  
  const commented = (strings, ...values) => {
    const pattern = /\/{2}.+$/gm; // basic idea

    return strings.map(
          (str, i) => 
            `${str}${values[i] !== undefined ? values[i] : ''}`
          )
          .join('')
          .replace(pattern, '');
      };

  const d = 10;
  const fields = commented`
    ${d}
    id, // post ID
    ${d}
    message, // post/status message
    created_time, // ...
    permalink_uri,
    type
  `;
  ```
- firefox与chrome滚动条样式不一致，应该如何处理
  - 结论
    - 选择1：放弃自定义滚动条，使用系统默认的，各操作系统实现的滚动条不一致
    - 选择2：remove scrollbars
      - 使用箭头导航，add some arrows to scroll the content
      - 放弃滚动条，使用分页
  - 可参考perfect-scrollbar(MIT)实现跨浏览器样式一致的滚动条
    - https://mdbootstrap.com/snippets/jquery/filipkapusta/765760
    - No manipulation on DOM tree
    - Use plain scrollTop and scrollLeft
    - 最外层的(竖直)滚动条问题仍未解决，firefox是自动隐藏且收窄的
  - 自定义滚动条样式时要注意
    - scrollbar styling is part of the OS
    - 在触摸板上向上滑动时，页面顶部会逐渐隐藏，此时滚动条下移
    - 直接向上拖动滚动条时，页面顶部已隐藏的部分逐渐显示，与上面相反
  - ref
    - https://stackoverflow.com/questions/47138603/scroll-issue-on-firefox-vs-webkit-browsers-side-navigation-text-truncate-and
    - https://www.zhihu.com/question/278165453
    - chrome支持滚动条的样式修改，但是又有多少网站去改变了滚动条的样式呢？为什么这几个相关的css私有伪元素，为什么一直没有被w3c标准采纳？
      - 换个样式，并不能让操作变得更方便。而样式方面的问题，用户完全可以按照自己的喜好选择操作系统中的主题
      - Every other browser, with the exception of chrome, uses the default OS UI for the scrollbar, which means, the scrollbars will look almost the same regardless which browser you use.
        - In Windows is a thick gray scrollbar with two buttons on the edges that work for going up/down.  
        - In OSX for instance, scrollbar never appear, until you scroll, and it looks like a discrete rectangle moving downward to the page you are scrolling.  
        - In contrast chrome uses a customized scrollbar instead of the default so it looks consistent in every OS it uses.
- 前后端分离导致的单点登录不可用如何解决
  - 使用json web token，每个请求都带身份认证id


