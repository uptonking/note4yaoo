---
title: thread-viz-base-webgl
tags: [thread, web, webgl]
created: '2021-01-08T18:52:59.126Z'
modified: '2021-03-11T11:26:12.335Z'
---

# thread-viz-base-webgl

# pieces

- ## 

- ## just added clock control, @_josh_ellis_ making progress w/ three-test-renderer. 
- https://twitter.com/0xca0a/status/1369775216818323457
  - being able to snapshot scenes, advance frames & events, expect the outcome. 
  - this'll do so much to push webgl into professional front end. 
  - with tests, a11y and small bundlesize, no reason not to
- We are quite happy with the rendering quality of three (r3f), and are now thinking about replacing some product renderings from Blender to automatic headless browser screenshots. Is that what I would want to try for this scenario?
  - These are unit tests, for visual regression tests or automatic images that you create you still need something like puppeteer, a headless browser, but it would be similar. You can look in the current testing folder in v5, it's doing that.

- ## might have found a solution to threejs being way too big 
- https://twitter.com/0xca0a/status/1368122900398637058
  - this is @gordonnl's ogl running through react-three-fiber in a thin wrapper that aliases ogls api into classes that resemble threejs. 
  - it even inherits three types. 
  - ogl clocks in at about 14kb. react 2kb. r3f v6 15-20kb.
- Do you think doing a react ogl fiber renderer is too much of an effort?
  - already parked react-ogl. 
  - with the new v6 infra it will be very easy to do it. though the eco system is mostly empty and that's a concern. 
  - i also like threes architecture a little better, objects are all loose-coupled. the only wart left is the large size tbh.

- ## One of my favorite GLSL things is being able to rearrange vector components. This is a simple JS utility to do just that with three.js
- https://twitter.com/ggsimm/status/1365379890267254784
  - https://codesandbox.io/s/three-swizzle-41d1l?file=/src/index.js
- Also found this by @mattgperry that does it using proxies, which is even better
- https://github.com/mattgperry/vekta
  - A JavaScript vector type with GLSL-inspired swizzling

- ## 90% of award winning sites are webgl enriched experiences that'd be impossible with html/css
- https://twitter.com/0xca0a/status/1355535059684646914
  - for react devs it can be the same level of complexity as forms/routes maybe easier
- sound like hyperbole, but all the demos we've made are testament to that. react gives us sth the webgl space lacked: clean abstraction. 
- you can get by without knowing much math, bc things are shareable and re-usable. like in the flash days you can put ideas on screen rapidly.
- ppl often wonder why react, and not framework x. 
  - bc it set out to abstract platforms from the get go. 
  - threejs is just one of many. 
  - whereas everything else was just worried about the dom.
  -  this is why react devs now get to write webgl apps with the same knowledge they already have.
- if framework x wanted to tackle three, they can wrap it, but it exports 467 symbols, w/ jsm you're probably in the 1000s, maintenance effort would be out of this world, or re-invent the wheel with a new lib w/o community & experts. 
  - ⚛️ has renderers, and renderers are the future.
- if that interests you check out the core of react-three-fiber. in 180 LOC you can make a barebones renderer that lives alongside three peacefully without ever needing updates if three changes/adds/removes things

- ## Apple is proposing a new schema for USD(Universal Scene Description)
- https://twitter.com/donrmccurdy/status/1275186885346746368
- Once again, Apple creating their own schemas instead of improving the open source ones we already have.
  - GLTF is extensible therefore it can easily match the quality of USDZ and work on older implementations as well, making it both quality and compatibility.
- This is due to apple’s advantage in hardware software optimization. 
  - And their “closed” tailor made experiences. 
  - Unfortunately open sourced often comes at the cost of quality.
  - It doesn't have to, it just requires a positive feedback loop that circumstances haven't allowed
  - Given XR is so new we have a chance to establish quality open XR systems.
- AR should fundamentally be about how the virtual interactes WITH the physical environment. The only interaction your video example shows of this is plane detection haha
  - that's a good example, the reflections and diffuse lighting look great. Getting that kind of lighting information from the scene is (as far as I know?) not yet available from the WebXR APIs, and I hope it's added! But it has nothing to do with glTF or USDZ. 
  - It'sthe advantage of having a renderer in a sandbox, and not having to deal with the privacy implications of giving camera information to a website (which WebXR has to be very careful about)
  - On formats: Is delivering 3D experiences with two formats and two engines is harder than having a single out-of-the-box solution? Definitely! And Apple has created a great out-of-the-box solution (for iOS, only)
  - Examples like interactivity, physics, and animation, (IMO) the web actually has an advantage — scripting is built into the platform, and you don't need to wait on standards like glTF to have a scripting API. You can use any 3D engine you want, and your content will work. 
