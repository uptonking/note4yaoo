---
title: web-style-css-in-js-lib-glaze-calico
tags: [calico, css-in-js, glaze, style]
created: '2020-10-29T10:46:45.637Z'
modified: '2021-01-01T20:06:24.571Z'
---

# web-style-css-in-js-lib-glaze-calico

# guide

- glaze pros
  - 支持使用约束限制的值
  - 能编译出atomic css

- glaze cons
  - 设置样式通过类似style属性的sx
  - 部分样式是动态生成的，这部分不支持静态提取
    - 支持treat file形式的静态样式，
    - 也支持在sx方法中书写带theme约束的样式值，但这部分样式会动态生成
    - To enable client-side injection of styles, wrap the entry point of your application with `StyleInjectorProvider`
    - 使用glaze能利用design tokens好处，却无法提取静态css了，glaze本身的设计原则就是结合动态css的灵活性和静态css的高性能
  - 要使用glaze定制的ThemeProvider传入theme
    - 不能使用react-treat的TreatProvider传入theme

- calico pros
  - 支持直接使用约束限制的值，书写一次性样式也方便
  - 支持预先静态提取出所有css，使用atomic css的形式
  - 直接基于treat和react-treat，所有主题的样式均可静态提取
    - theming不依赖css vars

- calico cons
  - 依赖react-polymorphic-box，clsx，fp-ts
  - 只支持react组件
  - 必须使用提供的Box组件创建，这里实现了属性别名的解析，
    - 设置样式使用类似style属性的styles属性
    - Box组件基于react-polymorphic-box的Box，封装层次有点多
  - 以原子类的形式，预先静态提取所有样式时，经常生成的样式名超级多，
    - 适合大规模应用，不适合小应用
  - 实现层没有考虑使用css vars

- **calico生成样式的原理解析**

``` JS
// 组件源码
import { TreatProvider, useStyles } from 'react-treat';
import { theme } from './theme1.treat';
import * as styles from './MyTreatTitle.treat';
import { Box } from './calico';

export const CalicoBox = (props) => (
  <Box
      styles={{
        color: 'red5',
        margin: [1, 0],
      }}
    >
        {props.children}
    </Box>
);

<TreatProvider theme={theme}>
  <CalicoBox>calico box 组件</CalicoBox>
</TreatProvider>

// 打包后
var CalicoBox = function CalicoBox(props) {
  return /*#__PURE__*/ react__WEBPACK_IMPORTED_MODULE_0___default.a.createElement(
    _calico__WEBPACK_IMPORTED_MODULE_4__["Box"], {
      styles: {
        color: 'red5',
        margin: [1, 0]
      }
    }, props.children);
};
```

# glaze-docs

- This project was born to combine the best of its predecessors into a single solution:
- Near-zero runtime, made possible by treat
  - Theming support with legacy browsers in mind
  - Static style extraction while retaining type safety
- Utility-first CSS, as implemented by Tailwind CSS
  - Fully static, but customizable upfront
  - Embraces reusability with no duplicated rules
- Constraint-based layouts, popularized by Theme UI
  - Highly dynamic, thankfully to Emotion
  - One-off styles can be defined naturally

- An element's appearance can be customized through objects. 
  - Similarly to `style` attributes in React, properties are camelCased. 
  - Aliases and shorthands may also be used (and even defined)

- Firstly, define a theme, preferably by overriding the default tokens
- Keeping the runtime as small as possible, 
  - only a few tokens (breakpoints, shorthands and aliases) are embedded into production JS bundles. 
  - Other values can only be accessed exclusively for styling, as shown in usage.
- Apply the theme through `<ThemeProvider>` , by wrapping the component tree
- A single-purpose CSS class needs to be generated for each design token at build time. 
- Afterwards, selector-based CSS rules may be created with globalStyle() in *.treat.{js|ts} files.  
  - They have to be applied as a side effect, e.g. from a top-level layout component

- How it works
  - At first,                          `sx` tries mapping themed values to statically generated CSS class names. 
    - Unresolved rules are injected at runtime and detached when no components reference them anymore.
  - Transform each alias to its corresponding CSS property name or custom shorthand.
  - Resolve values from a scale if available.

