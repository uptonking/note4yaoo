---
title: thread-viz-examples-canvas-webgl
tags: [canvas, examples, thread, viz, webgl]
created: '2021-03-24T10:24:38.895Z'
modified: '2021-04-04T14:43:15.420Z'
---

# thread-viz-examples-canvas-webgl

# pieces

- ## 

- ## 

- ## 3d房间动画
- https://twitter.com/0xca0a/status/1522312934864879616

- ## 奥运会游泳比赛过程在新闻中以动画示例方式重现
- https://twitter.com/Rich_Harris/status/1424016284073738244
- is this a video or something developed with a web framework and SVG animation?
  - all real-time - it's @threejs plus @sveltejs
- are the videos (i.e. on twitter) rendered out as frames using node-canvas? or screen recorded? or some other witchcraft?
  - Going to blog about it next week, but we have a messy SvelteKit app with an admin page with a bunch of renditions - we click a button, it screenshots them one frame at a time then feeds them to `ffmpeg-wasm` , then posts the resulting mp4 to a slack thread for social editors to use
- I do something similar for a project, and use `puppeteer` to grab screenshots
  - It's just using canvas.toBlob (for the webgl layer and again for the overlay, then composited on a third canvas) then writing the data to ffmpeg's virtual fs
- Paywalled

- ## New side project featuring some AIs from cool movies! 
- https://twitter.com/lorismat_/status/1393932200530358276
  - https://www.lorismat.com/almosthumans
  - 线条动画构建文字的过程，源码是纯html网页，未混淆

- ## replicating amazing noisy stripy look from beautiful @leonard_agency website with @threejs
- https://twitter.com/akella/status/1391401430741921794
  - 人脸由黑白变彩色
  - https://www.youtube.com/watch?v=_qJdpSr3HkM

- ## Drag & drop with 50'000 objects using instanced meshes. 
- https://twitter.com/flavioschneide/status/1387152027143360516
  - In the process of making this even more declarative - this shouldn't be possible in a web browser. 
  - @reactjs + @threejs_org + R3F + React Spring
  - write a custom gesture control for D&D
  - https://codesandbox.io/s/drag-and-drop-instanced-meshes-lwd1r

- ## CPC Scrolling with Three.js & GSAP 
- https://twitter.com/shunyadezain/status/1383367473114742789
  - https://codepen.io/shunyadezain/pen/RwKBZBd
  - 屏幕画面从远到近扑面而来的效果

- ## Tetris made with @babylonjs and AmmoJS Physics.
- https://twitter.com/HiteshSahu_/status/1319177977297539073
  - https://codepen.io/hiteshsahu/pen/LYZbjGq
  - 用积木方块构建城市的效果

- ## @github 's new Skyline feature is built with Babylon.js!
- https://twitter.com/babylonjs/status/1362469058310938627
  - let's you see your contributions in as a beautiful city skyline!
  - https://skyline.github.com/

- ## Infinite tiles in an Infinite zoom-loop.
- https://twitter.com/MattDzugan/status/1379229467227398144
  - pushing and pulling the cubes 方块自动移动拼接的效果
  - [Cube Pushing Loop notebook ](https://observablehq.com/@mattdzugan/cube-pushing-loop)

- ## Infinite Zoom Cubes 方块自动拼接
- https://twitter.com/MattDzugan/status/1381613290036588546
  - [Cube Swivel Loop ](https://observablehq.com/@mattdzugan/cube-swivel-loop)

- ## mixing html+webgl couldn't be any easier, there's literally no code, just declaration. they share the same graph & state. 
- https://twitter.com/0xca0a/status/1374515365875650567
  - the example uses antd UI components, dropped into a threejs scene like it's nothing.
  - https://codesandbox.io/s/r3f-basic-demo-forked-kjil2?file=/src/App.js
  - [here](https://codesandbox.io/s/r3f-basic-demo-forked-7ucso?file=/src/App.js) is another where both html and webgl share the same state model
- Haven’t we had forms on cubes in static vanilla html+css for the better part of a decade?
  - its not about cubes and forms. its about composition. 
  - this technique is mostly used for annotation in 3 space scenes, but it's complicated and forces people to maintain and render two separate scenes. 
  - this makes it accessible to anyone with ease and it's more effective/performant
- that is not HTML
  - anything within `<Html>` is reconciled to html. the header is an h1 for instance in that demo, antd are dom/html components
- Nice! I guess it must be a CSS transform using the matrix computed for the plane, so the HTML layer is not really in the same scene (e.g. it can’t receive shading)
  - exactly. it's mostly being used for light annotations.
