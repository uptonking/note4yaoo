---
title: lib-styled-components-dev
tags: [styled-components]
created: '2020-08-08T08:07:31.739Z'
modified: '2020-08-18T06:13:52.606Z'
---

# lib-styled-components-dev

## faq-not-yet

- styled装饰过的components如何不通过 `Comp.defaultProps` 的方式设置默认值？
  - 如何采用类似FunctionComponent的参数默认值的方式设置
- 如何只添加样式到组件最外层而不引入新的div标签？
  - `styled（'div'）''` 替换成类似 `styled(()=><></>)''` 的形式

## styled-system

- ### [Unable to extend styled-system components with styled-components](https://spectrum.chat/styled-system/general/unable-to-extend-styled-system-components-with-styled-components-as-in-the-docs~6d82a0b9-a453-4202-b4bb-a1b2f4d2dbfc)

``` typescript
const Box = styled('div')(color)
// 首先要明确，不能直接在styled中写theme中的value，需要使用@styled-system/css
// 如果在这里styled中写的color是 silver(未在theme中定义)，那最终就会显示silver色，因为继承组件的样式会生成在后面，最终覆盖原组件定义的颜色
const ExtendedBox = styled(Box)({ color: 'themeColour' })

<ExtendedBox color='anotherThemeColour' />
```

- This won’t work as you are expecting. 
- Each argument to the function to create the styled component is evaluated on render as a ruleset. 
- So objects get evaluated out, functions get run. 
- When one component extends another part of what happens is those rulesets get combined via concatenation.
- There will be 2 rules in this set, 1 from box for the color function and 1 from ExtendedBox for the styling object. These get evaluated in that order.
- The color function will evaluate and turn `anotherThemeColour` into whatever string is in the theme and attach that css styling rule. 
- The next rule is then evaluated, which is an object, so no transformation is applied, styled-components attaches verbatim `themeColour` as another color rule.
- This produces something like:

``` CSS
/* the hsl here is interpolated from 'themeColour' */
.de6dh: {
  color: 'hsl(0, 100%, 55%)';
  color: 'anotherThemeColour';
}
```

- CSS specificity being what it is, the rule at the 'bottom' of the block 'wins', however, in this case, 'anotherThemeColour' is junk and invalidates the rule, so this element gets a red colour. 
- If you had supplied 'tomato', 'rebeccapurple', '#ff0', 'hsl(0, 10%, 100%)', or any other genuine css value to `ExtendedBox` then your inline declaration would have 'lost' the specificity war.
- 解决方法1

``` JS
const ExtendedBox = styled(Box)({})
ExtendedBox.defaultProps = {
  color: 'themeColour'
}
```

- This passes the prop to the base component, so color will know about it. 
- 解决方法2

``` js
import { css } from '@styled-system/css
const ExtendedBox = styled(Box)(
  css({
    color: 'themeColour'
  })
)
```

- This function returns another function which, when evaluated, will attempt to convert values to their theme counterparts.

- ### What still I am missing is what are the advantage of accessing theme file values through styled system `css` or `themeGet` functions, compared to import the theme file and access those values directly in style components instead, like: `color: ${theme.colors.primary}`
- Evaluating from theme using `themeGet` or `css` is effectively lazy, it happens only when it needs to. Contrast this with directly importing from `theme.js` which is static.
- If you know your theme never ever changes for the lifetime of your application (which is true in many cases) then you're ok to statically include the theme (which may have some advantages in terms of less calculations, but I doubt there is any significant difference here).
- If you think your theme might change, or might change in a later iteration of your application, then use the convenience methods to pull from `context.theme` and perform lazy evaluation.
- It isn't super tricky to change from direct imports to using the convenience methods, but if your app grows large that will be a very annoying task to update (which can probably be automated via a codemod). 
- So you could live 'fast and loose' and go with direct imports to start, but, its not much work to import the functions and use them in place, so its probably worth going that route to start with, even if your theme is static.
- tldr: use the convenience methods as 'best practise' and make it a habit.

- ### [Improve performances before styled-system v5](https://github.com/styled-system/styled-system/pull/470)
  - [pr: mprove performances](https://github.com/styled-system/styled-system/pull/479)
    - not merged

- ### [possible to use styled-system with zero-runtime CSS in JS libraries?](https://github.com/styled-system/styled-system/issues/510)
  - help wanted

## linaria

- ### [linaria: Styled System support](https://github.com/callstack/linaria/issues/465)
  - Supporting this in linaria would be tricky.
    - It would end up with support for runtime assigned styles since we cannot statically generate the output for each possible value of props.
  - I think something effectively similar to styled-system could be built on linaria, 
    - but styled-system (whether using styled-components or emotion) depends on passing the `theme` via React Context, so that the style-prop functions have access to it. 
    - To do this in linaria would require fundamentally retooling the way the style-prop functions are generated AFAIK
  - , the theme system would require context like you said, but supporting the responsive props themeless seems theoretically possible no?

- ### [Conditional CSS with styled tag](https://github.com/callstack/linaria/issues/409k)
  - Is it possible to do something like the following?
  - `${props => props.dark && ({ color: 'black', })}`
  - This is currently not possible due to the way CSS is extracted at build time, the value of active is unknown at that time.
