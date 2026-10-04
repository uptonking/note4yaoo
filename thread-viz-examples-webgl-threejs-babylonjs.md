---
title: thread-viz-examples-webgl-threejs-babylonjs
tags: [babylonjs, examples, react-three-fiber, thread, threejs, viz]
created: 2021-08-07T16:43:46.584Z
modified: 2021-08-07T16:44:32.377Z
---

# thread-viz-examples-webgl-threejs-babylonjs

# guide

- threejs vs babylonjs
  - https://npm-compare.com/babylonjs,three/#timeRange=ALL
# repos
- https://github.com/brunosimon/my-room-in-3d
  - https://my-room-in-3d.vercel.app/
  - 依赖three、gsap
  - 房间的电视机在播放，电脑在操作，非常逼真
# discuss-threejs
- ## 

- ## 

- ## 

- ## 

- ## 我相信通用游戏引擎会被 ThreeJS 淘汰。现在日常刷屏的酷炫 web 游戏 demo，正是 AGI 时代内容创作的起点。
- https://x.com/ewind_dev/status/2106531299817324871
  - 通用引擎是软件产能匮乏时代的产物：定制太贵，只能将能力不断堆进一个大而全的系统。AI 正在让垂直引擎和专用渲染管线变得廉价，很多所谓引擎能力拆开看，无非是可以按需重建的 pipeline。
- 你这是都不怎么玩3A游戏的人吧。V8虽然可以全JIT执行，但js动态类型等特质就注定了它不可能和C#在同一个性能纬度上，尤其是对渲染管线至关重要的多线程能力。
- 执行效率还是低

- 真正可能被淘汰的不是游戏引擎，而是“先造一个通用引擎，再让所有人适配它”的生产方式。AI把定制成本打下来后，未来可能是需求出现了，专用引擎才随之生成。

- 可是threejs也不是最优解，还可以再拆分。我觉得最终是围绕WebGPU协议的可组合工具形成的生态。

- ## to discover that something was made with pmndrs libraries, fiber in this case, still gives me thrills. whoever did this site is a beast.
- https://twitter.com/0xca0a/status/1743029701520642318
  - [KidSuper World - landing.love](https://www.landing.love/sites/kidsuper/)

# discuss
- ## 

- ## 

- ## 

- ## Over the past few month I experimented building beautiful shaders of cloudscapes with Volumetric Raymarching
- https://twitter.com/MaximeHeckel/status/1719372655923486966
  - [Real-time dreamy Cloudscapes with Volumetric Raymarching](https://blog.maximeheckel.com/posts/real-time-cloudscapes-with-volumetric-raymarching/)

- ## I feel like `@react-three/fiber` is *almost* what I want. 
- https://twitter.com/JungleSilicon/status/1645699043388170242
  - I want a data-driven version of Three JS, but I'd like Three JS to be ejected from React and have React update based on changes to the internal state.
- Check out pex-renderer@4. Maybe that's something for you? Sill alpha but used in production already. PBR capable and ECS driven. Happy to answer any questions.
- isnt this how it works? three is separated from react and functions and renders on its own, react is never involved until that moment when the data model changes, where it quickly updates threejs classes and goes idle again.
  - Yeah but I don’t want to declare the scene graph within React. I just want to be able to render data as properties.
  - It’s the opposite of what I want, I want to use non-react state management to drive the application and have react respond to it.
- imo that makes little sense. the component graph is what allows you to ... react, this is what react is for. you can of course use any state management implementation, but all it will do is complicate and slow down matters. react is very efficient in figuring out what updates.
  - if you divide threejs & react and let three run imperatively, you let two antagonistic worlds compete against one another, one imperative and update driven one declarative and state driven. it would be like making a part of your app run w/ queryUpdates and appendChild.
  - this isn't to say imperative three has no use, that's what useEffect/layoutEffect/useMemo is for, but if you want it completely imperative, imo react isn't what you want at all, it would conflict with its purpose.
- I’m going to agree to disagree here. I barely want to use React in the application. I’m just using it for a property inspector. I’m driving the code by a networked ecs.
  - It sounds like you want to .listen() to property changes (outside of react), have a single object in which you write these updated values, and explicitly call ReactDOM.render with the object as props every time listen() fires.

- Sounds similar to what  we've been building at Ethereal Engine. High performance ECS with btitECS wrapped in hookstate & react for reactive declarative logic - all data oriented. Threejs logic sits mostly in component reactors and systems.

- I’ve also struggled with this when making a game like runtime on top of r3f. I haven’t settled yet on a solution. Miniplex is the best ECS/react/r3f hybrid thinking of seen so far
- miniplex will normalise (real) games in react. @hmans is hashing it out still, but you'll see things next year you wouldn't have thought are possible that easily. it's a new interpretation of ECS (entity component system), mixing it with react semantics. 

- ## an interactive visualization of the major languages in the world using #threlte.
- https://twitter.com/DataVizStefan/status/1642394779991547904
  - 3d条形图

- ## Experimenting with #threejs is a fun.
- https://twitter.com/dotAadarsh/status/1621906462770626560
  - https://dotaadarsh.github.io/Null-Polaroid/
  - 多种视图切换，table/grid/sphere/helix
  - https://github.com/dotaadarsh/Null-Polaroid

- ## beating heart
- https://codepen.io/Mamboleoo/pen/YzQzQgo
  - 类似心型软糖

- ## Photo to 3D RGB Model using @threejs .
  - https://observablehq.com/@analyzer2004/photo-to-3d-rgb-model
  - 任意照片都可以执行颜色形式的形变
