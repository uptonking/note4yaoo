---
title: pattern-arch-plugin-system
tags: [architecture, pattern, plugin-system]
created: 2020-10-17T13:55:35.958Z
modified: 2020-12-20T15:46:29.566Z
---

# pattern-arch-plugin-system

# guide

- 很多成熟优秀的系统都是插件式架构
  - react hooks
  - vscode
  - eclipse
  - [The Power Of The Plugin Architecture In Python - YouTube](https://www.youtube.com/watch?v=iCE1bDoit9Q)
  - [前端插件式可扩展架构设计心得](https://www.51cto.com/article/675413.html)
# blogs

## [Designing a JavaScript Plugin System](https://css-tricks.com/designing-a-javascript-plugin-system/)

```JS
const betaCalc = {
  currentValue: 0,

  setValue(value) {
    this.currentValue = value;
    console.log(this.currentValue);
  },

  core: {
    'plus': (currentVal, addend) => currentVal + addend,
    'minus': (currentVal, subtrahend) => currentVal - subtrahend
  },

  plugins: {},

  press(buttonName, newVal) {
    const func = this.core[buttonName] || this.plugins[buttonName];
    this.setValue(func(this.currentValue, newVal));
  },

  register(plugin) {
    const { name, exec } = plugin;
    this.plugins[name] = exec;
  }
};

// Our Plugin
const squaredPlugin = {
  name: 'squared',
  exec: function(currentValue) {
    return currentValue * currentValue;
  }
};

betaCalc.register(squaredPlugin);

// Using the calculator
betaCalc.setValue(3); // => 3
betaCalc.press('plus', 2); // => 5
betaCalc.press('squared'); // => 25
betaCalc.press('squared'); // => 625
```

## [Towards a well-typed plugin architecture - Adventures in Typescript](https://code.lol/post/programming/plugin-architecture/)

- [How to Build A Plugin System with TypeScript](https://javascript.plainenglish.io/how-to-build-a-plugin-system-with-typescript-e7efb9f7e1ab)

- [typescript - Extend class with Plugin Architecture - Stack Overflow](https://stackoverflow.com/questions/58600812/extend-class-with-plugin-architecture)

- [I was hoping to implement something similar to this in TypeScript: Plugin Factory.](https://www.reddit.com/r/learnprogramming/comments/8p6pze/typescript_writting_a_simple_plugin_pattern/)

## [Build a Plugin System With Node.js](https://stateful.com/blog/build-a-plugin-system-with-node)

- https://github.com/stateful/blog-examples/tree/main/plugin-system

- This blog post will cover how to build a plugin system from scratch. 
- We’re going to build a CLI application that allows a user to select and apply a text transformation plugin to an entry text.
- Let’s define the main components acting in our plugin system:
  - System Core: Defines the minimum functionalities of the system.
  - System Services: Extended functionalities from the system implemented via plugins.
  - Plugin Manager: Manage the plugin’s lifecycle. It handles the registration and loading of the plugins.
  - Plugin: Represents an independent functionality executed in the context of a system service that extends the system functionality. All the system plugins follow a standard interface.

## [How to roll your own plugin system - slate | jkrsp](https://jkrsp.com/slate-js-plugin-system/)

```JS
// First - let’s assume this signature for our plugins:
type Plugin = (editableProps: EditableProps, editor: Editor) => EditableProps;

export const composeEditableProps = (
  plugins: Plugin[],
  editor: ReactEditor,
): EditableProps => {
  let editableProps: EditableProps = {};
  for (const plugin of plugins) {
    editableProps = plugin(editableProps, editor);
  }
  return editableProps;
};

const editableProps = composeEditableProps([
  defaultPropsPlugin,
  headerplugin
], editor)

type PluginProps = {
  editableProps: EditableProps;
  renderToolbar: () => JSX.Element;
}
```

## [Build A Plugin System — Node.js | Medium | JavaScript in Plain English](https://javascript.plainenglish.io/how-to-build-a-plugin-system-with-node-js-68c097eb3a2e)

- [Complete plugins.js](https://gist.github.com/TheOtterlord/d2babe41cab5e7cbbe989bdd03425391)

```JS
const fs = require("fs");

class Plugins {
  constructor(app) {
    super();
    this.app = app;
    this.plugins = {};
  }

  async loadFromConfig(path = './plugins.json') {
    const plugins = JSON.parse(fs.readFileSync(path)).plugins;
    for (let plugin in plugins) {
      if (plugins[plugin].enabled) {
        this.load(plugin);
      }
    }
  }

  async load(plugin) {
    const path = plugins[plugin];
    try {
      const module = require(path);
      this.plugins[plugin] = module;
      await this.plugins[plugin].load(this.app);
      console.log(`Loaded plugin: '${plugin}'`);
    } catch (e) {
      console.log(`Failed to load '${plugin}'`)
      this.app.stop();
    }
  }

  unload(plugin) {
    if (this.plugins[plugin]) {
      this.plugins[plugin].unload();
      delete this.plugins[plugin];
      console.log(`Unloaded plugin: '${plugin}'`);
    }
  }

  stop() {
    for (let plugin in this.plugins) {
      this.unload(plugin);
    }
  }
}
```

- We’ll define our plugins using an abstract class that is implemented by each plugin.

## [figma: How to build a plugin system on the web and also sleep well at night_201908](https://www.figma.com/blog/how-we-built-the-figma-plugin-system/)

- Attempt #1: The `<iframe>` sandbox approach
  - Problem #1: async/await is not user friendly
- Problem #2: copying the scene is expensive
  - Back to the drawing board, and the main thread
  - Implications of running on the main thread
  - What does it mean for eval to be dangerous?
  - Hiding the global variables
- Attempt #2: Compile a JavaScript interpreter to WebAssembly
- Attempt #3: Realms
  - Implementing the API using Realms securely
- The problem is that building the Figma API directly on top of Realms makes it so that each API endpoint needs to be audited, including its input and output values. The surface area created is too large.
- Despite the fact that code inside the Realms sandbox runs using the same JavaScript engine (and gives us convenient tooling benefits), it still helps to pretend that we live under the restrictions of the WebAssembly approach.

- We now have a sandbox that can run arbitrary plugins safely, and an API that allows these plugins to manipulate Figma documents. This already opens up a lot of possibilities.
- However, the original problem we were trying to solve was to build a plugin system for a design tool. 
  - To be useful, most of these plugins will want the ability to create a user interface, and many will want some form of network access. 
  - More generally, we would like plugins to be able to leverage as much of the browser and JavaScript ecosystem as possible.
- We solve this problem by reintroducing, yet again, the null-origin `<iframe>`. Plugins can create an `<iframe>` (which we show inside the Figma editor as a modal) and put any arbitrary HTML and Javascript in it.

- Conclusion
  - The Realm shim allowed us to isolate third-party code while still letting it run in a familiar browser-like environment.
- While this is the best solution for us, it may not be the right approach for every company or platform.
  - If you need to isolate third-party code, it’s worth evaluating if you have the same performance and API ergonomic concerns as we did. 
  - If not, isolating code via iframes may be sufficient, and simple is always good. We would have liked to stay simple!

### [How to build a plugin system on the web and also sleep well at night | Hacker News](https://news.ycombinator.com/item?id=20770105)

- This is one of the cleverest things I've seen in JS in a while.
  - In a nutshell, they use a same origin iframe to ensure the plugin gets its own copy of globals (so it can't mess up the globals your app uses), coupled with a proxy object which whitelists certain globals for the plugin to use along with certain vars from your app.
  - Really rather clever, although the guys who develop browsers should consider an API for something like this as it's becoming such a common use case.

- The Realms polyfill is a polyfill for an actual TC39 JS proposal [0]. 
  - https://github.com/tc39/proposal-shadowrealm
  - [ES6 Realms API](https://gist.github.com/dherman/7568885)
  - It's currently at stage 3.
  - If the proposal gets accepted, you will not need the polyfill. This would also work with any JS embedding (browsers, node, etc...) as it would be baked in the language.

- Google Gadgets (on the iGoogle custom homepage) used a similar scheme for exposing a select API to untrusted JS running in frames.

## [The Complete Guide to the Fastify Plugin System - NearForm](https://www.nearform.com/blog/complete-guide-fastify-plugin-system/)

- We have seen the Fastify Plugin System and how it works, but why is it not easy to understand?
  - The answer is simple: it is a powerful tool, but it is not easy to control when things become bigger.
- The plugin hell is not wrong, but it makes the code hard to read and understand. This denotes it is less maintainable, and you may be forced to add some global variables to solve some issues.
  - To solve this problem, you can use the fastify-overview plugin to visualize the tree structure and be able to navigate within your code base without any difficulties.
- Thanks to the plugin, you will be able to see the runtime application graph:
  - ALL the Fastify routes
  - ALL the Fastify plugins
  - ALL the Fastify decorators
  - ALL the Fastify hooks

## [精读《插件化思维》](https://github.com/ascoders/weekly/blob/master/%E5%89%8D%E6%B2%BF%E6%8A%80%E6%9C%AF/53.%E7%B2%BE%E8%AF%BB%E3%80%8A%E6%8F%92%E4%BB%B6%E5%8C%96%E6%80%9D%E7%BB%B4%E3%80%8B.md)

- [精读《插件化思维》 - 知乎](https://zhuanlan.zhihu.com/p/35997606)

- 插件化无处不在，所有的框架都希望自身拥有最强大的可拓展能力，可维护性，而且都选择了插件化的方式达到目标
  - 插件化就是将不断扩张的功能分散在插件中，内部集中维护逻辑，这就有点像数据库横向扩容，结构不变，拆分数据。

- 可拓展性体现在这三个方面：
  - 让代码以功能为纬度聚合起来，而不是某个片面的逻辑结构，在代码数量庞大的场景尤为重要。
  - 让社区可以贡献代码，而且即使代码存在问题，也不会影响核心代码的稳定性。
  - 支持二次开发，满足不同业务场景的特定需求。

- 插件化许多都是从设计模式演化而来的，大概可以参考的有：命令模式，工厂模式，抽象工厂模式等等，笔者根据个人经验，总结出三种插件化形式：
  - 约定/注入插件化。
  - 事件插件化。
  - 插槽插件化。

### 约定/注入插件化

> 举例：fis、gulp、webpack、egg。

- 按照某个约定来设计插件，这个约定一般是：入口文件/指定文件名作为插件入口，文件形式.json/.ts 不等，
  - 只要返回的对象按照约定名称书写，就会被加载，并可以拿到一些上下文。

- json 能力很弱，定义函数部分需要单独在 ts 文件中完成，
  - 那么更广泛的方式是直接写 ts 文件，但按照文件路径决定作用，比如：项目的 ./controllers 存在 ts 文件，会自动作为控制器，响应前端的请求。

- 如果功能相对杂乱，没有清晰的功能入口规划，比如 gulp 这种插件，那用对象会更简洁，而且更倾向于用一个入口，因为主要操作的是上下文，而且只需要一个入口，内部逻辑种类无法控制。

- webpack plugin 约定和事件都有，混用也是很常见的

### 事件插件化

> 举例：koa、service worker、dom events。

- 通过事件的方式提供插件开发的能力。
- 比如 dom 事件： document.on("focus", callback); 
- 虽然只是普通的业务代码，但这本质上就是插件机制：
  - 可拓展：可以重复定义 N 个 focus 事件相互独立。
  - 事件相互独立：每个 callback 之间互相不受影响。
- service worker 就更明显，业务代码几乎完全由一堆事件监听构成，比如 install 时机，随时可以新增一个监听，将 install 时机进行 delay，而不需要侵入其他代码。
- 在事件机制玩出花样的应该算 koa 了，它的中间件洋葱模型非常有名，
  - 换个角度理解，可以认为是能控制执行时机的事件插件化，也就是只要想把执行时机放在所有事件执行完毕时，把代码放在 next() 之后即可，如果想终止插件执行，可以不调用 next()

### 插槽插件化

> 举例：gaea-editor

- 这种插件化一般用在对 UI 元素的拓展。
- html 默认布局是物理结构，那插槽布局方式就是 html 中的 redux。

- 这样插件中的代码可以不受物理结构的约束，直接插入到任何插入点。
  - 更重要的是，实现了 UI 解耦，父元素就不需要知道子元素的具体实例。
  - 一般来说，决定一个组件状态的都是其父元素而不是子元素

### 分型插件化

> 举例：egg。

- 特点是插件结构与项目结构分型，也就是组成大项目的小插件，自身结构与项目结构相同。
- 当然不是所有插件都能写成目录分形的

### 核心代码如何加载插件

- 插件注册方式非常多样
  - 通过 npm 注册：比如只要 npm 包符合某个前缀，就会自动注册为插件
  - 通过文件名注册：比如项目中存在 xx.plugin.ts 会自动做到插件引
  - 通过代码注册：这个很基础，就是通过代码 require 就行
  - 通过描述注册：比如在 package.json 描述一个属性，表明了要加载的插件
  - 自动注册：比较暴力，通过遍历可能存在的位置，只要满足插件约定的，会自动注册为插件。

- 确定插件注册方式后，一般第一件事就是加载插件，后面就是根据框架业务逻辑不同而不同的生命周期了，插件在这些生命周期中扮演不同的功能

- 插件之间难免有依赖关系，目前有两种方式处理，分为：依赖关系定义在业务项目中，与依赖关系定义在插件中。
- 依赖关系定义在业务项目中，比如 webpack 的配置，执行逻辑是 ts-loader -> babel-loader，当然这个规则由框架说了算
- 另一种行为，将插件依赖写在插件中，比如 webpack-preload-plugin 就是依赖 html-webpack-plugin。
- 这两种场景各不同，
  - 一个是业务有关的顺序，也就是插件无法做主的业务逻辑问题，需要把顺序交给业务项目配置；
  - 一种是插件内部顺序，也就是业务无需关心的顺序问题，由插件自己定义就好啦。
  - 注意框架核心一般可能要同时支持这两种配置方式，最终决定插件的加载顺序。

- 插件之间通信也可以通过 hook 或者 context 方式支持，hook 主要传递的是时机信息，而 context 主要传递的是数据信息，但最终是否能生效，取决于上面说到的插件加载顺序。
- context 可以拿 react 做个类比，一般都有作用域的，而且与执行顺序严格相关。
- hook 等于插件内部的一个事件机制，由一个插件注册。业界有个比较好的实现，叫 tapable，这里简单介绍一下。

### 核心功能的插件化

- 插件化框架的核心代码主要功能是对插件的加载、生命周期的梳理，以及实现 hook 让插件影响生命周期，最后补充上插件的加载顺序以及通信，就比较完备了。
- 衡量代码质量的点就在于，是不是所有核心业务逻辑都可以由插件完成？因为只有用插件实现核心业务逻辑，才能检验插件的能力，进而推导出第三方插件是否拥有足够的拓展能力。
  - 如果核心逻辑中有一部分代码没有通过插件机制编写，不仅让第三方插件也无法拓展此逻辑，而且还不利于框架的维护。

- 哪些插件需要内置
  - 这个是业务相关的问题，但总体来看，开源的，基础功能以及体现核心竞争力的可以内置

- [插件化架构设计(2): 插件化从设计到实践该考量的问题汇总 - zhoulujun - 博客园](https://www.cnblogs.com/zhoulujun/p/17231013.html)

## more-plugins-blog
- [Discussion: The limits of actions and reducers - discuss.ProseMirror](https://discuss.prosemirror.net/t/discussion-the-limits-of-actions-and-reducers/551/4)
# plugin-examples
- https://github.com/unjs/unplugin /ts
  - Unified plugin system for Vite, Rollup, Webpack, esbuild, and more
  - unplugin is very high level to adapt plugins to bundlers
  - parsing/transforming is still babel

- https://github.com/Webpack/tapable /3.5kStar/MIT/202109/js/inactive
  - The tapable package expose many Hook classes, which can be used to create hooks for plugins.
  - Hook types: basic, waterfall, bail, loop, sync, async
  - interception, context, hookMap, multiHook

- https://github.com/JonasKruckenberg/duck-taps /ts
  - Modular and tree-shakeable Hooks your plugins can tap into 
  - The biggest under-the hood change from tapable is the fact that duck-taps uses hook phases, each hooks can define custom phases that plugins can tap into. 

- https://github.com/gr2m/javascript-plugin-architecture-with-typescript-definitions /js/202107/inactive
  - The goal of this repository is to provide a template for a simple plugin Architecture which allows plugin authors to extend the base API as well as extend its constructor options.
  - This plugin architecture was extracted from `@octokit/core`

- https://github.com/TimoBechtel/krog /ts
  - Add a hooks-based plugin system to your library.
  - krog adds typescript aware hooks to your library to allow for more flexible and powerful plugins.
  - supports async hooks
  - full control over how plugins are configured / loaded

- https://github.com/SkyIsTheLimit/pluggin /ts
  - A library for creating plugin systems.
  - There are 2 types of plugins, a function style plugin and a class style plugin
  - Plugins can be combined in series or parallel.

- https://github.com/rosaric/zhook /ts
  - Tiny hook library, with event dispatcher and filters, mostly for creating plugin system.

- https://github.com/benedyktdryl/apilar-pluggable /ts
  - Simple and light plugins architecture engine with dependencies handling
- https://github.com/bevry/pluginloader /ts
  - A class for loading, verifying, and creating plugins. Used by DocPad for years.
- https://github.com/alcuadrado/ts-plugin-system /ts
  - show how a Node.js plugin system can use TS, while also letting plugins extend the application types.

- https://github.com/rekit/js-plugin /js
  - a general and simple plugin engine for creating extensible and maintainable JavaScript applications for both browser and nodejs.
  - how extension points work. It's pretty simple with two parts:
    - Define/use extension point in an extensible module/component.
    - Define plugin object structure following the extension point.
  - **Every plugin is just a JavaScript object**, normally every path to leaf property means it contribute some extension point.

- https://github.com/e0ipso/plugnplay /202110/js/inactive
  - Plugin system for reusable code in node.js
  - Imagine that you want to use a different logger for your local environment than from the production environment.
  - You want to use console.log in your local and you want to send to Logstash in production
  - Plugins offer several features that you can't easily obtain with require('./some/code')
  - Can all the pluggability resolve at build time? almost

- https://github.com/adaltas/node-plug-and-play /js
  - Easily create hooks and let users plug their own logic across your code to make it extensible by everyone with new features.

- https://github.com/riktar/plerry /ts
  - Plerry is a pluggable system that makes it easy for developers to extend the functionality of their NodeJS applications.
  - To write a plugin for Plerry, create a javascript module that exports a function. 
  - This function will be called with the Plerry instance as an argument, allowing you to register event handlers and access other plugins.

- https://github.com/conversejs/pluggable.js /js
  - https://conversejs.github.io/pluggable.js/
  - a tiny library that lets you make your JS project extendable via plugins, while still keeping sensitive objects and data private through closures.
  - It was originally written for converse.js, to provide a plugin architecture that allows 3rd party developers to extend and override private objects and classes, but it does not require nor depend on either library.

- https://github.com/easeway/js-plugins /201405/js
  - This module is an extension-point based framework for loading plugins, inspired by Eclipse plugin system.
  - A plugin is a library/module providing a few extensions for certain extension-points.

- https://github.com/moonrailgun/mini-star
  - [介绍 | MiniStar](https://ministar.moonrailgun.com/zh-Hans/docs/tutorial/intro)
  - A micro-kernel framework which can pluginize your project. Progressive Migration!
  - mini-star 是一个为实现项目微内核(插件化)前端库，旨在帮助大家能更简单、无痛的构建(或改造成)一个生产可用微内核(插件化)架构系统。
  - 技术栈无关，任意技术栈的应用均可 使用/接入，不论是 React/Vue/Angular/Svelte/JQuery 还是其他等框架。
  - 拓扑依赖排序，防止时序性的问题。
  - 提供了一套完整的cli/runtime/bundler开发链路。
    - 设计是渐进式的, 就算是已有的项目也能一点点进行插件化进程而无需一次完成。
  - [MiniStar 一个用于实现微内核(插件化)架构的前端框架 - V2EX](https://www.v2ex.com/t/781263)

- https://github.com/c9/architect /js/2012
  - A simple yet powerful plugin system for large-scale node applications
  - Each plugin registers itself with Architect, so other plugins can use its functions. 
  - Plugins can be maintained as NPM packages so they can be dropped in to other Architect apps.
- https://github.com/brianreavis/microplugin.js /2013
  - Plugins can declare dependencies to other plugins and can be initialized with options (in a variety of formats). 
  - It's AMD-compatible and it works identically in Node.js and in a browser.

- https://github.com/jalaali/moment-jalaali
  - A Jalaali (Jalali, Persian, Khorshidi, Shamsi) calendar system plugin for moment.js.

- https://github.com/lorry2018/minimajs /201807/js
  - MinimaJs is a OSGi-like, simple yet powerfull plugin framework based on NodeJS.

- https://github.com/codotype/codotype
  - Plugin-based framework for generating custom boilerplate code and scaffolding
  - 类似代码生成器

- https://github.com/azu/JavaScript-Plugin-Architecture
  - The purpose of this book is to learn the implementation of the plugin architecture in JavaScript and the libraries and tools that make up its ecosystem.
  - 分析了 jquery、eslint、redux、gulp

- https://github.com/jameswilddev/shanzhai
  - A crude, plugin-based plugin system built upon NodeJS.

## dynamic-modules

- https://github.com/microflows/nodeVM
  - Dynamically load and run JS module from remote for the Browser or Node.js.
  - Lazy Load Modules to keep initial load times down and load modules just in time, similar to Webpack's code splitting.

- https://github.com/daangemist/superplug
  - A generic purpose plugin loading system to be used in node projects. 
  - It uses npm modules and annotations in package.json to easily set up a project with plugin support. 
  - It is fully Promise-based.

- https://github.com/mortalYoung/plugin-system
  - A mock simple plugin system for learning
  - This is a repository refer to umi.

## plugin-react

- react-table.v7的plugin存在的问题是rerender过多

- https://github.com/GeekyAnts/react-pluggable
  - https://react-pluggable.github.io/
  - 插件基于IPlugin接口，给出的例子基于class实现
  - With React Pluggable, we can think of our app as a set of features instead of a set of components
  - A plugin can be added or removed by a single line (which is perfect for A/B testing)

- https://github.com/cawfree/redacted
  - A plugin architecture for React.

## iframe

- https://github.com/elijahgreen/plugin-frame
  - plugin-frame is a library for running untrusted code in a sandboxed iframe.

- https://github.com/krakenjs/zoid
  - Cross domain components
  - Render an iframe or popup on a different domain, and pass down props, including objects and functions
# discuss
- ## 

- ## 

- ## [How to design a pluggable system in functional style? - Stack Overflow](https://stackoverflow.com/questions/29069095/how-to-design-a-pluggable-system-in-functional-style)
- Functional programming is all about the explicit composition of functions. No magic. If you need plugins, compose functions by some configuration. That's all.
  - OK, that's not all. You were asking about handling the state.
  - In FP programming, you have only two options.
  - 1) Manual partial application as Mark described.
  - 2) Automatic partial application by Reader, State, or some another monad.
  - Via monad, core functions can be pure, while dangerous state is handled by monad itself.

# ref
- [The Architecture of Open Source Applications](http://aosabook.org/en/index.html)
  - 500 Lines or Less

- [如何设计一个JavaScript插件系统，编程思维比死磕API更重要](https://zhuanlan.zhihu.com/p/211072788)

- [前端开发，如何优雅的实现这样一个插件机制？](https://www.zhihu.com/question/294560351)
