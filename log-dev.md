---
tags: [log/dev]
title: log-dev
created: '2019-06-09T15:54:12.063Z'
modified: '2019-10-19T04:34:21.625Z'
---

# log-dev

## summary
- 不要省事直接使用别人的例子，15年的project到19年方法就不一致了，自己编译更透彻
- 现在写的代码能够稳定执行至少6个月吗？
- 开发工作很多时候是用同一语言的不同框架，或用不同语言，在不同的平台将相同功能重复实现
- 技术选型或框架选型时，对开发者友好和对用户友好的取舍
    - java的简单与功能丰富对开发者更友好，c++的高性能对用户友好

## dev-tricks
- 少用if-else，多用卫语句
    - 先对可能的条件进行检验，程序的主逻辑在验证之后才开始运行
- 文档生成的解决方案还是基于markdown更方便
    - 参考`react-markdown-loader`, 可以自动读取md内容，根据模板生成demo插入页面

## dev-frontend
- console.log打印对象时打印的是引用，一旦后面有修改，当你查看打印出的对象属性时就是查看后面修改过后的
    - 建议使用`console.log(JSON.stringify(obj))`
    - 若obj的属性值也是对象，则打印的对象也是最终值，不是之前的
- debug时尽量使用单元测试或实现单独功能的页面，在原来复杂的源码中不便于分析生命周期顺序
    - 准备好 boilerplate

## dev-backend
- 多线程/并发相关


## dev-logging

- onclick的玄学
    - clear()不能执行因为默认会执行document.clear()
    - 纯手打的handleClick1()不能执行，但ide自动补全的handleClick1()能执行，在线codepen手打也能执行
        - 可能与编辑环境的编码有关
```
<button onclick="clear()">Clear</button>
<button onclick="clear2()">Clear2</button>
<button onclick="handleClick1()">Click1</button>
<button onclick="handleClick1()">单击或双击我</button>
<button οnclick="handleClick1()">单击或双击我</button>
```
- Warning: React.createElement: type is invalid -- expected a string Check the render method of
    - refer to react conditional rendering
- react-data-grid
    - simple-grid-demo运行起来，单元格的border未显示
        - 因为未导入bootstrap样式
    - Arrow function should not return assignment
- TS2605: JSX element type 'ReactTable' is not a constructor function for JSX elements.
    - Type 'ReactTable' is missing the following properties from type 'ElementClass': context, setState, forceUpdate, props, refs
    - TS2607: JSX element class does not support attributes because it does not have a 'props' property
- this implicitly has type any because it does not have a type annotation.ts(2683)
    - https://stackoverflow.com/questions/41944650/this-implicitly-has-type-any-because-it-does-not-have-a-type-annotation
- Type 'string' is not assignable to type PositionProperty
    - ts中style对象的position值要写成 position : 'absolute' as 'absolute'
- ResizableBox组件的componentWillReceiveProps用getDerivedStateFromProps替换后拖拽失效
    - 原因是方法的逻辑书写错误
    - 解决方法是这两个方法都去掉，不需要作手动比较
- 在render()方法中将children作为函数调用会有异常，能运行，但控制台会提示异常信息
```
return this.props.children(value);

TS2349: This expression is not callable.
No constituent of type 'ReactNode' is callable.
Cannot invoke an expression whose type lacks a call signature. Type 'ReactNode' has no compatible call signatures.ts(2349)

```
类似的，下面也会异常
```
type F =   
  ((a: string) => void) |
  ((b: boolean) => void)
// 将上面的联合类型|改成交叉类型&就可以正常编译通过了

let f: F = (a: string) => {}
f('foo')

function f2 (f: F) {
  f('foo')
  ^^^^^
}
// Cannot invoke an expression whose type lacks a call signature. Type 'F' has no compatible call signatures.
```   

- 当children类型声明为`children?: ((props: T) => React.ReactNode) | React.ReactNode;`时，会异常，解决方法有2个
    - `(children as ((props: T) => React.ReactNode))(renderRest);`
    - use type guard
    ```
    if (typeof children === 'function') {
      children(renderRest);
    }
    ```   
    
- 参考
    - https://stackoverflow.com/questions/56076608/cannot-invoke-an-expression-whose-type-lacks-a-call-signature-in-typescript
    - https://github.com/Microsoft/TypeScript/issues/7960

