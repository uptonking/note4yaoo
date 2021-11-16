---
title: dev-ing-error
tags: [dev, error]
created: '2020-02-20T10:43:37.374Z'
modified: '2021-03-29T19:29:32.505Z'
---

# dev-ing-error

# logging 

 

- ckeditor writer-incorrect-use
  - 原因待确定
  - 修改方式为将writer.insertText()这类修改model部分的代码放在方法的第一层

- CKEditorError: model-position-before-root
  - 检查ckeditor修改model部分的代码，可能是当前选择的position和要插入的position不匹配

- postcss-loader在ckeditor项目中使用的问题
  - You did not set any plugins, parser, or stringifier. Right now, PostCSS does nothing. Pick plugins for your case 
  - 异常时有时无，不能稳定复现
  - 按官方文档中的postcss-loader@3和style-loader@1会出现问题，编辑器样式异常
  - 实测使用postcss-loader@4和style-loader@2编辑器样式能够正常显示

- ckeditor的css加载问题
  - 需要使用 postcss-loader@3
- ValidationError: Invalid options object. PostCSS Loader has been initialized using an options object that does not match the API schema.
 - options has an unknown property 'plugins'.

- Webpack: Bundle.js - Uncaught ReferenceError: process is not defined
  - 可以实现读取自定义环境变量，如 REACT_APP_ENV

```JS
const webpackConfig = {
  plugins: [
    new webpack.ProvidePlugin({
      process: 'process/browser',
    }),
    new webpack.DefinePlugin({
      'process.env': JSON.stringify(process.env)
    })
  ],
};
```

- Module not found: Error: Can't resolve '/home/yaoo/Documents/repo/template/all-react/react-starter-ts/src/render.ts'
  - 注意入口文件是 render.tsx，而不是 render.ts

