---
title: thread-dev-enginnering-perf-optimization
tags: [engineering, optimization]
created: 2022-03-18T20:55:57.435Z
modified: 2022-03-18T20:56:35.254Z
---

# thread-dev-enginnering-perf-optimization

# guide

# discuss-stars
- ## 

- ## ☕️ 调优，高并发这些基本上都是伪需求。
- https://www.zhihu.com/question/602234735/answer/3056761380
- 首先，JVM调优那是面试八股文
  - 其次，总说JVM调优，是因为你只要敢在面试的时候回答，把Java8升级到Java17，你就可以“下周等结果”了
  - 同理高并发问题，大部分企业实际上最终方案都是多买几台服务器，但是你这么回答也是“下周等结果”

- 调优，高并发这些基本上都是伪需求。
  - 调优都是优化慢sql
  - 👉🏻 索引，缓存，分库分表，三件套一上，调个p的jvm

- 一说调优一坨八股，一说升级JDK都沉默了
- 然而的确是这样，很多公司解决性能问题的方案就是多加服务器，一台不够就加两台，两台不够就四台。
  - 底层架构不是说调整就调整的，至于说jvm调优的，架构师早就做了，哪有面试进来教架构师调优的，也就那些野鸡项目经理或者卖课的总提这破事

- 再大厂有没有用我不知道，刚入行时我也以为是八股文，直到我遇到了实际服务器性能问题深入学习了jvm之后才敢说略知一二。
  - 通过gc日志反向检查代码，保证生产中仅用2台服务器满足日常业务。在我没优化代码和调优之前只要到业务高峰期服务就奔溃。
  - 还有好处以前只是直观感觉哪些代码性能低效，现在能从内存层面分析

- 实际工作中，调优就是你看服务器有多少内存，然后你看看你这个服务最多能给多少，再不行，总是gc要不就考虑提高服务器的内存，要不就多买几台负载均衡。关于八股文里面的这个参数那个参数，都是奇技淫巧。-Xms 和 -Xmx可能就是你职业生涯调的极限了

- 自打用上java8以后，调优就不多了吧。以前用cms，工程放在4个虚拟机上，每个虚拟机2核256m，不调一调容易内存不够，从而挂掉 。full-gc那是一会儿一下，压测能明显感觉到gc对项目性能造成的波动。
  - 后来都用g1了，限制好最大堆，内存给稍微大一点，一般都没事了 
# discuss-rateLimitter
- ## 

- ## 

- ## 发现现在 Deepseek 每次请求, 都要算一下 PoW , 如果 Deepseek 现在发一个 POW 的币将绝杀.
- https://x.com/holegots/status/1888153737497296958
- ChatGPT网站接口也有这个保护
  - 看来大家面对大量调用都找到相同的解法
- 只是前端限制么
  - 每次请求会带到 Header 里面去调用

- 比特币白皮书里提到的hashcash陷门算法啊，验证容易求解难所以才有的PoW

- pow一开始就是用来防止垃圾邮件上
# discuss
- ## 

- ## 

- ## 

- ## JSON parsing is nearly ALWAYS the final boss when fighting bottlenecks in web apps
- https://twitter.com/wesleytodd/status/1783844714287972697
- It’s not really the JSON that’s the issue… it’s dumping a crap ton of data over the wire *as* JSON, so the parsing step is the bottleneck. Do that with almost any interchange format & you’ll end up in the same place.
- What would you suggest when fighting that boss in nodejs ?
  - Find other ways to parse less json (and no not like the other person said with binary formats). There are tons of well known ways to cache and optimize network optimizations and avoid unnecessary json parsing.
  - The best perf optimization is *always* remove the code. Remember that, no matter how fast you make the code, it is *always* slower than not running the code at all.
- Do you have some links to read about the best ways to "optimize network operations" ?
  - I dont have any. But a good place to start is just capturing a HAR file of your app and seeing how much data you are receiving over the wire. Look to reduce this, either via safe caching, slimming down response bodies, etc. Gotta measure it for it to improve!
- Back in the early days of microservices popularity someone told me over half of their compute was spent parsing and serializing JSON.

- ## 不是指数级的优化, 其实不用在意. 都是草台班子....
- https://twitter.com/hylarucoder/status/1783777605805629600

