---
tags: [animation, style, web]
title: note-web-animation
created: '2019-10-16T06:58:19.848Z'
modified: '2019-10-17T09:09:49.857Z'
---

# note-web-animation

## animation
- 动画原理
    - 当页面最小化或被切换成后台标签页时，页面为不可见，浏览器会触发visibilitychange事件,并设置document.hidden属性为true；切换到显示状态时，页面为可见，也同样触发一个 visibilitychange事件，设置document.hidden属性为false
    - 每个Document都有一个动画帧请求回调函数列表，该列表可以看成是由`<handlerId, callback>`元组组成的集合。其中handlerId是一个整数，唯一地标识了元组在列表中的位置；callback是回调函数
    - 屏幕刷新频率，即图像在屏幕上更新的速度，也即屏幕上的图像每秒钟出现的次数，单位是赫兹(Hz)。对于一般笔记本电脑，这个频率大概是60Hz，这个值的设定受屏幕分辨率、屏幕尺寸和显卡的影响
    - 眼前所看到图像正在以每秒60次的频率刷新，由于刷新频率很高，因此你感觉不到它在刷新。而动画本质就是要让人眼看到图像被刷新而引起变化的视觉效果，这个变化要以连贯的、平滑的方式进行过渡
    - 刷新频率为60Hz的屏幕每16.7ms刷新一次，我们在屏幕每次刷新前，将图像的位置向左移动一个像素。这样一来，屏幕每次刷出来的图像位置都比前一个要差1px，因此你会看到图像在移动；由于我们人眼的视觉停留效应，当前位置的图像停留在大脑的印象还没消失，紧接着图像又被移到了下一个位置，因此你才会看到图像在流畅的移动，这就是视觉效果上形成的动画
    - `handlerId = requestAnimationFrame(callback)`
        - 传入一个callback函数，即动画回调函数
        - 返回值handlerId为浏览器定义的、大于0的整数，唯一标识了该回调函数在列表中位置
    - 浏览器执行过程
        - 首先要判断document.hidden属性是否为true,即**页面处于可见状态才会执行**- - 浏览器清空上一轮的动画函数
        - 方法返回的handlerId值会和动画函数callback，以`<handlerId,callback>`  进入到动画帧请求回调函数列表
        - 浏览器会遍历动画帧请求回调函数列表，根据handlerId的值大小，依次去执行相应的动画函数
- 可以用setInterval来实现动画，这种做法不太好，因为不同浏览器的刷新频率不一样（一般认为将间隔时间设置16ms为最佳,按每秒60帧算，1000/60≈16.67）
- `window.requestAnimationFrame()`
    - method tells the browser that you wish to perform an animation and requests that the browser call a specified function to update an animation before the next repaint.
    - The method takes a callback as an argument to be invoked before the repaint.
    - 此方法用来在页面重绘之前，通知浏览器调用一个指定的函数，以满足开发者操作动画的需求
        - 接受一个函数为参数，该函数会在重绘前调用
        - 该函数只会被传入一个DOMHighResTimeStamp参数，这个参数指示当前被 requestAnimationFrame序列化的函数队列被触发的时间
        - 如果想得到连贯的逐帧动画，函数中必须重新调用requestAnimationFrame()
    - 以浏览器的显示频率作为动画动作的频率，这样就不会过度绘制，也不会掉帧
        - 由系统来决定回调函数的执行时机，能保证回调函数在屏幕每一次的刷新间隔中只被执行一次
    - 优点
        - setInterval控制的动画其调用的间隔由程序员设置，而requestAnimationFrame无须设置调用间隔，它自动紧跟浏览器的刷新帧率(一般来说每秒60帧)，不会掉帧
        - cpu节能。使用setTimeout实现的动画，当页面被隐藏或最小化时，setTimeout仍然在后台执行动画任务，浪费CPU资源。而requestAnimationFrame则不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销
        - 函数节流。在高频率事件(resize,scroll等)中，为了防止在一个刷新间隔内发生多次函数执行，使用requestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销。一个刷新间隔内函数执行多次时没有意义的，因为显示器每16.7ms刷新一次，多次绘制并不会在屏幕上体现出来。
        - requestAnimationFrame会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成
            - 比如在1s的间隔内，在前半秒触发的10次事件，被推迟到1s的时候执行回调，可以认为是一个节流
        - 在隐藏或不可见的元素中，requestAnimationFrame将不会进行重绘或回流，这就意味着更少的的cpu、gpu和内存使用量
- ref
    - https://juejin.im/post/5b6020b8e51d4535253b30d1
- animation by js
    - js控制的动画大多使用`setInterval`或`setTimeout`每隔一段时间刷新元素的位置，来达到动画的效果
    - 这种方式并不能准确地控制动画帧率，尽管主流的浏览器（相当一部分的浏览器的显示频率是16.7ms,按每秒60帧算，1000/60≈16.67）对于这两个函数实现的动画都有一定的优化，但是这依然无法弥补它们性能问题
        - 主要原因是js的单线程机制使得其可能在有阻塞的情况下无法精确到毫秒触发
    - setTimeout是通过设置一个间隔时间来不断的改变图像的位置，从而达到动画效果
        - setTimeout的执行时间并不是确定的。在js中，setTimeout任务被放进了异步队列中，只有当主线程上的任务执行完以后，才会去检查该队列里的任务是否需要开始执行，因此setTimeout的实际执行时间一般要比其设定的时间晚一些
        - 不同设备的屏幕刷新频率可能会不同，而setTimeout只能设置一个固定的时间间隔
        - setTimeout的执行只是在内存中对图像属性进行改变，这个变化必须要等到屏幕下次刷新时才会被更新到屏幕上。如果两者的步调不一致，就可能会导致中间某一帧的操作被跨越过去，而直接更新下一帧的图像。这就一起了丢帧。



## css animation
- CSS Animations is a module of CSS that lets you animate the values of CSS properties over time, using keyframes 
- The behavior of these keyframe animations can be controlled by specifying their timing function, duration, their number of repetitions, and other attributes
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
