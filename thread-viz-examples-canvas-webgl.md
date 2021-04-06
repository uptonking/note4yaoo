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

- ## Infinite tiles in an Infinite zoom-loop.
- https://twitter.com/MattDzugan/status/1379229467227398144
  - pushing and pulling the cubes 方块自动移动拼接的效果
  - [Cube Pushing Loop notebook ](https://observablehq.com/@mattdzugan/cube-pushing-loop)

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
