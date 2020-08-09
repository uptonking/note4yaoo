---
title: note-style-css-in-js-blog
tags: [blog, css-in-js]
created: '2020-08-07T17:50:19.599Z'
modified: '2020-08-07T17:50:44.516Z'
---

# note-style-css-in-js-blog

## [CSS-in-JS：一个充满争议的技术方案](https://zhuanlan.zhihu.com/p/165089496)

- CSS-in-JS （后文简称为 CIJ）在 2014 年由 Facebook 的员工 Vjeux 在 NationJS 会议上提出：可以借用 JS 解决许多 CSS 本身的一些“缺陷”，比如全局作用域、死代码移除、生效顺序依赖于样式加载顺序、常量共享等等问题。
- CIJ 的一大特点是它的方案众多。发展初期，社区在各个方向上探索着用 JS 开发和维护 CSS 的可能性。每隔一段时间，都会有新的语法方案或实现，尝试补充、增强或是修复已有实现。
- 随着时间流逝，他们中的大多数不是被官方宣布废弃，就是长时间不再维护
- 争议主要集中在以下几点：
  - 使用 CIJ 是一种伪需求，只靠 CSS 就足以完成任务
  - CIJ 方案和工具过多，缺乏标准，使用起来有被遗弃的风险
  - CIJ 有运行时性能损耗
- 虽然 CIJ 还没有形成真正的标准，但在接口 API 设计、功能或是使用体验上，不同的实现方案越来越接近，其中最受欢迎的两个解决方案是Emotion 和 styled-components。
  - 通过几年间的竞争，为了满足开发者的需求，同时结合社区的使用反馈，在不断的更新过程中，它们渐渐具有了几乎相同的 API，只是在内部实现上有所不同。
  - 不管是现有的主流方案还是新出现的方案，几乎在接口上使用同样的（或是一部分的）接口设计：CSS prop 与样式组件（styled）。同时，这两种方案都支持模板字符串或是对象样式。
  - 两种方案在内部实现中都会享受当代前端工程化的福利，如语法检查、自动增加浏览器属性前缀、帮助开发者增强样式的浏览器兼容性等等。
  - 同时利用 vscode-styled-components、stylelint 等代码编辑器插件，我们可以在 JS 代码中增加对于 CSS 的语法高亮支持。
- css prop 可以算是内联样式的升级版，用户定义的内联样式以 JSX 标签属性的方式与组件紧密结合，可以帮助用户快速迭代开发，让用户可以更快速的定位问题。不过由于样式直接内嵌在JSX中，势必在一定程度上会影响组件代码的可读性。
- styled样式组件更像是 CSS 的组件化封装，将样式抽象为语义化的标签，把样式从组件实现中分离出来，让 JSX 结构更“干净整洁”。相对而言，样式组件定义的样式不如内联样式更方便直接，而且需要给额外多出来的样式组件定义新的标签名，会在一定程度上影响开发效率；但从另外一个角度来说，样式组件以更规范的接口提供给团队复用，适合有成熟确定的设计语言的组件库或是产品。
- 选择用哪一种方案并没有决定性方法论，可根据项目需要进行取舍。
- 在框架内部，Emotion和styled-components在浏览器中都有一个运行时，这不光增加了最终构建产物大小，更严重的问题是还带来了运行时成本。 举例来说，CSS 属性的实现思路是这样的：
  - 解析用户样式，在需要时添加前缀，并将其放入CSS类中
  - 生成哈希类名
  - 利用 CSSOM，创建或更新样式
  - 生成新样式时更新css节点/规则
- 有些新方案选择将 CSS 在构建时输出为静态 CSS 文件，如 Linaria。
  - 不过这种方案有一些语法上的限制，比如不支持内联CSS样式。
- 值得一提的是 @compiled/css-in-js，这个库会用类似于 Angular 的预先（AoT）编译器，将组件样式预先编译为 CSS 字符串，嵌入转译的 JS 代码中。这种方式显著减少了因变量引起的 CSS 冗余问题。
- 以 Tailwind CSS 为代表，CSS 原子化是使用纯 CSS 的一种流行方案。这种方案中，用户使用库提供的功能性CSS 类修饰DOM结构。
  - 使用原子化 CSS 有一些好处，比如：减少CSS规则冲突可能性（Specificity）；CSS 的大小恒定，不会跟随项目的增长而增长；用户可以直接修改 HTML 属性而不用修改 CSS，改变最终渲染的效果 。
  - CIJ 给 CSS 原子化带来了一些新的可能性，社区正在探索利用 CIJ 完成自动化的原子化 CSS 的可能性，比如 Styletron、Fela、Otion 等
  - 原子化 CSS 可能会给 CIJ 带来不少好处，比如CSS规则去重。CIJ 在运行时会产生许多新的CSS类，增加浏览器的负担，遗憾的是这需要框架本身支持把CSS抽离为静态文件的需求。目前流行的CSS-in-JS框架，比如Emotion，暂时还无法支持这样的特性。
