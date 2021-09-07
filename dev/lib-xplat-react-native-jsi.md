---
title: lib-xplat-react-native-jsi
tags: [cross-platform, jsi, react-native]
created: '2021-09-07T15:25:31.081Z'
modified: '2021-09-07T15:25:55.522Z'
---

# lib-xplat-react-native-jsi

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## JSI (JavaScript Interface) & JSC (JavaScript Core) Discussion
- https://github.com/react-native-community/discussions-and-proposals/issues/91
  - With this issue I'd like to try and create a "one stop" for all the information available around the JavaScript Interface, the unified lightweight general purpose API for (theoretically) any JavaScript virtual machine.
  - Currently, the default Javascript Virtual Machine used by React Native is JavaScriptCore (JSC) - it is used in WebKit.
- Terminology
  - Fabric: just the UI layer re-architecture, to take full advantage of concurrent React architecture. 
  - TurboModules: re-architecture of NativeModules, also using JSI.  
  - CodeGen: a tool to "automate" the compatibility between JS and native side.  
- Instead of using the bridge for queuing messages, the new architecture allows us to directly "invoke" (think RPC) Java/ObjC methods.
  - An analogy would be how we call DOM methods from JavaScript in the browser. 
  - For example, in the statement `var el = document.createElement('div');` the variable el holds a reference not to a JavaScript object, but to an object that was possibly instantiated in C++. 
  - When JavaScript calls `el.setAttribute('width', 100)` , we end up synchronously invoking the `setWidth` method in C++ that changes the actual width of that element.
  - In React Native, we can similarly use the JavaScript interface to invoke methods on UI Views and Native Modules that are implemented in Java/ObjC.

- 202105: In fact the `JSIExecutor` C++ impl today is already accessing the VM using JSI for a while now. All JSI code is already in github

- ## React native JSI - when?__202101
- https://www.reddit.com/r/reactnative/comments/kqha6k/react_native_jsi_when/
- You got confused about the terms, JSI is not an engine. 
  - It's an interface which enables JavaScript (whether it's JSC or Hermes) to communicate with native (C++) and vice versa. 
  - It replaces the bridge (which currently works by serializing everything to JSON)

- You can use JSI now if you are bold. 
  - It actually works really well and you can write fast code with C++. 
  - Turbo modules and codegen are more hairy tho.
- I'm currently betting on a lot of rearchitecture technologies, and TurboModules is one of them. Writing normal modules works great, but I didn't have any luck creating UI modules yet. Codegen is also far from stable

- Am I right in thinking JSI will break existing plugins?
  - Not until they disable their loading mechanism. You can use JSI modules alongside native modules today. In fact reanimated uses JSI already