# pieces

- I’m planning on migration glaze to use otion instead of treat as the underlying CSS-in-JS library 
  - and thus, critical CSS will by inlined to documents. 
  - The change comes at a runtime cost of ~2kB, but unlocks way more possibilities.
  - The API is very similar and was heavily influenced by glamor. 
    - Scoped CSS rules work out of the box, including support for pseudos, @​media, @​supports and even custom selectors like "& > *". 
    - Everything is decomposed to atomic rules and the specificities are managed automatically.
  - https://twitter.com/kripod97/status/1271881199615688705

- Recently, I've been working on a CSS-in-JS library built upon treat
  - https://twitter.com/kripod97/status/1241524939473248256
  - It works by picking atomic CSS classes on the fly, generated from a theme. 
  - Inline styles are applied as a fallback, when a static `className` is not available.
  - The theme interface was carefully crafted with extensibility in mind. Inspired by Theme UI and styling tokens from TailwindCSS.
  - The value of a given property is resolved from a scale. Custom shorthands (e.g. paddingX) and aliases (e.g. px, bg) can also be specified.
  - Firstly, aliases are mapped to their corresponding CSS property names or custom shorthands. 
  - After that, each item of a shorthand (or the CSS property itself) gets assigned to a value of the given scale. 
  - If not found, an inline style gets applied.
  - the main benefit is that the runtime is lightweight. The philosophy is similar to TailwindCSS, but one-off styles are inlined automatically.

- I just stumbled upon otion today. I really like the API and writing type-safe styles with auto completion is a big win 
  - https://twitter.com/kripod97/status/1266401730297806850
  - I’m planning to provide a more comprehensive theming approach with an other project glaze (to be built upon otion)
  - The `sx` prop will possibly be reverted, as it causes too many edge cases.
  - Static extraction is brought to glaze by the underlying CSS-in-JS library called treat. 
  - On the long term, it will be replaced with otion. 
  - With atomic CSS, the overhead of inlined critical styled is manageable. Especially with HTTP 1, the overall cost is less with inlining.
- The otion project will provide the foundation to build glaze upon. 
  - Eventually, it will replace treat for static style management.

- Based upon my recent(202004) experiences with glaze, I'm building a lightweight CSS-in-JS runtime as a tiny wrapper around Stylis v4. 
  - It will encourage the use of a `css` prop, but a separate package for a `styled` API could also be provided later.
- Today I've been experimenting with CSS injection techniques. 
  - https://twitter.com/kripod97/status/1254101422511185922
  - Interestingly, body-embedded `<style>` tags (as used by @emotioncss) perform much worse than a singleton `<style>` in the `<head>`.
  - I tested this on a tree of 70000 elements. It'd be nice to see detailed benchmarks
  - So, as a quick visual comparison, here's how @emotioncss would load styled elements 
    - It's non-blocking, but takes a long time to process.
  - As reference, a `<style>` singleton in `<head>` would load as fast as shown with glaze
    - It's blocking for ~5 seconds due to the large amount of CSS classes to process, but renders the entire tree after that.
  - This is why emotion uses a single style `tag` in the `head` for SSR. I’d also be curious to know where the divergence in perf starts to show in your ex. 10k elements, 20k? I’m not surprised a list of 70k element with 70k style tags is slow

