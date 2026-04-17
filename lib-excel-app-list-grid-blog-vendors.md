---
title: lib-excel-app-list-grid-blog-vendors
tags: [blog, excel, grid, spreadsheet, vendors]
created: 2023-11-12T06:45:18.495Z
modified: 2023-11-12T06:45:39.195Z
---

# lib-excel-app-list-grid-blog-vendors

# guide

- resources
  - [Comparison of Spreadsheet Programs](https://eylenburg.github.io/excel.htm)
# blogs-onlyoffice

## [精读onlyoffice在线表格存储设计 - 掘金](https://juejin.cn/post/7202252704978386999)

- 由于表格分布本质上是m*n矩阵，所以问题转换为矩阵的存储方案，目前主要有两种：二维矩阵和稀疏矩阵。

- 二维矩阵
  - 这种方案就是用二维数组存储数据，适合在纯数据展示场景下使用，在大数据量下进行插入/删除操作时性能差。所以一般不作为在线表格的存储方案

- 稀疏矩阵
  - 稀疏矩阵存储方案有多种
- 基于字典：这种实现有多种表达方式
  - 针对前端开发者，比较常见的写法是：`dict[row] = {}; dict[row][col]=value；`其执行效率和Javascript的执行引擎有关，
  - 以Chrome浏览器内部的V8为例，数组/对象默认就支持稀疏存储形式，查询、插入效率高，而且对象的key是有序的，但删除操作下由于引擎内部设计决定其效率不高；所以在数据量不大时，可以作为表格的存储方案
- 基于压缩稀疏列：这个本意是通过压缩技术减少空单元格的数量，实际工程里有多种实现方式
  - 用三个数组（value、row、column偏移）来存储矩阵
  - **葡萄城开发的SpreadJs也是使用类似方案** 
- 上述介绍的存储方案只考虑value数组中每个元素值为数值的情况，
  - 从表格功能看，每个单元格的内容还包括其他类型信息，包括存储值value、UI属性信息、状态标记（比如是否公式）、公式内容、行/列信息，value可能的数据类型包括数字、字符串、多行文本等
- 如果用普通对象形式作为格子的底层存储结构，受制于V8引擎内部内存分配策略，其很难支撑千万量级格子下的操作，因此考虑通过压缩技术来节省内存消耗

- 通过观察Cell内部结构字段内容，这里列出以下直观想法
  - 从数据类型看，Cell内部包含boolean、string、number三种基本类型，boolean和number类型的数据考虑通过字段压缩技术，将这几个字段的内容编码在一个Byte内，例如：type是一个枚举类型，假设有三种类型，用2个bit来表示，加上isDirty和isCalc类型，基本上一个Byte就能表示三个字段的值
  - 一般来说业务表格内会包含重复的字符串，或者单元格之间共享默认的样式信息，所以参照XLSX协议，引入共享字符串表技术，保证workbook中唯一的字符串类型出现一次，然后单元格通过索引（而不是内联方式存储到单元格中）来引用字符串。

- 上述也是Onlyoffice内部使用思路，结合矩阵的稀疏列存储思想，Sdk内部最终的存储效果如下，
  - 简单来说，是通过类型数组，将表格数据以二进制格式存储，通过字段压缩+共享字符串表来优化内存空间。
- 这里说明下和上述稀疏列存储的区别
  - 由于单元格通过字段压缩技术，所以row数组按照索引顺序依次排列，而不是只保存非空的行。
  - col索引数组是稀疏的，其内容指向具体row数组，这和上述提到的column数组是不一样。当然好处是直接通过下标访问到row数组，编程上更符合开发者的直觉

- 单元格信息压缩
  - 通过二进制形式，将一个Cell内容压缩成如下结构
  - 一个Cell的基本信息占用了17B，即使是空的Cell。
  - 如果单元格实际数据是Number类型，那么数据直接存储在Cell结构内；
  - 如果是字符串类型，那么通过索引+SST表来表示一个字符串
  - 样式下标、公式索引下标也是类似的，它们都存在类似SST的表，同样实现内存压缩目的。
  - 关于Cell内部状态信息，通过字段压缩技术，事先枚举所有状态信息的可能值，确定每个状态占用的bit大小，然后约定好协议在单个Byte内编码各个状态位置和bit大小，最后通过位操作从Byte内设置/获取对应的状态信息。

- 单元格列表
  - 为了存储单元格列表，onlyoffice内部开发SheetMemory数据结构，通过Js提供的类型数组（TypeArray）用来存储某段连续的二进制格式数据，包括某行/某列下单元格列表。
- 关于SheetMemory的设计读者可以先尝试想下需要考虑的因素，这里根据表格上层支持的功能，总结如下考虑要点：
  - 支持灵活扩容：由于表格稀疏特性，决定了调用者可以在任何一个Cell位置设置内容；所以如果设置的Cell行/列索引超过当前数据结构大小时，就要扩容，那么在具体编码时就要考虑扩容的策略
  - 支持批量插入/删除单元格：想象下用户批量插入/删除多行数据，这个行为对底层存储的要求就是在指定位置插入多个空的记录
  - 支持拷贝某个范围内的数据，比如用户通过拷贝/移动某个列的数据到另一个列，或者某个列进行排序操作结束后交换单元格区域
  - 在指定数据类型下，支持设置/获取某个位置的数据：数据类型有UInt8、Uint32、Uint64等，所以需要提供API方便上层调用设置Cell数据

- 扩容策略是在（当前数据量大小*1.5倍）和index之间取最大值，为何是1.5？
  - 这和分配时间复杂度有关，假设当前数据大小要扩大到maxIndex位置，如果按照structSize块大小进行扩容，那么内部会按照线性递增进行扩大，时间复杂度是O(N)；
  - 按照指数倍数（比如2倍）扩容，那么执行log(N)次数即可，时间复杂度最优。
  - 但是考虑到2倍的扩容策略可能会使内存浪费比较多，所以在时间和空间之间做了权衡，取1.5作为扩容指数。

- onlyoffice设计的这套存储方案支持在千万个格子下内存消耗足够少，这就为表格上层计算、渲染环节的缓存机制提供更多内存空间。
  - 该方案也说明了在设计数据结构时要结合语言特性来优化，特别是前端应用程序涉及大数据量存储，要考虑脚本执行引擎的限制，了解引擎内部的内存管理机制，方便应用层编写更高性能的程序。

## [onlyoffice表格字体渲染实现思路 - 掘金](https://juejin.cn/post/7175924445490446393)

- 字体渲染是浏览器自带的基本能力，不管是基于HTML还是Canvas渲染技术；
- 针对大型Excel表格，onlyoffice内部使用Canvas技术来渲染表格内容
- 现代浏览器实现Canvas内字体设置和渲染的方案有成熟的API直接使用，代码简写如下：

```JS
const canvas = document.createElement('canvas');
const ctx = canvas.getContext('2d');
ctx.font = '微软雅黑';
ctx.fillText('中', 0, 0)
```

- 这种方案能满足大部分场景需求，不过不同浏览器在字体解析和渲染实现存在差异，这会出现一致性问题
  - 同样的字符，在不同操作系统、不同浏览器展示效果可能不一致
  - 如果编辑器产品方案要考虑浏览器兼容性和渲染一致性问题时，那么编辑器内部就要接管字体的解析和渲染工作。

- onlyoffice整体方案类似浏览器底层文本渲染引擎的实现思路，浏览器内部展示文本的整体流程包括三个步骤：
  - 查找字体：根据CSS font-face语法指定一系列字体列表，查找时按照顺序遍历列表，找到第一个符合条件（比如本地是否有该字体的TTF文件）的字体
  - 加载字体：加载符合条件的本地字体文件
  - 渲染字体：这个步骤浏览器调用OS提供的文本排版引擎，然后调用浏览器的渲染引擎（一般是CG图形接口）直接绘制，不同OS实现了不同文本排版引擎，比如IOS提供CoreText，Window7后提供DirectWrite引擎，每种排版引擎都是各自自研的。
- 读到这里了解到字符展示的全流程，但是网页包括很多字符，这些是通过HTML标签和CSS来组织结构，最终通过浏览器布局引擎决定文本位置，而布局引擎内部涉及到文本排版相关也是调用了OS提供的文本排版API实现。

- 本文介绍onlyoffice表格编辑器内部文字渲染的基本流程，
  - 为了效果一致性考虑，它并没有直接调用浏览器内部提供的fillText这样API，而是基于FreeType字体库重新实现了一套全生命周期的渲染逻辑，包括字体查找、加载和渲染的流程；
  - 通过前后端协同，服务端事先准备字体的元信息、字体集列表、字体索引区间表信息并返回给前端页面，然后页面内部根据指定的文字和设置的字体集，查找对应的字体文件，通过FreeType库渲染得到该文字对应的位图信息，最终绘制该位图到Canvas画布上以展示文字

- 当然这套逻辑比较定制化，这部分源码不那么清晰易懂，而且FreeType渲染引擎和操作系统自带的文字渲染引擎差异可能会出现同样的文字渲染出细微差异，这给用户体验上也带来困扰，所以上述技术实现思路在大部分业务场景是使用不到的。
  - 但不妨作为一次学习机会了解文字渲染底层思路，以及wasm技术的应用，也能帮助理解基于Canvas技术内部的文字渲染原理

## [onlyoffice webExcel整体架构解读 - 掘金](https://juejin.cn/post/7139915650964815909)

- 最近由于业务需要，需要一个web-excel平台给用户提供数据分析能力，经过一番评估，确定使用onlyoffice提供的web-excel能力
- 文档管理服务
- 协同服务
- 转换服务

## [精读《WOPI协议》 - 掘金](https://juejin.cn/post/7105322391597187103)

- WOPI是微软基于REST API的协议，定义了一组Http操作，使客户端能够访问和改变服务器存储的文件。
- 假设开发者在Host机器上部署某个业务Web服务，某天产品提到要在这个Web服务上展示和编辑Excel文件，这个需求解决方案目前主要有两种：
  - 利用Javascript SDK，以纯前端方案打开该Excel文件，这类库包括LuckySheet、SpreadJS等
  - 集成已有的在线office平台，比如微软提供了Office Online App Server平台，允许第三方集成业务直接在网页中以Iframe方式嵌入Office页面，Office页面内部打开指定的Excel文档
- 第二种就是本文要讨论内容依赖的前提，它的好处是对前端开发者而言集成成本低，只需要通过Iframe嵌入到Host页面即可。那Office页面是如何知道去哪里打开获取到文档内容，文档信息是怎么告知给在线Office平台？这就是WOPI协议解决的问题。
- WOPI协议约定了Office Online服务和集成业务侧之间的通信协议，协议约定了一组接口操作，指明怎么从集成业务方获取和改变文件，该操作基于REST协议，这样对集成方而言只要提供了这些接口实现即可，开发成本可控。

- 在文档编辑器领域微软是业界的标杆，它设计了好几种开放协议，包括本文讨论的WOPI协议，还有后来者Vscode为了支持多语言的语法补全功能提出了LSP协议等，这些平台设计思路是类似的：希望开发者能基于协议共建平台的生态，放大平台的价值和产品生命力
# blogs-vendors

## 📝📈 [Making GRID's spreadsheet engine 10% faster_202310](https://alexharri.com/blog/grid-engine-performance)

- GRID's product sports a feature-complete spreadsheet engine running in the browser, with advanced features such as spilling, iterative calculation, and the QUERY function. It's a beaut.

- Profiling the recalculation, about 12.5% of the time was spent in a method called _makeCalcCellEvaluationContext.
- The cost of recalculation can be split into two distinct parts:
  - Determining which cells to recalculate, and in which order.
  - Recalculating cells.
- The recalculation of cells can further be split up into 
  - the fixed cost associated with recalculating a cell, 
  - and the variable cost associated with recalculating a cell.
- The variable cost is more immediately obvious: A cell invoking an expensive function like QUERY on a large dataset will take longer to recalculate than a cell adding two numbers together.
  - For the most part, the variable cost is derived from how expensive the cell's user-written formula is.
- The fixed cost arises from setting up the context needed to evaluate the formula. 
  - For example, when evaluating a reference like A1, the engine needs a bit of context to know which workbook and sheet to resolve the reference to.
  - there's other contextual information that the engine may require during recalculation. For example: structured references, mode-specific functions

- When recalculating a cell, the evaluation context is created and passed to a function that evaluates the cell's formula (more specifically, evaluates the formula's AST).
  - Whether a piece of information is used during evaluation depends entirely on the cell's formula, and the functions it invokes. By computing all properties ahead of time, we expend a fixed amount of effort for a variable amount of benefit.
