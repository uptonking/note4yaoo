---
title: web-style-css-in-js-lib-linaria
tags: [css-in-js, linaria, style]
created: 2020-10-27T06:49:35.370Z
modified: 2021-01-01T20:06:36.094Z
---

# web-style-css-in-js-lib-linaria

# guide

- linaria pros
  - 基于css vars实现，现代浏览器的选择
  - 支持styled和css两种方式

- linaria cons
  - css支持所有，但框架集成只支持react
  - 不直接支持动态样式
  - styled自身就是一个wrapper，引入了额外的计算
    - styled本身是一个代表高阶组件的方法，会导致每个styled组件都会多一层额外计算
    - styled的css字符串TTLs就算不使用props中的theme或其他变量属性，也会有这层额外计算
    - 若要实现theme切换，需要自己再加一层高阶组件来传入props.theme或context.value.theme，会增加额外计算
  - 样式书写只支持css字符串样式，不直接支持object style syntax
    - It might be tricky to introduce this syntax to linaria since we are strongly basing on TaggedTemplateExpressions
    - 代码实现紧密依赖css字符串字面量的处理逻辑，实现style object难度较大
  - No IE11 support when using dynamic styles in components with styled, since it uses CSS custom properties
  - Dynamic styles are not supported with css tag. 
  - Modules used in the CSS rules cannot have side-effects.
    - css `color: ${colors.text};`.
    - We recommend to move helpers and shared configuration to files without any side-effects.