- [403 forbidden error in Apache with document root on an NTFS partition](https://askubuntu.com/questions/163685)
  - 结论是站点不适合放在win分区；若默认放到win分区，则linux分区的内容可能出问题
  - Please try editing the default sites-available file with that path, restart Apache with sudo service apache2 restart and see if it works.
  - it appears Nautilus mounts NTFS partitions with odd permissions so that no user but yourself (and root, of course) can read or write from/to it.

- docker run -p 80:80 docker/getting-started
  - 80: bind: address already in use.
  - docker run -p 8080:80 docker/getting-started

- Error: Multipart: Boundary not found
  - [Fetch API and multer error while uploading file](https://stackoverflow.com/questions/35795529)
  - There is no need to assign a header `{Content-Type': 'multipart/form-data'}`: the browser substitutes its own.
  - But if you expose it, then it is not specified `boundary` after `content-type:multipart/form-data; boundary=...` in Request Headers before Request Payload and that is causing the error on the server-side.

- Access to fetch at 'http://localhost:11122/account/login' from origin 'http://localhost:8999' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: The value of the 'Access-Control-Allow-Credentials' header in the response is '' which must be 'true' when the request's credentials mode is 'include'.
- Response to preflight request doesn't pass access control check: The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*' when the request's credentials mode is 'include'.
  - credentials为include时，origin不能为 *

- bcrypt install error: gyp: Undefined variable module_name in binding.gyp while trying to load binding.gyp
- https://github.com/nodejs/node-gyp/issues/508
  - I couldn't make it work on npm v7.x no matter what I did so I had to go back to latest npm v6.
  - For anyone looking for a quick fix, this worked for me. There seems to be a dep issue with NPM 7.

- [Can't perform a React state update on an unmounted component. ](https://stackoverflow.com/questions/56442582)
  - This is a no-op, but it indicates a memory leak in your application. 
- The easiest solution is to use a local variable that keeps track of whether the component is mounted or not.
- [setState hook inside useEffect can cause unavoidable warning Can't perform a React state update](https://github.com/facebook/react/issues/14369)

- [TS2339: Property 'span' does not exist on type 'JSX. IntrinsicElements'](https://stackoverflow.com/questions/47694227)
- I had the same problem but for me, it was the p element. The reason for the error was that I refactored a p element to h3 for instance and VSCode changed also the type definition.
- As you pointed out cleaning the node_modules and doing a fresh npm install does the trick.

- [React suspense looks for the chunk in the wrong directory](https://stackoverflow.com/questions/59467067)
- webpack `output.publicPath` .
  - This option specifies the public URL of the output directory when referenced in a browser. 
  - A relative URL is resolved relative to the HTML page (or `<base>` tag). 
  - Server-relative URLs, protocol-relative URLs or absolute URLs are also possible and sometimes required, i. e. when hosting assets on a CDN.
  - The value of the option is prefixed to every URL created by the runtime or loaders. 
  - Because of this the value of this option ends with `/` in most cases.
- I had the best experience using react lazy when the folders were in the same folder as the one using the import, or if they were inside a child folder of that folder, anywhere else i got chunk error. 

- TAR_BAD_ARCHIVE: Unrecognized archive format
  - npm install registry https://registry.npmjs.org
  - 漏写了--

- Webpack resolve extension “Module not found”
  - 找了很久，原因是漏写了一个点号 
  - `extensions: ['.ts', '.tsx', '.js', 'jsx']`

- sass-loader/dist/cjs.js: TypeError: this.getOptions is not a function
  - sass-loader v11(2021-02-05): minimum supported webpack version is 5
  - sass-loader v8.0 Breaking Changes
    - move all sass (includePaths, importer, functions) options to the sassOptions option. 

- Unhandled Rejection (ScriptExternalLoadError): Loading script failed.  
(error: http://localhost:8000/mf-va_remoteEntry.js)
while loading "./core-js" from webpack/container/reference/mf
  - 解决方法是 将npm7降级到npm6，因为控制台提示esbuild install incorrectly. 
  - "lockfileVersion": 1

- [How can I properly define a type interface when using React useContext?](https://stackoverflow.com/questions/61775657)

```JS
const AppContext = createContext < [AppStateType, React.Dispatch < React.SetStateAction < AppStateType >> ] > ([{ isOnline: false }, () => false]);
```

- Cannot update a component (`WidthEmitter`) while rendering a different component (`Context. Consumer`).
  - [Warning: Cannot update a component while rendering a different component.](https://stackoverflow.com/questions/62694745/)
  - 一种思路是将调用setState()写在useEffect/componentDidUpdate中
  - 一种思路是检查onClick的值应该是function，而不是函数调用的返回值
  - ref
    - https://stackoverflow.com/questions/67030576

- Uncaught RangeError: Duplicate use of selection JSON ID cell
  - https://github.com/ueberdosis/tiptap/issues/316
  - this is a version problem. why do you installed prosemirror-tables?
  - npm installs prosemirror-utils at verstion 0.9.6 by default, witch requires a peer of prosemirror-tables@^0.9.x. It cause error because tiptap requires prosemirror-tables@^1.0.0.

- @atlaskit/editor-core minimal App 无法正常运行
  - 异常相关信息
  - 一直未跑通

```
Should not import the named export 'version' (imported as 'listenerVersion') from default-exporting module (only default export is available soon)

WARNING in ../../node_modules/@atlaskit/analytics-listeners/dist/esm/atlaskit/process-event.js
Should not import the named export 'version' (imported as 'listenerVersion') from default-exporting module (only default export is available soon)

WARNING in ../../node_modules/@atlaskit/emoji/dist/esm/util/analytics.js 25:19-30
Should not import the named export 'name' (imported as 'packageName') from default-exporting module (only default export is available soon)

```

- @babel/template placeholder "$1": Property expression of ExpressionStatement expected node to be of a type ["Expression"] but instead got "TSModuleBlock"
  - https://stackoverflow.com/questions/64343700
  - This might probably due to a namespace being exported which only contain interfaces/types (Not actual classes/functions/objects but type declarations).

```JS
// A quick fix is to add declare to the exported namespace.

export declare namespace SomeNameSpace {}

// instead of

export namespace SomeNameSpace {}
```

- esbuild  esbuild: Failed to install correctly
  - If you're using npm v7, make sure your package-lock.json
  -  file contains either "lockfileVersion": 1
  - 只是esbuild这个包未安装成功，可以查看 node_modules/esbuild/bin/esbuild，这个文件内容为空
  - 因为npm安装此包时，未执行postinstall，需要自己单独执行npm rebuild esbuild，
  - 若还是异常，可以进一步手动执行 node node_modules/esbuild/install.js

- [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './v4' is not defined by "exports
  - https://github.com/uuidjs/uuid/issues/444
  - I fixed it by running `npm ci`

- Warning for 'exhaustive-deps' keeps asking for the full 'props' object instead of allowing single 'props' properties as dependencies
  - https://github.com/facebook/react/issues/16265
  - The problem is Typescript's discriminated unions. With destructuring we have to null-check everything.

```JS
// This way I get the proper warning (if I omit props.whatever from the array).
useEffect(() => {
  const whatever = props.whatever;
  whatever();
}, [props.whatever]);

// By reading the function before the call you’re avoiding the problem:
// This is the preferred solution.
const { whatever } = props;

useEffect(() => {
  // at some point
  whatever();
}, [whatever]);

// To avoid destructuring or assigning in the outer scope, I'll prefer this syntax:
useEffect(function() {
  const onWhatever = props.onWhatever;
  if (typeof onWhatever === 'function') {
    onWhatever();
  }
}, [props.onWhatever]);
```

- Uncaught Error: Cannot find module '../../src/components/accordion/Accordion.docs.mdx'
  - webpack 的dynamic import不支持 `import(pathAllVar)`的情况
  - 作为参数的路径必须写一部分出来
  - https://webpack.js.org/api/module-methods/
  - It is not possible to use a fully dynamic import statement, such as `import(foo)`.
  - The import() must contain at least some information about where the module is located. 

- README.md: Support for the experimental syntax 'jsx' isn't currently enabled 
  - 因为workspace的子项目中配置 @mdx-js/loader的babel-loader时，也要设置 `options: { rootMode: 'upward', }, `.

- SassError: expected "{".
  - [SassError: expected "{".](https://github.com/webpack-contrib/sass-loader/issues/867)
  - 注意webpack-merge会自动合并module.rules，所以注意不要在子项目重复写css-loader

- react_devtools_backend.js:2557 Warning: Cannot update a component (`BrowserRouter`) while rendering a different component (`Login`). To locate the bad setState() call inside `Login`, 
  - [v6] Cannot update a component from inside the function body of a different component.
  - https://github.com/ReactTraining/react-router/issues/7199
  - 原因是 `navigate()`没有放在`useEffect()`中

- Conflict: Multiple assets emit different content to the same filename index.html
  - 删掉前面配置文件定义的html-webpack-plugin的配置对象即可
  - 因为使用了 webpack-merge，不同文件的html-webpack-plugin合并后却成了2个，所以要注意某些对象的属性不同不会合并

- Errorr: ENOENT: no such file or directory, open 'build/scripts.js'
  - 若uglify输出的目录不存在，则需要开发者提前手动创建，否则会抛出异常
    - 系统依赖本身也会有依赖，有时难以分析出到底缺哪个包
  - 开发调试时，可将图片优化处理替换为copy
  - [Create output directory](https://github.com/mishoo/UglifyJS/issues/1278)
- 使用jpegtran优化jpg图片的示例
  - `find src/ -name "*.jpg" -type f -exec  jpegtran -copy none -optimize -outfile {} {} \; `
  - `find src/ -type f -exec  jpegtran -copy none -optimize -outfile {} {} \; `
  - 注意，上述命令会原地优化，立即覆盖图片，记得先备份；图片优化后体积可能会变大

- npm err Unsupported platform for fsevents@2.1.3: wanted {"os"
  - [linux下fsevents模块引起的npm ls报错解决办法](https://segmentfault.com/a/1190000018759308)
    - fsevents只能在macOS下安装，无法在linux系统安装。
    - linux下会跳过fsevents模块，也不会安装fsevents依赖的模块。
    - 这其实算是npm的一个bug，npm i时报Warn，npm ls又报Err，前后不一致，容易有误解。
      - 目前无论用哪个版本的npm都会有这个问题，npm i --no-optional也不能解决这个问题。
      - 这些报错不影响项目的正常运行，因为linux不需要fsevents。
    - 如果不希望看到npm Err，可以用`npm i -f`强制安装，
      - 安装过程没有warn，安装完后npm ls可以看到在node_modules目录下了
    - chokidar这个模块依赖了fsevents，chokidar又是browser-sync、webpack等依赖的。

- ENOENT: no such file or directory, scandir '**/node_modules/node-sass/vendor'
  - npm rebuild node-sass

- ide不停的提示
  - Definition for rule '@typescript-eslint/interface-name-prefix' was not found
  - Definition for rule '@typescript-eslint/no-duplicate-imports' was not found.
  - 重启ide后，魔法般地消失了
  - 注意检查rule是否已经deprecate

- git push error
  - git push origin HEAD:main

```

error: src refspec main does not match any
error: failed to push some refs to 'git@github.com:
```

- npm install时的异常
  - did you edit package.json only? if npm-shrinkwrap.json is still there, please remove it or try `npm i -f`
  - https://github.com/angular/angular/issues/13935

```

Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin"} (current: {"os":"linux","arch":"x64"})
```

- ag-grid使用@babel/preset-typescript编译源码时多次碰到的异常

```

agAbstractLabel.ts:48 Uncaught TypeError: Super expression must either be null or a function
    at _inherits (agAbstractLabel.ts:48)
```

- create-react-app 初次创建示例项目时异常
  - 原因是缺少编译node-canvas的环境

```

Downloads/react-cra-es6/node_modules/canvas
npm ERR! command failed
npm ERR! command sh -c node-gyp rebuild
npm ERR! make: Entering directory '/home

../src/backend/../closure.h:6:10: fatal error: jpeglib.h: No such file or directory
npm ERR!     6 | #include <jpeglib.h>

../src/Image.h:18:10: fatal error: gif_lib.h: No such file or directory
npm ERR!    18 | #include <gif_lib.h>

```

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

```JS
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
  - It means that the object has a circular reference, something like: `var a = {}; a.b = a; `
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
  - element.type should be a string or class/function
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
