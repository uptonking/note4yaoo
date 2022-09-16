---
title: web-style-css-in-js-styled-components
tags: [css-in-js, style]
created: 2019-08-17T10:19:06.636Z
modified: 2021-05-13T02:58:45.832Z
---

# web-style-css-in-js-styled-components

# dev-tips

- 如何复用现有项目的样式和第三方库的样式
  - 必需支持class或className
- 如何将本项目作为库提供给其他人使用
  - 直接复用组件，而不是复用样式，
  - 若必须复用样式，则提取出变量通过theme来复用
  - 还可考虑实现一套css，再另外实现一套css in js
- why you should use css-in-js
  - possible to author CSS in JS syntax
  - Styles are "scoped" to a specific component
    - no naming collision
    - include only the styles that are really used，like lazy-styling
    - make dead code elimination easier
  - Colocate styles with components
  - Many libraries offer support for theming
  - Most libraries offer ways to handle dynamic styling
  - Take advantage of native JS syntax features
  - Take advantage of anything from the JS ecosystem
  - type check and code auto suggestion with ts
  - easier to write unit tests with CSS-in-JS
  - ref
    - https://jxnblk.com/blog/why-you-should-learn-css-in-js/
    - https://mxstbr.com/thoughts/css-in-js
    - 技术选型时，参考知名项目或大公司项目的选择
- 使用styled-components这种css-in-js的优缺点
  - 优点是局部样式、动态样式、主题切换
    - 基于css in js实现theming复杂度更低
      - 因为基于css vars实现theming需要考虑变量值层叠
  - 缺点
    - runtime cost
      - 对于交互不频繁、性能要求不极限的场景，使用styled组件时可行的
      - 因为就算自己用js计算新的样式名本身也有一定的计算，样式变化不多的情况下对性能影响可忽略
    - 会创建重复的样式
# linaria

## basic

- https://github.com/callstack/linaria
- https://linaria.now.sh/
- https://github.com/callstack/linaria/blob/master/docs/BENEFITS.md

## pieces

# emotion

## basic

- https://emotion.sh/
- https://github.com/emotion-js/emotion
- Emotion is a library designed for writing css styles with JavaScript

## faq

- emotion创建样式的组件，可以提取成单独的css吗
  - 旧版本可以，v10新版本不行
  - extractStatic is not recommended because it breaks composition and other powerful patterns from libraries like facepaint.
  - facepaint provides responsive and dynamic style values for css-in-js. 常用语media-query
  - https://github.com/emotion-js/emotion/blob/master/docs/extract-static.mdx
- use case
  - 变量
  - theme
  - ref
    - https://github.com/jsjoeio/styled-components-vs-emotion
- s-c的问题
  - 嵌套过深，每个组件如styled.button下有StyledComp, 还有2个Context. Consumer
    - styled-components v5已解决嵌套过深的问题
  - css prop需要babel插件支持 
- emotion优势
  - framework agnostic, 框架无关的，可以额外引入与框架对应的emotion包
  - 兼容s-c的styled组件写法
  - ref
    - https://theme-ui.com/motivation/  (why emotion)
- emotion问题
  - 缺少 `.attrs()` 方法传递属性
    - https://github.com/emotion-js/emotion/issues/821
    - `const withAttrs = (Component, attrs) => props => <Component {...attrs} {...props}/>`
    - 使用css prop `const MyComponent = props => (<input css={{}} {...props} />`
- styled形式组件的样式可通过再次styled复用已有组件的样式，如何复用css prop的样式
- className vs css prop
  - className属性的值是字符串，想在生成字符串的过程中获取组件props，要么显式传入this.props，要么创建高阶组件隐式获取props再计算，所以通用的方法推荐使用css prop
  - className example

```js
  <div
    className={css({
      backgroundColor: 'hotpink',
      '&:hover': {
        color
      }
    })}
  >

  <div
    className={css`
      background-color: hotpink;
      &:hover {
        color: ${color};
      }
    `}
  >
  
```

  - css prop example

