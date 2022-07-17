---
title: thread-lang-tips
tags: [lang, thread]
created: 2021-04-30T11:09:55.766Z
modified: 2021-04-30T11:10:26.083Z
---

# thread-lang-tips

# guide

- ## This is how I have been learning TypeScript 
- https://twitter.com/alexpage_/status/1392338786193870851
- One multiplier I have been leaning into while learning new technologies is searching open source repos on GitHub.
  - Sort by recently indexed for up to date examples
  - Filter by language and code usage
  - Lurk(潜伏；诡计) pull requests to learn the why
  - I have this as my go to..have done for years.
# pieces
- ## 

- ## 

- ## 

- ## promise.unthen(cb) would be pretty useful
- https://twitter.com/justinfagnani/status/1422783049159221250
- Nowadays so many things are  Promises / async/await that EventEmitters and such have almost been forgotten.
  - It’s an interesting thing to remind oneself of: That Promises may not always be the better choice, sometimes events are preferable, like in this case 
- `Abort` works with fetch fine. But generic promises is a no go currently. Lots of holdup on exactly how to handle and expose aborting inside a custom executor.

- ## The thing I appreciate the most from @rustlang is its mentality that it explicitly shows all possible problems and race conditions in your code. 
- https://twitter.com/CompuIves/status/1387830838792970243
  - You have to decide how to handle it, and you can decide to ignore it, but then you made that as a conscious decision.
- An example of this is parsing a string. 
  - Many languages would implicitly handle invalid strings by throwing an error, or worse, by returning something unexpected.
  - In Rust, the return type specifies that this can go wrong, and you can decide to handle the error or to let it panic.
