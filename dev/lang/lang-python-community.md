---
title: lang-python-community
tags: [community, python]
created: 2023-08-28T06:14:04.458Z
modified: 2023-08-28T06:14:28.873Z
---

# lang-python-community

# guide

# discuss
- ## 

- ## 

- ## What is wrong with “is” in Python
- https://twitter.com/clcoding/status/1718350871610708374
- “is” operator compares address of both variable and return True if they are pointing at same address, otherwise False
  - If number is between 0 to 256, then that variable will point at fixed address only irrespective of shallow copy, deep copy or separate variable.
  - If number is >256 then it’ll create new address if they are deep copied or created separately.
  - But for larger numbers like 257, "a is b" is False because they are stored in different places in memory.

- The behavior we are observing is due to a memory optimization in Python, which is specific to small integer objects. 
  - In Python, small integer objects (typically in the range -5 to 256) are cached and reused for memory efficiency. 
  - When you assign the same integer value to multiple variables within this range, they will refer to the same memory location, which is why `is` returns `True` in such cases. 
  - 👉🏻 This is an optimization mechanism known as "interning."

- ## 🧐 TIL python does not recreate default function params each function call
- https://twitter.com/ethanniser/status/1716612454568861903
- Yep if the param is mutable this issue happens sadly
- Yea that’s known and not fixed
- One of the most annoying known quirks of Python

- ## 你们现在是用什么来管理Python版本和库依赖的？_202310
- https://twitter.com/river_leaves/status/1710489478924783778
- docker+pip
- 对于单机运行环境，例如科研、个人开发环境来说，conda固然是不错的，我也会用。但是如果需要CI/CD，conda太重了，大，慢，并且配套的生态也不是为CI/CD准备的。
