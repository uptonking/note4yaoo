---
title: lib-viz-base-webgl-community
tags: [community, lib, viz, webgl]
created: '2021-05-20T13:46:26.354Z'
modified: '2021-05-20T13:46:51.503Z'
---

# lib-viz-base-webgl-community

# guide

# discuss-stars

# discuss

- ## 

- ## 

- ## 

- ## 

- ## two.js
- https://news.ycombinator.com/item?id=9897329
- What I am struggling with, is the use case of a library like this.
  - I think the main difference and the selling point is that it is "renderer agnostic" but I don't understand the benefits of that.
- Renderer-agnostic is nice, actually, when you need to support lots of different browsers.
  - Some mobile browsers can't do WebGL as fast as they do Canvas, for instance. Other browsers will have a huge speed advantage with WebGL.
  - being able to do some test renders quickly in all three modes should allow you to select the fastest for a particular browser.
- Game developers are better off with a game-oriented library, IMO. 
  - Even if you used something like two.js to do your rendering, there are a lot of things still useful in a game library to justify using it -- 
  - and most games will need more than geometric figures.
- I love SVG support because it means you can render something in vector art in the browser which is also downloadable as a file by the user. 
  - So here we appear to get the best of all worlds: render to whatever is fastest in the browser but get automatic "export as SVG" for free.
  - We could make an HTML-Canvas-compliant library that renders SVG. (eg, node-canvas)
  - node-canvas can create SVG documents instead of images.
- Awesome...but. No text? That suddenly wipes out my use case (data viz). 
  - Unfortunately, this is a library authored and maintain by one person, me. I'd love to get to text at some point, but until then you'll have to stick with DOM. Also, depending on your renderer you have full access to SVG, Canvas, and WebGL so you can write text with those APIs...
  - Text is actually pretty tricky in WebGL. Lots of ways to do it, all very dependent on your application. I think it would be better to keep it out of the library but allow plugins/etc to compose easily with the rest of two.js.