- The first way to do less work is to lazily compute information, which we implemented through the use of getters.
- By only creating a single shared evaluation context object, we avoid spreading the workbook into a new object repeatedly — which also creates less work for the garbage collector.

- Conclusion
- Aside from the positive effect this change had on GRID's performance, I think it serves as a useful example to think about performance:
  - Which information do we need to evaluate now, and which can we evaluate later?
  - What is the fixed cost associated with performing this operation?
  - Do we need to do this work in the first place?
  - Can we cache the result of this operation? How does that impact memory usage?
- Bear in mind that changes yielding a performance boost in some cases might cause degraded performance in others. Consider the worst case scenario and the circumstances under which it might occur.

## 👥 [Making GRID's spreadsheet engine 10% faster | Hacker News_202310](https://news.ycombinator.com/item?id=37842914)

- I wonder how exactly do you name this category of spreadsheet app for SEO purposes? When i search top spreadsheet apps or Excel alternatives, apps like yours don’t often show up, instead I get AirTable, SmartSheets and other general spreadsheet apps that are not calculation intensive. 
- When we set out to build GRID, we quickly realized that what people use spreadsheets for can broadly be split in two categories: Models and tables.
  - Models are free-form sheets with formulas that typically generate insights in the form of output based on a set of inputs.
  - Tables are the structured sheets that typically have (somewhat) defined columns detailing the attributes of each row of data. Insights from tables generally come from filtering, grouping, aggregating and sorting the row-level data.