- who is using #linaria-css-in-js
  - [Airbnb's Trip to Linaria_202206](https://medium.com/airbnb-engineering/airbnbs-trip-to-linaria-dc169230bd12)

- tips
  - 尽量在`style`属性中使用属性名和变量值，而不是`style={{'--var-prop': value}}`，减少抽象层次更便于理解，减少修改入口便于定位
  - 使用css vars实现theming，目前的主流方案，但不用来做状态管理

- 切换样式的实践
  - 样式定义在 w3c-design-tokens-theme1.json 文件，可通过figma生成
  - 开发使用theme1-vars.js，切换theme使用 theme1/2.css
  - 通过cobalt工具生成，因为要转换单位或别名
    - theme1-vars.js  js对象映射到css变量名  {font:{family:{size:{f3}}}}: 'var(--font-family-size-f3)',
    - theme1.js        扁平的js-kv  'font.family.size.f3': '16px',
    - theme1.css       扁平化的css变量  --font-family-size-f3: 16px;

- compiled-css-in-js会编译出atomic css
  - linaria也支持

- **linaria生成样式的原理解析**
- `styled`纯静态样式

```JS
// 组件源码
const MyLinariaTitle = styled.h1 `
    color: teal;
`;
<MyLinariaTitle>Hello Linaria 202010</MyLinariaTitle>

// bundle后
var MyLinariaTitle =
  /*#__PURE__*/
  // 打包后也会存在执行styled函数计算样式的runtime，虽然runtime很小
  // 注意这里会返回react组件，这里包含创建组件的过程，后面还有一次创建组件的过程
  Object(linaria_react__WEBPACK_IMPORTED_MODULE_1__["styled"])("h1")({
    name: "MyLinariaTitle",
    class: "mm0as6w"
  });

react__WEBPACK_IMPORTED_MODULE_2___default.a.createElement(MyLinariaTitle, null, "Hello Linaria 202010");
```

- `css()`工具方法编写静态样式不存在runtime，比styled方式少了一层react组件

```JS
// 组件源码
const myH2class = css `
    color: lightcoral;
`;

<h2 className={myH2class}>h2标题</h2>

// bundle后
var myH2class = "m13mnax5";
react__WEBPACK_IMPORTED_MODULE_2___default.a.createElement("h2", {
  className: myH2class
}, "h2\u6807\u9898");
```

- resources
  - [Use CSS Variables instead of React Context](https://epicreact.dev/css-variables/)
# issues
- [webpack build silently fails after Linaria update](https://github.com/callstack/linaria/issues/1135)
  - Short answer: Webpack + linaria plugin with custom babel options

- [Build linaria is very slow using webpack5](https://github.com/callstack/linaria/issues/1199)

- [Using the "css" tag in runtime is not supported. Make sure you have set up the Babel plugin correctly.](https://github.com/callstack/linaria/issues/617)
  - If you use ts-jest for jest test, you should mock linaria in setupTest.ts
  - Digging into another issue, I found that linaria will trigger @linaria/babel-preset/lib/transform-stages/helpers/loadLinariaOptions.js's loadLinariaOptions will multiple times on the same files.
# examples
- https://github.com/remirror/remirror
  - https://github.com/user-focus/remirror-extension-note

- https://github.com/adazzle/react-data-grid
  - https://adazzle.github.io/react-data-grid/
  - Feature-rich and customizable data grid React component

- https://github.com/inokawa/react-animatable
  - composable animation library for React, built on Web Animations API and React hook.

- https://github.com/essential-randomness/boba-editor-next
  - There is no widely-available visual editor that supports the MDX file format.

- https://github.com/Kiikurage/drawing
  - Simple drawing app

- more-linaria-comp
  - https://github.com/paritytech/table-renderer
  - https://github.com/id-ui/react-tree

## ui-using-linaria

- https://github.com/locol23/design-system-boilerplate
  - design-system-boilerplate

- 
- more-linaria-ui
  - https://github.com/cloudshadow/cloudshadow-core-ui
  - https://github.com/webzard-io/dovetail
  - https://github.com/tuanemuy/unflexible-ui-core
# docs
- ## [Why use Linaria](https://github.com/callstack/linaria/blob/master/docs/BENEFITS.md)
- Advantages over regular CSS
  1. Selectors are scoped
  2. Styles are in same file as the component
  3. Refactor with confidence: 可放心修改和删除样式而不影响其他组件
  4. No pre-processor needed
  5. Automatic unused styles removal
  6. Automatic vendor prefixing
  7. Declarative dynamic styling with React
- Advantages over CSS preprocessors
  1. No new syntax to learn
  2. Same advantages as regular CSS
- Advantages over inline styles
  1. Full power of CSS
  2. Performance: class names perform much faster than inline styles.
- Advantages over other CSS-in-JS solutions
  1. CSS is downloaded and parsed separately from JS
  2. No extra parsing needed for CSS
  3. No style duplication on SSR
  4. Catch errors early due to build-time evaluation
  5. Familiar CSS syntax
  6. Works without JavaScript

- ## [How it works](https://github.com/callstack/linaria/blob/master/docs/HOW_IT_WORKS.md)
- The Babel plugin will look for css and styled tags in your code, extract the CSS out and return it in the file's metadata. It will also generate unique class names based on the hash of the filename
- When using the styled tag, dynamic interpolations will be replaced with CSS custom properties.
- Plugins for bundlers such as webpack and Rollup use the Babel plugin internally and write the CSS text along with the sourcemap to a CSS file. 
- The CSS file is then picked up and processed by the bundler (e.g. css-loader in case of webpack) to generate the final CSS.

- ## [Theming](https://github.com/callstack/linaria/blob/master/docs/THEMING.md)
- CSS custom properties(CSS variables)
  - The basic concept is that we add a className to represent the theme to our root element, 
  - and use different values for our CSS variables based on the theme

```typescript
// Create class names for different themes
const a = css`
  --color-primary: #6200ee;
  --color-accent: #03dac4;
`;

const b = css`
  --color-primary: #03a9f4;
  --color-accent: #e91e63;
`;

// Apply a theme to the root element
<Container className={a} />;

// Now, we can use these variables in any of the child elements:
const Button = styled.button`
  background-color: var(--color-accent);
`;
```

- CSS child selectors with themeName
  - add a class name representing the theme (e.g. - theme-dark) in the root element
  - take advantage of CSS child selectors to theme the elements based on this parent class name.
  - This approach works in all browsers, and is the best approach

```typescript
<Container className="theme-dark" />

const Header = styled.h1`
  text-transform: uppercase;

  .theme-dark & {
    color: white;
  }

  .theme-light & {
    color: black;
  }
`;

// Put your colors in an object grouped by the theme names
const colors = {
  light: {
    text: 'black',
  },
  dark: {
    text: 'white',
  },
};
// Create a small helper function to loop over the themes and create CSS rule sets
const theming = cb =>
  Object.keys(colors).reduce((acc, name) => Object.assign(acc, {
    [ `.theme-${name} &` ]: cb(colors[name]),
  }), {});
// Use the helper in your styles
const Header = styled.h1`
  text-transform: uppercase;

  ${theming(c => ({
    color: c.text,
  }))};
`;
```

- React Context
  - use React Context to pass down colors, and then use function interpolations with the styled tag to use the colors in your component. 
  - You could use something like @callstack/react-theme-provider or write your own HOC.
  - Note that this approach also uses CSS custom properties under the hood since function interpolations compile down to CSS custom properties.

```typescript
const Button = withTheme(styled.button`
  background-color: ${props => props.theme.accent};
`);
```

- ## [Dynamic styling](https://github.com/callstack/linaria/blob/master/docs/DYNAMIC_STYLES.md)
- Sometimes we have some styles based on component's props or state, or dynamic in some way. 
  - If you use the `styled` helper with React, this is automatically handled using CSS custom properties. 
  - But we cannot do the same for `css` tags since they aren't linked to any component, and so we don't have access to state and props.
- Inline styles
  - Inline styles are the most straightforward way to use dynamic styles. 
  - Pass a style object with the dynamic styles, and you're done

```typescript
export function Pager({ index, children }) {
  return (
    <div style={{ transform: `translateX(${index * 100}%)` }}>
      {children}
    </div>
  );
}
```

- CSS custom properties
  - custom properties cascade, so if you don't override the value for the current element, and a custom property with the same name exists for a parent element, it'll be used instead.

```typescript
import { css } from 'linaria';

const box = css`
  height: var(--box-size);
  width: var(--box-size);
`;

export function Box({ size }) {
  return (
    <div
      className={box}
      style={{ '--box-size': size }}
    />
  );
}
```

- Data attributes
  - `data-*` attributes allow us to store extra information on standard, semantic HTML elements 
  - without other hacks such as non-standard attributes, extra properties on DOM, or Node.setUserData().

```typescript
import { css } from 'linaria';

const box = css`
  &[data-valid] {
    color: yellow;
  }
  &[data-valid="invalid"] {
    color: red;
  }
  &[data-valid="valid"] {
    color: green;
  }
`

export function Box({ color, valid }) {
  return (
    <div
      className={box}
      data-valid={valid ? 'valid' : 'invalid'}
    />
  );
}
```

# faq
- 如何使用object style形式的样式
  - https://github.com/callstack/linaria/issues/464

```typescript
// 暂不支持
const Title = styled.h1({ color: 'red' })

// 变通方式
const sectionStyles = css`
  ${{
    marginTop: '1rem',
    background: 'green',
  }};
`
<section className={sectionStyles} />
```
