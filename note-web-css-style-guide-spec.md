---
title: note-web-css-style-guide-spec
tags: [css, spec, style]
created: '2020-07-18T06:25:58.384Z'
modified: '2020-07-18T06:35:10.808Z'
---

# note-web-css-style-guide-spec

## style-guide-catalog

- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [Airbnb CSS/Sass Styleguide](https://github.com/airbnb/css)
- [Order of the Day: CSS Properties](https://web.archive.org/web/20130227044124/http://fordinteractive.com/2009/02/order-of-the-day-css-properties/)
- [Mozilla Organizing your CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Organizing)
- [CSS guidelines for MDN code examples](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Organizing)
- [The Firefox codebase: CSS Guidelines](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/CSS_Guidelines)
- [css-tricks CSS Style Guides catalog](https://css-tricks.com/css-style-guides/)
- [Poll Results: How do you order your CSS properties?](https://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)
  - 45% - grouped by type
  - 39% - randomly
  - 14% - alphabetical
  - 2%  - by line length
- [Outside In - Ordering CSS Properties by Importance](https://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685)
  - Layout Props (position, top, display, float, z-index)
  - Box Model Props (width, height, padding, margin)
  - Visual Props ( border, box-shadow, background, color)
  - Text Props (font, line-height, text-align/transform)
  - Misc Props (cursor, transition, animation)
- [fex-team/styleguide](https://github.com/fex-team/styleguide/blob/master/css.md)
- [Code Guide by @AlloyTeam](http://alloyteam.github.io/CodeGuide/)
- misc
  - https://primer.style/css/principles/scss
  - [CSS属性书写顺序及命名规则](https://www.cnblogs.com/wybie/p/3689867.html)
  - [CSS书写规范和顺序](https://juejin.im/post/5d552252f265da03a14852cc)
  - [CSS 属性排序千千万，我只爱那一种](https://zhuanlan.zhihu.com/p/32905439)

## css书写顺序建议

- layout 位置布局，影响文档流
  - display
  - float/clear/overflow
  - position
  - top/left/right/bottom
  - z-index
  - table/table-layout
- box 盒模型
  - width/height
  - padding
  - margin
  - border-radius/collapse/spacing
  - box-shadow
  - outline
- text 文字排版对齐
  - font-family/size/weight/style
  - line-heght
  - text-align
  - vertical-align
  - text-transform/decoration/shadow/wrap/indent/overflow
  - letter/word-spacing  
  - whitespace
- background visual 背景视觉装饰
  - background-color/clip/origin/size
  - color
  - visibility
  - opacity
- misc 其他
  - order
  - content
  - quotes
  - list-style
  - transition
  - animation

- tip
  - 将layout相关的属性集中起来放在最前面，避免多次layout/reflow

## Google CSS Style Guide

- Alphabetize declarations.
- Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain.
- Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).
- 避免使用类型选择器，影响范围太大，为了性能应避免使用父节点做选择器
- url()中不要使用引号
- 避免使用css hacks

## Airbnb CSS/Sass Styleguide

- Prefer dashes over camelCasing in class names.
  - Underscores and PascalCasing are okay if you are using BEM (see OOCSS and BEM below).
- We encourage some combination of OOCSS and BEM for these reasons
- Ordering of property declarations
  1. Property declarations
  2. `@include` declarations
  3. Nested selectors
- 不要使用ID选择器，因为不可重用
- 类名建议使用破折号代替驼峰法。如果你使用BEM，也可以使用下划线
- 在一个规则声明中应用了多个选择器时，每个选择器独占一行
- 在定义无边框样式时，使用 0 代替 none
- sass    
  - 推荐使用scss
  - 应避免使用 @extend 指令，因为它并不直观，而且具有潜在风险，特别是用在嵌套选择器的时候，推荐使用mixin函数复用代码

## Mozilla Organizing your CSS

- Does your project have a coding style guide?
  - CSS guidelines for MDN
- Keep it consistent
- Formatting readable CSS
- Comment your CSS
- Create logical sections in your stylesheet
  - set up a default style  
- Avoid overly-specific selectors
  - If you create very specific selectors, you will often find that you need to duplicate chunks of your CSS to apply the same rules to another element.
- Break large stylesheets into multiple smaller ones
- CSS methodologies
  - OOCSS
  - BEM
  - SMACSS
  - ITCSS
  - Atomic CSS

##  CSS guidelines for MDN code examples

- The following guidelines cover how to write CSS for MDN code examples.

- ### High-level guidelines
  - Don't use preprocessors
  - Don't use specific CSS methodologies
  - Use flexible/relative units
  - Don't use resets
  - Plan your CSS — avoid overriding
- ### General CSS coding style
  - Use expanded syntax
  - Favor longhand rules over terse shorthand
  - Use double quotes around values
  - Spacing around function parameters
  - CSS comments
  - Don't use `!important`
- ### Specific CSS syntax points
  - Turning off borders and other properties
    - When turning off borders (and any other properties that can take `0` or `none` as values), use `0` rather than `none`
  - Use "mobile first" media queries
    - make the default styling before any media queries have been applied to the document the narrow screen/mobile styling, 
    - and then override this for wider viewports inside successive media queries.
- ### Selectors
  - Don't use ID selectors
    - harder to override if needed
    - less flexible
  - Put multiple selectors on separate lines

## pieces

- 长名称或词组可以使用中横线来为选择器命名，不建议使用下划线来命名CSS选择器
  - 输入的时候少按一个shift键； 
  - 能良好区分JavaScript变量命名（JS变量命名是用“_”） 
  - 浏览器兼容问题 （比如使用_tips的选择器命名，在IE6是无效的） 
- 有时候可以给选择器添加一个表示状态的前缀，让语义更明了，如 `is-`
- 需要添加 hack 时应尽可能考虑是否可以采用其他方式解决。
  - 尽量使用 选择器hack 处理兼容性，而非 属性hack