```js
  <div
    css={{
        backgroundColor: 'hotpink',
        '&:hover': {
          color: 'lightgreen'
        }
      }}
  >

  <div
    css={css`
      background-color: hotpink;
      &:hover {
        color: ${color};
      }
    `}
  >
```

- s-c vs emotion
  - https://github.com/jsjoeio/styled-components-vs-emotion
  - https://github.com/emotion-js/emotion/issues/113
  - https://material-ui.com/zh/guides/interoperability/
  - https://spectrum.chat/styled-components/general/styled-components-vs-emotion~47206c1b-a688-424e-9e96-6f265993587e

## emotion-docs

- emotion - framework agnostic
  -  use `css` function to generate class names and `cx` to compose them
  - Requires no additional setup, babel plugin, or other config changes.
  - `css` prop is not used or needed.
  - Server side rendering requires additional work to set up
  - Emotion is not using a "standard" autoprefixer (which works during build) - it ships with its own runtime parser ( thysultan/stylis.js ) which comes with autoprefixing and it's enabled for you by default.

```js
  import { css, cx } from 'emotion'
  const colorW = 'white'
  render(
    <div
      className={css`
        padding: 32px;
        background-color: hotpink;
        border-radius: 4px;
        &:hover {
          color: ${colorW};
        }
      `}
    >
      Hover to change color.
    </div>
  )
```

- @emotion/core - for react (emotion vs @emotion-core)
  - `css` prop support
      - Similar to the `style` prop but adds support for nested selectors, media queries, and auto-prefixing
      - Allows developers to skip the styled API
  - Server side rendering with zero configuration
  - Theming works out of the box
- @emotion/styled 
  - use the styled.div style API for creating components
  - https://github.com/jsjoeio/styled-components-vs-emotion
- react-emotion
  - Because Emotion 10 has more React-specific APIs and they shouldn’t all be bundled together, it doesn’t make sense to have a package called react-emotion, so we’re changing some package names. 
  - The new APIs for React are in @emotion/core and styled is in @emotion/styled. 
  - The emotion package exports nearly the same API as in v9 except for some internals that have changed.
  - APIs such as css & keyframes are part of emotion, but in general react-emotion re-exports everything that is already in emotion. so react-emotion can just use a single package instead of importing some things from emotion & some from react-emotion.
  - emotion itself is react-independent. it doesn't really have theming built in 
- changelog
  - 10.0.0-201810-new package name, better css prop, Global comp
# styled-components

## basic

- https://www.styled-components.com/docs/basics
- https://github.com/styled-components/styled-components

## community

- ### [Styled components fills head tag with additional unused style tags, doesn't clean them up](https://github.com/styled-components/styled-components/issues/1431)
- Yeah, we don't remove styles as it'd add unnecessary performance overhead—why does it hurt you to have more style tags in the head?
  - Also, how are you using styled-components so that you "add anywhere between 5 to 20 additional classes appearing on every click/navigation in our app"? That seems like a usage problem rather than a library problem
- A separate component will be created every time you call styled(). This component receives a componentId and injects it’s styles under there with a hash.
  - The amount of styles you have there might mean that you have a large app.
  - But it might also indicate that you’re calling styled() in a render function / stateless component and are recreating it every time. Or it might mean that you’re passing arbitrarily complex float values to it
- It's not something on our roadmap to change in the near future, since it doesn't appear to be a burning issue. I'd recommend following @kitten's advice and working on reducing the dynamicness of whichever component(s) is generating all that excess CSS.

- ### [How to remove component styles for unmouned components?](https://stackoverflow.com/questions/56950754)
- use the new style-loader API, something like this via injectType
  - `{ loader: "style-loader", options: { injectType: "lazyStyleTag" } }` lazy配置
- styleTag
  - Automatically injects styles into the DOM using multiple `<style></style>`. It is default behaviour.
- lazyStyleTag
  - Injects styles into the DOM using multiple `<style></style>` on demand.
  - injects the styles lazily making them useable on-demand via `style.use()` / `style.unuse()`.
