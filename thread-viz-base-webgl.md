---
title: thread-viz-base-webgl
tags: [thread, web, webgl]
created: 2021-01-08T18:52:59.126Z
modified: 2021-03-11T11:26:12.335Z
---

# thread-viz-base-webgl

# guide
- ## [Why WASM is not the future of Babylon.js](https://babylonjs.medium.com/why-wasm-is-not-the-future-of-babylon-js-5832b09c9b10)
  - What about WebGPU? Webgpu can be seen like webgl3. so no difference

- https://github.com/observablehq/stdlib
  - If you are using WebGL (rather than 2D Canvas), you should use `DOM.canvas` or the html tagged template literal instead of `DOM.context2d`.

- ## [Two.js released](https://news.ycombinator.com/item?id=9897329)
- What I am struggling with, is the use case of a library like this.
  - Is this oriented towards gaming or substitute something like d3.js or is it has a simplier api, for the developer than other libraries. 
  - Or is it a library to showcase the cool stuff that can be done with new technologies.
  - I think the main difference and the selling point is that it is "renderer agnostic" but I don't understand the benefits of that.
- Renderer-agnostic is nice, actually, when you need to support lots of different browsers.
  - Some mobile browsers can't do WebGL as fast as they do Canvas, for instance. Other browsers will have a huge speed advantage with WebGL.
  - being able to do some test renders quickly in all three modes should allow you to select the fastest for a particular browser.
  - Game developers are better off with a game-oriented library, and most games will need more than geometric figures.
- I love SVG support because it means you can render something in vector art in the browser which is also downloadable as a file by the user. Drawing stuff in the browser which is then stuck there is cute but lacks an important layer of interoperability with the rest of the computing ecosystem. So here we appear to get the best of all worlds: render to whatever is fastest in the browser but get automatic "export as SVG" for free.
  - We could make an HTML-Canvas-compliant library that renders SVG. node-canvas
- Even Dojo Toolkit's dojox.gfx from 2007 supported multiple rendering contexts: SVG, canvas, VML, Silverlight.
- I notice that this can render ThreeJS objects. Any reason to construct and object with ThreeJS and render it with Two?
  - No no, you can create shapes and render/extrude them in Three.js. The puzzle piece in this example is a 2D path made in Two.js and then extruded in Three.js
- As someone using D3.js a lot (even for a puzzle game) - what is the benefit of using Two.js? Jumping between SVG and Canvas? (But then, is it worth the price of reducing possibilities to circles and squares?)
  - You can do quite a bit with "circles and squares". Two.js focuses on Path drawing and has robust SVG interpretation for complex vector shapes.
  - I've found the portability to be fantastic. For instance http://patatap.com runs svg on iOS and canvas on Android. Two.js makes it simple to run either on the fly.
- An alternative library that is Canvas only but works well with input is ZRender
- Awesome...but. No text? That suddenly wipes out my use case (data viz). I was super encouraged reading this post, multiple renderers including canvas / webgl (so I assume speed - unlike D3), smart, clean, indeed creative looking logo/site...suggests the author has taste...but no text kills this for me. I see no obvious use case for animated 2d that does not do textures (personally happy to do without) but also does not do text.
  - Unfortunately, this is a library authored and maintain by one person, me. I'd love to get to text at some point, but until then you'll have to stick with DOM. Also, depending on your renderer you have full access to SVG, Canvas, and WebGL so you can write text with those APIs...
- Text is actually pretty tricky in WebGL. Lots of ways to do it, all very dependent on your application. I think it would be better to keep it out of the library but allow plugins/etc to compose easily with the rest of two.js.
  - Maybe the author could utilize some npm modules to enable this. https://github.com/mattdesl/text-modules
# babylon
- ref
  - https://twitter.com/search?q=babylon%20(from%3A0xca0a)&src=typed_query&f=live
# discuss-stars
- ## Is there at TWO JS counterpart to THREE JS
- https://stackoverflow.com/questions/11456758
- pixi.js was released just recently - it's a 2D engine backed by WebGL for performance, but with a 2D canvas fallback for compatibility. I haven't used it myself but it's worth checking out.
  - The API also seems to be very inspired by three.js
- ivank.js is more complete , it also uses webgl(fallback to canvas or Dom) , I am testing it right now and it have alot of events (click , drag ) and vectors. It seems more complete
  - http://lib.ivank.net/
# discuss
- ## 

- ## 

