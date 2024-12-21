---
title: lib-collab-yjs-blog
tags: [blog, collaboration, yjs]
created: 2022-10-22T18:44:19.236Z
modified: 2022-10-22T18:45:00.382Z
---

# lib-collab-yjs-blog

# guide

# blogs

## 🌰 [Postgres and Yjs CRDT Collaborative Text Editing, Using PowerSync _202401](https://www.powersync.com/blog/postgres-and-yjs-crdt-collaborative-text-editing-using-powersync)

- we’re excited to release an initial Yjs + PowerSync demo which uses the Tiptap rich text editor
  - We built the demo as a React app with the PowerSync Web SDK, and used Supabase as our Postgres backend for simplicity.

## [YJS协同编辑入门，集成slate/codemirror](https://juejin.cn/post/7033041594911883271)

- 在slate-yjs的实现中，Element/Text 与 YMap 对应；
  - Element.children 与 YArray 对应；
  - Text.text 与 YText 对应。
- 对于 应用数据 与 协同数据 的绑定，忽略掉 yjs 的内部细节，在应用层只需要做两件事：
  - 第一，通过 AbstractType.observeDeep 监听协同数据，当其他副本的改动应用到本副本时，调用监听函数，然后将对应的改变应用于本副本；
  - 第二，将本副本的改动应用于协同数据，然后 yjs 会将协同数据的改动广播到其他副本。
- 需要注意的一点是，在 slate 中，通过 原子操作控制应用数据，并且编辑器的操作也会转化为原子操作。
- 所以在 slate-yjs中，通过 协同数据 和 原子操作 的相互转化完成了多副本的协同。

- 原子操作 到 协同数据
  - 将 Slate 的原子操作应用到 yjs 的数据上。
  - slate 的原子操作包括了九种。
  - 其中涉及到了 Node、Text 和 Selection 的操作。
  - 因为 Selection 不会对 slate 的数据造成影响，所以可以忽略。

- 协同数据 到 原子操作 
  - 将其他副本的协同数据产生的事件应用到原子操作。
  - 协同数据 产生的事件包括了 YText、YMap 和 YArray 的事件。
  - YArray 和 YText 都是链表结构。
  - 对他们的更改包含在 event.changes.delta，包括了 retain、insert 和 delete 操作。
  - YArray 的操作对应remove_node和insert_node原子操作；
  - YText 的操作对应 remove_text和insert_text原子操作。
  - YMap 是健值结构，对他的更改包含在 event.changes.keys 中，对应set_node原子操作。

## [Hocuspocus with Supabase _202306](https://emergence-engineering.com/blog/hocuspocus-with-supabase)

- prosemirror-colab will resolve conflicts for you, but you have to implement the backend yourself
  - Hocuspocus is a standalone server library for synchronizing Ydocs from Y.js across multiple clients. It was developed by the amazing engineers at TipTap. If you want collaborative editing in your application, you will probably come across Yjs and CRDT
- 
- 
- 

# yjs-usecase

## [CRDTs and collaborative playgrounds | Cerbos _202412](https://www.cerbos.dev/blog/crdts-and-collaborative-playground)

- One of the tools we offer is a collaborative IDE and testing environment we nicknamed the "Playground"
  - The Playground is a fully integrated collaborative IDE with built-in testing that provides feedback in real-time, and easily integrates into your GitOps workflow
- Cerbos leverages the power of CRDTs to facilitate real-time collaboration in our Playground, ensuring a seamless and efficient development experience. 

## [深入浅出 OpenSumi 协同编辑的原理 - SegmentFault 思否 _202304](https://segmentfault.com/a/1190000043721913)

- OpenSumi 选择基于 Yjs 的多人协同编辑方案
- 当前版本的协同模块设计还处于早期阶段，仍有一些限制，如
  - 不支持终端、调试的协同
  - 不支持来自非编辑器的文件改动协同（如 git pull）
  - 不支持重命名重构或其他需要跨文件级别的改动协同

## 📔 [How we made Jupyter Notebooks collaborative with Yjs _202106](https://blog.jupyter.org/how-we-made-jupyter-notebooks-collaborative-with-yjs-b8dff6a9d8af)