- The upcoming version of glaze will feature near-zero config setup for a better onboarding experience.
  - https://twitter.com/kripod97/status/1253473511462645761
  - Theme UI could work without a `@types/theme-ui` package by suggesting the JSX pragma approach, as it results in an import from 'theme-ui' itself, which may have global types embedded `import { jsx } from 'theme-ui'`
  - I prefer **using a single `<style>` tag for dynamic injection through the CSSOM**, so the amount of applicable rules is limited by browsers (65536 slots for most).
    - the runtime with an inlined `<style>` is limited (by most modern browsers) to use at most 65536 rules at once.
    - While Styled Components warns about too many injected rules and slows down the page eventually by leaving leftovers, glaze aims to take a manageable cost & allow injecting thousands of ever-changing rules (e.g. tracking mouse pos). The theory must be backed by benchmarks, though.
  - During glaze SSR: If a static treat className can't be resolved for an `sx` entry, then the style is inlined
  - The core concept of glaze is modularity. 
    - **Use static or runtime styling as desired, balancing between overhead and flexibility.**
    - Each approach is opt-in, and the unused code gets tree shaken most of the time.
  - Static and dynamic styling are independent from each other. 
    - If no treat-generated static className can be found, then the styling rule gets injected dynamically as a fallback
  - So, static and dynamic styles can be used alongside each other, without conflicts.
  - glaze detaches styles which are not used by any component anymore, through reference counting and `useEffect`. 
  - `sx` is a lightweight runtime function returned by `useStyling()`. 
    - It acts like a lookup table, pairing object entries to their corresponding static (treat-generated) classNames. 
    - If that cannot be found for a rule, then a dynamic injection is made. SSR is encouraged.

- The `useStyling` hook of glaze works as shown. 
  - Firstly, it maps each alias to its corresponding property/shorthand.
  - After that, the resulting CSS properties are looked up from `staticClassNames`. 
  - If a rule can't be found, use dynamic injection as fallback

- Today I encountered an interesting gotcha with atomic CSS. 
  - Source declaration order matters, especially when injecting styles dynamically. 
  - When using e.g. `border` and `borderColor` simultaneously, the latter should take precedence.
  - Solved with lookups
  - One of the biggest gripes(抱怨) with styled-system. I’m definitely got my eyes on glaze now
  - Yes, source declaration order matters, it's called the *Cascade* 
  - It has to do with the dynamic injection of Atomic CSS, though. 
    - For example, if a rule for `margin-left` is injected before a rule for `margin`, then the left margin wouldn’t take effect with a className like "m-0 ml-4". Or in libraries like Theme UI, sx={{ m: 0, ml: 4 }}
    - It has nothing to do with Atomic CSS but how people end up creating stylesheets.
    - A reset/rule declaration must come first for the same reason as this would not work either

- CSS-in-JS library newsflash: #glaze now has proper server-side rendering with CSSOM-based cheap rehydration on the client side!
  - Contrary to other libs, dynamic style injection is entirely optional, as inspired by treat project.
  - Do you mind explaining what is "dynamic style injection" exactly?
  - When a style is not available as a static class, it has to be generated on the fly. 
    - For simple rules, this can be achieved with inline styles. 
    - CSS-in-JS libraries like glaze do it through the CSS Object Model for better performance and flexibility, e.g. supporting media queries.
  - In development, a warning is fired when dynamic injection is required to apply a style, but the component tree is not wrapped inside a `<StyleInjectorProvider>`
- A quick demo about dynamic styles in glaze 
  - When a CSS rule is unavailable, a class gets generated in `<head>`. 
  - For example, the black boxes' background below is styled at runtime. 
  - Even the generated rules are atomic and reused among elements. 
  - Styles detach when not used anymore.
- Styles which are not statically available get appended to the document head. 
  - Reusable atomic classes are now here as an alternative of inline styles.
  - New possibilities also arise, e.g. inline-defined pseudo classes and media queries. All of that hoisted to the` <head>`.

- Experimenting with a new ThemeProvider implementation for glaze
  - Trying to count references of hashed classNames for dynamically generated styles during runtime, inspired by std::shared_ptr. 
  - This will allow inline-defined styles to be handled as if each had an own className.

- The secret to better composability is building side effect-free UI components i.e. no margin, width, position other than static or relative, translations etc. set on the component's root.
  - We should ban margin from our components. No more margin, anywhere in our apps.
  - every design system built with Modulz will by default have some of these decisions built in (ie: no margin)
  - Also avoid giving position to the component.
  - So spacer components would have their own margin instead of using competent margins right?
  - Yeah of course, until flex-gap is fully supported (it's coming!) we'll still have to use margin as an implementation detail for the ponyfill.
  - No margin, no absolute/fixed position. Make wrapper components for grids, lists, and other kind of "glue" spacing and layout.
