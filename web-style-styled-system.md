---
title: web-style-styled-system
tags: [css-in-js, design-system, style]
created: '2019-12-17T03:13:59.953Z'
modified: '2021-01-01T20:18:56.579Z'
---

# web-style-styled-system

## summary

- styled-system解决的问题
  - 组件样式属性值webweb的一致性，本质通过重用预定义的工具函数
  - 解决组件临时添加样式的问题，需要新增props
    - https://medium.com/@karthikbalaji99/styled-system-for-better-styled-components-a87a5eb2059c
  - 使用theme时需要写很长的解析表达式 `props => props.theme.colors.primary`
    - `@styled-system/css` 的css()方法，传入的实参对象属性值可直接写theme对象中的值
- tips
  - 可以逐步采用s-s，比如只用layout
  - s-s由modulz研发工程师证实存在一定的性能问题，对于性能要求高的场景慎用
  - s-s的优势与参考：api设计思路，type定义，theme-spec
- s-s特点
  - first-class theme, with scalar values instead of remembering numbers
    - interoperable theme
  - consistent prop names and values, thin/small
  - Component Hierarchy and Extensibility
  - Allow for setting single properties, such as width or font-size, responsively without needing to handle media queries
  - Write less CSS
- s-s缺点
  - this approach basically replaces vanilla CSS with tons of props
  - styles are abstracted away, sometimes it takes time to understand
  - one of the biggest appeals of styled-components is how easy & straightforward it makes "just writing CSS", without the need for a lot of abstraction to keep things maintainable.
  - ref
    - https://spectrum.chat/styled-components/general/using-styled-system-vs-pure-styled-components~b9afb6f3-a675-4f97-bc78-66411292fab1
- Three Tenets of Styled System
  - Style consistently with a global theme
      - Consistency is the bedrock of any constraint-based design.A hard-coded font size or color value in a code review is easy to smell, and developers naturally opt-in to keeping values stored in a globally shared theme object.
  - Respond to changing requirements quickly
      - Developers are frequently working in short sprint cycles to finish tasks that likely didn't account for styling consistency. Over time this leads to technical debt and parts of the CSS code base quickly become obsolete pieces of legacy code.
      - By putting some of the styling control into a component's props, developers can **keep these one-off changes isolated to the parts of the codebase** where they are used. And later modify it to s-s.
  - Create mobile-first responsive layouts with ease
      - Styled System includes an opinionated syntax for how to style things responsively that's meant to help shape the way people think about designing for mobile devices. 
      - Instead of burying conditionals for a single CSS property across multiple media query blocks, Styled System uses an array syntax to force developers into thinking how a singular dimension, such as font size or width, should change from one breakpoint to the next. 
- Writing those mini functions like `${props => props.bg ? props.bg: 'orange' }` can be very annoying when you see lots of repeated code with exactly same pattern. 
- To avoid this we could create some functions that will do the exact same thing which can be reused and is easy to write. Styled system does exactly that.
- how to use 
  - You define your design system as a theme object and then provide it using the ThemeProvider component.
  - Style functions will try to find a value from the theme object, these could be deeply nested values, and fallback to a hard-coded value if they are unable to.
  - Each key in the theme object corresponds to a certain set of CSS properties.
- changelog
  - 5.0.0-201906-completely refactored in version 5
      - New system API for custom style props
      - https://styled-system.com/guides/migrating/
      - https://github.com/styled-system/styled-system/blob/master/CHANGELOG.md
  - 4.0.0-201902-rewritten core for less code duplication
  - 3.0.0-201806-performance rewrite
- use case
  - style props vs variants
      - The built-in buttonStyle function is really meant to be an all-in-one approach that would include size, color, and anything else. For what you're going for, I'd suggest possibly looking into using a custom variant for size prop.
      - The other approach for things like this that I, personally prefer, is to create a base Button component that uses the lower-level parts of styled-system, e.g. space, color, fontSize, and then wrap that in a more modulz-specific component that takes props like size and variant and converts those into the lower level props – with an approach like this, more of the logic stays in React components and might be a little bit more readable IMO
      - You get to define Modulz's Button api the way you want it, and the logic to remap this to the lower level parts of styled-system remain within the boundaries of that component. 
- limitations
  - s-c的as prop和styled-system的color, width等一起出现时，as会失效
  - s-c编写的svg属性可能会失效

## faq

- s-s迁移到ts的开发计划
  - https://github.com/styled-system/styled-system/issues/464
- variant的使用
  - 如何实现支持type, size, color3个variant的button
      - https://spectrum.chat/styled-system/general/dealing-with-multiple-variants~b808556e-80e9-4c8e-be3f-dde9ae186c44
  - variant不支持在模板字符串中使用
      - https://spectrum.chat/styled-system/general/is-it-possible-to-use-multiple-arrays-for-fontsizes-for-media-queries~883222fa-1148-4260-98f7-ed0cf872bf17
