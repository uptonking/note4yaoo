---
title: note-web-layout-flexbox
tags: [layout, style, web]
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-17T08:53:14.923Z'
---

# note-web-layout-flexbox

## guide

- ref
  - [30分钟学会Flex布局](https://zhuanlan.zhihu.com/p/25303493)

 

## pieces

## Flexbox layout isn't slow

 - [Flexbox layout isn't slow](https://developers.google.com/web/updates/2013/10/Flexbox-layout-isn-t-slow)

- Wilson notes: some flexbox layouts were taking close to 100 milliseconds; reworking our layouts without flexbox reduced this to 10 milliseconds!
- Wilson's comments were about the original (legacy) flexbox that used `display: box;`
- We asked Ojan Vafai, who wrote much of the implementation in WebKit & Blink, about the newer flexbox model and implementation.
  - The new flexbox code has a lot fewer multi-pass layout codepaths. 
  - You can still hit multi-pass codepaths pretty easily though (e.g. `flex-align: stretch` is often 2-pass). 
  - In general, it should be much faster in the common case, but you can construct a case where it's equally as slow.
  - That said, if you can get away with it, regular block layout (non-float), will usually be as fast or faster than new flexbox since it's always single-pass. 
  - But new flexbox should be faster than using tables or writing custom JS-base layout code.
- Old vs New Flexbox Benchmark
  - Old is 2.3x slower than new.
  - I also ran the benchmark using `display:table-cell` and it hit 30ms, right between the two flexbox implementations.
  - The benchmarks above only represent the Blink & WebKit side of things. Due to the time of implementation, flexbox is nearly identical across Safari, Chrome & Android.