- 经过了一段时间的探索与实践，FreeWheel 最终确定使用Emotion 作为目前的 CIJ 方案，将其应用于部分前端项目

## [Tip: ChromeDevTools now supports CSS-in-JS!](https://twitter.com/addyosmani/status/1289818213983883270)

- This should be a standard for all other browsers. They should help  Frontend Developers' lives and make life easy. 
- Thanks for the tip! Can you recommend us posts about performance comparison of css in js vs CSS modules? Seems like CSS in JS always will be slower because it's overloading the JS main thread.
- There's CSS-in-JS libraries with zero overhead; I've used Linaria. The CSS becomes real .css files as part of the build, and there's no JS overhead (it just compiles to class name strings).
- CSS, JS and html are all needed to define some interactive component on the page. Their common concern is that component. It's separation of concern, not separation of syntax.
- for performance most libraries use Constructable Stylesheets to add those styles. Chrome did not allow to edit those before. it's fixed in chrome canary - so will be available in chrome 85.
- CSS in JS hurts load time. Especially critical CSS. The CSS is not immediately discoverable by the browser and can hurt metrics like Largest Contentful Paint
  - I recommend folks using CSS-in-JS configure their bundlers to extract/output real CSS files for production. You avoid the double-parse costs, get better caching and can still benefit from the DX. like linaria.
  - Good CSS-in-JS libraries can have the CSS extracted out into real .css files as part of the build(linaria, style-sheet). They can use atomic CSS so that growth of the CSS file is relatively small and growth slows down significantly over time
  - Plus, SSR sends only the critical CSS, so the browser has to do less work at first.