- the first collaborative Jupyter Notebook implementation, Colaboratory (or Colab), was created by Google engineers. They rewrote the UI for Jupyter Notebooks and gave it a collaborative notebook model via Google’s Realtime API, which was deprecated in 2017. 
- In 2013 William Stein launched CoCalc, a Jupyter notebook service with collaborative editing support right from the beginning. Like Colaboratory, CoCalc wrote a new UI for Jupyter Notebooks, while reusing other parts of the Jupyter architecture. They made different choices and implemented a custom solution for conflict resolution
- In 2017, Chris Colbert started the ambitious endeavor to build high-performance CRDT data structures that can be used as an observable data model.
- In 2019, Vidar Tonaas Fauske, Ian Rose, and Saul Shanabrook started work to integrate the Lumino CRDT into JupyterLab. Their work lived for a time in JupyterLab#6871 and has later been moved to a separate repository JupyterLab/rtc.
- While the Lumino CRDT is pretty awesome, in 2020 Brian Granger created a Lumino CRDT performance benchmark that revealed critical performance and algorithm issues (such as the so-called interleaving anomoly). In the process, Brian discovered my CRDT implementation Yjs and the two of us began to discuss CRDT implementations and Yjs in particular.
- After many discussions with Eric, we finally came up with a compromise that I’m now really excited about. Yjs and ModelDB only provide raw data structures to build collaborative applications. Our plan was to build a notebook model with an easy-to-use API to manipulate, observe, and synchronize changes on the notebook.

## [Syncing text files between browser and disk using Yjs and the File System Access API_202205](https://motif.land/blog/syncing-text-files-using-yjs-and-the-file-system-access-api)

- Wrote this blog post on how to sync files between browser and disk using Yjs and the File System Access API. It works really well! 
- https://twitter.com/michaelfester/status/1523698983117684736

- https://news.ycombinator.com/item?id=31315717

## 🧊 [yjs在runjs在线代码沙盒的应用](https://runjs.work/projects/b86ef5c4eddf4cc8) 

### 背景

- 当前大家使用协同文档编辑工具，应该已经比较普遍了，比如飞书、Google Docs、石墨、语雀等等。在线编辑器方面，CodePen有Collab Mode，Codesandbox已经实现了完整项目的协同。在线协同编辑代码(Collab Editing)，很酷，对吧？所以，我也希望能让RunJS支持协同模式。

