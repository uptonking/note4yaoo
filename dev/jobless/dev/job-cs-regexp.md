---
title: job-cs-regexp
tags: [job, regexp]
created: 2021-09-23T08:20:59.194Z
modified: 2021-09-23T08:21:59.990Z
---

# job-cs-regexp

# guide

- 从字符串中提取出有用信息
  - data = str.replace(reg, '$3-$1-$2')

# [regexp.exec(str)的返回值总是不同](https://stackoverflow.com/questions/11477415)
- A JavaScript `RegExp` object is stateful.
  - If your regular expression uses the "g" flag, you can use the exec method multiple times to find successive matches in the same string.
  - exec with a global regular expression is meant to be used in a loop, as it will still retrieve all matched subexpressions.
  - `exec()` will stop on each occurrence so you can run again on the remaining part. This behavior also exists with `test()`

- Personally, I prefer to go the other way around with `str.match(regexp)`

- `/regex/.exec()` returns only the first match found, while `"string".match()` returns all of them if you use the `g` flag in the regex.

# 正则表达式(括号)、[中括号]、{大括号}的区别小结

- () 是为了提取匹配的字符串。表达式中有几个()就有几个相应的匹配字符串。
  - (\s*)表示连续空格的字符串。
- []是定义匹配的字符范围。
- {}一般用来表示匹配的长度

- ()内的内容表示的是一个子表达式，()本身不匹配任何东西，也不限制匹配任何东西，只是把括号内的内容作为同一个表达式来处理，
  - 例如(ab){1,3}，就表示ab一起连续出现最少1次，最多3次。
  - 如果没有括号的话，ab{1,3},就表示a，后面紧跟的b出现最少1次，最多3次。