- ## Trying to compile https://github.com/madmann91/bvh to WASM to speed up the BVH building and tracing. No suprises it fails to render...again
- https://twitter.com/pissang1/status/1645338783615950853
- I’m using the bvh implementation in https://github.com/hoverinc/ray-tracing-renderer . It’s already very fast. But I’m wondering if WASM with threading can bring it to another level. I think I will benchmark these approaches in the future.

- ## a self-contained WebGL flexbox layout engine, called Red Otter (otters are cute, red cars are fast).
- https://twitter.com/tchayen/status/1638651222742691842
  - It's a combination of: canvas-like WebGL renderer, TTF file parser, text rendering engine based on the SDF method, flexbox layout engine very very similar to Yoga (the one that powers React Native), and JSX support achieved by cheating IDEs to think that I am writing React.

- What's the performance like compared to web rendering?
  - I haven’t done any comparisons yet but it might be quite interesting.
- Why it could be faster:
  - Way less overhead (no DOM), 
  - Potentially faster rendering (full CSS implementation requires supporting a lot of legacy stuff that might involve CPU rendering…
- on the other hand I made a very restricted system that does literally one GPU draw call for the whole UI and all styling is GPU-computed. I bet there’s a huge potential to optimize array operations around it.
- Why it could be slower?
  - It’s written in TS.
- I will at some point try rewriting part of it as a WASM module (potentially a huge win for the layout construction part) but on the other hand all GPU calls have to bridge back from WASM to JS which increase overhead a bit. Code should be structured carefully.

- ## Chromium has queryLocalFonts API to list all available local fonts. 
- https://twitter.com/pissang1/status/1629819868286709760
  - It's strange I didn't notice it when I started this project and looking for something similar... #webgl

- ## there was always something unfriendly about node editors, @splinetool saw that and used a more design oriented approach: layers. 
- https://twitter.com/0xca0a/status/1504140883167703044
  - now @CantBeFaraz made this into an oss lib, think of lamina as tailwind for shaders.
  - https://github.com/pmndrs/lamina
  - https://codesandbox.io/s/lamina-1-x-ledhe1
- with nodes you didn't have to know shaders, but it's still atomic & takes some skill. 
  - with layers you work in a confined, visual env, you blend pluggable abstractions like depth, gradient etc. 
  - these are simpler to configure and do one thing only. more will be added, PR's welcome!

- ## RIP to AWS Sumerian, which was officially laid to rest yesterday. 
- https://twitter.com/visageofscott/status/1496263200786239492
  - @babylonjs is now the officially recommended migration destination of Sumerian users, making babylon the suggested engine for both AWS and Azure customers.

- ## Just released v2 of TinySDF, my ~1.2kb browser-side SDF font generator (useful for rendering crisp scalable text in WebGL) 
- https://twitter.com/mourner/status/1440713101049929745
- Can this be used on labels on maps? Trying to understand the use cases for this better.
  - Yes. Currently it’s being used in Mapbox GL JS to render Chinese/Japanese/Korean labels locally, as there have too many glyphs to download SDFs from a server (which happens for other languages)
  - Ah thanks for the explanation.  I could see you could maybe use something like this to render dynamic data driven symbols.  Eg and arrow pointing in a specific direction

- ## With the next major release of react-three-a11y, I want full WebGL user interface to become a thing.
- https://twitter.com/AlaricBaraou/status/1418879357679030278
- WebGL is difficult to work with
  - Libraries like three.js or Babylon.js made working with WebGL way easier, but only when it comes to displaying animated 3D computer graphics inside a canvas.
- Your canvas isn't accessible, you have no layout system, no search engine support etc
  - Achieving the same level of features/support would take a lot of work/time, which is not realistic for a single website.
- I'll give examples that works with react-three-fiber because AFAIK it's the only ecosystem that have all this things.
- Layout: react-three-flex
  - Organise your canvas content with flexbox
- Accessibility:react-three-a11y
  - Tab index and keyboard navigation
  - Focus indication
  - Screen reader support
  - Roles and cursor shapes
  - Descriptive links
- Accessible text: troika-three-text
  - Comes with support for text selection, copy, live browser translation(WIP)
- SEO and speed optimisation: react-three-next
  - Combined with the previous libraries, the server side rendering could allow the page to be loaded with full semantic HTML for better SEO.
- At this point it looks like that If you're working with react-three-fiber, you have everything you need to make an accessible WebGL UI that would have 99% of the features that a classic HTML based page has.
- So why even with all that we don't see any WebGL UI yet ?
  - Well most of the issues come from the way the current version of react-three-a11y works.
  - Regarding SEO, the HTML generated by react-three-a11y is reliant on the WebGL context, which means that it won't be generated for search engine crawlers.
  - Regarding accessibility too, while react-three-a11y brings a lot of accessibility, it doesn't give the option for the developer to use semantic HTML to its full extent.
  - Things like a list inside a `<nav>` inside a `<header>` aren't supported yet, while essential for screen readers.
  - Again on accessibility, you have no possibility to mix the HTML generated by react-three-a11y with existing HTML in order to have it in the right order in the dom.
  - You also can't use any kind of inputs or select yet.
  - All of this obviously make full WebGL UI a bad choice for now
- But I might have good news soon, I'm working on fixing all those issues in the next major release of react-three-a11y.

- ## from unity to r3f, three and nextjs" — i know the web is far from being as powerful as native, 
- https://twitter.com/JDihlmann/status/1407733892564631555
  - but the possibilities that are opening up to reach broad audiences with visual experiences like that, that is still amazing to me
  - 场景展示的动画，web太强了
  - Today I want to share our one year dev progress from #unity to #r3f #threejs #nextjs. 
  - https://saysom.app/
- https://twitter.com/0xca0a/status/1407775411384225795

- ## can react outperform threejs? updated my old scheduler test for r3f v6
- https://twitter.com/0xca0a/status/1383165072554532865
- now let's see how react handles the same amount of data in concurrent mode. distributed. and at once. 
- i believe react is still behind most frameworks when it comes to base read/write ops. 
  - but at this point it's the only one that can balance load which often is the real bottleneck.

- ## #MicrosoftMesh is also coming to WebXR! Though @babylonjs and React Native. Awesome!
- https://twitter.com/worksalt/status/1369533623636881408
- Would there be a JavaScript lib that is not dependent on a specific framework? It would help to use it in other web frameworks
  - React Native code is ReactJS, ReactJS can be used on the web as well. React Three Fiber (r3f) is the best integration of React and Threejs that I have seen so far. Its the basis of React XR, and mobile apps made with r3f can run at native speed thanks to React Native.
  - I bet that building support for Babylon Native & React Native first for maximum on device performance was the driving factor for this being Microsoft's focus.

- ## With Babylon.js 4.2 releasing on 2020-11-12, you'll be able to use Babylon on React Native to power your cross-platform 3D apps! Code once, deploy everywhere!
- https://twitter.com/0xca0a/status/1314867358918475777
- i have only ever used three, but babylon building on RN to get onto native mobile (and desktop some day), with microsoft being behind react-native-windows and macos, that's pretty radical!
- Babylon RN is actually built on top of Babylon Native, which is a bit different from Expo. Rather than polyfilling WebGL, we shim the engine layer and translate the shaders to run natively per platform: DirectX, OpenGL, and Metal (Vulkan WIP). It's pretty fun stuff!

- ## Even WebGL is being translated into native GL by Expo & Babylon. Rendering(not web) is the future.
- https://twitter.com/0xca0a/status/1345523434487488520
  - Everything seems to point towards a future where platforms converge, or simply do not matter, where browsers are just render targets. 
  - Imo "rendering" is the future, not having to rely on a fat Chrome for "web apps".
- Browser: a native polyfill
- Yes the web platform is just another render target 
  - but its still the best way to reach users on every platform, everywhere, outside walled-gardens and with a standard API.
- i think that's now changing. the web is absolutely not the best medium to reach users on mobile, they prefer apps, always will, 
  - and it's a quite heavy compromise on desktop, too (electron). 
  - i'd be glad if the web is for web-pages and acts as a transpile target for x-platform apps
  - Many of my clients now use WebView in React Native containers. Social login is the only native part. Even Apple Pay is in the web part. As always, hybrid can be a good compromize.
- [expo-gl pkg](https://github.com/expo/expo/tree/master/packages/expo-gl)
- [Babylon Native](https://github.com/BabylonJS/BabylonNative)

- ## React community jumping on the WebGL bandwagon 
- https://twitter.com/0xca0a/status/1290243186019971072
- threejs的下载量远超其他方案
- aframe is based on three, you install it, three comes along. 
  - r3f more or less *is* three, that is, it's just a different way to express it + some utilities. 
  - the only one that competes with three is babylon. 
  - three gets ~400k hits/week, so all these results turn into a flat line 

- ## WebGL Frameworks: Three.js vs Babylon.js 
- https://twitter.com/reddotblues/status/1306581610440134656

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
