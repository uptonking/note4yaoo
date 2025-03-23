---
title: toc-lib-animation
tags: [animation, lib, toc]
created: 2020-08-02T07:25:52.024Z
modified: 2020-10-05T06:22:02.107Z
---

# toc-lib-animation

# guide

- ref
  - [react-spring vs react-motion vs gsap vs framer-motion vs animate.css vs animejs](https://www.npmtrends.com/react-spring-vs-react-motion-vs-gsap-vs-framer-motion-vs-animate.css-vs-animejs)
  - [Pose is deprecated in favor of Framer Motion__202001](https://popmotion.io/blog/20200115-pose-is-deprecated/)
# animation-with-flip
- flipping /MIT/1.1kStar/202006
  - https://github.com/davidkpiano/flipping
  - https://codepen.io/davidkpiano/pen/xLKBpM
  - A library (and collection of adapters) for implementing FLIP transitions.
  - [Animating Layouts with the FLIP Technique](https://css-tricks.com/animating-layouts-with-the-flip-technique/)
- react-flip-toolkit /MIT/2.5kStar/202007/ts
  - https://github.com/aholachek/react-flip-toolkit
  - https://codesandbox.io/s/list-transitions-ju549
  - A lightweight magic-move library for configurable layout transitions
  - depends on rematrix, to create and combine matrix transformations that work seamlessly with CSS.
  - use transformation matrices under the hood to describe rotation, translation, scale and shear. 
- react-overdrive /MIT/3kStar/202003
  - https://github.com/berzniz/react-overdrive
  - https://react-overdrive.now.sh/
  - Super easy magic-move transitions for React apps
- react-flip-move /MIT/3.2kStar/202003/inactive
  - https://github.com/joshwcomeau/react-flip-move
  - http://joshwcomeau.github.io/react-flip-move/examples
  - Effortless animation between DOM changes (eg. list reordering) using the FLIP technique.
  - Flip Move uses the FLIP technique to work out what such a transition would look like, and fakes it using 60+ FPS hardware-accelerated CSS transforms.
  - Flip Move was inspired by Ryan Florence's awesome [Magic Move/2016](https://github.com/ryanflorence/react-magic-move)
# waapi/web animations api
- https://github.com/motiondivision/motionone /ts
  - https://motion.dev/
  - Motion One is the smallest fully-featured animation library for the web.
  - It can animate HTML or SVG elements using the Web Animations API, which means some animations can run off the main thread.
  - Additionally, it can animate anything by passing it a custom function, like innerText or Three.js.

- https://github.com/inokawa/react-animatable
  - composable animation library for React, built on Web Animations API and React hook.

- @okikio/animate
  - https://github.com/okikio/native/tree/master/packages/animate
  - https://okikio.github.io/native/demo/animate.html
  - 提供的示例包括形变动画、轨迹动画、多运动目标动画
  - It utilizes the Web Animation API to deliver butter smooth animations at a small size, it weighs ~11.6 KB

- use-web-animations /MIT/622Star/202007
  - https://github.com/wellyshen/use-web-animations
  - https://use-web-animations.netlify.app/
  - hooks for highly-performant and manipulable animations using Web Animations API.
- https://github.com/shoelace-style/animations
  - Your favorite animate.css effects available as ES modules for use with the Web Animations API.
  - This module was built for Shoelace, but it works well as a stand-alone library too!
  - This script parses all animation stylesheets found in node_modules/animate.css and generates keyframe objects that you can use with the Web Animations API.
  - As animations are tweaked and added to animate.css, the keyframes herein will be kept in sync when rerunning the script.
- web-animations-js /Apache2/3.4kStar/201906
  - https://github.com/web-animations/web-animations-js
  - http://web-animations.github.io/
  - JavaScript implementation of the Web Animations API
  - https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API
- animations.js /3Star/MIT/202006
  - https://github.com/robertoentringer/animations.js
  - Web Animations API based in Animate.css
# animation-editor
- https://github.com/motion-canvas/motion-canvas
  - https://motion-canvas.github.io/
  - Web-based tool for creating animations programmatically
  - consists of two main components:
    - A TypeScript library used to program animations.
    - An editor providing a real-time preview of said animations.
  - It's a specialized tool designed to create informative vector animations and synchronize them with voice-overs. 
  - It's not meant to be a replacement for traditional video editing software.

- https://github.com/AndrewPrifer/framer-motion-theatre /MIT/202407/ts/inactive
  - Toolset for creating animated React components built on Theatre.js and Framer Motion
  - Seamlessly integrate Theatre.js with Framer Motion and React and get the best of Theatre.js' animation sequencer and React's declarative API. 
  - 👉🏻 Animate Framer Motion's motion values using Theatre.js, and have all the complexity like sheets, objects, animation instancing and wiring taken care of. 
  - Automatically get WYSIWYG editing tools with 1 line of code.
  - While Theatre.js provides a framework-agnostic toolset, its concepts map directly to React and Framer Motion.

- https://github.com/theatre-js/theatre /11.5kStar/apache2/202401/ts/inactive
  - https://www.theatrejs.com/
  - Motion design editor for the web
  - Theatre.js is an animation library for high-fidelity motion graphics.
  - ⛏ Theatre.js can be used both programmatically and visually.
  - Animate 3D objects made with THREE.js or other 3D libraries
  - Animate HTML/SVG via React or other libraries
  - https://github.com/theatre-js/theatre/tree/main/packages/dataverse
    - Dataverse is the reactive dataflow library Theatre.js is built on. 
    - It is inspired by ideas in functional reactive programming and it is optimised for interactivity and animation.
  - [Our plan to make Theatre.js Local-First _202407](https://github.com/theatre-js/theatre/issues/492)
    - Theatre.js 0.8 (upcoming) supports real-time collaboration similar to GDocs and Figma.
    - Local-first removes the lock-in of a central server (although Theatre's server is also open-source). It also simplifies our backend and reduces maintenance costs.
    - But since local-first sync algorithms (CRDTs) haven't yet matured enough for creative apps, we decided to start with a server-ful approach and gradually transition to local-first.
    - Our server-ful implementation is called Saaz. Saaz' algorithm is a simple tree of registers, which allows us to gradually bring in domain-specific CRDT implementations for specific features (such as text, brush strokes, non-destructive bitmap editing, etc). As each of thse CRDTs mature, we can swap them in, and at some point, remove the server.
# react-native-animation
- https://github.com/LegendApp/legend-motion
  - Supports react-native and react-native-web
  - Legend Motion is a declarative animations library for React Native, to make it easy to transition between styles without needing to manage animations.
  - API similar to Framer Motion for easy mixing of React Native with React
  - 0 dependencies using the built-in Animated
# react animation
- react-transition-group /BSD/7.5kStar/202005
  - https://github.com/reactjs/react-transition-group
  - https://reactcommunity.org/react-transition-group/
  - perform animations when a React component enters or leaves the DOM
- framer-motion /MIT/6.3kStar/202007
  - https://github.com/framer/motion
  - https://framer.com/motion
  - production-ready animation and gesture library for React
  - based on popmotion9, @popmotion/popcorn, @popmotion/easing
  - Framer Motion is the successor to the Pose animation library
- react-motion /MIT/18.6kStar/201911
  - https://github.com/chenglou/react-motion  
  - http://chenglou.github.io/react-motion/demos/demo0-simple-transition/
  - A spring that solves your animation problems.
- react-spring /MIT/17.7kStar/202005
  - https://github.com/react-spring/react-spring
  - https://www.react-spring.io/
  -  a spring-physics based animation library
- react-move /MIT/6.2kStar/202006
  - https://github.com/sghall/react-move
  - https://react-move-docs.netlify.app/
  - data-driven animations for React
- react-simple-animate /MIT/1.4kStar/202006
  - https://github.com/bluebill1049/react-simple-animate
  - https://react-simple-animate.now.sh/
  - Follow CSS animation standard
- ant-motion /MIT/3.8kStar/202006
  - https://github.com/ant-design/ant-motion
  - http://motion.ant.design/
  - a motion design specification from Ant Design
  - animation-components
    - rc-animate
    - rc-tween-one
    - rc-scroll-animate
    - rc-queue-animate
    - rc-banner-anim
- renature /MIT/243Star/202007
  - https://github.com/FormidableLabs/renature
  - https://formidable.com/open-source/renature/docs/
  - A physics-based animation library for React focused on modeling natural world forces.
  - Taking influence from other popular physics-based animation libraries like react-spring and elements of framer-motion, 
  - renature focuses on using non-traditional physics primitives like gravity, friction, and fluid resistance.
  - It also provides a simple two-dimensional API for creating visual experiences similar to Processing or p5.js.
- react-keyframes /NALic/535Star/202002
  - https://github.com/vercel/react-keyframes
  - https://npmjs.com/react-keyframes
  - A React component for creating frame-based animations.
- react-circle /MIT/912Star/201903
  - https://github.com/zzarcon/react-circle
  - https://zzarcon.github.io/react-circle
  - Renders a svg circle + percentage
- element-motion /MIT/840Star/201908
  - https://github.com/madou/element-motion
  - https://elementmotion.com/
  - Tween between view states with declarative zero configuration element motions for React
  - repo has been archived.
  - If you're looking for a solid implementation of an animation engine/FLIP style animations that are easy to use, I highly recommend checking out Framer Motion.
  - Orchestration 
    - collecting DOM data, enabling motion between disconnected React elements, executing motions
  - Motions 
    - animation concerns, CSS transitions/animations, JS animations, whatever you can imagine
# js animation
- https://github.com/formkit/auto-animate /MIT/202311/ts
  - https://auto-animate.formkit.com/
  - A zero-config, drop-in animation utility that adds smooth transitions to your web app. 
  - You can use it with React, Vue, or any other JavaScript application.

- https://github.com/jeremyckahn/shifty
  - https://jeremyckahn.github.io/shifty/doc/
  - Shifty is a tweening engine for JavaScript

- anime /MIT/36.3kStar/202004
  - https://github.com/juliangarnier/anime
  - https://animejs.com/
  - a JavaScript animation library working with CSS properties, SVG, DOM attributes and JavaScript Objects.
- mojs /MIT/15.9kStar/202004
  - https://github.com/mojs/mojs
  - https://mojs.github.io/
  - The motion graphics toolbelt for the web
- velocity /MIT/16.7kStar/202007
  - https://github.com/julianshapiro/velocity
  - http://velocityjs.org/
  - Accelerated JavaScript animation.
- GSAP (GreenSock Animation Platform) /NoChargeLic/11.1kStar/202007
  - https://github.com/greensock/GSAP
  - https://greensock.com/
  - JavaScript animation library (including Draggable).
- scenejs /MIT/1.7kStar/202007
  - https://github.com/daybrush/scenejs
  - https://daybrush.com/scenejs
  - a JavaScript & CSS timeline-based animation library.

- https://github.com/uber/hubble.gl
    - Hubble.gl is a JS library for animating data visualizations.
    - Render within the browser without a backend. 
# css animation

- https://github.com/ingram-projects/animxyz /MIT/202302/js/inactive
  - The first truly composable CSS animation library. 
  - Powered by CSS variables to allow a nearly limitless number of unique animations without writing a single keyframe. 

- transition.css /13Star/Apache2/202010/css
  - https://github.com/argyleink/transition.css
  - https://transition.style/
  - 46 pre-built transitions! Drop-in CSS transitions
  - 偏向形状渐变的动画效果
- animate.css /MIT/67.5kStar/202007
  - https://github.com/animate-css/animate.css
  - https://animate.style/
  - A cross-browser library of CSS animations. 
  - Animate.css supports the prefers-reduced-motion media query so that users with motion sensitivity can opt out of animations. 
- magic /MIT/6.6kStar/202007
  - https://github.com/miniMAC/magic
  - https://www.minimamente.com/project/magic/
  - CSS3 Animations with special effects

- https://github.com/sanjayaharshana/AnimTrap
  - AnimTrap is a CSS Framework for animations. 

- https://animista.net/play/basic/flip
  - Animista is a CSS animation library and a place where you can play with a collection of ready-made CSS animations and download only those you will use.
# canvas animation
- https://github.com/shzlw/zeu
  - /1.7kStar/MIT/201811/js/作者poli
  - a collection of prebuilt visualization components for building real-time TV dashboard, monitoring UI and IoT web interface.

- https://github.com/spite/ccapture.js
  - a library to help capturing animations created with HTML5 canvas at a fixed framerate.

- https://github.com/kennethcachia/shape-shifter
  - http://www.kennethcachia.com/shape-shifter/
  - A canvas experiment in which a set of particles is used to render different shapes based on the user's input.
  - It supports multiple modes: text, countdown, time and icons.
  - 粒子动画示例的效果amazing

- https://github.com/vizzuhq/vizzu-lib
  - https://lib.vizzuhq.com/
  - Library for animated data visualizations and data stories.
  - Designed with animation in focus; 
  - Automatic data aggregation & data filtering; 
  - HTML5 canvas rendering; 
  - Written in C++ compiled to WebAssembly; 
  - Dependency-free.
# interactive-ui-components
- scrollreveal /GPLv3/18.9kStar/202007
  - https://github.com/jlmakes/scrollreveal
  - https://scrollrevealjs.org/
  - Animate elements as they scroll into view.
- https://github.com/ai/easings.net
  - Easing Functions Cheat Sheet to help developers pick the right easing function.

- https://github.com/ConnorAtherton/loaders.css
# animation-examples
- https://github.com/ozrenkosi/flow
  - Animation inspired by @sasj, made with p5.js
  - 斑点上下移动
- https://github.com/hakimel/kontext
  - http://lab.hakim.se/kontext/
  - 页面切换时的三维效果
# animation-utils
- svg.js /MIT/8.2kStar/202006
  - https://github.com/svgdotjs/svg.js
  - http://svgjs.com/
  - library for manipulating and animating SVG, without any dependencies.
- vivus /MIT/13.2kStar/201909
  - https://github.com/maxwellito/vivus
  - http://maxwellito.github.io/vivus
  - JavaScript library to make drawing animation on SVG
- https://github.com/mattboldt/typed.js
  - Enter in any string, and watch it type at the speed you've set
- https://github.com/Popmotion/popmotion
  - /ts
  - Simple animation libraries for delightful user interfaces
  - It supports keyframe and spring animations for numbers, colors and complex strings.
  - designed to be composable and portable into any JavaScript environment, with an eye on worklets in the future.
  - react-pose is deprecated for framer-motion
  - [Document deprecation in favour of Framer Motion · Issue · Popmotion/popmotion](https://github.com/Popmotion/popmotion/issues/834)
  - [Popmotion 9 [WIP] by mattgperry · Pull Request · Popmotion/popmotion](https://github.com/Popmotion/popmotion/pull/859)
- https://github.com/kimmobrunfeldt/progressbar.js
  - Responsive and slick progress bars
- https://github.com/alexfoxy/lax.js
  - vanilla javascript plugin to create smooth & beautiful animations when yo scroll
- https://github.com/barbajs/barba
  - Create badass, fluid and smooth transition between your website's pages.
- https://github.com/HaikuTeam/core
  - Interactive UI animation engine for the Web. Core renderer for Haiku Animator.
- https://github.com/wadackel/sweet-scroll
  - dependency-free smooth scroll library using raf
# physics
- https://github.com/liabru/matter-js /MIT/202308/js
  - https://brm.io/matter-js/
  - a 2D rigid body physics engine for the web
  - 一个高性能的 2D 物理 js 库
# page-transition
- https://github.com/michalzalobny/plain-page-transition
  - https://zesty-cocada-b5eb44.netlify.app/
  - Transition between pages made from scratch with plain JavaScript and no external libraries
# math
- https://github.com/3b1b/manim /MIT/202405/python
  - Animation engine for explanatory math videos
  - System requirements are FFmpeg, OpenGL and LaTeX (optional, if you want to use LaTeX). For Linux, Pango along with its development headers are required
# more
- awesome-web-animation /202006
  - https://github.com/sergey-pimenov/awesome-web-animation
  - https://awesome-web-animation.netlify.com/
    - 可按标签查看

- https://github.com/software-mansion/react-native-reanimated
  - https://docs.swmansion.com/react-native-reanimated/
  - React Native's Animated library reimplemented
  - Reanimated 2 is here! 
- https://github.com/IanLunn/Sequence
  - http://sequencejs.com/
  - responsive CSS animation framework for creating unique sliders, presentations, banners, and other step-based applications.

- https://github.com/alexjlockwood/ShapeShifter
  - a web-app that simplifies the creation of icon animations for Android, iOS, and the web.

- https://github.com/veltman/flubber
  - Some best-guess methods for smoothly interpolating between 2-D shapes.
  - animating morphing SVG paths with Framer Motion. 
    - We make a custom useFlubber hook to repackage @veltman 's amazing Flubber library into a MotionValue.

- https://github.com/Cuberto/mouse-follower
  - A powerful javascript library to create amazing and smooth effects for the mouse cursor 
  - 依赖 gsap
