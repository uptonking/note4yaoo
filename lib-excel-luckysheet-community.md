---
title: lib-excel-luckysheet-community
tags: [community, luckysheet]
created: 2021-05-06T09:56:41.040Z
modified: 2022-08-21T09:57:42.969Z
---

# lib-excel-luckysheet-community

# guide

- fans
  - 图图
# discuss-stars
- ## [作为普通开发人员，最需要的在线预览Word和Excel](https://github.com/dream-num/univer/issues/11)
- 能把Office三大利器制作成在线编辑这个难度极高。
  - 👉🏻 但是，我们目前遇到的最大问题其实是：在线预览Word和Excel
  - 这个需求极大，或者说这个是刚需，至于在线编辑Word和Excel，反而并不那么大。
  - 因为，更多用户还是喜欢用Office软件本地编辑。

- 所以，希望能最先开发这个功能：在线预览Word和Excel。
  - （1）比如 https://officeweb365.com?src=Word_Online_URL
  - （2）微软的 view.officeapps.live.com/op/view.aspx?src=URL
  - （3）葡萄城的开发组件 grapecity.com.cn 等
  - 都是通过云服务收费，提供在线预览。

- 你这个如果做成这种最好，通过URL传递远程word或者excel， 然后在线预览。
  - dream-num.github.io/xls?url=http://xx.com/test.xls

- ## [Feature request]精简数据结构
- https://github.com/dream-num/Luckysheet/issues/418
- 通常excel导入后数据量会膨胀很多倍，
  - 方案一是pako压缩，
  - 再者，Luckysheet的本身数据也可以做优化，因为有许多配置是重复的，考虑写一个转换引擎作为前置插件，获取到用户操作类的配置，走插件转化为Luckysheet可识别的格式

- 我目前的做法是后端只保存表头跟开始行的数据结构，其余行的数据根据开始行这一行的数据结构，在前端去遍历组装。这样数据量就少很多很多
# discuss-fortune-sheet
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 各位好，鉴于目前Univer新版开发进度的问题，大家都在使用Luckysheet进行相关的应用系统的开发，
  - 但是由于版本bug比较多，给大家都带来很多困扰，为了能够更好服务大家，现团队会空出部分人力进行支持，帮助项目顺利开展。团队会根据大家报名顺序进行优先沟通交流。
- 这个意思就是：新版遥遥无期了，旧版基础上可以给用户定制开发，收费。挺好的路线
  - 现在开源太难了，搞点定制开发收入，不要伤了开源大佬的心
  - 我前年就在群里说过，大佬得搞定制开发，基础开源，上层定制开发
  - 有了基础开源，用户比较信任，上层定制的项目比较好谈。不像咱谈个项目，人家就不信任，因为看不到东西
- 前面有个高山，但是用户可不管这些，excel有的功能你都的有
- 走excel路线就死了，wps作为老二，半死不活。IT业没有老三的生存空间，何况lucky之上还有很多商业级类似系统
  - 只有卖增值服务才有饭吃
  - 走excel是通用路线，卖增值是定制路线
- 增值要建立在用户量基础上，通用是引流品
  - 对只会vue的不友好

- ## 我要写个什么数据格式才能把数据渲染到表格中呢
- 目前我们做法是模板和数据单独存储，前端页面加载时再把数据加到模板的data中
  - 单个sheet里面的data，最外层的data是完整的表格对象

- ## 有团队的自己做肯定会更好一点，没团队的就只能外接第三方的
- 我们已经直接对接WPS了, 自己折腾太费精力了， 还没别人用的好
- 早期spreadjs是按开发授权，后来变了，按部署收费了
  - spreadjs 按部署收费还要绑定ip，麻烦

- ## 现在再去看Luckysheet, 感觉有点功能太多. 拖累了速度，不能按需

- ## 我一直觉得LUCKYSHEET是个伤心的故事，_2022111
  - 看系统外表，还可以，看功能，还可以，看内部，哎。说明当初经历了一个漫长且极其伤心的例程
