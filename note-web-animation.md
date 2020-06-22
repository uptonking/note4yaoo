---
tags: [animation, style, web]
title: note-web-animation
created: '2019-10-16T06:58:19.848Z'
modified: '2020-06-22T09:16:37.879Z'
---

# note-web-animation

## summary
- 根据应用场景，选择动画实现方式
- 对于普通ui切换效果，使用css transition或animation
- 对于连续执行，或依次执行，或包含3种以上效果的动画，采用js动画
- 从长期维护的角度，还要考虑svg、canvas、webgl等元素实现动画的方式
- 具体实现方式在github上的热度

## faq
- 组件的hover effect如何实现
- 类似条形图悬停时加长某根柱子，饼状图加长某个扇形
- 类似卡片变大

## js animation
- 动画原理
  - 当页面最小化或被切换成后台标签页时，页面为不可见，浏览器会触发visibilitychange事件,并设置document.hidden属性为true
  - 切换到显示状态时，页面为可见，也同样触发一个visibilitychange事件，设置document.hidden属性为false
  - 每个Document都有一个动画帧请求回调函数列表，该列表可以看成是由`<handlerId, callback>`元组组成的集合。其中handlerId是一个整数，唯一地标识了元组在列表中的位置；callback是回调函数
  - 屏幕刷新频率，即图像在屏幕上更新的速度，也即屏幕上的图像每秒钟出现的次数，单位是赫兹(Hz)
    - 对于一般笔记本电脑，这个频率大概是60Hz，这个值的设定受屏幕分辨率、屏幕尺寸和显卡的影响
  - 眼前所看到图像正在以每秒60次的频率刷新，由于刷新频率很高，因此你感觉不到它在刷新。而动画本质就是要让人眼看到图像被刷新而引起变化的视觉效果，这个变化要以连贯的、平滑的方式进行过渡
  - 刷新频率为60Hz的屏幕每16.7ms刷新一次，我们在屏幕每次刷新前，将图像的位置向左移动一个像素。这样一来，屏幕每次刷出来的图像位置都比前一个要差1px，因此你会看到图像在移动；由于我们人眼的视觉停留效应，当前位置的图像停留在大脑的印象还没消失，紧接着图像又被移到了下一个位置，因此你才会看到图像在流畅的移动，这就是视觉效果上形成的动画
  - 可以用setInterval来实现动画，这种做法不太好，因为不同浏览器的刷新频率不一样（一般认为将间隔时间设置16ms为最佳,按每秒60帧算，1000/60≈16.67）
  - `handlerId = requestAnimationFrame(callback)`
      - 传入一个callback函数，即动画回调函数
      - 返回值handlerId为浏览器定义的、大于0的整数，唯一标识了该回调函数在列表中位置
  - 浏览器执行过程
      - 首先要判断document.hidden属性是否为true,即**页面处于可见状态才会执行**
      - 浏览器清空上一轮的动画函数
      - 方法返回的handlerId值会和动画函数callback，以`<handlerId,callback>`进入到动画帧请求回调函数列表
      - 浏览器会遍历动画帧请求回调函数列表，根据handlerId的值大小，依次去执行相应的动画函数
