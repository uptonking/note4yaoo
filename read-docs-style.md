---
tags: [style, web]
title: read-docs-style
created: '2019-08-17T10:19:06.636Z'
modified: '2019-10-15T10:36:06.734Z'
---

# read-docs-style

## dev-tips
- 如何复用现有项目的样式和第三方库的样式
- 如何将本项目作为库提供给其他人使用

## docs-bulma
### basic
- https://bulma.io/documentation/overview/start/
- https://github.com/jgthms/bulma

### docs
- By default, columns are only activated from tablet onwards. 
    - This means columns are stacked on top of each other on mobile.
- Bulma is compatible with all icon font libraries: Font Awesome 5, Font Awesome 4, Material Design Icons, Open Iconic, Ionicons etc.  

### booking-Creating Interfaces with Bulma_Jeremy Thomas_2018
- bulma features
    - modern css framework with flexbox
    - 100% responsive, designed to be both mobile and desktop friendly
    - customizable with over 300 sass variables
    - css only, no js

## docs-styled-components
### basic
- https://www.styled-components.com/docs/basics
- https://github.com/styled-components/styled-components

### faq
- should react components use inline styles or classNames ?
    - Ordinarily, inline styling is discouraged by the react team, a concern that is very valid because inline styles do not allow the use of pseudos and media queries
    - Also, inline styles should not be used due to a lot of concerns about browser compatibility, camel-casing, and automatically appended scalar quantities
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
    - s-c会为每个状态生成一个样式表,动画一般会有很多中间值，在短时间内进行变化，如果动画值通过props传入该StyledComponent来应用样式，这样会生成很多样式,动画场景最好使用style内联样式来做
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
    - 能通过`$(CompName)`直接选择其他react组件设置样式
    - 支持ssr和react-native
    - powerful js
    - 保持dom结构与样式分离的同时，不使用class，不需要跳转多文件，也不是内联样式
- s-c**缺点**
    - 不能用stylelint检查CSS代码，不能使用prettier来格式化css，ide语法高亮与自动提示支持不完善
    - 父组件覆盖子组件的className较复杂，需要使用.container.container{}
    - 国内关注度不高，资料不丰富
    - s-c样式组件是一层包裹，层层包裹会消耗性能
    - Biggest drawback: changes to styles require bundle re-compilation and app's state might reset
    - 不支持css提取为静态文件，参考[issue](https://github.com/styled-components/styled-components/issues/1018)
    - 复杂组件开发时会产生嵌套地狱wrapper hell，这也是react的一个问题
        - custom hooks试图解决wrapper hell的问题
    - s-c只支持React，如果你用其他的JS框架你必须寻找其他CSS方案
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
            - Instead of relying on two separate style objects and having to use React event handlers to setup a simple hover state, we use a styled component. This makes it easy to inject values that only exist in JavaScript into our CSS while still allowing CSS to handle the various UI states.
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

### summary
- s-c是典型的css-in-js样式解决方案
- s-c使用ES6的字符串模板方式来定义css样式，这样使得css的写法与原生的css写法基本一致，不用按照react的camelCase写样式
- css()
    - A helper function to generate CSS from a template literal with interpolations
- s-c原理
    - When you import the library first time in you app, it creates an internal `counter` variable to count all the components created via the `styled` factory.
    - When styled-components creates a new component, it also creates internal identifier componentId using MurmurHash algorithm
    - As soon as the identifier is created, styled-components inserts new HTML `<style>` element into the` <head>` (if it is the first component and the element is not inserted yet) of your page and adds special comment marker with the componentId to the element which will be used later. 
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
        -  react-transition-group is so simple. If we use styled-componets,`<Transition>` component may be better than `<CSSTransition>`
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
- s-c vs emotion
    - https://github.com/jsjoeio/styled-components-vs-emotion
    - https://github.com/emotion-js/emotion/issues/113
    - https://material-ui.com/zh/guides/interoperability/
    - https://spectrum.chat/styled-components/general/styled-components-vs-emotion~47206c1b-a688-424e-9e96-6f265993587e



### docs
- The rule of thumb is to use `attrs` when you want every instance of a styled component to have that prop, and pass `props` directly when every instance needs a different one
    - you can set a property on attrs to a function that computes that prop based on other props.
- ThemeProvider provides a theme to all React components underneath itself via the context API
- existing css
    - styled-components generates an actual stylesheet with classes, and attaches those classes to the DOM nodes of styled components via the className prop. It injects the generated stylesheet at the end of the head of the document during runtime.
    - You can use its existing class names alongside your components.
    - If you want the class to always be attached to the component, you should use the `attrs` method to attach it. 
    - If you want to attach it only in some cases, you can use `className` props like you always have.
    - If the framework has a bunch of raw global CSS that needs to be included on the page, you can add it using the createGlobalStyle API. This is also useful for things like CSS resets.

    
### qucikstart
- demo
```
import styled from 'styled-components';
const Wrapper = styled.div`
  margin: 0 auto;
  width: 300px;
`;
const Button = styled.button`
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
```
const Button = () => <button></button>
const StyledButton = styled(Button)`
  //style goes here
`;
export default StyledButton;
import Button from './Button';
const FormContainer = styled.form`
  ${Button] {
    //additional style goes here
  }
  `
  //给样式组件添加额外的样式
  const StyledButton = styled(Button)`
 //additional style goes here
`
```

## bootstrap

- faq
    - bootstrap.css vs bootstrap-theme.css
        - bootstrap.css is the core css for BootStrap that defines all the style for various controls/components
        - bootstrap-theme.css defines the themes (gradient/animation) for buttons,dropdown menu,navbar,progressbar,panels
        - Most of the times adding bootstrap.css is enough for bootstrap to work, but for gradient/animation, you can use bootstrap-theme.css
