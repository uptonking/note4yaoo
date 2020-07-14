---
title: coding-snippet
tags: [coding, draft]
created: '2019-09-04T03:02:06.457Z'
modified: '2020-07-14T09:15:48.967Z'
---

# coding-snippet

``` JS
// js
```

- react-jquery(plugins)-dom-ref

``` js
class SomePlugin extends React.Component {
  componentDidMount() {
    this.$el = $(this.el);
    this.$el.somePlugin();
  }

  componentWillUnmount() {
    this.$el.somePlugin('destroy');
  }

  render() {
    return <div ref={el => this.el = el} />;
  }
}
```

``` js
// react包装一个jquery的插件
import React, { Component } from 'react'
import ReactDom from 'react-dom'

class QRCode extends Component {
  componentDidMount() {
    // returns the corresponding native browser DOM element
    let node = ReactDom.findDOMNode(this);
    if (this.props.text) {
      $(node).qrcode({ ...this.props });
    }
  }

  componentWillReceiveProps(nextProps) {
    if (this.props.text != nextProps.text) {
      let node = ReactDom.findDOMNode(this);
      $(node).qrcode({ ...this.props });
    }
  }

  render() {
    return (
      <div/>
    );
  }
}
```

``` js
import React from‘ react’;
import { findDOMNode } from‘ react - dom’;
import $ from‘ jquery’;
class FullDesc extends React.Component {
  constructor() {
    super();
  }
  handleToggle = () => {
    const el = findDOMNode(this.refs.toggle);
    $(el).slideToggle();
  };
  render() {
    return (
      <div className=”long-desc”>
  <ul className=”profile-info”>
   <li>
     <span className=”info-title”>User Name : </span> Shuvo Habib
   </li> <
      /ul> <
      ul className = ”profile - info additional - profile - info - list” ref = ”toggle” >
      <li>
    <span className=”info-email”>Office Email</span> me@shuvohabib.com
  </li> <
      /ul> <
      div className = ”ellipsis - click” onClick = { this.handleToggle } >
      <i className=”fa-ellipsis-h”/>
  </div> <
      /div>
    );
  }
}
```

- react-setState

``` js
class App extends React.Component {
  state = { val: 0 }

  componentDidMount() {
    this.setState({ val: this.state.val + 1 })
    console.log(this.state.val)

    this.setState({ val: this.state.val + 1 })
    console.log(this.state.val)

    setTimeout(_ => {
      this.setState({ val: this.state.val + 1 })
      console.log(this.state.val);

      this.setState({ val: this.state.val + 1 })
      console.log(this.state.val)
    }, 0)
  }

  render() {
    return <div>{this.state.val}</div>
  }
}
// 0,0,2,3
// https://juejin.im/post/5b45c57c51882519790c7441
```

- class-extends

``` js
class A {
  print() {
    console.log('print a');
  }
}
class C extends A {
  print() {
    super.print();
    console.log('print c');
  }
}
const c = new C();
c.print();
// print a
// print c

class B {
  print = () => {
    console.log('print b');
  }
}
class D extends B {
  print() {
    super.print();
    console.log('print d');
  }
}
const d = new D();
d.print();
// print b

// 类的非静态属性都是定义在类的原型对象上，而不是类的实例上的
// 但通过箭头函数定义的方法时绑定在this上，而this是指向当前创建的类实例对象
// 类D继承B，不仅会继承类B原型上的属性和方法，也会继承其实例上的属性和方法
// 当访问一个对象实例的属性时，会先在实例上进行查找，如果没有，则顺着原型链往上查找，直到原型链的顶端。若在实例上查找到对应属性，则会返回，停止查找。即使原型上定义了同一个属性，该属性也不会被访问到，这种情况称为"属性遮蔽 (property shadowing)"。
// 只会输出print b，而不会输出print d
```

- cancelablePromise

``` js
export const cancellablePromise = promise => {
  let isCanceled = false;

  const wrappedPromise = new Promise((resolve, reject) => {
    promise.then(
      value => (isCanceled ? reject({ isCanceled, value }) : resolve(value)),
      error => reject({ isCanceled, error }),
    );
  });

  return {
    promise: wrappedPromise,
    cancel: () => (isCanceled = true),
  };
};
```

- HOW TO USE      

``` js
const somePromise = new Promise(r => setTimeout(r, 1000));

const cancelable = cancellablePromise(somePromise);

cancelable
  .promise
  .then(() => console.log('resolved'))
  .catch(({ isCanceled, ...error }) => console.log('isCanceled', isCanceled));

// Cancel promise
cancelable.cancel();
```

- 可以使用cancellablePromise来实现同时支持单击和双击    

   

