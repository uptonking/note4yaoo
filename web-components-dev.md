---
title: web-components-dev
tags: [web-components]
created: 2020-11-10T03:16:01.377Z
modified: 2021-01-01T18:24:23.850Z
---

# web-components-dev

# guide

- web components pros
  - web标准方案，浏览器提供实现的runtime

- web components cons
  - 只提供了组件组成的结构，没有解决前端经典问题
    - keep dom in sync with state/data，需自己实现
  - 提供的template/slot模版不够强，没有传统template engine的变量替换和控制流
    - 不适合用来split large html
  - 现在(202101)仍然没有提出ssr的标准方案，可选方案有Declarative Shadow DOM

# pieces

- 不太看好web components，
  - 不说markup语言对于数据类型的支持不行，
  - 只说web开发最大的魅力就在于web能够很方便地实现任何你想要的UI画面，而不是做好一个元件能够被全世界使用，
  - 想想现在还有多少人在使用原生的select，radio, checkbox, fieldset.

- Never used ShadowDOM and hopefully never will. 
  - It simply doesn’t work as nicely as built in extends, 
  - and it offers less than regular custom elements, where you can share, and reuse, CSS like we’ve been doing for 20+ years

# discuss
- ## 遇到 Component Library issues 时，要不要处理的 #判断标准
- https://twitter.com/ThaddeusJiang/status/1506899881751105537
  - 去 Library 官网或者其他主流网站（Google，Twitter etc）确认一下， 
    - 如果有相同问题，我们就不对应。 
    - 如果只有我们有问题，就对应
  - 如果是 Chromium 的问题，我们就不需要勉强自己，上世纪的软件开发公司才会对应这种问题。


- ## Why aren't web components fully supported yet? I remember hearing about them in 2015 and still I'm using React.
- https://twitter.com/justinfagnani/status/1161351100579999744
- It's a pretty complicated specification and many parts like shadow DOM can't be adopted in a backwards compatible way.
  - Web components are made up of a few different technologies, custom elements on their own are pretty viable these days...
- I want to be pedantic: 
  - React is implemented with imperative APIs but provides a declarative API. 
  - LitElement, lit-html, Stencil, Lightning... are implemented with imperative APIs and provides a declarative API. 
  - Imperative web components APIs enable declarative APIs.
- You're making my point for me. 
  - I pointed out lit-html and similar libraries exist, but originally WCs were meant to replace libraries like React. 
  - The WC APIs are all imperative and many are too low-level for app developers (rather than library/framework maintainers).
- I don't think it's quite fair to say "originally WCs were meant to replace libraries like React."
  - Yes, the spirit behind WC (and similar modern web features) is to reduce the set of problems that userland libraries and frameworks need to solve, by doing more in the platform.
  - But it's by no means universally believed by WC proponents—certainly not today that WC would ever obsolete userland solutions entirely.
  - That said, it's easy to see why people might think so...the vision has evolved, there's a wide range of opinions within the WC community, and messaging is hard.
  - For most teams currently using React, there's not a compelling reason to switch today. 
    - You might choose to if your use cases align well with WC's current strengths and limitations or if you are passionate about the long-term vision...
  - But otherwise, keep doing what works well for you.
    - Same goes for authors of existing frameworks & libs.
    - If adopting WC as your component model doesn't solve real problems for you today, then no one's forcing you.
- WC aren't causing people to leave React in droves doesn't mean that they're a failure or a disappointment. They're not done.
  - You could say the same about features like ES Modules and Web Packaging, with respect to userland solutions like Webpack.
  - These features are part of a long game, based on an opinionated vision of a healthy future web.

# ref

- [mdn: Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