- lazySingletonStyleTag
  - Source maps do not work.

- ### [Feature Request: Remove global (createGlobalStyles) styles on unmount](https://github.com/styled-components/styled-components/issues/2487)
- We do remove it, not sure what's going on for the OP but we absolutely do remove it on unmount.

- ### [emotion: Styles are not being removed from DOM after component unmount](https://github.com/emotion-js/emotion/issues/488)
- emotion is built around a function that returns a class name so it has no knowledge of whether or not it's being used. Keeping all the rules also means we can heavily cache rules. Is there a reason to not keep them?
- Some browsers (old-ish IE) have rules about the maximum number of stylesheets and/or styles you can have at once.
  - 💡 There will only be many style tags in development, in production we use one style tag per 65000 rules.
- What do you think of having too many CSS rules in a style element, will it affect a performance? have you guys done any performance tests on that?
  - It won't, it's been discussed in the past with glamor but it was found out that it didn't cause any problems and no one has ever reported it causing a problem.

- AFAIK styled-components doesn't remove "unused" styled from the DOM either.

- ### [Remove unused styles from a React SPA app](https://github.com/postcss/postcss/issues/1108)
- Sorry, I didn't hear about any uncss for React pensive.
  - My suggestion is to split CSS into small components as you split React components. Next put CSS and React code of each component in same dir. 
  - So when you will delete React code, you will delete CSS code as well.

- ### [PurgeCSS & styled-components: Does It Work?_202204](https://www.useanvil.com/blog/engineering/purgecss-styled-components/)
- 构建时 vs 运行时
- PurgeCSS analyzes your HTML and internally keeps track of which selectors are being used or not.
  - After finding which selectors are actually being used, PurgeCSS analyzes your CSS files and deletes the ones that aren't used. 
- Automatic critical CSS: styled-components keeps track of which components are rendered on a page and injects their styles and nothing else, fully automatically. 
  - Combined with code splitting, this means your users load the least amount of code necessary.

## faq