- ref
  - [google: Style editing for CSS-in-JS frameworks_chrome85_202006](https://developers.google.com/web/updates/2020/06/devtools)
    - The Styles pane now has better support for editing styles that were created with the CSS Object Model (CSSOM) APIs. 
    - Many CSS-in-JS frameworks and libraries use the CSSOM APIs under the hood to construct styles.
    - You can also edit styles added in JavaScript using Constructable Stylesheets now. Constructable Stylesheets are a new way to create and distribute reusable styles when using Shadow DOM.
    - For example, the h1 styles added with CSSStyleSheet (CSSOM APIs) are not editable previously. There are editable now in the Styles pane

  - [Firefox 79: Better source map references for SCSS and CSS-in-JS](https://hacks.mozilla.org/2020/07/firefox-79/)

## CSS-in-JS - styled vs css prop

- ### [CSS-in-JS - styled vs css prop](https://dev.to/a_sandrina_p/css-in-js-styled-vs-css-prop-229e)

- I like to use styled, since css prop depends on a bit more setup using babel or macro to reach the same result.

## style9: build-time CSS-in-JS

- [style9: build-time CSS-in-JS_202007](https://css-tricks.com/style9-build-time-css-in-js/)

- In April of last year, Facebook revealed its big new redesign, a rebuild of a large site with a massive amount of users. 
- To accomplish this, they used several technologies they have created and open-sourced, such as React, GraphQL, Relay, and a new CSS-in-JS library called stylex.
- This new library is internal to Facebook, but they have shared enough information about it to make an open-source implementation, style9, possible.
- style9 has the same benefits as all other CIJ solutions, as articulated by Christopher Chedeau, including scoped selectors, dead code elimination, deterministic resolution, and the ability to share values between CSS and JavaScript.
- There are, however, a couple of things that make style9 unique.
- Minimal runtime
  - Although the styles are defined in JavaScript, they are extracted by the compiler into a regular CSS file. 
  - That means that no styles are shipped in your final JavaScript file. 
  - The only things that remain are the final class names, which the minimal runtime will conditionally apply, just like you would normally do. 
  - This results in smaller code bundles, a reduction in memory usage, and faster rendering.
  - Since the values are extracted at compile time, truly dynamic values can’t be used. 
  - These are thankfully not very common and since they are unique, don’t suffer from being defined inline. 
  - What’s more common is conditionally applying styles, which of course is supported. 
  - So are local constants and mathematical expressions, thanks to babel’s path.evaluate.
- Atomic output
  - Because of how style9 works, every property declaration can be made into its own class with a single property. So, for example, if we use `opacity: 0` in several places in our code, it will only exist in the generated CSS once. 
  - The benefit of this is that the CSS file grows with the number of unique declarations, not with the total amount of declarations.
  - Since most properties are used many times, this can lead to dramatically smaller CSS files.
- Some may complain about this, that the generated class names are not semantic, that they are opaque and are ignoring the cascade. 
- This is true. We are treating CSS as a compilation target. But for good reason. By questioning previously assumed best practices, we can improve both the user and developer experience.
- In addition, style9 has many other great features, including: typed styles using TypeScript, unused style elimination, the ability to use JavaScript variables, and support for media queries, pseudo-selectors and keyframes.
- The syntax for creating styles closely resembles other libraries. 
- We start by calling `style9.create` with objects of styles
- Because all declarations will result in atomic classes, shorthands such as flex: 1 and background: blue won’t work, as they set multiple properties. Properties that can be can be expanded, such as padding, margin, overflow, etc. will be automatically converted to their longhand variants. If you use TypeScript, you will get an error when using unsupported properties.
- Summary
  - With CSS-in-JS, we are imposing a performance cost when embedding styles in our code. 
  - By extracting the values during build-time we can have the best of both worlds. 
  - We benefit from co-locating our styles with our markup and the ability to use existing JavaScript infrastructure, while also being able to generate optimal stylesheets.

## Facebook's CSS-in-JS Approach - stylex

- [Facebook's CSS-in-JS Approach - Frank Yan at React Conf 2019](https://www.infoq.com/news/2020/04/facebook-cssinjs-react-conf-2019/)

``` typescript
const styles = stylex.create({
  blue: {color: 'blue'},
  red: {color: 'red'}
});

function MyComponent(props) {
  return (
    <span className={styles('blue', 'red')}>
      I'm blue
    </span>
  )
}
```

## Why use css in js

- ### [Write CSS in JavaScript_mxstbr_201902](https://mxstbr.com/thoughts/css-in-js)

- What Does CSS-in-JS Look Like?

``` typescript
import styled from "styled-components";

const Title = styled.h1`
  color: palevioletred;
  font-size: 18px;
`;

const App = () => <Title>Hello World!</Title>;
```

- Why I like CSS-in-JS
- **Confidence from scoped styles**
  - Add, change and delete CSS without any unexpected consequences and avoid dead code.
  - Primarily, CSS-in-JS boosts my confidence. 
  - I can add, change and delete CSS without any unexpected consequences. 
  - My changes to the styling of a component will not affect anything else. 
  - If I delete a component, I delete its CSS too. 
  - No more append-only stylesheets!
- **Painless Maintenance**
  - Never go on a hunt for CSS affecting your components ever again.
- **Enhanced Teamwork**
  - Avoid common CSS frustrations to keep a neat codebase and moving quickly, regardless of experience levels.
  - With CSS-in-JS, we automatically sidestep common CSS frustrations such as class name collisions and specificity wars. 
- **Fast Performance**
  - Send only the critical CSS to the user for a rapid first paint.
  - CSS-in-JS libraries keep track of the components I use on a page and only inject their styles into the DOM. While my .js bundles are slightly heavier, my users download the smallest possible CSS payload and avoid extra network requests for .css files.
  - This leads to a marginally slower time to interactive, but a much quicker first meaningful paint
- **Dynamic Styling**
  - I can also easily adjust the styles of my components based on different states or a global theme. 
  - The component will apply the correct styles automatically when I dynamically change that context.
- CSS-in-JS still offers **all the important features of CSS preprocessors**. 
  - All libraries support auto-prefixing, and JavaScript offers most other features like mixins (functions) and variables natively.

## Styled Components vs. CSS Stylesheets

- [Styled Components vs. CSS Stylesheets_202001](https://getstream.io/blog/styled-components-vs-css-stylesheets/)

- s-c pros
  - No Globally Scoped Selectors
  - Dynamic Styling
  - Theming
  - Consistency
  - Sass Syntax Out-Of-The-Box
- s-c cons
  - Learning Curve
  - Integration With Legacy CSS Can Be Painful
  - not a standard
  - runtime cost
  - Colocating Can Bloat Your Components

- css pros
  - Unopinionated and Universal
  - Caching & Performance
  - Quickly Iterate A New Design
  - Ease of Use
  - abundant exsiting css frameworks
- css cons 
  - Readability, difficult to navigate
  - Legacy CSS Can Live On For Years
  - Global Scope & Specificity
  - No True Dynamic Styling
  - Maintaining Consistency for theme, variables

## ref

- [CSS and JS Are at War, Here’s How to Stop It_201901](https://dev.to/evilmartians/css-and-js-are-at-war-heres-how-to-stop-it-158a)
  - The warring factions are often labeled as:
    - “JS-JS-JS”: Developers who create SPA with client-side JavaScript frameworks like React, Vue.js, and Angular. They are heavy users of innumerable build tools (Babel, webpack, etc.) and JS libraries.
    - “UX developers”, “CSS developers”, “HTML-JS-CSS developers”: Developers who create static websites with vanilla JavaScript and plain CSS. Accessibility and performance are most important topics in their community.
  - The Solution
    - start a civilized discussion
    - have a public forum for a conversation