- styled-components  
  ```
  Type is not assignable to type 'Readonly<ThemeProviderProps<any, any>>'.
    Types of property 'children' are incompatible.
      Type 'any[]' is not assignable to type 'ReactChild'.
        Type 'any[]' is not assignable to type 'string'.
  ```   

    - 异常的位置是  

        ```
          <ThemeProvider theme={theme}>
              {/* 这个是绿色 */}
              <ThemedButton>Themed</ThemedButton>
          </ThemeProvider>
        ```    

    - 删除注释 ` {/* 这个是绿色 */}` 就没问题了
- `Uncaught Invariant Violation: Target container is not a DOM element.`
    - render的DOM用的是id还是class，别写错了
- `Cannot read property 'render' of undefined` at `ReactDOM.render()`
    - `import ReactDOM from 'react-dom';` means import the default export from the react-dom module as ReactDOM
    - but react-dom ships as a CommonJS module so technically it doesn't have a default export.
    - Setting `esModuleInterop` flag to true, lets you import its single exported value as if it was the default export of a TS or ES6 module.
    - add `"esModuleInterop": true` to `compilerOptions` of tsconfig.json 
- npm install, Maximum call stack size exceeded
    - verbose stack RangeError: Maximum call stack size exceeded 185 verbose stack     at RegExp.test (<anonymous>)
    - solution: delete `package-lock.json`
- Project 'com.datable:hello-poi:1.0.0' is duplicated in the reactor
    - 原因是父pom.xml指定了多个作为子module，某一个子module 的pom又指定了父 或者 同级 作为自己的子module，导致出现冲突
- 切换jdk版本 基于openjdk
   - update-java-alternatives --list
   - update-java-alternatives --set /usr/lib/jvm/java-7-openjdk-amd64
- 删除git commit后不希望版本控制的文件
    - `git rm -r --cached ./datable/.settings`
- junit测试类的方法上使用@Test后，方法名再以test开头会出现问题，如文件无法读取
- junit中方法的执行顺序并不一定按照源码中的书写顺序，如ExcelParserBasicTest类
- app-jcef-example  
    - 错误  
    ```
    thread "AWT-EventQueue-0" java.lang.NoSuchMethodError: onScheduleMessagePumpWork  
    ```
    maven打包后的main class是 example.simple.CefFrameExample  
    报错原因可能是cef不同版本的方法不一样  
    ```
    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:target/* example.simple.CefFrameExample
    ```
- jcef-quickstart
    - 运行成功，在任意目录
    ```
    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:/home/yaoo/Downloads/jcef-quickstart/target/classes  tests.simple.MainFrame
    ```
    - 运行成功，在maven项目根目录
    ```
    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:lib/jogamp/jar/*:target/classes  tests.simple.MainFrame
    ```
    ```
    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:lib/jogamp/jar/*:target/*  tests.simple.MainFrame
    ```
    - 运行失败，core dumped
    ```
    java  -Djava.library.path=lib/native/Release -cp .:lib/jogamp/jar/*:target/classes  tests.simple.MainFrame
    ```
    - jcef自带示例，运行成功，在任意目录均可
    ```
    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:/home/yaoo/Documents/repo/opensource/java-cef/src/out/linux64 tests.simple.MainFrame
    ```
- jcef build
- error1
    ```
    [ 71%] Linking CXX executable Release/jcef_helper
    /usr/bin/ld: cannot find -lX11
    collect2: error: ld returned 1 exit status
    native/CMakeFiles/jcef_helper.dir/build.make:122: recipe for target 'native/Release/jcef_helper' failed
    make[2]: *** [native/Release/jcef_helper] Error 1
    CMakeFiles/Makefile2:142: recipe for target 'native/CMakeFiles/jcef_helper.dir/all' failed
    make[1]: *** [native/CMakeFiles/jcef_helper.dir/all] Error 2
    Makefile:83: recipe for target 'all' failed
    make: *** [all] Error 2
    ```
    - sudo apt-get install libx11-dev -y
- error2    
    ``` 
    jdk1.8.0_201/include/linux/jawt_md.h:31:10: fatal error: X11/Intrinsic.h: No such file or directory   
    #include <X11/Intrinsic.h>
    ```
    -  sudo apt-get install libxt-dev -y
- npm WARN Invalid version: "1.0"
    - change 1.0 to 1.0.0


