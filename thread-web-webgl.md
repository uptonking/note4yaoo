---
title: thread-web-webgl
tags: [thread, web, webgl]
created: '2021-01-08T18:52:59.126Z'
modified: '2021-01-08T18:53:25.244Z'
---

# thread-web-webgl

# pieces

- ## 

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