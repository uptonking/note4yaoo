---
title: lang-c
tags: [c, lang]
created: 2019-09-07T04:06:53.538Z
modified: 2020-07-14T09:26:21.056Z
---

# lang-c

# guide 🧲

# basis

# discuss-toolchain
- ## 

- ## 

- ## 🐞 What tends to be more effective for finding memory leaks: valgrind, or a debug allocator (like dmalloc)? Or something else?
- https://twitter.com/eatonphil/status/1768242979192320430
  - In C it seems more common to use valgrind than to switch allocators.
  - Zig gives you a debug allocator though.
  - Curious about relative effectiveness or where one method works better on your experience.

- Use all the tools you can, Valgrind + custom memory allocator, with hints in your code to Valgrind works well. 
  - Valgrind can’t catch errors where you use a custom allocator on top of malloc/free. You can mark areas as (un)readable and (un)writable with the Valgrind API that are not “free” but  should not be accessed.
  - Since malloc/free are weak symbols it’s trivial to intercept them from the command line and run with your custom malloc/free.

- valgrind is pretty good. Some malloc implementations support flags to enable memory profiling and leak detection, which is not bad either. 
  - valgrind is linux only, so on BSDs people use the malloc flags to debug leaks.

- Both are fine, if you want to do it in prod custom allocators are better. Garbage collectors can be used this way as well (bdwgc, etc). They can also fix the leak for you temporarily (or permanently, if you can stomach that)

- I suggest Address/Leak Sanitizers for C.

- Address Sanitizer is SOTA imo when it comes to finding memory leaks.
  - Valgrind is a runner-up but tends to be slow at times.
  - You have your other competitors such as jemalloc and coverity. There's also purify
# discuss
- ## 

- ## 

- ## 

- ## [Why does C use the asterisk for pointers?](https://softwareengineering.stackexchange.com/questions/252023/why-does-c-use-the-asterisk-for-pointers)
- Simply - because B did.