- `window.requestAnimationFrame(callback)`
  - method tells the browser that you wish to perform an animation and requests that the browser call a specified function to update an animation before the next repaint.
  - The method takes a callback as an argument to be invoked before the repaint.
  - 此方法用来在页面重绘之前，通知浏览器调用一个指定的函数，以满足开发者操作动画的需求
      - 接受一个函数为参数，该函数会在重绘前调用
      - 该函数只会被传入一个DOMHighResTimeStamp参数，这个参数指示当前被 requestAnimationFrame序列化的函数队列被触发的时间
      - 如果想得到连贯的逐帧动画，函数中必须重新调用requestAnimationFrame()
  - 以浏览器的显示频率作为动画动作的频率，这样就不会过度绘制，也不会掉帧
      - 由系统来决定回调函数的执行时机，能保证回调函数在屏幕每一次的刷新间隔中只被执行一次
  - requestAnimationFrame的优点
      - setInterval控制的动画其调用的间隔由程序员设置，而requestAnimationFrame无须设置调用间隔，它自动紧跟浏览器的刷新帧率(一般来说每秒60帧)，不会掉帧
      - cpu节能。使用setTimeout实现的动画，当页面被隐藏或最小化时，setTimeout仍然在后台执行动画任务，浪费CPU资源。而requestAnimationFrame则不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销
      - 函数节流。在高频率事件(resize,scroll等)中，为了防止在一个刷新间隔内发生多次函数执行，使用requestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销。一个刷新间隔内函数执行多次时没有意义的，因为显示器每16.7ms刷新一次，多次绘制并不会在屏幕上体现出来。
      - requestAnimationFrame会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成
          - 比如在1s的间隔内，在前半秒触发的10次事件，被推迟到1s的时候执行回调，可以认为是一个节流
      - 在隐藏或不可见的元素中，requestAnimationFrame将不会进行重绘或回流，这就意味着更少的的cpu、gpu和内存使用量
- `setInterval`/`setTimeout `
- js控制的动画大多使用`setInterval`或`setTimeout`每隔一段时间刷新元素的位置，来达到动画的效果
- 这种方式并不能准确地控制动画帧率，尽管主流的浏览器（相当一部分的浏览器的显示频率是16.7ms,按每秒60帧算，1000/60≈16.67）对于这两个函数实现的动画都有一定的优化，但是这依然无法弥补它们性能问题
    - 主要原因是js的单线程机制使得其可能在有阻塞的情况下无法精确到毫秒触发
- setTimeout是通过设置一个间隔时间来不断的改变图像的位置，从而达到动画效果
    - setTimeout的执行时间并不是确定的。在js中，setTimeout任务被放进了异步队列中，只有当主线程上的任务执行完以后，才会去检查该队列里的任务是否需要开始执行，因此setTimeout的实际执行时间一般要比其设定的时间晚一些
    - 不同设备的屏幕刷新频率可能会不同，而setTimeout只能设置一个固定的时间间隔
    - setTimeout的执行只是在内存中对图像属性进行改变，这个变化必须要等到屏幕下次刷新时才会被更新到屏幕上。如果两者的步调不一致，就可能会导致中间某一帧的操作被跨越过去，而直接更新下一帧的图像。这就一起了丢帧。
- ref
  - https://juejin.im/post/5b6020b8e51d4535253b30d1


## css transition vs animation
- animation会竞争CPU资源，可能有延迟，transition使用GPU
- CSS3 animation will not lift the animation rendering process to the GPU like what CSS3 transition does. 
- This will cause lagging effect when many JS tasks are executing at the same time. Because all tasks are competing for the CPU. 
- While CSS3 transition may lift the animation to GPU so that it will not compete with CPU and can be renderrred separately
- animation使用GPU的方式是加上`transform: translateZ(0)` 或 `translate3d(0, 0, 0)` 或 `rotateZ(360deg)`. This will composite the elements into their own layers (by tricking the browser into thinking it will be doing 3D transforms) and the browser should, in most cases, take advantage of GPU acceleration, lessening the burden on the CPU.
- 动画完成时，是否会保存状态，animation会回到初始状态
- After each animation, the CSS3 animation will move back to its original state where before the animation starts While CSS3 transition will keep the animation state after each transition.
- 执行次数的区别，animation可设置循环次数
- CSS3 animation can have iteration count set(animation-iteration-count) which means how many times the animation will be repeated. 
- But CSS3 transition will only perform the animation once. 
- To repeat the animation with CSS3 transition, JavaScript may need to be used.
- 动画中间状态的控制，animation可设置多个中间态
- CSS3 animation gives more control to the developer on how the animation is performed. You can define what the state should be at different stages of the animation, e.g, 0%, 10%, 30%, 50%....
- CSS3 transition can only define the start and end state and the rest will be handled by the browser.
- 易用性
- CSS3 transition is more simpler to use, it doesn't require you to create your own keyframes. There are a predefined set of animations which can be used. And there are a set of effects you can use to transition an element.
- Animation takes a lot more code
- ref
- https://www.pixelstech.net/article/1434375977-CSS3-animation-vs-CSS3-transition