- react父组件渲染经典问题
    - render原理
      - you can think of the render() function as creating a tree of React elements，返回的是虚拟DOM用于diff
      -  On the next state or props update, that render() function will return a different tree of React elements
      - react的核心是通过diff算法找到新旧子树的最小差集，然后patch到真是DOM
      - render方法被调用不等同于更新DOM，没变化就不会重新渲染DOM
      - 一个组件执行setState之后，从这个组件为根的组件树会有一个更新的过程，
        - 每个组件都会根据自己的shouldComponentUpdate执行render方法，然后和上次render的结果比较，找到最小差集之后patch到真实dom上。
        - 若子组件的shouldComponentUpdate没有返回false的话，它的render是会执行的，但不一定会导致真实dom改变和重新渲染
    - 父组件A的state改变，会触发父组件A的rerender
        - render会调用 `React.createElement(componentType,props,children)`
        - 不能简单地根据jsx的关系来判断父子组件的render顺序，要将jsx转换成React.createElement来分析
        - 若父组件A中间是 `{this.props.children}` ，则children由父组件A的父组件P渲染，由于引用相等，本次无需更新子组件
            - 因为Child组件在父组件A的父组件P层级上创建，没有改变
            - this.props.children与父组件P内children处的组件引用相等
            - 若要child每次也render，解决方案
                - `React.cloneElement(this.props.children)`
        - 若父组件A中间是 `<Child />` ，则会重新创建子组件的虚拟DOM，调用子组件的render
            - 父组件A每次render时都会创建新的虚拟DOM，引用不相等，子组件就会重新render
    - 结论是父组件rerender，子组件不一定会调用render
    - If a parent component is updated, does React always update all the direct children within that component?
        - No. React will only re-render a component if shouldComponentUpdate() returns true. 
        - By default, that method always returns true
    - 参考
        - 强推 https://stackoverflow.com/questions/47567429/this-props-children-not-re-rendered-on-parent-state-change
        - https://stackoverflow.com/questions/50053064/react-do-children-always-rerender-when-the-parent-component-rerenders
        - https://stackoverflow.com/questions/40819992/react-parent-component-re-renders-all-children-even-those-that-havent-changed

``` js
class Application extends React.Component {
  render() {

    return (
      <div>
        {/* 
          Clicking this component only logs the parent's render function 
        */}
        <DynamicParent>
          <Child /> //这是Application传递的this.props.children
        </DynamicParent>

        {/* 
          Clicking this component logs both parents and child render funcs 
        */}
        <StaticParent />
      </div>
    );

  }
}

class DynamicParent extends React.Component {
  state = { x: false };
  render() {

    console.log("DynamicParent");
    return (
      <div onClick={() => this.setState({ x: !this.state.x })}>
        {this.props.children} 
      </div>
    );

  }
}

// -- -- -- -- -- -- -- -- -- --会转化-- -- -- -- -- -- -- -- -- -- --

function DynamicParent(props) {

  return React.createElement(
    "div", {
      onClick: () => this.setState({ x: !this.state.x }),
    },
    this.props.children
  );

}

React.createElement(

  DynamicParent, { children: React.createElement(Child, null) }, // children在props里

); // 只会创建一次Child

// -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -
class StaticParent extends React.Component {
    state = { x: false };
    render() {

      console.log("StaticParent");
      return (
        <div onClick={() => this.setState({ x: !this.state.x })}>
        <Child />
      </div>
      );

    }
  }
  -- -- -- -- -- -- -- -- -- --会转化-- -- -- -- -- -- -- -- -- -- --

function StaticParent(props) {
  return React.createElement(

    "div", { onClick: () => this.setState({ x: !this.state.x }) },
    React.createElement(Child, null) //在children参数里，每次都创建Child

  );
}

React.createElement(StaticParent, null);
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
function Child(props) {
  console.log("child");
  return <div>Child Texts</div>;
  // return React.createElement("div", null, "Child Text"); 
}
```

- ts接口兼容性测试
  - 属性多的对象可以被赋值给属性少的接口

``` typescript
interface Name {
    name: string;
}
let obj: Name; 
let dabao = {

    name: 'cxh',
    height: 180

}; 
obj = dabao; // ok

```

``` typescript
interface Name {
    name: string;
    age: number;
}
let obj: Name;
let dabao = {
    name: 'cxh'
};
obj = dabao;  // Property 'age' is missing
```

- ts接口实现参数数量测试
  - 结论是不能少，也不能多

``` typescript
interface Animal {
    name: string;
    age: number;
    // [propName: string]: any;
}

let printName = function (param: Animal) {
    if (param.age) {
        console.log( `Name is ${param.name}, and age is ${param.age}` );
    } else {
        console.log( `Name is ${param.name}` );
    }
};

printName({ name: 'Dog' });
printName({ name: 'Dog', age: 5 });
printName({ name: 'Dog', age: 5, extra: 123, extra2: 456 });
```
