---
title: log-dev-error
tags: [dev, log]
pinned: true
created: '2020-02-20T10:43:37.374Z'
modified: '2020-08-04T12:24:45.908Z'
---

# log-dev-error

## logging 

 
- console.log 打印iframe的window对象会报错

VM37226:1 Uncaught DOMException: Blocked a frame with origin "https://stackoverflow.com" from accessing a cross-origin frame.

  - 判断一个变量或对象是否是iframe的方法
    - iframeWindow !== window，说明不是window
  - 其他方法参考
    - window.parent.frames.length > 0
- [Violation] Added non-passive event listener to a scroll-blocking `<some>` event. Consider marking event handler as 'passive' to make the page more responsive.
  - Passive event listeners are a new feature in the DOM spec that enable developers to opt-in to better scroll performance by eliminating the need for scrolling to block on touch and wheel event listeners. 
  - Developers can annotate touch and wheel listeners with `{passive: true}` to indicate that they will never invoke `preventDefault` . 
  - 解决方法： `this.element.addEventListener(t, e, { passive: true} )`
- error  React Hook useCallback received a function whose dependencies are unknown. Pass an inline function instead 
  - useCallback is specifically designed for inline functions.

``` JS
// error
const throttledMethod = React.useCallback(
  _.throttle(abc, 500),
  [abc],
);

// ok
const throttledMethod = React.useMemo(
  () => _.throttle(abc, 500),
  [abc],
);
```

- 循环引用的问题
  - It means that the object has a circular reference, something like: `var a = {}; a.b = a;`
  - `JSON.stringify` cannot convert structures like this.
  - [How can I print a circular structure in a JSON-like format?](https://stackoverflow.com/questions/11616630/how-can-i-print-a-circular-structure-in-a-json-like-format)
    - 使用自定义replacer函数
    - Node.js可使用内置的 `console.log(util.inspect(myObject))`
  - [mdn: TypeError: cyclic object value](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Cyclic_object_value)
    - find and filter (thus causing data loss) a cyclic reference by using the replacer parameter of `JSON.stringify()`

``` 
TypeError: Converting circular structure to JSON
    --> starting at object with constructor 'Object'
    |     property 'cells' -> object with constructor 'Array'
```

- react-dom.development.js?e444:23965 Uncaught Error: Element type is invalid: expected a string (for built-in components) or a class/function (for composite components) but got: object. You likely forgot to export your component from the file it's defined in, or you might have mixed up default and named imports.
  - element.type should be a string or class / function
  - 因为忘记导出组件了 export Component
- 'App' refers to a value, but is being used as a type here
  - 将index.ts文件名改为index.tsx
- pentaho下载依赖慢或停止：多等等或使用mvn代理而不是terminal代理

``` 
Downloading from Twitter: http://maven.twttr.com/org/pentaho/pentaho-ce-jar-parent-pom/9.1.0.0-SNAPSHOT/maven-metadata.xml
[WARNING] Could not transfer metadata org.pentaho:pentaho-ce-jar-parent-pom:9.1.0.0-SNAPSHOT/maven-metadata.xml from/to Twitter (http://maven.twttr.com/): Transfer failed for http://maven.twttr.com/org/pentaho/pentaho-ce-jar-parent-pom/9.1.0.0-SNAPSHOT/maven-metadata.xml
Downloading from Twitter: http://maven.twttr.com/org/pentaho/pentaho-ce-parent-pom/9.1.0.0-SNAPSHOT/maven-metadata.xml
Downloading from Twitter: http://maven.twttr.com/pentaho/pentaho-big-data-assemblies/9.1.0.0-SNAPSHOT/maven-metadata.xml

[INFO] --- maven-assembly-plugin:3.1.1:single (assembly_package) @ pdi-google-analytics-plugin ---
Downloading from Twitter: http://maven.twttr.com/org/pentaho/pentaho-ce-jar-parent-pom/9.1.0.0-SNAPSHOT/maven-metadata.xml
[WARNING] Could not transfer metadata org.pentaho:pentaho-ce-jar-parent-pom:9.1.0.0-SNAPSHOT/maven-metadata.xml from/to Twitter (http://maven.twttr.com/): Transfer failed for http://maven.twttr.com/org/pentaho/pentaho-ce-jar-parent-pom/9.1.0.0-SNAPSHOT/maven-metadata.xml
Downloading from Twitter: http://maven.twttr.com/org/pentaho/pentaho-ce-parent-pom/9.1.0.0-SNAPSHOT/maven-metadata.xml

```

- tts-mscorefonts-installer在Ubuntu linux系统中安装微软字体
    - 手动下载字体exe
    -  sudo dpkg-reconfigure ttf-mscorefonts-installer 手动配置离线下载的字体位置
    -  remove the partial download: rm -R /var/lib/update-notifier/package-data-downloads/partial/

``` 
Failure to download extra data files
The following packages requested additional data downloads after package installation, but the data could not be downloaded or could not be processed.
ttf-mscorefonts-installer
The download will be attempted again later, or you can try the download again now.  Running this command requires an active Internet connection.
```

- storybook import .mdx into .stories.tsx，在单独项目可正常显示，放在back-garden-ui的子项目却无法显示
    - 原因是babel-loader没有配置的处理react的插件 
    - @babel/plugin-transform-react-jsx
    - 要多与官方文档示例对比，不要忽视细节，自我猜测

``` 
RROR in ./src/components/general/Button/__stories__/Button1.docs.mdx
Module build failed (from **/babel-loader/lib/index.js):
SyntaxError: __stories__/Button1.docs.mdx: Unexpected token (10:9)

   8 | const makeShortcode = name => function MDXDefaultShortcode(props) {
   9 |   console.warn("Component " + name + " was not imported, exported, or provided by MDXProvider as global scope")
> 10 |   return <div {...props}/>
     |          ^
  11 | };
  12 | 
  13 | const layoutProps = {

```

- index.esm.js  error  Import in body of module; reorder to top import/first
    - 未发现原因，只能每次手动调整顺序
- ts编译问题  

``` 
Option 'allowJs' cannot be specified with option 'declaration'.
"declaration": true
```  

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
- 当children类型声明为 `children?: ((props: T) => React.ReactNode) | React.ReactNode;` 时，会异常，解决方法有2个
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

    thread "AWT-EventQueue-0" java.lang. NoSuchMethodError: onScheduleMessagePumpWork  
    

``` 
    maven打包后的main class是 example.simple.CefFrameExample  
    报错原因可能是cef不同版本的方法不一样  
    ```

    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:target/* example.simple. CefFrameExample
    

``` 
- jcef-quickstart
    - 运行成功，在任意目录

    ```

    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:/home/yaoo/Downloads/jcef-quickstart/target/classes  tests.simple. MainFrame
    

``` 
    - 运行成功，在maven项目根目录

    ```

    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:lib/jogamp/jar/*:target/classes  tests.simple. MainFrame
    

``` 
    ```

    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:lib/jogamp/jar/*:target/*  tests.simple. MainFrame
    

``` 
    - 运行失败，core dumped

    ```

    java  -Djava.library.path=lib/native/Release -cp .:lib/jogamp/jar/*:target/classes  tests.simple. MainFrame
    

``` 
    - jcef自带示例，运行成功，在任意目录均可

    ```

    java  -Djava.library.path=/home/yaoo/Documents/repo/opensource/java-cef/src/jcef_build/native/Release -cp .:/home/yaoo/Documents/repo/opensource/java-cef/src/third_party/jogamp/jar/*:/home/yaoo/Documents/repo/opensource/java-cef/src/out/linux64 tests.simple. MainFrame
    

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
