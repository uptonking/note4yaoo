---
title: note-style-css-in-js-theme-spec
tags: [css-in-js, style, web]
created: '2019-11-30T10:00:18.020Z'
modified: '2020-10-27T05:27:35.596Z'
---

# note-style-css-in-js-theme-spec

## faq

- ### 为什么用css-in-js
- pros
  - naming is hard
  - scoped styles 局部样式
  - simple dynamic styling adapting to its props 动态样式
  - easy to create themeable components 切换主题
  - type check and code auto suggestion
  - support all of CSS plus nesting
  - better maintainability
    - easy to delete css
    - easy to find styles
    - css的样式层叠顺序更清晰，当很少使用全局样式时
    - 大型软件通常更重视可维护性和兼容性，性能通常不是最高
  - js is the future (for its ecosystem)
    - define style helper functions in js rather than sass
- cons
  - learning curve
  - css-in-js runtime cost in performance and size 
  - 技术选型时，参考知名项目或大公司项目的选择，但结论是大公司都没选css-in-js
- ref
    - css-in-js趋势：静态提取、theming支持、constraint-based props、atomic css-in-js
    - https://jxnblk.com/blog/why-you-should-learn-css-in-js/
    - https://mxstbr.com/thoughts/css-in-js
    - https://spin.atomicobject.com/2018/12/28/css-in-javascript-benefits/
    - https://medium.com/@lindsay_jopson/is-css-in-js-really-better-than-traditional-css-8ac5b3f7fc20
- css-in-js热门项目
  - Microsoft Fluent Design 自己实现了styled方法
  - Uber Base Design用的是styletron-react
  - SAP Fiori(react-jss)
  - 使用styled-components或emotion的项目
    - Atlassian Design, Github Primer Design
    - HP grommet, Zendesk Garden
    - Kiwi.com Orbit design, Esri Calcite Design
- 为什么用emotion/styled-components
  - styles written inline, but className auto generated and added to dom
- 为什么用styled-system
  - themed based component
  - consistent prop names and scalar values
- 为什么用glaze
  - Near-zero runtime, made possible by treat, Theming support, Static style extraction
  - Constraint-based layouts, popularized by Theme UI
  - Utility-first CSS, as implemented by Tailwind CSS
- 为什么采用styled形式的组件，而不用className，调用该api能够传入props，然后根据props计算新样式属性再添加到组件上
  - 只有高阶组件能做到，普通方法做不到
  - styled开发体验好，性能可能不是最好
- css prop vs scss prop，不用className
  - className不能给组件动态添加样式属性
    - 因为需要一个styled
  - 样式写法上，差别不大
  - debug时，emotion的styled比styled-components的组件少一层styled.button
  - css prop的组件有时比styled的少一层Context. Consumer
  - css prop比styled少一层styled
- className vs css prop
  - emotion的css方法返回的是字符串，@emotion/core的css方法返回的是一个对象，包含字符串和扁平化的样式属性值，可被styled方式使用，兼容性更好
  - 写法上，采用object style时，css prop可以少写一个css
  - className不会wrapper hell
- css prop可以类似styled，给组件添加样式属性吗
  - @emotion/core的css()方法中可以类似styled-system给组件添加样式属性吗
  - css prop的原理是通过babel插件调用库相关的jsx函数而不是React.createElement来创建组件，这个过程会通过高阶函数给组件添加样式属性
    - https://www.felixjung.io/posts/the-css-prop-in-emotion-10/
    - Babel’s React JSX plugin has an option to specify the function it uses to transpile JSX expressions. The plugin defaults to using React.createElement. But by relying on React.createElement, you can only use syntax, such as props, supported by React.createElement. So, if you provide a different function to transpile JSX, you can support a different syntax.
    - we use the jsx pragma (/** @jsx jsx */) to tell Babel it should use the jsx function imported from @emotion/core to transpile JSX. And that is all you need to do to use the css prop. You do not need Emotion’s Babel plugin.
    - Importing React in a component is not an actual module import. It merely tells Babel that your JavaScript module contains JSX, which should be transpired using the React JSX plugin (i.e., with React.createElement). Using the jsx pragma allows you to opt into the css prop on a per component basis, by changing the way that component’s file is transpiled by Babel. You only need to specify the pragma, if you use the css prop in your component’s JSX.
    - The styles will be evaluated and stored in Emotion’s cache under a class name. The class name is passed down to the React element through the className property.
    - you now have direct access to the theme context created by a ThemeProvider
  - css prop和styled最终生成组件的结构非常相似