- breakpoint的默认值问题
  - 默认使用数组的第一个值，或对象中default属性的值
  - https://spectrum.chat/styled-system/general/understanding-breakpoint-aliases~42db51e3-2483-42f0-bb1b-bc329c460f04
- 组件api的设计-灵活vs限制
  - s-s v5的style categories会over expose style props
  - the API is meant to give developers the flexibility to do things like that when they're asked to do them. The same thing could be done with the css prop, an inline style attribute, a global CSS override, etc.
  - https://spectrum.chat/styled-system/general/permissive-vs-restrive-component-apis~475715ea-a538-41be-8366-779226339650
  - https://spectrum.chat/styled-system/general/strict-component-api-with-styled-system~a6582471-99d2-4d2c-94d2-2a05de61d4c4
  - https://github.com/styled-system/styled-system/issues/562
- Duplicated className style props
  - https://github.com/styled-system/styled-system/issues/546
- How do you style nested elements with styled-system
  - try to avoid child selectors in CSS as much as possible – instead create styled components for each element that you are styling
  - https://spectrum.chat/styled-system/general/how-do-you-style-nested-elements-with-styled-system~3e7030ce-8b80-4eea-92b6-8c554657895b
- 如何结合sketch对design编写组件
  - Sketch is a great tool but it's not optimised for Design Systems. Most designs in Sketch will lack enough information needed in a Design System, and of course, the output is always static images, which means it's hard to interact with the design and all its possible states.
  - https://spectrum.chat/styled-system/general/working-with-designers-styled-system~9ff97168-ac85-483a-8cf7-3d694799ca
  - 还可以考虑结合figma
- 样式相关的defaultProps是写在单独的Comp.defaultProps=代，还是写在styled模板字符串
  - react支持defaultProps，在hooks成熟后可能变化
  - 使用ts时，defaultProps无法进行类型检查
      - ts推荐**在函数参数中直接指定props默认值**
          - https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#support-for-defaultprops-in-jsx
          - ts3.0添加了LibraryManagedAttributes类型类辅助解决问题
      - In functional components only, we can set default values with ES6 Destructuring assignment syntax
      - defaultProps   
          - it gives us a unified way of setting default values to props in both class components and functional components. 
          - syntax is simple and straightforward
          - problem: it'll slow down `createElement()` beacause of check
      - es6 destructuring parameter
          - native syntax in ES6 with smaller bundle size
          - setting default values is different for FC and ClassComp
          - 有时候获取部分参数名会较难，如获取restProps中的某个参数
          - The object we created as a default value will be recreated in every function call, so if we pass it down to a child component, the component will get a new reference every time and will cause a render on each parent render.
              - To fix that problem we will need to create the default value globally as a const so the reference won’t change
          - with hooks, react team seems to deprecating defaultProps
      - because type checker cannot infer types from generic class extentions definition to its static properties.
      - you can set anything to your static defaultProps
      - We can fix this by extracting color and type type properties to separate type and then use type intersection by mapping our defaults to be optional via `Partial` mapped type helper from TS standard library
      - Last thing what I tend to do, is to extract defaultProps and initialState(if state is used) to separate constants, which will give us also another benefit → obtaining type definition from implementation, which introduces less boilerplate
      - 方法1：Non-null assertion operator
      - 方法2：Component type casting via as
      - 方法3：High order function for defining defaultProps
      - 方法4：Props getter function
  - ref
      - https://spectrum.chat/styled-system/general/default-values-default-props-css-rules~4e397705-763d-4cef-8ed2-3d8da481b7c0
      - https://medium.com/@martin_hotell/react-typescript-and-defaultprops-dilemma-ca7f81c661c7
      - https://github.com/Microsoft/TypeScript/issues/23812
      - https://medium.com/@matanbobi/react-defaultprops-is-dying-whos-the-contender-443c19d9e7f1       
- style object中也可以使用pseudo
  - 不work

``` js
  {
    "&::before": {
      content: ""
    }
  }
```

  - 要改成 `content: JSON.stringify("")` 或  content: `""` 或 '""'
- Styling: Object Styles vs Strng Styles
  - 涉及到pseudo-class/elements或选择器时，字符串形式更方便，也更易读
  - JS objects are based on types within the language itself, making transformations easier and avoids having to parse CSS syntax – it's similar to how JSX represents function calls vs using template literals and parsing HTML out with other approaches
  - https://spectrum.chat/styled-system/general/styling-object-styles-string-styles~b58a5b23-6981-4944-87ed-48d8d27601f8
- Box组件
  - How many times do you actually use Box in your design systems?
  - I'm mostly using Box in other components and exposing whatever props I want rather than extending the entire API. 
  - So far we're just extending Box for building the rest of our design system components like Flex, layout, etc., but not so much for situations like NotificationBar.
  - 可以先只用所需的style prop function，然后根据新组建逐渐增加
  - started out with the default one but in the end put everything in it, I use these pretty much everywhere in my layout
  - https://spectrum.chat/styled-system/general/whats-in-your-box~6f41c990-f49f-4063-ba64-fcea702014f9
