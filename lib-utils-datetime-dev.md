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

- ## [What is your favorite date and time format in a file name? - Stack Overflow](https://stackoverflow.com/questions/1248747/what-is-your-favorite-date-and-time-format-in-a-file-name)
- Double dashes to separate the pieces, making each piece easy to see

- ## [Which Date-Time formats do humans prefer to read? - User Experience Stack Exchange](https://ux.stackexchange.com/questions/56646/which-date-time-formats-do-humans-prefer-to-read)
- This is about UX and the best UX is to let the user choose the one they are most familiar and comfortable with.

# discuss-date-ux
- ## 

- ## 

- ## 

- ## 🌰 Just built a mini video generator and shipped it to Vercel in less than 100 minutes!
- https://twitter.com/JNYBGR/status/1715035990446723101
  - github日历热力图的动画
- That’s a simple square div with background. Nothing fancy

# discuss-date-utils
- ## 

- ## 

- ## 

- ## [Why is 'getTimezoneOffset' implemented in the Date.prototype and not as a static method of Date? - Stack Overflow](https://stackoverflow.com/questions/50141269/why-is-gettimezoneoffset-implemented-in-the-date-prototype-and-not-as-a-static)
- Because of Daylight Saving Time. The UTC offset will be different in the same time zone depending on whether the date is before or after the DST change.
  - The time zone offset returned is the one that applies for the Date that it's called on. Where the host system is configured for daylight saving, the offset will change depending on the date and time that the Date represents and that daylight saving applies.

- ## I'm in the middle of replacing date-fns with temporal-polyfill.
- https://twitter.com/evoluhq/status/1749545877545378011

- ## No need for `moment` or `date-fns` .
- https://twitter.com/cpojer/status/1712697130589344192
  - 给出了计算relativeTime的简单代码
- I prefer to use date-fns rather than maintain all this code and dealing with browsers compatibility
- 👉🏻 Days don't always have 24 hours, months don't always have 30 days, years don't always have 365 days, users don't always use Gregorian calendars
- `new Intl.RelativeTimeFormat()` for every tick could become performance overhead for low devices. it's better to separately memoize it with just `locale` dependency
- Another time-based snippet, to convert e.g. `"2hours"` to `7_200_000` (with many different units). A simplified fork of @jkroso 's `parse-duration` library