## js animation vs css animation
- There are two primary ways to create animations on the web: with CSS and with JavaScript. 
- Which one you choose really depends on the *other dependencies* of your project, and what kinds of effects you're trying to achieve.
- Use CSS animations for simpler "one-shot" transitions, like toggling UI element states.
- Use JavaScript animations when you want to have advanced effects like bouncing, stop, pause, rewind, or slow down.
- If you choose to animate with JavaScript, use the **Web Animations API** or a modern framework that you're comfortable with.
  - web animations api 在github上不受欢迎
  - 还要考虑对svg、canvas的支持
- Use CSS when you have smaller, self-contained states for UI elements. 
  - CSS transitions and animations are ideal for bringing a navigation menu in from the side, or showing a tooltip. 
  - You may end up using JavaScript to control the states, but the animations themselves will be in your CSS.
- Use JavaScript when you need significant control over your animations. 
  - The Web Animations API is the standards-based approach, available today in most modern browsers. 
  - This provides real objects, ideal for complex object-oriented applications. 
  - JavaScript is also useful when you need to stop, pause, slow down, or reverse your animations.
- Use requestAnimationFrame directly when you want to orchestrate an entire scene by hand. This is an advanced JavaScript approach, but can be useful if you're building a game or drawing to an HTML canvas.
- Alternatively, if you're already using a JavaScript framework that includes animation functionality, such as via jQuery's .animate() method or GreenSock's TweenMax, then you may find it more convenient overall to stick with that for your animations.
- Animating with CSS is the simplest way to get something moving on screen. This approach is described as declarative, because you specify what you'd like to happen.
- JavaScript animations are imperative, as you write them inline as part of your code. You can also encapsulate them inside other objects.
- In terms of performance, there is no difference between implementing an animation with CSS transitions or animations. Both of them are classified under the same CSS-based umbrella in this article.
-  Compared to setTimeout()/setInterval(), which need a specific delay parameter, requestAnimationFrame() is much more efficient. Developers can create an animation by simply changing an element's style each time the loop is called (or updating the Canvas draw, or whatever.)
- Like CSS transitions and animations, requestAnimationFrame() pauses when the current tab is pushed into the background.
- The fact is that, in most cases, the performance of CSS-based animations is almost the same as JavaScripted animations — in Firefox at least. 
- Some JavaScript-based animation libraries, like GSAP and Velocity.JS, even claim that they are able to achieve better performance than native CSS transitions/animations. 
- This can occur because CSS transitions/animations are simply resampling element styles in the main UI thread before each repaint event happens, which is almost the same as resampling element styles via a requestAnimationFrame() callback, also triggered before the next repaint. 
- If both animations are made in the main UI thread, there is no difference performance-wise.
- we'd argue that CSS animations are the better choice. But how? 
- The key is that as long as the properties we want to animate do not trigger reflow/repaint (read CSS triggers for more information), we can move those sampling operations out of the main thread. 
- The most common property is the CSS transform. If an element is promoted as a layer, animating transform properties can be done in the GPU, meaning better  performance/efficiency, especially on mobile. 
- In summary, we should always try to create our animations using CSS transitions/animations where possible. If your animations are really complex, you may have to rely on JavaScript-based animations instead.
- shortcomings of CSS-based animation
- Lack of independent scale/rotation/position control
  - In CSS, they’re all crammed into one “transform” property, making them impossible to animate in a truly distinct way on a single element