- spreadjs是做的真好，就是升级之后，授权变了，玩不起了
  - 给客户部署一套，就得给人家钱

- LUCKYSHEET是应对很多烂项目的神器
  - 烂项目，钱没多少，用户要求还想啥都有，此时LUCKY就展示威力了

- luckysheet没有做好基础架构时，就开始大量的堆积功能上去了，功能真挺全乎，实现不堪目睹
  - 这个luckysheet功能强，如果走报表，功能太强，如果走协同，协同这块代码又太弱。3.0的方向和代码压力很大。我感觉
  - 只能做小报表

- ## LUCKYSHEET每次操作都会保存全部，为了UNDO/REDO
  - 不支持变化量UNDO/redo
  - 随便做个操作他都会深拷贝所有数据用来撤销重做，这是最大的性能问题
- 渲染与计算，需要有挂起、启用机制，不然代码里一系列操作，会出现频繁渲染，频繁计算的问题
- 做电子表格，是个艰难的赛道。想搞好变化量算法，难啊
- 群里大部分是把它作为一个报表展示工具，不频繁编辑
- 想优化好，需要引入webworker+离屏渲染
  - 公式需要按需计算

- 表格里撤销重做都是简单粗暴的深拷贝一份原始数据，所以你想让他支持上万行数据不慢才怪呢
  - 就算能忍受性能低，数据多了后随便操作一会内存都能给你飙到几个G

- ## 大家有没好用的在线设计sql表的工具推荐下.js可集成那种. 类似这种.
- 一个毫无意义的功能[表情]，研发人员不需要，非研人员不会用
- 对于非研人员，数据库的字段定义和关系都是个迷局
- 微软的WPF都消亡了，脚手架大行其道，历史已经一再证明那些所谓的能简化编程的傻瓜界面，都是个摆设
- 如果要自己整合，推荐用mxGraph

- ## 我学的时候，都是js一把梭，出来发现都要框架
- JQ效率低，除非深入理解JQ的人，大部分都是写成DOM查找，更新。效率很低
- 双向绑定技术，编译阶段解决了查找问题，更新时直接定位到目标DOM
  - GET/SET时，已经是目标对象身上了。效率不是一个数量级啊
  - 用JQ也能高效率，把查找过的DOM对象都存起来，下次直接访问。用双向绑定也能低效率，对绑定变量大量重复赋值，每次赋值都会调用SET（有些SET会影响一大片）。所以，还是靠对底层的理解。理解不深，啥框架都白搭。

- ## 大数据量建议采用外挂模式，数据在外面处理，让luckysheet只处理当前你看到的

- ## ajreport\springreport\excel服务器\smartbi 都在用这个做报表设计器[表情]

- ## 那现在有什么好的方式能获得持续开发的支持呢？我看ruoyi是卖视频
- 走商业化，靠情怀多半会饿死
  - 走商业组件，开源版仅为了给点希望，核心功能只放在商业版本
  - 按年收费，不做买断
  - 一个商业用户抵得上你全部的打赏
  - 自己还没有吃饱的时候千万不要想着搞开源。
- 走商业的话，竞争对手会往死了搞你
  - 因为动了蛋糕
  - 大公司可以分分钟搞死Luckysheet
  - 看不看得上，要看有没有商业价值
- 葡萄城都不答应你起来
  - 那玩意现在都卖到一百万了，买断得一百万
- 不说商业了，就现在这个项目如果搞得非常成功，触碰到其他相同商业的项目，他们会想办法把你这个项目灭掉的。
- 撑不到中期
  - 就像某云服务器厂商因故障把某用户数据搞丢了，弄不回来了，然后把这个用户收购了

- 商业的话，组件技术支持必须跟得上，因为商业数据灾难，哪怕出现一次，都可能入狱

- 还是那个问题：究竟朝什么方向走？
  - 报表？现在开源的太多！
  - 协同？这个工作量超级大，需求还少！

- wps有web版本
  - 永中有web版本
  - onlyoffice有web版本

- ## 10 powerful Google Sheets formulas advanced users should know
- https://twitter.com/benlcollins/status/1511054363363524621
- 1) QUERY
- 2) SPARKLINE

