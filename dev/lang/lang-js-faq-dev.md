---
title: lang-js-faq-dev
tags: [dev, js, lang]
created: 2021-09-19T15:14:54.696Z
modified: 2021-09-19T15:16:22.324Z
---

# lang-js-faq-dev

# not-yet

# [String replace vs replaceAll](https://stackoverflow.com/questions/67296652)
- when calling `replaceAll` with a regex literal or `RegExp`, it must use the global flag `/g`. 
  - one difference with replaceAll is that when passing it a string, it will automatically do a global replacement. 
  - This is where you might save yourself a bit of typing, by not having to enter a global flag.
