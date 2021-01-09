---
title: web-css
tags: [css, optimization, style, web]
created: '2019-12-17T04:23:15.125Z'
modified: '2020-12-21T07:45:28.814Z'
---

# web-css

# guide

- 技术选型：css特性 vs js api
  - 可选择
    - css animation vs waapi
  - 兼容性：注意ios的safari、qq浏览器

- Best practices of using efficient CSS selectors (by Google Page Speed) (已过时)
  - Avoid descendant selectors: table tbody tr td
  - Avoid redundant ancestors: body section article (body never needed)
  - Avoid universal (*) selectors: body *
  - Avoid tag selectors as the key (right-most): ul li
  - Avoid child or adjacent selectors: ul > li > a
  - Avoid overly qualified selectors: form#UserLogin (# is already specific)
  - Make your rules as specific as possible (class or id).
  - ref
    - https://stackoverflow.com/questions/8640692/slow-response-when-the-html-table-is-big?
    - https://stackoverflow.com/questions/25618138/what-happened-to-the-use-efficient-css-selectors-rule

# pieces

 

- I am quoting Benjamin Poulain, a WebKit Engineer who had a lot to say about the CSS selectors performance test:
  - ~10% of the time is spent in the rasterizer. 
  - ~21% of the time is spent on the first layout. 
  - ~48% of the time is spent in the parser and DOM tree creation 
  - ~8% is spent on style resolution 
  - ~5% is spent on collecting the style – this is what we should be testing and what should take most of the time. 
  - The remaining time is spread over many many little functions
- I completely agree **it is useless to optimize selectors upfront**, but for completely different reasons:
  - It is practically impossible to predict the final performance impact of a given selector by just examining the selectors. 
    - In the engine, selectors are reordered, split, collected and compiled. 
    - To know the final performance of a given selectors, you would have to know in which bucket the selector was collected, how it is compiled, and finally what does the DOM tree looks like.
    - **All of that is very different among the various engines**, making the whole process even less predictable.
  - The second argument I have against web developers optimizing selectors is that they will likely make things worse. 
    - The amount of misinformation about selectors is larger than correct cross-browser information. 
    - The chance of someone doing the right thing is pretty low.
    - In practice, people discover performance problems with CSS and start removing rules one by one until the problem go away. 
    - I think that is the right way to go about this, it is easy and will lead to correct outcome.”
- There are approaches, like BEM for example, which models the CSS as flat as possible, to minimize DOM hierarchy dependency and to decouple web components so they could be "moved" across the DOM and work regardless.

# ref

- [CSS performance revisited: selectors, bloat and expensive styles](http://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/)
- [Use efficient CSS selectors rule by Google PageSpeed](https://stackoverflow.com/questions/25618138/)what-happened-to-the-use-efficient-css-selectors-rule
- [Which CSS selectors or rules can significantly affect layout/rendering performance](https://stackoverflow.com/questions/12279544/which-css-selectors-or-rules-can-significantly-affect-front-end-layout-renderi)
- [CSS进阶系列](https://github.com/chokcoco/iCSS)
- [30-seconds-of-css](https://github.com/30-seconds/30-seconds-of-css)
  - Short CSS code snippets for all your development needs
- [You-Dont-Need-JavaScript](https://github.com/you-dont-need/You-Dont-Need-JavaScript)
  - CSS is powerful, you can do a lot of things without JS.
- [solved-by-flexbox](https://github.com/philipwalton/solved-by-flexbox)
  - https://philipwalton.github.io/solved-by-flexbox/
  - problems once hard or impossible to solve with CSS alone, now made trivially easy with Flexbox.