- ## s-c实现原理
  - [Demystifying styled-components](https://www.joshwcomeau.com/react/demystifying-styled-components/)
  - https://dev.to/stereobooster/styled-components-one-more-time-5g0l
  - https://medium.com/styled-components/how-styled-components-works-618a69970421

- ## styled(MyComp)会传递所有属性，如何只传递指定属性
  - 对于styled('tag')，s-c只传递html属性
  - 手动选出不需要传递下去的属性，然后传递给底层组件restProps

- ## Why write styles inline with jsxstyle library?
  - Naming things is hard
  - Jumping between JS and CSS in your editor wastes time
  - inline styles are easy to find styles and to delete
  - Styles written inline don’t remain inline
  - Building tooling around inline styles is simple and straightforward
  - webpack plugin , at build time, extracts static styles defined on jsxstyle components into separate CSS file and in some cases entirely removes the need for runtime jsxstyle

- ## inline styles/js vs external .css/.js 
  - Inlining everything is the ultimate way to reduce the number of requests (in theory to one). But it’s not the best way to make your site faster.  
      - inline的3个问题：缓存、按需加载、预加载、修改与维护
      - If the HTML holds all the resources, and the HTML is not cacheable by itself, the resources are re-downloaded every time.
      - Even if the HTML is cacheable, the cache duration has to be the shortest duration of all the resources on the page. If your HTML is cacheable for 10 minutes, and a resource in the page is cacheable for a day, you’re effectively reducing the cacheability of the resource to be 10 minutes as well.
      - The traditional value of CDNs is called Edge Caching: caching static resources on the CDN edge. Cached resources are served directly from the edge, and thus delivered much faster than routing all the way to the origin server to get them.When inlining data, the resources are bundled into the HTML, and from the CDN’s perspective the whole thing is just one HTTP response. If the HTML is not cacheable, this entire HTTP response isn’t cacheable either. Therefore, the HTML and all of its resources would need to be fetched from the origin every time a user requests the page, while in the standard case many of the resources could have been served from the Edge Cache.
      - Browsers offer a built-in loading on demand mechanism for CSS images. If a CSS rule references a background image, the browser would only download it if at least one element on the page matched the rule.Since inlining resources is a decision made on the server, it doesn’t benefit from loading on-demand. This means all the images (CSS or page images) are embedded, whether they’re needed by the specific client context or not
      - Modern browsers use smart heuristics to try and prefetch resources at the bottom of the page ahead of time. If you’re making heavy use of inlining, the HTML itself becomes much bigger
  - Ordinarily, inline styling is discouraged by the react team, a concern that is very valid because inline styles do not allow the use of pseudos and media queries
  - Also, inline styles should not be used due to a lot of concerns about browser compatibility, camel-casing, and automatically appended scalar quantities    
  - size of inline styles can be huge, especially if we repeat elements
  - Using the style attribute, the browser only paints the rule for that particular element. This reduces the amount of look up time for  CSS engine to find which elements match the CSS selector (e.g. a.hover).
  - However, putting styling at element level would mean that you cannot cache the CSS style rules separately. Usually putting styles in CSS files would allow the caching to be done, thus reducing the amount of load from the server each time you load a page.
  - Putting style rules at the element level will also make you lose track of what elements are styled what way. It might also backfire the performance boost of painting a particular element where you can repaint multiple elements together. Using CSS files separates the CSS from HTML, and thus allows you to make sure that your styles are correct and it's **easier to modify** later on. Inline styles are not easy to maintain.
  - className可复用现有的大量css样式库
  - I can suggest using JavaScript codes to create the CSS codes ahead of time and then just post the compiled CSS codes on the server for download by the client, rather than having the CSS codes being made up by the client. Also, I think you should not use the HTML "style" attribute; it is bad for accessibility. Use the "class" attribute instead.
  - It's around three times as fast to create and render elements that use classNames, rather than style attributes. I was quite surprised by that. Browser processes className CSS rule only once, whereas it has to do it each time when it encounters style in an attribute. Furthermore browser might keep in cache already processed CSS file (if you use external CSS file) and on repeated view style calculations might be much faster.
  - ref       
      - https://jsperf.com/style-element-vs-attr
      - https://stackoverflow.com/questions/4244886/rendering-performance-style-attributes-or-classnames-and-stylesheet-rules
      - https://mathiasbynens.be/notes/inline-vs-separate-file
      - https://calendar.perfplanet.com/2011/why-inlining-everything-is-not-the-answer/
- s-c如何复用第三方库的css样式，如何复用第三方库的s-c样式
  - `attrs(props=>({}))`
  - 优先考虑直接复用组件，而不是复用样式，若要复用样式，尽量通过变量或对象复用
- s-c对css原生特性的支持如何
  - Within a styled component, we support all of CSS plus nesting
  - Since we generate an actual stylesheet and not inline styles, whatever works in CSS works in styled-components!
- s-c性能如何
  - There will always be some overhead for a runtime CSS-in-JS library since it's ultimately doing more work. But for that overhead you're also getting a lot of flexibility and power.
  - If all your styles are actually static, then a pure CSS approach will definitely be the most performant. But, that comes with its own caveats in terms of managing your stylesheets, writing efficient selectors, and such.
  - s-c每次渲染都会重新计算cssRule，并进行hash计算出className，如果已经对应的className还没插入到样式表中，则使用stylis进行预处理，并插入到样式表中
  - s-c对静态cssRule(没有任何内插函数)进行了优化，它们不会监听ThemeContext变化, 且在渲染时不会重新计算
  - s-c并不会对已有样式中的不变的部分规则进行复用，一旦状态变化s-c会生成一个全新的样式规则和类名, 这避免了样式复用的复杂性，同时保持样式的隔离性，问题是会产生样式冗余
  - s-c会为每个状态生成一个样式表, 动画一般会有很多中间值，在短时间内进行变化，如果动画值通过props传入该StyledComponent来应用样式，这样会生成很多样式, 动画场景最好使用style内联样式来做
      - 不是指不要使用CSS动画(animation|transition), 而是指js控制动画，变动StyledComponent的props值
  - does not use inline styles
  - 参考
      - https://github.com/styled-components/styled-components/issues/1735
- s-c**优点**
  - 兼容现有的className方式，迁移无痛
  - 在代码设计层面消除css命名冲突
  - 样式相关变量可以共享，都是作为在js中的变量
  - 支持样式组件继承(styled)，方便代码复用
  - 样式也作为一种组件
  - 能通过 `$(CompName)` 直接选择其他react组件设置样式
  - 支持ssr和react-native
  - powerful js
  - 保持dom结构与样式分离的同时，不使用class，不需要跳转多文件，也不是内联样式
- s-c**缺点**
  - 每次点击会创建新class，但不会删除旧class，debug体验不好      
  - 不能用stylelint检查CSS代码，不能使用prettier来格式化css，ide语法高亮与自动提示支持不完善
  - 父组件覆盖子组件的className较复杂，需要使用 `.container.container{}`
  - 国内关注度不高，资料不丰富
  - s-c样式组件是一层包裹，层层包裹会消耗性能
  - Biggest drawback: changes to styles require bundle re-compilation and app's state might reset
  - 不支持css提取为静态文件，参考[issue](https://github.com/styled-components/styled-components/issues/1018)
  - 复杂组件开发时会产生嵌套地狱wrapper hell，这也是react的一个问题
      - custom hooks试图解决wrapper hell的问题
  - s-c只支持React，如果你用其他的JS框架你必须寻找其他CSS方案
- css-in-js-pros
  - Enforce only local styles
  - Developer productivity
  - Better theming support
  - Better support for dynamic styles
  - Easier to consume packages
  - Typesafe styles
- css-in-js-cons
  - Worse runtime performance
  - Bigger bundle size
  - Fragmentation of ecosystem
  - Idiosyncratic additions to css
- Why do my DOM nodes have two classes
  - Each node actually has two classes connected to it
  - One is static per component, meaning each element of a styled component has this class. 
      - It hasn't any style attached to it. 
      - Instead, it's used to quickly identify which styled component a DOM objects belongs to or to make minor changes in the DevTools. - It's also used for component selectors. The static class probably will look something like: `.sc-fVOeaW`
  - The other is dynamic, meaning it will be different for every element of your styled component with different props, based on what the interpolations result in. It will probably look like `.fVOeaW`
- styled-components: to use or not to use?
  - For our use case, we didn’t convert our entire project to Styled Components. We chose to keep majority of CSS in the more traditional (i.e. separated) file structure and **use styled-components for elements whose styling (colors, images, etc.) is configured by the user**
  - What We Loved About Styled Components
      - It Makes Components Less Bulky
        - s-c also helps to keep the concerns of styling and element architecture separated 
        - s-c gives control of those states back to CSS instead of using a multitude of conditional class names
        - Instead of relying on two separate style objects and having to use React event handlers to setup a simple hover state, we use a styled component. 
        - This makes it easy to inject values that only exist in JavaScript into our CSS while still allowing CSS to handle the various UI states.
      - ThemeProvider is useful when building a configurable page
      - powerful CSS Function
        - use props to conditionally render css instead of rendering conditional class names based on props
        - easy if we wanted to add a third state of button style
      - easy to test
  - What We Found Frustrating About Styled Components
      - There were certain style rules that we found hard to apply to Styled Components; namely, rules that set the placement of an element on a page (e.g. margin or display properties). They were difficult to standardize, so we still ended up leaning heavily on plain ol’ CSS for component placement in the flow of elements.
      - The syntax takes some time to get used to
  - Reasons not to use styled components
      - Extra page weight as you add lots of extra divs to style your components
      - More page weight as you need to include a library to replace something you get for free in all browsers
      - Less code re-use compared to using proper CSS
      - Slower than using stylesheets as there is no caching ~ bad for user
      - Slower as you have to create inject the styles into the head on each page load
      - Hard to get a consistent style across a site
  - 参考
      - https://medium.com/building-crowdriff/styled-components-to-use-or-not-to-use-a6bb4a7ffc21
      - https://blog.logrocket.com/8-reasons-to-use-styled-components-cf3788f0bb4d/
      - https://dev.to/christopherkade/styled-component-what-why-and-how-5gh3

## summary

- s-c是典型的css-in-js样式解决方案
- s-c使用ES6的字符串模板方式来定义css样式，这样使得css的写法与原生的css写法基本一致，不用按照react的camelCase写样式
- css()
  - A helper function to generate CSS from a template literal with interpolations
- s-c原理
  - When you import the library first time in you app, it creates an internal `counter` variable to count all the components created via the `styled` factory.
  - When styled-components creates a new component, it also creates internal identifier componentId using MurmurHash algorithm
  - As soon as the identifier is created, styled-components inserts new HTML `<style>` element into the ` <head>` (if it is the first component and the element is not inserted yet) of your page and adds special comment marker with the componentId to the element which will be used later. 
  - components are inherited from hidden `BaseStyledComponent` class which implements several lifecycle methods
  - `componentWillMount()` of BaseStyledComponent
      1. Evaluating tagged template
      2. Generating CSS class name. Each component instance with uniq props has it’s own CSS class name which generated by means of the same MurmurHash algorithm but from the componentId and the evaluatedStyles string
      3. CSS Preprocessing
      4. Injecting CSS string into the page
  - each component has 2 class names
      - `class="sc-bdVaJa jsZVzX"`
  - when `componentWillReceiveProps()` is called
      - as above 1234
      - one small optimization here: **components without interpolations in the style string are marked as isStatic** and this flag is checked in componentWillReceiveProps() in order to skip unnecessary calculations of the same styles 
  - 使用babel-plugin-styled-components插件，设置好后，就可以在浏览器里看到可读的class名
  - 参考
      - https://medium.com/styled-components/how-styled-components-works-618a69970421
      - my personal rule is to use the style attr for all dynamic styles with undermined number of results.
      - But if you have variety of buttons like default, primary, warn and etc. in one component it is ok to use interpolation with conditions in the styles string.
      -  react-transition-group is so simple. If we use styled-componets, `<Transition>` component may be better than `<CSSTransition>`
      - if you are using animations with styled-components you need to put them on the .attrs({})`` and not the style itself. Look at your inspector, the className changes on each redraw
- s-c最终生成的是随机字符串类名，能解决命名冲突，设置到dom中的不是内联样式
- s-c也有一套用JS实现的预处理器工具库polished，其中包括一些常用的CSS方法，比如 clearfix、hsl、mix 等，让开发者可以完全不再使用css预处理器来写css了
- 也可以将样式对象写在单独文件，再导入，类似grommetv2的处理方式
- 移除了组件和样式之间的映射关系，将样式也作为组件或组件的一部分
- 通过attrs()方法可以传入html标签的属性，还可以传入className，方便使用第三方样式
- s-c支持动画的@keyframe
- s-c支持类似sass的嵌套语法，但不推荐使用嵌套，因为样式组件的子组件的className不会被编译成随机值，这些子组件的类还是会受CSS的全局作用域影响
- 使用了逻辑组件与样式展示组件分离的思想
- jss也是css-in-js的一种解决方案
  - 用户包括material-ui
  - 使用类似于json的语法描述css
- 调整特指度的方式
  - The ampersand(&) can be used to refer back to the main component
  - The ampersand(&) can be used to increase the specificity of rules on the component

## styled-components-docs

- The rule of thumb is to use `attrs` when you want every instance of a styled component to have that prop, and pass `props` directly when every instance needs a different one
  - you can set a property on attrs to a function that computes that prop based on other props.
- ThemeProvider provides a theme to all React components underneath itself via the context API
- existing css
  - styled-components generates an actual stylesheet with classes, and attaches those classes to the DOM nodes of styled components via the className prop. It injects the generated stylesheet at the end of the head of the document during runtime.
  - You can use its existing class names alongside your components.
  - If you want the class to always be attached to the component, you should use the `attrs` method to attach it. 
  - If you want to attach it only in some cases, you can use `className` props like you always have.
  - If the framework has a bunch of raw global CSS that needs to be included on the page, you can add it using the createGlobalStyle API. This is also useful for things like CSS resets.
- changelog
  - 4.0.0-201810-A brand new createGlobalStyle API, support as, ref prop
  - 4.1.2-201811-native support for the css prop
  - 5.0.0-2019-alpha-no breaking, rewrite with hooks to no wrapper hell

## qucikstart

- demo

```js
import styled from 'styled-components';
const Wrapper = styled.div `
margin: 0 auto;
width: 300px;
`;
const Button = styled.button `
width: 100px;
color: blue;
`;
render(
  <Wrapper>
  <Button>Hello World</Button>
</Wrapper>
);
```

- demo2

```js
const Button = () => <button></button>
const StyledButton = styled(Button)
`
//style goes here
`;
export default StyledButton;
import Button from './Button';
const FormContainer = styled.form `
${Button] {
  //additional style goes here
}
`
//给样式组件添加额外的样式
const StyledButton = styled(Button)
`
//additional style goes here
`
```

## styled under the hood

- ref
    - https://medium.com/styled-components/how-styled-components-works-618a69970421
    - https://mxstbr.blog/2016/11/styled-components-magic-explained/
    - https://medium.com/@_jmoller/how-does-styled-components-work-under-the-hood-28cb035d48c6
- styled用法

```js
const Button = styled.button `
color: coral; 
padding: 0.25rem 1rem; 
border: solid 2px coral; 
`;

// 等价于  

const Button = styled('button')([
  'color: coral;' +
  'padding: 0.25rem 1rem;' +
  'border: solid 2px coral;'
]);
```

- 自定义styled

```js
// styled(Button)返回一个tag function，而标签函数返回高阶组件而不是拼接后的字符串
const myStyled = (TargetComponent) =>
  // tag function第一个参数是字符串字面量数组，随后参数是占位符表达式的值
  (strs, ...exprs) => class extends React.Component {
    interpolateStyle() {
      const style = exprs.reduce((result, expr, index) => {
        const isFunc = typeof expr === 'function';
        const value = isFunc ? expr(this.props) : expr;

        return result + value + strs[index + 1];
      }, strs[0]);

      this.element.setAttribute('style', style);
    }

    componentDidMount() {
      this.interpolateStyle();
    }

    componentDidUpdate() {
      this.interpolateStyle();
    }

    render() {
      return <TargetComponent {...this.props} ref={element => this.element = element } />
    }
  };

const primaryColor = 'coral';
const Button = myStyled('button')
`
background: ${({ primary }) => primary ? primaryColor : 'white'};
color: ${({ primary }) => primary ? 'white' : primaryColor};
padding: 0.25rem 1rem; 
border: solid 2px ${primaryColor}; 
border-radius: 3px;
`;
```

# bootstrap
- bootstrap-components
  - bootstrap中input添加.form-control类，表示为input元素添加表单控件样式
- faq
  - bootstrap.css vs bootstrap-theme.css
      - bootstrap.css is the core css for BootStrap that defines all the style for various controls/components
      - bootstrap-theme.css defines the themes (gradient/animation) for buttons,dropdown menu,navbar,progressbar,panels
      - Most of the times adding bootstrap.css is enough for bootstrap to work, but for gradient/animation, you can use bootstrap-theme.css
- theme-for-bootstrap
  - https://bootswatch.com/
  - https://themes.3rdwavemedia.com/bootstrap-templates/free/

## bootstrap-bootswatch-themes

- default
- 绿色系
  - minty 薄荷味的 *****
- 蓝色系 
  - cerulean ***
  - cosmo ***
  - lumen
  - yeti
- 黑色系
  - darkly
  - cyborg
  - lux *****
  - sandstone
  - slate
  - solar
  - superhero
- 红色系
  - journal
  - united
- 紫色系
  - pulse
- flatly ***
- litera *****
- materia
- simplex
- sketchy
- spacelab
