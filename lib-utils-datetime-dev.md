---
title: lib-utils-datetime-dev
tags: [datetime, i18n, utils]
created: 2023-10-13T16:44:04.050Z
modified: 2023-10-13T16:44:29.825Z
---

# lib-utils-datetime-dev

# guide

# examples

# discuss

- ## 

- ## 

- ## 🌰 Just built a mini video generator and shipped it to Vercel in less than 100 minutes!
- https://twitter.com/JNYBGR/status/1715035990446723101
  - github日历热力图的动画
- That’s a simple square div with background. Nothing fancy

- ## No need for `moment` or `date-fns` .
- https://twitter.com/cpojer/status/1712697130589344192
  - 给出了计算relativeTime的简单代码
- I prefer to use date-fns rather than maintain all this code and dealing with browsers compatibility
- 👉🏻 Days don't always have 24 hours, months don't always have 30 days, years don't always have 365 days, users don't always use Gregorian calendars
- `new Intl.RelativeTimeFormat()` for every tick could become performance overhead for low devices. it's better to separately memoize it with just `locale` dependency
- Another time-based snippet, to convert e.g. `"2hours"` to `7_200_000` (with many different units). A simplified fork of @jkroso 's `parse-duration` library
