---
title: pm-list-pivot-table-views
tags: [pivot-table, pm]
created: 2023-08-02T10:32:16.941Z
modified: 2023-08-02T10:32:34.380Z
---

# pm-list-pivot-table-views

# guide

# views
- flexible-tabs
  - 当水平菜单项太多时，挤在一起无意义，参考过多的浏览器标签页

- image-view
  - 为了保护数据或各端一致的视觉效果，支持分享为图片
# draft

# view-split

- tips
  - 对三维场景或超宽画布更有用，可从不同角度查看同一场景的细节

- ## Here is how these multi-browser demos are being made. It's not websockets!
- https://twitter.com/wesbos/status/1727730566143803522
- https://github.com/wesbos/hot-tips/blob/main/fun-windows/scripts.ts
  - 20 popup windows moving them every 1 second

- ## so a lot of people have been asking me for code/writeup of this so I made a stripped down example (works with an infinite amount of windows)
- https://twitter.com/_nonfigurativ_/status/1727657155409363120

- https://github.com/bgstaal/multipleWindow3dScene /202311/js
  - https://bgstaal.github.io/multipleWindow3dScene/
  - quick example of how one can "synchronize" a 3d scene across multiple windows using three.js and localStorage

- I mucked about with localstorage events ages ago; BroadcastChannel is probably the preferred (and faster) way to do this now! Single file demo here
  - [Example of using BroadcastChannel to communicate with pages in the same domain](https://gist.github.com/davestewart/ae16e30091f457e3f4ddeeac569b8f2a)

- Could the delay when moving  be solved by using a service worker for communication between tabs?
  - The delay is actually related to `window.offsetX` for some reason lagging behind the windows' actual position for some weird reason, not communication.

- I've created a library that abstracts messages and Window/tab management.
- https://github.com/jcubic/sysend.js /202306/js
  - a small library that allows to send messages between pages that are open in the same browser
  - It also supports Cross-Domain communication (Cross-Origin). 
  - The library doesn't have any dependencies and uses the HTML5 `LocalStorage` API or `BroadcastChannel` API. 

- ## 分屏原型或球体: Entangled #fxhash
- https://twitter.com/_nonfigurativ_/status/1727322594570027343
  - 示例2个window，url分别为 eg.com/?seq=2&i=0 和 eg.com/?seq=11&i=1
- Clever. Same rendering left and right with different camera settings. When the window moves the x, y of the right object updates in both. Did I get it?
  - Yup
- Was thinking about something similar but forgot the different camera settings.

- Are you sharing window's positions via node (eventsource / socket / ...) ?
  - localStorage
- JS code in each window is writing positions to local storage
  - and window is reading other window's data to adapt the  other position.
  - You got the same scene in both windows
The url define which "globe" should be focused
- do you listen for “storage” event? Or just re-reading localStorage on requestAnimationFrame?
  - Using the event yes
- Has to be same origin though
- you can also use broadcast channels for cross-window communication
- eventsource API are the best, switch from socket to that you'll see

- How do the windows know their proximity?
  - `window.getScreenDetails()` + localStorage
  - Funny how this has been supported by Chromium based browsers since April of last year and still doesn't have support from FireFox and Safari

- Sync i=0 and i=1 over a websocket for multi users.

- I'm 99.9% certain it would not work on Wayland. But it's damn interesting and overall cool
  - It's security it's very tight, so info like window position is not possible I think because of fingerprinting etc

- ## 2、3、4个圆逐个测试
- https://twitter.com/jw1dev/status/1727641690775990671
- https://github.com/jw-12138/multi-window-collab-demo /vue
  - https://multi-window-collab-demo.vercel.app/
- 有什么好的应用场景呢
  - 多个屏幕之间的app协作？尤其是视觉类的，比如figma？
  - 跨屏渲染

- https://twitter.com/unixzii/status/1727912094513901669
- 跨窗口通信，本身复杂，鼠标的事件在两个窗口中继更麻烦。如果做出来的只是视觉效果，那就属于受益小的事情。大家都没有动力去做，只会在脑子里想想。如果有人做出来了，那确实足够酷，属于最原始最纯粹的好奇心驱动，当然要去看看。
- demo 里的方案只停留在 prototype 阶段，很多边缘情况都没有考虑，竞态读写、异常关闭怎么处理都是比较麻烦的。
- demo 里的窗口都在一个显示器里，其实还有窗口跨显示器的情况。不过这种也没有好的录屏方式放出来给大家看。
- 复杂是事情的固有属性，它不会随着你拿出一套解决方案而变得简单（simple）。如果你有一套成熟方案或第三方库，把复杂性隐藏起来，那么它会变得容易（easy）而不是简单。

- ## 这个神奇效果的应用场景是啥？除了炫技
- https://twitter.com/PenngXiao/status/1727627795554353464
- 跨窗口拖拽比较有用，其他的感觉没啥用啊
- 👉🏻 方便把其他文档的数据拖到自己的文件中使用。
- 分屏联动，百八十个屏幕一起，应该有很震撼的演出效果
- PPT?
- 应该是为了vr弄的吧
- 能跨两个屏幕才有应用场景
- 一个项目做组件库, 另一个项目使用组件库的时候! 如Figma中的2个文件

- ## 跨tab拖拽 tldraw: We're doing this? 
- https://twitter.com/steveruizok/status/1727625036159234555
  - cross browser too (chrome x safari)
  - the `window.roomDetails()` API is incredible. only in chrome unfortunately
- But why we doing this ? Really curious ?
  - 90% clout, 10% preventing stale tabs from overwriting local data when the same document is open in two tabs
- the cross tab sync is critical to avoid data loss, everyone app that uses local persistence either does this or prevents multiple tabs from being open at the same time

- Now do it so that it works on two different computers based on geolocation

- how are you getting the exact dimensions and position of those windows ???
  - screenLeft

- Did you have to do anything special to support dragging out of the window? Or does the browser still fire drag events even though the pointer is outside the window?
  - pointer capture API!
# more
