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