- ## Which latency numbers should a developer know?
- https://twitter.com/Franc0Fernand0/status/1779853436604805379
  - I found a website where you can visualize how those numbers changed. 
  - [Numbers Every Programmer Should Know By Year](https://colin-scott.github.io/personal_website/research/interactive_latency.html)

- As you rightly pointed out the data is questionable but nice visualization of how numbers have evolved over time.

- ## Terminal flamegraph tools feel under-appreciated.
- https://twitter.com/eatonphil/status/1764992041602187296
  - My default flow used to be: record a profile, scp it off my server, `<input type="file" />` upload it into some website, click to generate.
  - TUI flamegraph tools are much simpler!

- I should really figure out how to run pprof

- My typical workflow is to run bcc profile then run the flame graph perl script and then scp the SVG back to my own machine. Terminal would be a lot more convenient.

- ## [UUID Benchmark War | Hacker News _202402](https://news.ycombinator.com/item?id=39254871)
- 
- 
- 

- ## Have a lag radar that tells you if something takes longer than some interval, in real-time, no profile recordings.
- https://twitter.com/fabiospampinato/status/1650188305248518148
- I like your visualizing and framing as a "performance radar". I've built this FPS meter for the same purpose
  - https://twitter.com/schickling/status/1617637913935884290
- I had implemented an FPS meter too at some point, but it was harder to spot drops in frame rate (green vs red on the bar is more evident), and things can still be slow while fitting within one frame, the FPS meter won't spot that.

- I've seen stuff like this, but I'm always curious, how is it actionable? With log statements, you'd be able to look back through the history, and see which things took the most out of your time budget
- I'm using it like this:
  01.    I play with my components.
  02.    I take a note of which interactions cause the lag radar to show me some red.
  03.    Lastly I turn on the profiler and see exactly what's going on.
  - The radar is good for knowing when to profile, it's not a replacement for it.

- ## If importing an SVG is the best thing for you ergonomically, choose a solution that returns a URL for use with `<img>` , or extracts them into `<defs>` for use with `<use href="#">` .  
- https://twitter.com/_developit/status/1382838803866521601
  - Unlike JS, SVGs inlined into HTML are pretty cheap.
  - SVG in HTML is fine - it gets parsed and rendered once by the browser. 
  - SVG in JSX requires the JS to download & execute first, generate VDOM for the SVG, render that to DOM

- ## 最最简单的性能改善方法
- https://twitter.com/ThaddeusJiang/status/1511151150095298560
  01. frontend 分页请求数据
  02. frontend 不要重复请求相同 API
  03. backend 精简 response，提高 networking 响应速度
- 进阶：
  01. frontend 缓存从 API 请求的数据

- ## How to write fast code: reduce memory access. 
- https://twitter.com/devongovett/status/1504476131818237967
- All of these tips stem from that:
  01. Reduce the size of your data structures so more can fit in CPU cache.
  02. Replace strings with numbers.
  03. Make use of bit flags. Don’t waste space on booleans.
  04. Access memory linearly.
  05. Make judicious use of the heap. Inline the most commonly accessed values, move large or less common ones to the heap.
  06. Model data like a database. Normalize commonly used structures and pass ids rather than copying them around.
  07. Consider using a struct of arrays rather than an array of structs. For example, if you have two types of value, store them in separate arrays instead of a single one with a type field. This reduces memory usage and makes iterating by type linear.
  08. Maybe obvious, but avoid copying things, especially strings. Use pointers for substrings, and reference counting or interning to avoid multiple copies of the same string.
  09. Don't store data you can recompute quickly. It's often faster to do more CPU work with smaller data structures than it is to compute less but with more memory use. Memoizing and caching often _reduces_ performance. Always measure first.
  10. Use indexes rather than pointers. This expands on tip 6. Indexes often use less memory than pointers (e.g. <= 32 bit vs always 64 bit), allowing structures to be packed tighter, among many other advantages (e.g. all values of a type in one place)

- Another one to add: prefer sorted arrays to unsorted arrays

- the #1 rule for a fast code: choose the right algorithm and data structure for your problem.
  - You can also improve performance by increasing memory usage, for example by using Memoization
  - Re memoization, it's overused IMO. Measure first.

- Avoid branches as much as possible. Frequently is better to put number crunching code before and out of if-blocks even if there are cases that this calculations wouldn't be used.