- ### style object vs template literals(TTLs) 书写样式，使用模板字符串，还是对象
  - style object
    - 当需要动态变化的样式属性有很多时，使用对象cleaner
    - 样式对象更方便计算及复用，如spread operator和destructuring
    - 对象更容易进行类行检查，字符串css可能后面难以检查
  - TTLs
    - 更接近熟悉的css
    - ide的提示更容易实现
    - 动态变化的属性较少时，插值函数少，cleaner
    - 可以直接在末尾添加重复行，方便调试
  - conclusion  
    - The more interpolations you use, the more object notation tends to win over template strings in terms of readability.
  - The interoperable `theme` object itself is an object, and keeping styles in a similar format helps reduce the API surface area. 
  - Using and parsing strings that represent embedded DSLs introduces overhead when mapping over key-value pairs.
    - Theme UI avoids this overhead for reasons related to performance, testing, and overall bundle size. 
    - For some of the same reasons that React itself uses JSX (i.e. function calls) instead of tagged template literals
  - In Stitches, you write CSS using the object style syntax. 
    - The reasons for this are: performance, bundle size and developer experience (type checks and autocomplete suggestions for both properties and values)
  - ref
    - https://theme-ui.com/motivation/ 
    - 要考虑熟练度、提示需求(对象比str适合)、复用现有样式等
    - 还可以使用分散写的单独的属性，类似 `<Box color="primary" size="lg" />`
    - https://levelup.gitconnected.com/react-css-in-js-es6-objects-vs-tagged-template-literals-71670e78995f
    - https://medium.com/@oleg008/template-strings-vs-objects-in-cssinjs-4028ecc420b2
    - https://spectrum.chat/styled-components/general/style-object-vs-template-literalls~789509f2-7460-4b4c-84bc-b169c2230132
    - https://www.christopherbiscardi.com/post/composition-of-styles-strings-vs-objects/
- pros for style object
  - css within component 
  - better type checking
- pros for template literal
  - support media queries, pseudo
  - easier to reuse existing css
  - better readability
- Permissive vs Restrictive component API
  - styled-system v5中一个函数暴露一组样式api，可能会过多，对性能影响大吗
  - 有人提出一种通用组件 `<comp type='ul/h1/input' p1='' p2=''>` ，支持1000+属性，每次创建都会遍历所有属性，并且性能也不差
  - theme-ui allows use of any styled-system prop on any component (or element) through use of the sx prop
  - https://spectrum.chat/styled-system/general/permissive-vs-restrive-component-apis~475715ea-a538-41be-8366-779226339650
  - https://github.com/universalstandard/ook (any camelCased css property)
  - https://spectrum.chat/styled-system/general/strict-component-api-with-styled-system~a6582471-99d2-4d2c-94d2-2a05de61d4c4
  - https://github.com/styled-system/styled-system/issues/562 (Style functions exposing extra props)
- 是否使用box based component
  - reflexbox is a ergonomic, responsive React layout and grid system. The original Box component™ since 2015