- ## 🚀🪟 [Luckysheet, an open-source spreadsheet | Hacker News_202007](https://news.ycombinator.com/item?id=23994619)
- One reason I prefer Apple Numbers to Excel is that in Numbers you arrange tables on a canvas. 
  - The tables can refer to each other. 
  - I think it makes it easier to work with, for example, an input table and an output table because they are separate entities and not just different ranges on the same grid. 
  - It’s similar to how some websites enable you to configure a dashboard view of multiple tables and charts.
  - I’m wondering if the Numbers approach might work better. 
  - In particular it might be more natural for dynamic arrays because they would not “overlay” a range of cells.
  - They would be their own dynamically resizing table on the canvas.
- The main reason I tend to avoid Google Sheets is that they're slow. Slow to open, slow to update more complex sheets

- I will keep saying this every single time some one gets this wrong (which is at least 49 times out of 50): 👉🏻 the only way to handle scrolling properly on the web is for your `scroll` events to fall onto a real scrollable area, and to observe the effect it has (e.g. apply the scroll position to what you’re rendering with). 
  - This can be tricky to achieve well when you have dynamic content that the mouse needs to be able to interact with within that area, but it is possible to do well, with careful application of `position: sticky` and/or `position: fixed`.
  - As it stands, scrolling is nigh(几乎) unusable on my Surface Book: vertical scrolling goes at a million times the speed it should, and horizontal scrolling goes a million times as fast as it should in the wrong direction.
  - Don’t do scrolljacking. It’s bad, every single time. With the tools the web gives you it’s not possible to get it completely right that way.
- Absolutely. In the development process of our product DataGridXL we've also experimented a lot with "scrollwheel" events and such, for months really. It's just not possible to get it to feel natural. You might be able to get it working nicely on one specific OS+browser combo, but that's about it. 👉🏻 Always listen to the native "scroll" event
- You know your stuff, I can tell! In a pre-release version, we had hidden the native scrollbar and put our own scrollbar graphic on it that would animate using CSS transform according to native scroll offsets vs. DGXL viewport dimensions. The scrollbar size (width/height) and position made more sense, but at the end we couldn't get it to feel quite right. We're quite happy with the native scrollbar. It's fine on mobile too.
- The way I solved this in my own (not finished) web-based spreadsheet app is to have a scrollable div positioned over the canvas and to size the transparent div contents to the width/height of the sheet. Then I register scroll event handlers and redraw the canvas appropriately when the scroll changes. I think this is how Google sheets works, although it's a bit difficult to tell for sure.
- It seems difficult for a canvas-based spreadsheet to do native scrolling. The DOM is drawn in advance and there is no cost to scroll. But canvas is different, every frame of scrolling means calculation. In this case, the use of native scrolling will cause jamming and poor experience.

- With infinite scrolling, you can also just set the container to be absolutely huge, and use the scroll position to index. This works especially well for computed layouts like tables, where culling rows and columns is a simple scan over run lengths of row and column sizes. Likewise if you know things will be inserted at the top of a scroll view, you can pre-allocate above the “top”. The one thing that is hard to do well (but less hard now with new CSS features I think) is scrolling that feels good but always ends with the border of a cell being aligned to an edge of the scroll view (the Excel behaviour).
# discuss-collab
- ## 

- ## 

- ## [[BUG]ot算法有问题](https://github.com/dream-num/Luckysheet/issues/224)
- 并发插入列（行），插入在相同位置，文档状态不一致。

- ## [[BUG]两个bug](https://github.com/dream-num/Luckysheet/issues/1212)
  - 开启协同功能后, 前端websocket发给后端的数据无法用pako解压报, 报头错误, , , 我下断点拦截压缩之前的数据, 然后复制到本地用测试(直接copy的controller/server.js里面一模一样的代码)pako压缩后数据居然和我正常后端收到的数据不一样
- 已经解决了, 将luckysheet的pako升级到最新版重新build即可解决, 官方能不能走点心啊, 还是这个项目彻底摆烂了?