- 经过初步的调研，有两种比较可行的方案。 
  - 第一种，将RunJS编辑器由CodeMirror5升级到CodeMirror6，其已支持[Collaborative Editing](https://codemirror.net/examples/collab/)。
  - 第二种，将RunJS编辑器升级为[Monaco Editor](https://microsoft.github.io/monaco-editor/)，并配合专门做数据协同的开源项目[Yjs](https://github.com/yjs/yjs)来实现Monaco Collab Editing.
- 由于CodeMirror6还不成熟，代码编辑体验不如Monaco，并且Yjs已经提供了集成Monaco的[示例](https://demos.yjs.dev/monaco/monaco.html)，最终我选择了Monaco。这部分工作已经完成。而协同编辑的部分，经过两周的技术调研，仍将持续。

为什么看似简单的协同编辑功能（人家连Monaco的示例代码都提供了），还要花这么长时间呢？这值得吗？围绕【深入研究Yjs的意义】，又引发了我更多的思考。

### 一、技术研究的深度问题。

对于Yjs的调研，是做到可以使用就行，还是深入源码和原理，彻底弄明白才好？

- 最初，我是希望可用就行。把Yjs+Monaco Editor的Demo运行起来后，赶紧想办法集成到RunJS产品中，仿佛RunJS Collab Mode近在眼前。现实给了我一记重锤：协同编辑，没那么容易！

- 首先是持久化。Yjs示例的服务端程序，只将数据持久化到文件（y-indexeddb），而线上产品显示不能这么干。为了协作数据的实时性，我采用了Yjs提供的y-redis包（没有文档）。经过一番尝试，redis持久化搞定了。
- 接着是身份认证。如果不修改Yjs的开源依赖包，认证所使用的token，只能通过第一次websocket请求的url传输，也太不安全了。而websocket连接一旦建立，Client和Server端的数据全是Yjs定制版的二进制Encoding/Decoding，并且只传输文档协作数据。不支持自定义第三方数据结构。后来，只能将部分Yjs包下载下来，自己修改、打包(RunJS-Yjs)，并建立私有npm仓库。这个问题算是勉强解决了吧。
- 然后是调试。引入了自定义的RunJS-Yjs，就得为其建立独立于项目的开发环境。难道要在这个项目里面再引入Monaco和React不成？NONONO！开源仓库的开发，并不像写为务代码，看一页面调试一个页面。Yjs的开发调试，完全依赖Unit Testing。做到这里，我又不得不将Yjs的开发、调试技术搞明白。在断点调试测试用例的过程中，又意外发现，Yjs的测试框架、加密解密算法，以及很多工具函数，也都是其作者完全自研的。不得不佩服他们的技术深度与广度！
- 最难的还是协作算法本身。Yjs实现了p2p的协作方式，并不是一定需要一个Sever端。只是现实业务中，总是需要有一个或多个中心化的服务器来做存储和权限控制。我最终是通过研读测试用例和源码，来试图理解算法的，结果发现效果并不好。我这才意识到，源码是理解代码实现的最佳方式，却不是理解架构和算法的好方法。架构和算法，在作者写的博客、做的访谈里面。果然，在官网的[Talks and Podcast](https://docs.yjs.dev/other-resources/talks-and-podcasts)部分，我开始了解到Yjs所实现的协作模式，叫做CRDT。Yjs项目从开始到现在，已经迭代了8年之久！

OK，Yjs大牛都研发了8年的开源项目，我能在2周之内消化掉吗？显然不能。对于Yjs的学习，得从长计议。那么，对Yjs的深入了解，还要继续吗？是的。站在RunJS的角度，从长计议的技术方案，并不具备当下的价值。但是，Yjs的持续学习，让我有机会将很多并不熟悉的技术串联在一起，比如websocket、二进制数据压缩与传输、npm私仓搭建、Visual Studio断点调试NodeJS源码、CRDT的实现原理等等。这都将为下一步的Yjs甚至其他技术的学习，打好基础。

把8年长跑的Yjs看作是一个产品，也能给RunJS以启发。核心竞争力的建立，并非一朝一夕。只有坚定的信念、持续的热情和死磕的精神，才能匹配一个人人称道的产品。

而技术人的成长，只有以以目标为画布，深度为底蕴，以广度为画笔，才能画出更好的明天。

### 二、产品研发的优先级问题。

- 对于RunJS而言，当前有比协同编辑更实用的功能。比如团队版，只要实现成员管理和他人可共享与编辑就可能，实时协作只是锦上添花。在资源有限的创业条件下，是短期实用优先，还是长期创新优先？

对此，我并没有准确答案，只是试图做一些解读。

如果将RunJS的生命周期放在1-2年，那么商业模式是最为重要的事情。为了挣钱去做的业务，却不能挣钱，有意义吗？没有。这可能是一种更为务实的思路，也许RunJS只是一种试错产品。不行，那就换个方向。

如果将RunJS的期望放在更长的周期，比如也像Yjs一样，至少做五年。那么，暂时的用户、流量、营销，都不再是重点。我将有充足的时间来打磨产品做创新。

所以，优先级的问题，就变成了定位问题。

就像一句诗句所言：渔夫出海前并不知道鱼在哪里，可是他们还是选择了出发。当我开始做RunJS时，我也不清楚它究竟会变成什么。直到现在，我也没有找到RunJS究竟会为用户带来什么，除了那个用户，是我自己。不过没有关系，有些产品的生命力，只会在未来绽放。

只要保持RunJS的产品创新不停止，产品体验持续优化，它终将变成一个为更多用户创造价值的产品。

## [从零实现一个在线面试工具](https://lifelonglearni.ng/Implement-an-online-interview-tool-from-scratch)

- https://github.com/naiba/axolotl
  - small online conference for interviewing or pair programming.
  - 依赖vue、go、yjs
# more