- 是否需要提取使用css-in-js创建的样式到单独的文件
  - 有利有弊
  - https://github.com/emotion-js/emotion/blob/master/docs/extract-static.mdx
    - extractStatic is not recommended because it breaks composition and other powerful patterns from libraries like facepaint.
    - https://github.com/emotion-js/emotion/issues/858
  - https://github.com/styled-components/styled-components/issues/1018
    - There's SSR which sends only critical CSS, instead of all static CSS, for the entire page. You don't even need to do SSR, but can use snapshotting (react-snapshot) or generate a static page (gatsby, et al), which basically saves a SSR result to a html.
    - Static extraction doesn't generate dynamic CSS, which means your page will either appear broken until the JS executes, or you'll need to defer until the JS is loaded
    - Caching doesn't actually buy you an advantage, because the JS bundles will likely always change in tandem with the extracted CSS
  - https://github.com/callstack/linaria/issues/465
    - The reason this doesn't work is because styled system interpolates both the declaration name and the value. With linaria, you should only interpolate the value.
  - https://github.com/callstack/linaria/issues/409
    - No support for conditional CSS using the styled tag is the biggest hurdle for us moving to linaria from styled-components
  - use styled-system with linaria
    - not possible
    - https://github.com/styled-system/styled-system/pull/868
    - In terms of dynamic style from props, Linaria only accepts function interpolations on the value side of CSS property, and it must return the correct value. Neither accept style objects nor dynamic CSS string.

## css-in-js-spec

- Interoperable Style Transfer Format
  - https://github.com/cssinjs/istf-spec

## pieces

- https://calendar.perfplanet.com/2019/the-unseen-performance-costs-of-css-in-js-in-react-apps/
  - Don’t over-compose styled components
  - Prefer “static” components
  - Avoid unneeded React re-renders
  - Investigate whether a zero-runtime CSS-in-JS library like linaria can work
- https://github.com/necolas/react-native-web/tree/master/packages/benchmarks
- https://dev.to/wilsmex/css-in-2020-a-practical-guide-2p6g
- https://sebastienlorber.com/atomic-css-in-js
- https://areknawo.com/introducing-prototope-utility-first-css-in-js-library/
- https://www.infoq.com/news/2020/04/facebook-cssinjs-react-conf-2019/
  - stylex
  - new Facebook website: React/GraphQL/Relay 
- https://www.infoq.com/news/2020/01/css-cssinjs-performance-cost/
- https://dev.to/macsikora/css-in-js-did-we-do-something-wrong-l1j
- https://spectrum.chat/styled-components/general/styled-components-vs-emotion~47206c1b-a688-424e-9e96-6f265993587e
- https://itnext.io/css-in-js-vs-pre-post-processors-in-2019-8b1e20c066ed

## theme-specification

- https://github.com/system-ui/theme-specification
- use case:styled-system, theme-ui, rebass, xstyled, onno
- 对样式主题的需求
  - If you’ve ever worked on a large application that has been worked on by many different people over time, you know that consistency can be hard to maintain. The amount of different colors, spacing, font-sizes and media queries can easily get out of control. 
  - Having a style guide combats that by providing a set of constraints that your application’s UI should adhere to, helping to maintain a consistent look and feel.
  - Having a style guide also leads to a more enjoyable developer experience. There’s less time spent worrying about the precision values, such as a specific padding value
  - common style such as UI Theme Spec makes themes portable between libraries
- 样式的写法
  - 写法上采用类似内联样式的style对象更方便查看，但采用类似className性能更高
  - css属性名编写时的代码提示，可在样式库解决，也可在ide解决，也可借助typescript
    - 只需要代码提示，没必要用typestyle库
    - csstype provides autocompletion and type checking for CSS properties and values
    - styled-system让组件上的css属性有提示且有限制，但要使用styled组件写法
    - typestyle书写样式对象返回className，和emotion类似，但写样式有提示，样式对象要作为参数传入style()，类似于emotion的css()
    - typestyle基于free-style，两者都存在一个问题，嵌套时内层逗号分隔的选择器只在最后一个选择器元素处生效
    - https://github.com/blakeembrey/free-style/issues/69
- ref
  - System UI is an open source organization that houses a Theme Specification for creating interoperable UI components.
  - https://mitchgavan.com/styleguide-driven-development/
  - https://github.com/primer/components/blob/master/src/theme.js

  
