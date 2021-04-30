---
title: thread-lang-tips
tags: [lang, thread]
created: '2021-04-30T11:09:55.766Z'
modified: '2021-04-30T11:10:26.083Z'
---

# thread-lang-tips

# pieces

- ## 

- ## 

- ## 

- ## 

- ## The thing I appreciate the most from @rustlang is its mentality that it explicitly shows all possible problems and race conditions in your code. 
- https://twitter.com/CompuIves/status/1387830838792970243
  - You have to decide how to handle it, and you can decide to ignore it, but then you made that as a conscious decision.
- An example of this is parsing a string. 
  - Many languages would implicitly handle invalid strings by throwing an error, or worse, by returning something unexpected.
  - In Rust, the return type specifies that this can go wrong, and you can decide to handle the error or to let it panic.
