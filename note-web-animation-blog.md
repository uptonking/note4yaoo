---
title: note-web-animation-blog
tags: [animation, blog, web]
created: '2020-08-04T04:46:58.013Z'
modified: '2020-08-04T04:47:53.115Z'
---

# note-web-animation-blog

## Animating Layouts with the FLIP Technique

- [Animating Layouts with the FLIP Technique_2017](https://css-tricks.com/animating-layouts-with-the-flip-technique/)
- Animation brings user interfaces to life. 
- However, adding meaningful transitions and micro-interactions is often an afterthought, or something that is “nice to have” if time permits. 
- All too often, we experience web apps that simply “jump” from view to view without giving the user time to process what just happened in the current context.
- In this article, we’ll explore a technique called “FLIP” that can be used to animate the positions and dimensions of any DOM element in a performant manner, regardless of how their layout is calculated or rendered (e.g., height, width, floats, absolute positioning, transform, flexbox, grid, etc.)
- In short, our goal is to be short – we want to calculate the least amount of style changes necessary, as quickly as possible. 
- The key to this is only animating transform and opacity, and FLIP explains how we can simulate layout changes using only transform.

- FLIP is a mnemonic device and technique first coined by Paul Lewis, which stands for First, Last, Invert, Play.
- First: 
  - before anything happens, record the current (i.e., first) position and dimensions of the element that will transition. 
  - You can `use element.getBoundingClientRect()` for this, as will be shown below.
- Last: 
  - execute the code that causes the transition to instantaneously happen, 
  - and record the final (i.e., last) position and dimensions of the element.
- Invert: 
  - since the element is in the last position, we want to create the illusion that it’s in the first position, by using `transform` to modify its position and dimensions. 
  - This takes a little math, but it’s not too difficult.
- Play: 
  - with the element inverted (and pretending to be in the first position), 
  - we can move it back to its last position by setting its `transform` to `none` .

- Below is how these steps can be implemented with the Web Animations API

- Shared Element Transitions
  - One common use-case for transitioning an element between app views and states is that the final element might not be the same DOM element as the initial element. 
  - In Android, this is similar to a shared element transition, except that the element isn’t “recycled” from view to view in the DOM as it is on Android.
  - Nevertheless, we can still achieve the FLIP transition
- Parent-Child Transitions
  - Since the previously calculated bounds are relative to the `window` , our calculations for the child element are going to be off. 
  - To solve this, we need to ensure that the bounds are calculated relative to the parent element instead

- I’ve created a small library called Flipping.js with the same idea in mind. 
  - By adding a `data-flip-key="..."` attribute to HTML elements, it’s possible to predictably and efficiently keep track of elements that might change position and dimensions from state to state.
  - flipping.js: tiny and low-level; only emits events when element bounds change
  - flipping.web.js: uses WAAPI to animate transitions

## FLIP Your Animations

- [FLIP Your Animations_2015](https://aerotwist.com/blog/flip-your-animations/)
  - [github: flipjs](https://github.com/googlearchive/flipjs)
    - /Apache2.0/1.3kStar/201601
- Animations in your web app should run at 60fps. 
- Not always easy to achieve that, and it really depends on what you're trying to do, but I'm here to help. With FLIP.
- What we’re trying and do is to turn animations on their head (flip, see? Gosh darnit, I’m so funneh) and, instead of animating “straight ahead” and potentially doing expensive calculations on every single frame we precalculate the animation dynamically and let it play out cheaply.
- FLIP stands for First, Last, Invert, Play.
  - First: 
    - the initial state of the element(s) involved in the transition.
  - Last: 
    - the final state of the element(s).
  - Invert: 
    - You figure out from the first and last how the element has changed, so – say – its width, height, opacity. 
    - Next you apply transforms and opacity changes to reverse, or invert, them. 
    - If the element has moved 90px down between First and Last, you would apply a transform of -90px in Y. 
    - This makes the elements appear as though they’re still in the First position but, crucially, they’re not.
  - Play: 
    - switch on transitions for any of the properties you changed, and then remove the inversion changes. 
    - Because the element or elements are in their final position removing the transforms and opacities will ease them from their faux First position, out to the Last position.
- The reason you can afford to do this relatively expensive precalculation is because there is a window of 100ms after someone interacts with your site where you’re able to do work without them noticing. 
  - If you’re inside that window users will feel like the site responded instantly!
  - It’s only when things are moving that you need to maintain 60fps.
  - We can use that window of time to do all that getBoundingClientRect work (or getComputedStyle if that’s your poison) in JavaScript, and from there we make sure that we’re reducing the animation down to nice-and-fast, compositor-friendly, look-ma-no-paints transform and opacity changes
- Sometimes you will need to rethink your animations to fit this model, and on many occasions I’ve separated and animated elements individually just so that I can animate them without distortion, and FLIP as much as possible. 
- My colleague and friend Paul Kinlan recently ran a survey on what people want from a news app. 
  - The most popular answer (which was a surprise to him, at least) wasn’t offline support, sync, notifications, or anything like that. 
  - It was smooth navigation. Smooth, like no jank, no stutter, no judder. (/me mutters something about #perfmatters.)
- There are a couple of things to bear in mind if you FLIP
  - Don’t exceed the 100ms window. 
    - It’s important to remember that you shouldn’t exceed that window, because your app will appear non-responsive if you do. 
    - Keep an eye on it through DevTools to know if you’re busting that budget.
  - Orchestrate your animations carefully. 
    - Imagine, if you will, that you’re running one of these animations all transformy and opacity-y and then you decide to do another, which requires a bunch of precalculation. 
    - That’s going to interrupt the animation that’s in flight, which is bad. 
    - The key here is to make sure your precalculation work is done in idle or the “response window” I talked about, and that two animations don’t stomp over each other.
  - Content can get distorted(v, 变形，扭曲). 
    - When you’re working in a scale and transform world, some elements can get distorted. 
    - As I said above I’ve been known to restructure my markup a little to allow me to FLIP without distortion, but it can end up being quite the wrangle(争论).
- I’ve come to love FLIP as a way of thinking about animations, because it’s a good match of JavaScript and CSS. 
  - Calculate in JavaScript, but let CSS handle the animations for you. 
  - You don’t have to use CSS to do the animations, though, you could just as easily use the Web Animations API or JavaScript itself, whatever’s easiest. 
  - The main point is that you’re reducing the per-frame complexity and cost (which normally means transform and opacity) to try and give the user the best possible experience.

## history of web animations

- [Navigating the sadistic world of web animations_2019](https://weareferal.com/blog/navigating-the-sadistic-world-of-web-animations)

- To get a good overview of where we cur­rent­ly stand with brows­er ani­ma­tions, here’s what we’re going to look at:
  - Flash 
  - SMIL (​“smile”)
  - CSS Tran­si­tions and Animations
  - JavaScript ani­ma­tions
  - Web Ani­ma­tion API (WAAPI)
  - 3rd par­ty ani­ma­tion frame­works and libraries

- Flash was a pro­pri­etary, closed-source appli­ca­tion (even­tu­al­ly owned by Adobe) that allowed devel­op­ers to build these inter­faces and games and then dump them into the brows­er via the `<object>` tag and a brows­er plug-in. 
  - The brows­er could inter­act with them but it was the respon­si­bil­i­ty of the installed Flash plug-in to run every­thing. 
  - Essen­tial­ly the brows­er was out­sourc­ing its job to Flash.
  - While Flash was a great tech­nol­o­gy, it went against the core prin­ci­ple of the web; to be open and acces­si­ble. 
- SVG and SMIL give you the toolset to cre­ate Flash-like ani­ma­tions in the brows­er using an open stan­dard.
  - It’s lim­it­ed to ani­mat­ing SVG ele­ments. You can’t use it to ani­mate oth­er ele­ments on a page.
  - a huge and com­plex spec­i­fi­ca­tion. It’s scope is much larg­er than just ani­ma­tions so get­ting start­ed is hard.
- One of the most antic­i­pat­ed fea­tures of HTML5 and CSS3 was the joint-intro­duc­tion of CSS ani­ma­tions, tran­si­tions and trans­forms via the fol­low­ing properties transform, transition, animation
  - The `transform` prop­er­ty allows you change the appear­ance of an ele­ment. 
    - a transform has absolute­ly noth­ing to do with ani­ma­tion. Trans­forms can be ani­mat­ed but they have noth­ing to do with ani­ma­tion themselves.
  - The `transition` prop­er­ty is the baby-sib­ling in the CSS ani­ma­tion fam­i­ly, dis­tinct from its old­er sib­lings animate
    - tran­si­tions and ani­ma­tions are sep­a­rate fea­tures to be used in dif­fer­ent circumstances.
    - tran­si­tions require a trig­ger to run.
    - Tran­si­tions only run once, in response to their trigger.
    - Tran­si­tions only have two ​“states”.
  - The `animate` prop­er­ty and `@keyframes` at-rule address some of the ques­tions left unan­swered by tran­si­tions
    - While tran­si­tions are good for one-off ani­ma­tions, these are used for cre­at­ing mul­ti-stage ani­ma­tions that run more than once.
- Final­ly it’s worth under­stand­ing that we could write an ani­ma­tion that does exact­ly what our tran­si­tion does. It would be a bit more labo­ri­ous but you can write all tran­si­tions as ani­ma­tions (but not visa-ver­sa).
- To be able to ani­mate with JavaScript we need tim­ing func­tions
  - setTimeout
  - setInterval
- Well with JavaScript we are telling the brows­er exact­ly how to per­form the ani­ma­tion — we’ve writ­ten the imple­men­ta­tion our­selves.
- With the CSS tran­si­tion, we out­lined what our ani­ma­tion should do but we did­n’t say how to actu­al­ly do it — we left that to the brows­er to actu­al­ly imple­ment behind-the-scenes.
- The inten­tion of WAAPI stan­dard is to encap­su­late all the above approach­es and give us a com­mon lan­guage to describe and con­trol ani­ma­tions in the browser

> CSS Tran­si­tions, CSS Ani­ma­tions, and SVG all pro­vide mech­a­nisms that gen­er­ate ani­mat­ed con­tent on a Web page. Although the three spec­i­fi­ca­tions pro­vide many sim­i­lar fea­tures, they are described in dif­fer­ent terms. This spec­i­fi­ca­tion pro­pos­es an abstract ani­ma­tion mod­el that encom­pass­es the com­mon fea­tures of all three spec­i­fi­ca­tions. This mod­el is back­wards-com­pat­i­ble with the cur­rent behav­ior of these spec­i­fi­ca­tions such that they can be defined in terms of this mod­el with­out any observ­able change

- WAAPI gives us the abil­i­ty to declar­a­tive­ly define our ani­ma­tions in a CSS-like fash­ion, while pro­vid­ing the abstrac­tions, func­tions and meth­ods we need to prop­er­ly con­trol our ani­ma­tions in JavaScript.
- At a high lev­el, the WAAPI dis­tils every­thing we’ve dis­cussed so far into three concepts:
  - Timeline the abil­i­ty to sequence animations
  - Animation the abil­i­ty to con­trol animations
  - Effects the actu­al ani­ma­tions themselves
- These con­cepts are back­wards com­pat­i­ble, so they should con­cep­tu­al­ly map onto CSS tran­si­tions and ani­ma­tions as well as SMIL.

- The bad news is that this is a rel­a­tive­ly new stan­dard and there­fore does­n’t have full sup­port. 
  - Fur­ther­more, only some of the API has been built-out so far, so some of the more advanced fea­tures are still a lit­tle while off (ani­ma­tion motion along a path for example).
- With the Web Ani­ma­tions API still in the works, for com­plex ani­ma­tion we may want to fall back to tried-and-test­ed 3rd par­ty libraries
- The impor­tant thing to note is that all these libraries use one or more of the approach­es we’ve men­tioned: ful­ly cus­tom JavaScript, CSS transitions/​animations, WAAPI or a mix of all three.

## Tips for Writing Animation Code Efficiently

- [Tips for Writing Animation Code Efficiently](https://css-tricks.com/tips-for-writing-animation-code-efficiently/)

- I will be using the GreenSock Animation Platform (GSAP). 
- It provides a simple, readable API and solves cross-browser inconsistencies so that you can focus on animating. 
- Use an animation library
  - Browser bugs, inconsistencies, and compatibility:
  - Animation workflow
  - Animate beyond the DOM: 
    - Canvas, WebGL, generic objects, and complex strings can’t be animated with native technologies. 
    - Using one consistent tool for all your animations is much cleaner. 
  - Runtime control
  - Easing options (bounce, elastic, etc.)
  - Lag smoothing
- Use timelines
  - A good animation library will provide some way of creating individual animations (called tweens) and a way to sequence animations in a timeline. 
  - Think of a timeline like a container for your tweens where you position them in relation to one another. 
  - Most anytime you need your animations to run in a sequence, you should be using a timeline.
- Use relative values
  - Animate values relative to their current value.
  - Use relative units 
  - Use methods like from to
- Use keyframes
  - No timeline necessary! 
  - To space out the tweens we just use the delay property in each keyframe
- Use smart defaults
  - It’s more common to set defaults for a particular timeline so that it affects only its children.
- Animate multiple elements at once
- Use function-based values, staggers, and/or loops
  - Use a function instead of a number/string for almost any property, and GSAP will call that function once for each target when it first renders the tween. 
  - Plus, it’ll use whatever gets returned by the function as the property value! 
  - This can be really handy for creating a bunch of different animations using a single tween and for adding variance.
- Modularize your animations
  - Use functions to return tweens or timelines and then insert those into a master timeline
  - Wrapping your animation-building routines inside functions also makes recreating animations (say, on resize) a breeze
  - With effects, you can turn a custom animation into a named effect that can be called anytime with new targets and configurations. 
- Use control methods
  - make transitions between animations more fluid (such as being able to reverse part way through) and more performant (by reusing the same tween/timeline instead of creating new instances each time).
  - Use case: interaction events that trigger animations
  - Use case: Animating between multiple states of a timeline
  - Use case: Animating based on the scroll position
- Bonus tip: Use GSAP’s plugins, utility methods, and helper functions

## High Performance Animations

- [High Performance Animations_2013](https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)

- Modern browsers can animate four things really cheaply: 
  - position: `transform: translate(Xpx,Ypx)`
  - scale: `transfrom: scale(ratio)`
  - rotation: `transform: rotate(Xdeg)`
  - opacity: 0~1
- If you animate anything else, it’s at your own risk, and the chances are you’re not going to hit a silky smooth 60fps.
- The process that the browser goes through is pretty simple: 
  - calculate the styles that apply to the elements (Recalculate Style), 
  - generate the geometry and position for each element (Layout), 
  - fill out the pixels for each element into layers (Paint Setup and Paint) 
  - draw the layers out to screen (Composite Layers).
- To achieve silky smooth animations you need to avoid work, and the best way to do that is to only change properties that affect compositing -- `transform` and `opacity` . 
- The higher up you start on the timeline waterfall, the more work the browser has to do to get pixels on to the screen.
- When you change elements, the browser may need to do a layout, which involves calculating the geometry (position and size) of all the elements affected by the change.
- Here are the most popular CSS properties that, when changed, trigger layout
  - position, display, top, bottom, float, clear
  - width, height, padding, margin, border, overflow
  - font-size/fam­i­ly/weight, white-space
  - text-align, vertical-align, line-height
- Changing an element may also trigger painting, and the majority of painting in modern browsers is done in software rasterizers. 
  - Depending on how the elements in your app are grouped into layers, other elements besides the one that changed may also need to be painted.
- There are many properties that will trigger a paint, but here are the most popular:
  - color
  - visibility
  - text-decoration
  - background-position/size
  - outline-style/width/color
- If you animate any of the above properties the element(s) affected are repainted, and the layers they belong to are uploaded to the GPU. 
  - On mobile devices this is particularly expensive because CPUs are significantly less powerful than their desktop counterparts, meaning that the painting work takes longer; 
  - and the bandwidth between the CPU and GPU is limited, so texture uploads take a long time.
- [CSS properties by style operation required](http://goo.gl/lPVJY6)
- There is one CSS property, however, that you might expect to cause paints that sometimes does not: `opacity` . 
  - Changes to `opacity` can be handled by the GPU during compositing by simply painting the element texture with a lower alpha value. 
  - For that to work, however, the element must be the only one in the layer. 
  - If it has been grouped with other elements then changing the `opacity` at the GPU would (incorrectly) fade them too.
  - In Blink and WebKit browsers a new layer is created for any element which has a CSS transition or animation on opacity, but many developers use `translateZ(0)` or `translate3d(0,0,0)` to manually force layer creation. 
  - Forcing layers to be created ensures both that the layer is painted and ready-to-go as soon as the animation starts (creating and painting a layer is a non-trivial operation and can delay the start of your animation), and that there's no sudden change in appearance due to antialiasing changes. 
- Changing the `transform` of an element boils down to changes to its position, rotation or scale. 
  - Often, position is animated by setting the `left` and `top` properties. 
  - The problem is left and top both trigger layout operations, and that's expensive. 
  - The better solution is to use a `translate` on the element, which does not trigger layout.
- Developers often have to decide if they will animate with JavaScript (imperative) or CSS (declarative). 
- Animating in JavaScript does give you a lot of control: starting, pausing, reversing, interrupting and cancelling are trivial(不重要的；琐碎的). 
  - Some effects, like parallax scrolling, can only be achieved in JavaScript.
  - The main pro of imperative animations happens to also be its main con: it’s running in JavaScript on the browser’s main thread. 
  - The main thread is already busy with other JavaScript, style calculations, layout and painting. 
  - Often there is thread contention. This substantially increases the chance of missing animation frames, which is the very last thing you want.
- The primary advantage of CSS animation is that the browser can optimize the animation. 
  - It can create layers if necessary, and run some operations off the main thread which, as you have seen, is a good thing. 
  - The major con of CSS animations for many is that they lack the expressive power of JavaScript animations. 
  - It is very difficult to combine animations in a meaningful way, which means authoring animations gets complex and error-prone.
- There is a proposal by Google’s Ian Vollick that investigates the concept of allowing JavaScript animations via workers, providing the animation does not trigger layout or style recalculations.
- Conclusion
  - You should always look to avoid animating properties that will trigger layout or paints, both of which are expensive and may lead to skipped frames. 
  - Declarative CSS animations are preferable to imperative since the browser has the opportunity to optimize ahead of time.
  - Today transforms are the best properties to animate because the GPU can assist with the heavy lifting

## React Web动画的5种创建方式 

- [React Web 动画的 5 种创建方式，每一种都不简单](https://zhuanlan.zhihu.com/p/28500217)
  - [React Animations in Depth_2017](https://medium.com/react-native-training/react-animations-in-depth-433e2b3f0e8e)

- CSS animation
  - 给元素添加class是最简单，最常见的书写方式
  - 赞同者： 我们只需修改 opacity 和 transform 这样的属性，就可构建基本的动画，而且，在组件中，我们可以非常容易地通过 state 去更新这些值
  - 反对者：这种方式并不跨平台，在 React Native 中就不适用，而且，对于较复杂的动画，这种方式难以控制
- JS Style
  - js styles 跟 CSS 中的 classes 类似，在 JS 文件中，我们就可以拥有所有逻辑
  - 赞同者：跟 CSS 动画 一样，且它的表现更加清晰。它也不失为一个好方法，可以不必依赖任何 CSS
  - 反对者：跟 CSS 动画 一样，也是不跨平台的，且动画一旦复杂，也难以控制
- React Motion
  - 提供的 spring 函数来逼真地模仿真实的物理效果，也就是我们常见的各类缓动效果
  - 赞同者：React Motion 可以在 React Web 中使用，也可以在 React Native 中使用，因为它是跨平台的。其中的 spring 概念最开始对我来说感觉挺陌生，然而上手之后，发现它真的很神奇，并且，它有很详细的 API
  - 反对者：在某些情况下，他不如纯 CSS / JS 动画，虽然它有不错的 API，容易上手，但也需要学习成本
- Animated
  - 是基于React Native使用的同一个动画库建立起来的
  - 赞同者：跨平台，它在 React Native 中已经非常稳定，如果你在 React Native 中使用过，那么你将不用再重复学习。其中的 interpolate 是一个神奇的插值函数
  - 反对者： 目前貌似不是 100% 的稳定，在老的浏览器中的，存在前缀和性能的问题，而且，它也有学习成本
  - https://github.com/animatedjs/animated
    - /MIT/1.7kStar/201810
    - Declarative Animations Library for React and React Native
    - 已废弃
- Velocity React
  - 是基于已经存在的 Velocity 建立起来的
  - 赞同者：上手容易，API 简单明了，相对其他库更易于掌握
  - 反对者：有些不得不克服的问题，比如 componentDidMount 后动画并没有真正地起作用等，而且，它不跨平台
- Conclusion
  - Overall, I think I will be using JS style animations for basic animations, and React Motion for anything crazy on the web. 
  - And for React Native, I will be sticking to Animated. 
  - Once Animated is more mature, I will also probably switch to it as well on the web, though I am starting to enjoy using React Motion!
