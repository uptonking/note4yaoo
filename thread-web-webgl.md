---
title: thread-web-webgl
tags: [thread, web, webgl]
created: '2021-01-08T18:52:59.126Z'
modified: '2021-01-08T18:53:25.244Z'
---

# thread-web-webgl

# pieces
 

- ## Apple is proposing a new schema for USD(Universal Scene Description)
- https://twitter.com/donrmccurdy/status/1275186885346746368
- Once again, Apple creating their own schemas instead of improving the open source ones we already have.
  - GLTF is extensible therefore it can easily match the quality of USDZ and work on older implementations as well, making it both quality and compatibility.
- This is due to apple’s advantage in hardware software optimization. 
  - And their “closed” tailor made experiences. 
  - Unfortunately open sourced often comes at the cost of quality.
  - It doesn't have to, it just requires a positive feedback loop that circumstances haven't allowed. 
    - Given XR is so new we have a chance to establish quality open XR systems.
- AR should fundamentally be about how the virtual interactes WITH the physical environment. The only interaction your video example shows of this is plane detection haha
  - that's a good example, the reflections and diffuse lighting look great. Getting that kind of lighting information from the scene is (as far as I know?) not yet available from the WebXR APIs, and I hope it's added! But it has nothing to do with glTF or USDZ. 
  - It'sthe advantage of having a renderer in a sandbox, and not having to deal with the privacy implications of giving camera information to a website (which WebXR has to be very careful about)
  - On formats: Is delivering 3D experiences with two formats and two engines is harder than having a single out-of-the-box solution? Definitely! And Apple has created a great out-of-the-box solution (for iOS, only)
  - Examples like interactivity, physics, and animation, (IMO) the web actually has an advantage — scripting is built into the platform, and you don't need to wait on standards like glTF to have a scripting API. You can use any 3D engine you want, and your content will work. 