- performance
  - The newer GSAP is also JavaScript-based but it’s literally up to 20x faster than jQuery.
  - Declaring your animations in CSS allows the browser to determine which elements should get GPU layers, and divvy them up accordingly.you can do that with JavaScript too
  - using a different CPU thread for animation-related calculations doesn’t come without costs
  - Also note that not all CSS properties get the GPU boost in CSS animations. In fact, most don’t. Transforms (scale, rotation, translation, and skew) and opacity are the primary beneficiaries.
  - CSS animations are significantly faster than jQuery. However, on most devices and browsers I tested, the JavaScript-based GSAP performed even better than CSS animations 
  - Although well-optimized JavaScript is often just as fast if not faster than CSS animations, 3D transforms do tend to be faster when animated with CSS, but that has a lot to do with the way browsers handle 16-element matrices today 
- Using css animations, You cannot seek to a particular spot in the animation, nor can you smoothly reverse part-way through or alter the time scale or add callbacks at certain spots or bind them to a rich set of playback events. JavaScript provides great control
- It is becoming increasingly common to animate canvas-based objects and other 3rd-party library objects but unfortunately CSS animations can only target DOM elements.
- There are a few more workflow-related conveniences that are missing in CSS Animations
  - Relative values, Nesting, Progress reporting, Targeted kills, Concise code
- css animation effects are
- 
- CSS Animations is a module of CSS that lets you animate the values of CSS properties over time, using keyframes 
- The behavior of these keyframe animations can be controlled by specifying their timing function, duration, their number of repetitions, and other attributes
- ref
- https://developer.mozilla.org/en-US/docs/Web/Performance/CSS_JavaScript_animation_performance
- https://developers.google.com/web/fundamentals/design-and-ux/animations/css-vs-javascript


## animation performance
- Take care that your animations don’t cause performance issues; ensure that you know the impact of animating a given CSS property.
- Animating properties that change the geometry of the page (layout) or cause painting are particularly expensive.
- Where you can, stick to changing transforms and opacity.
- Use will-change to ensure that the browser knows what you plan to animate.
- some properties are cheaper to animate than others. 
- For example, animating the width and height of an element changes its geometry and may cause other elements on the page to move or change size. 
- This process is called layout (or **reflow** in Gecko-based browsers like Firefox), and can be expensive if your page has a lot of elements. 
- Whenever layout is triggered, the page or part of it will normally need to be painted, which is typically even more expensive than the layout operation itself.
- Where you can, you should avoid animating properties that trigger layout or paint. For most modern browsers, this means limiting animations to `opacity` or `transform`, both of which the browser can highly optimize; it doesn’t matter if the animation is handled by JavaScript or CSS.
- The general rule of thumb is that if the animation might be triggered in the next 200ms, either by a user’s interaction or because of your application’s state, then having will-change on animating elements is a good idea. For most cases, then, any element in your app’s current view that you intend to animate should have will-change enabled for whichever properties you plan to change.
- CSS-based animations, and Web Animations where supported natively, are typically handled on a thread known as the "compositor thread". 
- This is different from the browser's "main thread", where styling, layout, painting, and JavaScript are executed. 
- This means that if the browser is running some expensive tasks on the main thread, these animations can keep going without being interrupted.
- Other changes to transforms and opacity can, in many cases, also be handled by the compositor thread.
- If any animation triggers paint, layout, or both, the "main thread" will be required to do work. This is true for both CSS- and JavaScript-based animations, and the overhead of layout or paint will likely dwarf any work associated with CSS or JavaScript execution, rendering the question moot.
- ref
- https://developers.google.com/web/fundamentals/design-and-ux/animations/animations-and-performance
- https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/
- https://css-tricks.com/myth-busting-css-animations-vs-javascript/


## css animation

- Animations consist of two components
  - a style describing the CSS animation
  - a set of keyframes that indicate the start and end states of the animation’s style, as well as possible intermediate waypoints
- key advantages to CSS animations over traditional script-driven animation
  - easy to use for simple animations without having to know JavaScript
  - css animations run well, even under moderate system load
      - The rendering engine can use frame-skipping and other techniques to keep the performance as smooth 
  - Letting the browser control the animation sequence lets the browser optimize performance and efficiency by, for example, reducing the update frequency of animations running in tabs that aren't currently visible.
- 参考
  - https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations
