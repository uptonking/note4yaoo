---
tags: [style, web]
title: docs-style
created: '2019-08-17T10:19:06.636Z'
modified: '2019-08-22T10:16:56.308Z'
---

# docs-style

## dev-tips
- 要考虑如何复用现有项目的样式和第三方库的样式

## docs-bulma
### basic
- https://bulma.io/documentation/overview/start/
- https://github.com/jgthms/bulma

### docs
- By default, columns are only activated from tablet onwards. 
    - This means columns are stacked on top of each other on mobile.
- Bulma is compatible with all icon font libraries: Font Awesome 5, Font Awesome 4, Material Design Icons, Open Iconic, Ionicons etc.  


## docs-styled-components
### basic
- https://www.styled-components.com/docs/basics
- https://github.com/styled-components/styled-components

### summary
- s-c是典型的css-in-js样式解决方案
- s-c使用ES6的字符串模板方式来定义css样式，这样使得css的写法与原生的css写法基本一致，不用按照react的camelCase写样式
- s-c最终生成的是随机字符串类名，能解决命名冲突，使用到dom中不是内联样式
- s-c也有一套用JS实现的预处理器工具库polished，其中包括一些常用的CSS方法，比如 clearfix、hsl、mix 等，让开发者可以完全不再使用css预处理器来写css了
- 也可以将样式对象写在单独文件，再导入，类似grommetv2的处理方式
- 移除了组件和样式之间的映射关系，将样式也作为组件或组件的一部分
- 支持ssr服务端渲染和react-native
- 通过attrs()方法可以传入html标签的属性，还可以传入className，方便使用第三方样式
- s-c支持动画的@keyframe
- s-c支持类似sass的嵌套语法，但不推荐使用嵌套，因为样式组件的子组件的className不会被编译成随机值，这些子组件的类还是会受CSS的全局作用域影响
- 使用了逻辑组件与样式展示组件分离的思想
- jss也是css-in-js的一直解决方案
    - 用户包括material-ui
    - 使用类似于json的语法描述css
- 优点
    - 兼容现有的className方式，升级无痛
    - 在代码设计层面消除css命名冲突
    - 样式相关变量可以共享，都是作为在js中的变量
    - 支持样式组件通过extend继承，方便代码复用
    - 样式也作为一种组件
- 缺点
    - 不能用stylelint检查CSS代码，不能使用prettier来格式化css
    - 父组件覆盖子组件的className较复杂，需要使用.container.container{}
    - 国内关注度不高
    - ide语法高亮与自动提示不全支持不完善

### docs
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
const Wrapper = styled.section`
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
