---
title: thread-dev-engineering
tags: [dev, engineering, thread]
created: '2021-01-21T17:51:54.496Z'
modified: '2021-01-21T17:52:13.333Z'
---

# thread-dev-engineering

# guide

# pieces

- ## 

- ## A little technique we use all the time to audit the layout shifts and avoid performance issues.
- https://twitter.com/smashingmag/status/1352185650091581441
1. Add * { outline: 3px solid red } to your CSS.
2. Record the loading of your site/app.
3. Review it by exploring what happens in slow motion.
4. Adjust and minimize shifts.

- Great tip, thanks! This one's less visual and more programmatic from the 'Performance' tab in Chrome.
  - You can hover over the 'Moved from' keys and this will visualise the movement in the browser window.
  - And using this method you can even see down to the shift caused by web fonts loading.
- We can also use a `PerformanceObserver` to log elements causing layout shift to the console
- Remember this trick from when i started to learn css.
  - Always use to troubleshoot when some problem arises while postioning elements..
