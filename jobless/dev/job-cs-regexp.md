---
title: job-cs-regexp
tags: [job, regexp]
created: '2021-09-23T08:20:59.194Z'
modified: '2021-09-23T08:21:59.990Z'
---

# job-cs-regexp

# guide

# [regexp.exec(str)的返回值总是不同](https://stackoverflow.com/questions/11477415)
- A JavaScript `RegExp` object is stateful.
  - If your regular expression uses the "g" flag, you can use the exec method multiple times to find successive matches in the same string.
  - exec with a global regular expression is meant to be used in a loop, as it will still retrieve all matched subexpressions.
  - `exec()` will stop on each occurrence so you can run again on the remaining part. This behavior also exists with `test()`

- Personally, I prefer to go the other way around with `str.match(regexp)`

- `/regex/.exec()` returns only the first match found, while `"string".match()` returns all of them if you use the `g` flag in the regex.