- As you point out, a lot more attention has been paid to the table use-case where people are essentially using their spreadsheets as small databases. 
  - Historically you could say this the usage pattern that gave birth to the modern BI tools (such as Qwik, Tableau and PowerBI). 
  - More recently, this is where companies like Airtable and Smartsheet play, but also to some extent what Coda and Notion are trying to achieve with their tables/databases.
- The models are where GRID shines. The unique value GRID offers is the ability to easily create and publish an interactive web document on top of spreadsheet calculations, whether the models are built in Excel, Google Sheets or in our own built-in GRID Sheets.
- I don't think this specific category has a name, but more broadly we've seen people talk about "next-gen spreadsheets" where - in addition to GRID - Equals, Rows and Spreadsheet.com also play, each with their own unique flavor.
- GRID is clearly the solution that leans most heavily into models and interactivity (hence the focus on our engine as evidenced e.g. by alexharri's article).
- While all the other solutions have capable calculation engines, I think it's fair to say that they are more focused on table-like use cases. 
  - Equals leans heavily into data connectivity, governance and reusability of spreadsheets, while Spreadsheet.com focuses a lot on project management use cases. Both offer an otherwise very traditional spreadsheet user experience. 
  - Rows has also focused a lot on connectivity, but lately they have leant heavily into AI to generate insights from data in their spreadsheets.

- Good write-up. What was understated but I appreciate was that this optimization was done late and after being picked up via profiling. For devs there is sometimes a drive to do this kind of work early. It really should always be done late just as in this post.

- This engine is closed source, it is used to power grid.is where you can make interactive blog posts, embeddable interactive graphs and so on.

## 📝📈 [Causal: Scaling our Spreadsheet Engine from Thousands to Billions of Cells - The Causal Blog_202207](https://www.causal.app/blog/scaling)

- [Scaling Causal's Spreadsheet Engine from Thousands to Billions of Cells: From Maps to Arrays](https://sirupsen.com/causal)

- Causal is a spreadsheet built for the 21st century to help people work better with numbers. 
- Behind Causal’s innocent web UI is a complex calculation engine — an interpreter that executes formulas on an in-memory, multidimensional database. 
  - The engine sends the result from evaluating expressions like `Price * Units` to the browser. 
  - The engine calculates the result for each dimension such as time, product name, country
- In the early days of Causal, the calculation engine ran in Javascript in the browser, but that only scaled to 10, 000s of cells. 
  - So we moved the calculation engine out of the browser to a Node.js service, getting us to acceptable performance for low 100, 000s of cells. 
  - In its latest and current iteration, we moved the calculation engine to Go, getting us to 1, 000, 000s of cells.
- But every time we scale up by an order of magnitude, our customers find new use-cases that require yet another order of magnitude more cells!
- how can we scale the calculation engine 100x, from millions to billions of cells?
- In summary: by moving from maps to arrays. 

- To understand, we have to explain two concepts from Causal that help keep your spreadsheet organized: dimensions and variables.
  - We might have a variable "Sales'” that is broken down by the dimensions "Product" and "Country". 

- 👣 Iteration 1: `map[int]*Cell`, 30m cells in ~6s ❌ 
  - In a first iteration we might represent Sales and its cells with a map. 
  - The integer index would be the dimension index to reference a specific cell.
  - An ostensible benefit of the map structure is that if a lot of cells are 0, then we don’t have to store those cells at all. In other words, this data structure seems useful for sparse models.
  - a nice property of the map is that it allows us to build sparse models with lots of empty cells. 
  - how do hashmaps work? You hash a key to find the bucket that this key/value pair is stored in. In that bucket, you insert the key and value. When the average size of the buckets grows to around ~6.5 entries, the number of buckets will double and all the entries will get re-shuffled (fairly expensive, and a good size to pre-size your maps)
  - by far the most expensive are these random memory reads that the map entails(使成为必然)
  - in this random-memory-read heavy world of using a hashmap that stores pointers, we can’t trust that cells will be adjacent. This is enormously wasteful for our precious memory bandwidth.
- 👣 Iteration 2: `[]Cell`, 30m cells in ~400ms
  - In the napkin math reference, random memory reads are ~50x slower than sequential access. A huge reason for this is that the CPU’s memory prefetcher cannot predict memory access.
  - We could consider mapping the index for the cells into a large, pre-allocated array. Then cell access would be just a single random-read of 50ns! 
  - This means that the CPU can be smart and prefetch memory because it can reasonably predict what we’ll access next.
- 👣 Iteration 3: Threading, 250ms 🤔
  - Generally, we expect threading to speed things up substantially as we’re able to utilize more cores. However, in this case, we’re memory bound, not computationally bound.
  - if you’re memory bound, you only need about ~3-4 cores to exhaust memory bandwidth. More won’t help much. But they do help, because a single thread cannot exhaust memory bandwidth on most CPUs.
  - When implemented however, we only get a 0.6x speedup (400ms → 250ms), and not a 3x speed-up (130ms)? I am frankly not sure how to explain this ~120ms gap.
  - Either way, we definitely seem to be memory bound now. Then there’s only two ways forward: (1) Get more memory bandwidth on a different machine, or (2) Reduce the amount of memory we’re using. Let’s try to find some more brrr with (2).
- 👣 Iteration 4: Smaller Cells, 88 bytes → 32 bytes, 70ms 😍
  - The cell stores things like formulas, but for many cells, we don’t actually need the formula stored with the cell. For most cells in Causal, the formula is the same as the previous cell. 
  - By more carefully writing the calculation engine’s interpreter to keep track of the context, we should be able to remove various pointers to e.g. the parent variable.
  - As a general pattern, we can reduce the size of the cell by switching from an `array of structs` design to a `struct of arrays` design, in other words, if we’re in a cell with index 328, and need the formula for the cell, we could look up index 328 in a formula array. These are called parallel arrays. Even if we access a different formula for every single cell the CPU is smart enough to detect that it’s another sequential access. This is generally much faster than using pointers.
  - None of this is particularly hard to do, but it wasn’t until now that we realized how paramount this was to the engine’s performance! 
  - Unfortunately, the profiler isn't yet helpful enough to tell you that reducing the size of a struct below that 64-byte threshold can lead to non-linear performance increases. You need to know to use tools like pahole(1) for that.
- 👣 Iteration 5: `[]float64` w/ Parallel Arrays, 20ms 🤤
  - We get to ~2.4s for 1B cells by moving allocations into the threads that actually need them
  - However, localizing allocations start to get into a territory(范围，领域) of what would be quite hard to implement generically in reality—so we’ll stop around here until we have the luxury of this problem being the bottleneck. 
- 👣 Iteration N: SIMD, compression, GPU …
  - there are lots of optimizations we can do. Go’s compiler currently doesn’t do SIMD, which allows us to get even more memory bandwidth. 
  - Another path for optimization that’s common for number-heavy programs is to encode the numbers, e.g. delta-encoding. Because we’re constrained by memory bandwidth more than compute, counter-intuitively, compression can make the program faster. Since the CPU is stalled for tons of cycles while waiting for memory access, we can use these extra cycles to do simple arithmetic to decompress.
  - Another trend from the AI-community when it comes to number-crunching too is to leverage GPUs. These have enormous memory bandwidth. However, we can create serious bottlenecks when it comes to moving memory back and forth between the CPU and GPU

- Conclusion
- Rethinking the core data structure from first principles, and understanding exactly why each part of the current data structure and access patterns was slow got us out of disappointing
- This way of thinking about designing software is often referred to as data-oriented engineering, and this talk by Andrew Kelly, the author of the Zig compiler, is an excellent primer that was inspirational to the team.
- With these results, we were able to build a technical roadmap for incrementally moving the engine towards a more data-oriented design. The reality is far more complicated, as the calculation engine is north of 40K lines of code. 

- The biggest performance take-aways for us were:
  - When you’re stuck with performance on profilers, start thinking about the problem from first principles
  - Use indices, not pointers when possible
  - Use array of structs when you access almost everything all the time, use struct of arrays when you don’t
  - Use arrays instead of maps when possible; the data needs to be very sparse for the memory savings to be worth it
  - Memory bandwidth is precious, and you can’t just parallelize your way out of it!

- Causal doesn’t smoothly support 1 billion cells yet, but we feel confident in our ability to iterate our way there. 

- discussions

- 

## 👥 [causal: Scaling our spreadsheet engine from thousands to billions of cells | Hacker News _202207](https://news.ycombinator.com/item?id=32000400)

- This brings me back to when I worked on Excel. The formatting structs (and most cell related ones) are so tightly packed and the byte code VM for the formulas is pretty neat.

- I work as a consultant and spend five out of eight hours a day in Excel, and I want the features in this app so bad. Sadly, the only way I’ll be able to use these features is if Microsoft bought them out and integrated them into Excel. 
  - It’s ubiquitous at almost every workplace you go to, but the only innovation of the past 20 years seems to be PQ (which is awesome), and xlookup.
- Excel added lambdas recently which is nice for defining custom functions without having to expect anything special on the client side (well, other than a newer copy of Excel at the moment).

- What is your strategy for storage? It seems that because you're offering this as SaaS, your customers both set a high bar for durability of their data and your COGS would be very high if you just kept a sheet this big in memory all the time.
  - Right now we keep our paid customer models' in memory. Models in free accounts are just evaluated every time (these models are usually much smaller). For now we want to avoid the complexity of distributed systems and just run this on very powerful machines with lots of RAM. 
  - For reference, one of our enterprise competitors has a calculation engine that can do 40B cells on a single host (using Java!).
- How are you ensuring the durability of the data?
  - We store the model representation (formulas, data) in Postgres. We just keep it in memory for computing updates faster.

- Indeed, moving memory back and forth from CPUs to GPUs has an overhead. There are ways to mitigate this though! I vaguely remember that one of the patterns in reducing this movement was to keep the data in the GPU as much as possible. I haven't kept up with the latest tech in GPUs off late. When I first played around with CUDA, ArrayFire (arrayfire.com) (no affiliation) was a promising library, and might be a good fit for your GPU prototypes?

- This needs to be able to be run locally/natively. Most companies would not want to run this with their proprietary data in a third party SaaS

- I’m curious how incremental updates fit into this? 
  - That's what I wonder about too. I imagine that a slow calculation would be fine if done once when the data is first loaded into the system. Once the results are in memory, any new data should only affect smallish subsets of cells.
  - 💡 This is the approach our product Grist (https://www.getgrist.com) takes for its calculation engine. Keeping track of dependencies slows it down for the initial load, but beyond that, it only needs to calculate what's needed, so most updates are fast. Even though the engine literally evaluates user-defined Python code for every cell.

- 🎮 Looks very similar to ECS-style data storage used in video games. Have you looked at using opaque index-based IDs instead of references?
  - I've implemented ECS many times but I still have a hard time to see what you're referring to. What are the similarities?

- I'm pretty sure this is better addressed with SQL.
  - We spent a fair amount of time trying to get this executing fast on SQL. However, with spreadsheets you recursively compute a lot of values. You can do this in SQL with recursive CTEs, but it’s slow, they’re not optimized for this. They also of course won’t do smart caching and dependency management for the cache. Fundamentally, it’s possible, but then we’d need to start hacking on a DB engine to make it work as a sheet. We concluded it’s better to continue on our existing engine.
# blogs-excel

## [Excel workbook layout and the performance of reading data with Power Query in Power BI_202311](https://blog.crossjoin.co.uk/2023/11/12/excel-workbook-layout-and-the-performance-of-reading-data-with-power-query-in-power-bi/)

- Excel workbooks are one of the slowest data sources you can use with Power Query in Excel or Power BI. 
  - So: reading a small amount of data from a table on a worksheet with a large amount of other data on it is very slow.
  - What can we learn from this? Well, if you can influence the structure and layout of the Excel workbooks you are using as a data source – and that’s a big if, because in most cases you can’t – and you only need to read some of the data from them, you should put the tables of data you are using as a source on separate worksheets and not on the same worksheet as any other large ranges or tables of data.
# blogs-airtable-like

## 📈🛢️ [mondayDB architecture _202307](https://medium.com/@liranbrimer/nice-to-meet-you-mondaydb-architecture-6d201b41e660)

- [Why Monday.com decided to build its new database instead of buying one | TechCrunch _202310](https://techcrunch.com/2023/10/22/monday-mondaydb-new-database/)

- mondayDB is the new in-house data engine we crafted at monday.com.
  - We refer to ourselves as a Work OS (Operating System) because we equip our users with a platform they can customize and extend, creating a tailored system to manage and automate any aspect of their work.
  - The key building block of our platform is the “board”. This is basically a very rich table to manage any kind of data — from tasks and projects through deals, marketing campaigns
  - Each board has columns, which can contain a range of things from basics like text, numbers, or dates to more complex types like a person, team, tag, or even files and formulas. 
  - We offer over 40 types of columns, and our users enjoy the freedom to filter, sort, or aggregate just about any column combination

- when a user landed on their board, we threw all the board data right into the client (usually a web browser running on a desktop computer).
  - but this approach had obvious limitations. First and foremost, the client is limited in its resources.
- Something clearly had to change. So we decided to move everything to the server side, allowing the client to receive only a subset of items in pages as they scrolled. It was easier for the client but not so trivial for the backend.

- we explored many of them, including traditional RDBMS databases with partitions (think MySQL instance per account with a dedicated table per board), ElasticSearch, analytical databases like Apache Pinot, ClickHouse or Apache Druid, and a wide range of NoSQLs like CockroachDB, Couchbase, and more.
  - Eventually, we found that none of these options completely met our requirements. 
  - The reasons varied from our data being mutable, our requirement for numerous tables, not knowing in advance what users would want to filter, and many more.

- Concept #1: Columnar storage
  - In a traditional RDBMS such as MySQL, the row is king, and all the row data is stored together on a disk as an atomic unit.
  - While this setup works smoothly when accessing all the data from that row, it’s less efficient when carrying out operations like filtering a specific column. 
  - This is because you’d need to pull all the table’s data unless you had prepared a column index in advance (which is something we can’t do without prior knowledge of the schema or queries).
  - A columnar database, on the other hand, slices the data vertically by column. What this essentially means is that the values of each column’s cells get stored together on the disk as an atomic unit.
  - An immediate downside that stands out is that we would have needed to store more data for the columnar store, as the item ID had to be repeated for each cell value. 
  - However, this issue is considerably less problematic when we realize that the data is highly compressible, especially when the column displays low cardinality, meaning we have limited repeating values.
  - the advantages are massive.we’d only need to fetch a mere fraction of the actual data involved in the filter. Furthermore, as many of our columns are quite sparse, even if the Board is extensive, the data you’d need to retrieve and process could be relatively small.
  - Lastly, the columnar structure opens up tons of optimization opportunities.

- Concept #2: Lambda architecture
  - we store all the column’s cells together as a single atomic data unit. It implies we can’t fetch or update a single cell separately. 
  - let’s face it, constantly fetching and re-writing an entire column for each single cell update is not only impractical
  - Lambda architecture to the rescue. Not to be confused with AWS lambda functions, it was invented by the big data industry to enable you to pre-calculate in advance query results on your data offline. This means queries are executed fast in runtime. 
  - The main advantage is that it still serves fresh data recently ingested after the last offline pre-calculation has occurred.
  - We divide our system into three components:
  - Speed layer — contains only recently changed data
  - Batch layer — contains all the past historical data
  - Serving layer — serves queries by merging the speed and batch layers’ data in runtime
  - data flows from speed to batch layer. This is handled by a scheduled offline job flushing the data, and building the metadata and other heavy pre-calculations along the way.
  - we utilize Redis as our speed layer storage, and Cassandra as our batch layer storage. 
  - Both of those storages are treated as a straightforward key-value store, where the key corresponds to the column id and the value is the column’s cells data.
  - I mentioned that we store the entire column data on a disk as a single data unit. The truth is, we break down large columns into smaller partitions. This aligns with best practices for Cassandra, our batch layer storage, to avoid oversized partitions. 

- Concept #3: Separate storage from compute
  - The bottom line is we want our architecture to be elastic. 
  - When we need more computational power (CPU) for heavier queries or during peak hours, we want to scale up processing servers. 
  - And similarly, we want to be able to scale our storage layer to meet our data capacity demands, separated from any data processing considerations.
  - Our architecture offers precisely that. Our batch layer is our storage layer and can be scaled independent of our servers engaged in executing query logic, and those servers also scale independently.
  - The beauty of that approach is that we don’t need to re-execute the query on every page the client requests. Plus, the client can skip by specific offset without having to go over all the items below that offset 
  - this approach isn’t without its drawbacks. For instance, how would the user know how to render the page to simulate a lengthy scrollbar? Or figure out what offset to skip when they scroll quickly? And how could they update the view with live mutations by others since the last snapshot? Those are excellent questions (+1 to myself), but they really deserve their own blog post.

- What’s next?
  - It’s a long journey as every component of the system needs to adapt to handle only subsets of the data using pagination, rather than having all data readily available to the client. We’ve implemented it for boards, but we have many other components such as our mobile apps, API, views, dashboards, and docs. 
  - Furthermore, we now need a more intelligent client that can function in hybrid mode. 
- there’s substantial room for improvement and lots of optimizations yet to be implemented. 
  - To name a few, we have many in-process executions we can parallelize, and we could considerably benefit from adding pre-calculations to generate metadata, indexes, and optimization structures like Bloom filter, among others.

- we have dozens of different column types, each one with its unique filter, sort, and aggregation logic. 
  - It’s all JavaScript, encapsulated in a shared package between our client and backend so it can run in hybrid mode. 
  - Accordingly, our engine is also JavaScript all the way down. 
  - We chose this direction to streamline our efforts, even though it’s no secret that JavaScript may not be the optimal choice for a high-performance system.

### 👥 [MondayDB: A new in-house data engine from monday.com | Hacker News_202310](https://news.ycombinator.com/item?id=37818562)

- > Unlimited tables
  - If you ever find yourself in a position where you need a database table per instance of an abstraction, you've almost certainly failed to model the domain appropriately.

- AirTable developed their own DB, but their case may be justified. I listened to an interview with a founder once - very thoughtful and reasonable. They fully understood what they were getting into.
  - Not sure why they needed own DB. Fibery.io has similar domain and we built everything on Postgres. Works like a charm and you even don't have Airtable bases connectivity problem. We have schema-per-customer and table-per-entity-type model, performance is quite good.

- don't tell them about SQLite! It's the secret sauce behind Grist (I am a founder), and we are sort of competitors. Wouldn't want Monday.com knowing about our competitive advantage!

- Honestly, the end result was a lot worse than I expected. Using Redis & Cassandra as 1 db, when your requirements where unlimited tables, fast filter/sort, etc. Literally the worst of all worlds imaginable.
  - Imagine maintaining that (2 separate distributed async-by-default, no transactions/indexes, limited-types, etc etc clusters).
- A lot of the architectural decisions, from a high-level, make sense: compute and storage are separated, redis and cassandra are used instead of reinventing those. It's a bit OLAP and a bit OLTP in that users might make a few point updates to things here and there OLTP but then the filtering and aggregating and showing all sorts of views and such is clearly in the analytics domain hence OLAP and the use of a columnar setup.

- Postgres / MySQL with a table per board (or one giant partitioned table with a JSONb column) would have been totally fine, as would have one SQLite database per customer that you can load the initial page of and then ship the whole thing to the client for richer interactivity.

- Article shows that Cassandra is slow to retrieve data, so they added Redis as a cache to fetch recent events from there.
  - It is now planet scale! Proper database design and indexes be damned!

## 📈 [airtable: Building a modular software toolkit | The Airtable Engineering Blog | Medium _202102](https://medium.com/airtable-eng/building-a-modular-software-toolkit-ce4efd06e75c)

- At Airtable, we’re building a toolkit that anybody can use to build their own software.
  - You can combine the many different building blocks provided in Airtable to create software that is truly tailored to your needs, rather than having to force your workflows into a one-size-fits-all solution that only vaguely applies to your problem.
  - Our toolkit-style approach brings significant benefits both for our customers and for our product development process

- Modularity as a lever
  - By building a flexible and modular set of building blocks, we can develop features that are highly leveraged. When we add a new building block to the toolkit, it can interact with every other existing building block
  - For example, take rich text formatting. Airtable currently provides over two dozen field types, from basic ones like text, number, and single select fields, to more advanced ones like formula, linked record
- Modularity’s costs
  - This means that each feature in Airtable is akin to a public API that other features can depend on. 
  - As we design new features or improve existing ones, we must think very critically about the interface that each feature exposes
- Addressing these challenges at Airtable

## 🧮 [notion: The data model behind Notion's flexibility_202105](https://www.notion.so/blog/data-model-behind-notion)

- 
- 
- 
- 

# more
