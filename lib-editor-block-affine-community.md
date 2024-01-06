---
title: lib-editor-block-affine-community
tags: [affine, block-editor, collaboration, community]
created: 2023-02-03T16:06:45.939Z
modified: 2023-02-03T16:12:13.346Z
---

# lib-editor-block-affine-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 这确实是目前 BlockSuite 最大的困扰之一, 跨 block 操作
- https://twitter.com/ewind1994/status/1743439055411708058
  - 最初，我将 BlockSuite 设计为在每个 block 里嵌入独立的富文本组件（即独立的 contenteditable）。这样再复杂的复杂 block 嵌套结构都能简单地用标准的前端框架渲染出来，只是其中的富文本部分走独立的 inline editor 而已。这种 inline editor 也特别简单， @flrande 刚来实习几周就搞定了
  - 这样开发效率非常高，但就会遇到横跨多个 block 时原生选区的问题。🐛 BlockSuite 沿用至今的方式是手动基于拖拽起止位置算选区，这样问题很多，其他编辑器都没有这么做。但我一段时间内都认为这属于框架的差异化亮点，现在看来这是个误区。
  - 但演化中我们逐渐发现，BlockSuite 真正的亮点并不是走单个 contenteditable 还是多个这种层面的实现细节，而是「能这么做」背后的本源：这种模式使得所有子 editor 的状态都全权由一份中心化的 CRDT 文档管理。换言之，以前做编辑器时围绕 editor 设计状态与数据生命周期的架构被推翻了。
  - 这使得 BlockSuite 允许你把传统上的一个大单体 editor 随便切分掉，只要各个组件都连到同一份 CRDT 数据层上就能即插即用。为此我们进一步支持了一种叫 fragment 的组件，这种组件能在 editor 外面独立存在。
  - 现在看来，单个还是多个 contenteditable 其实并不那么重要，学其他编辑器换回去也问题不大。且这也只是一个局部改造，已经设计好的 API 都能继续沿用。

- ## 传统上基于文件的文档同步粒度很粗，容易产生冲突。AFFiNE 则是将一篇文档的 block tree 编码到类似 protobuf 的 CRDT binary 格式，在多人协作时分发各自的 patch 来驱动状态更新。
- https://twitter.com/ewind1994/status/1717050757546168667
  - 你可以认为 AFFiNE 的 workspace 就是 clone 到你本地的特殊格式 git 仓库，自带字符粒度的冲突解决。
  - AFFiNE 的路线相比使用 JSON 或 protobuf 的不同之处在于，作为文档状态 source of truth 的 CRDT binary 支持在各个设备上以任意顺序互相合并 patch，同时保证最终一致性。这可以去掉在多人协作时传统上对中央节点的依赖，甚至允许 P2P 的数据同步（还没做，好多更优先的事情）
  - 但 CRDT 虽然对 local first 应用至关重要，它和 cloud app 并不冲突。一个想支持多人协作的 SaaS 产品完全可以将 CRDT 作为房间中同步数据的传输层来使用，这也是 AFFiNE 在自己的 cloud 服务中所使用的模式。所以基于 CRDT 的协作技术栈其实还是相当 progressive 的。
- 为什么这个协议不能是git
  - 基于 git 来做 local first 应用当然可行，只是这时的产品往往会更适合（或者说受限在）单人的数据同步，而不是多人实时协作。注意 git 的冲突处理粒度是单个文件，而 CRDT 是单个字符（且能自动合并），所以基于 git 天然地就要用户更多地手动解决冲突，不那么适合应用在重视实时协作的产品中。

- ## why you switch from Slate to Quill
- https://community.affine.pro/c/questions-answers/i-found-out-you-switched-from-slate-to-quill-in
- The original AFFiNE pre-alpha (open-sourced 2022/08) was using Slate as its editor framework. 
  - At that moment, we have already designed our architecture in a block-based way - this means that for a page with 100 blocks, we will hold 100 Slate instances, instead of a single monolith one, to render them. This allows us to use regular React components to compose our block tree, which greatly simplifies the block implementation of AFFiNE.
- However, there are several major cons with this approach:
  1. The selection and cursor states were managed by Slate autonomously, making it hard to reconcile the cursor after you edited multiple blocks and performed undo.
  2. The state synchronization between Slate and Yjs was too coarse grained. Every single edit within a text block will reset the block-level content, which bloats the history size and can't support character-wise collaboration.
  3. The code pattern was abusing hooks and didn't align to the best practice in React.

- So when I created BlockSuite, our own framework, I chose to leverage the block-based pattern with a more predictable tech stack. A major design decision here was to replace the rich text model with multiple Y. Text instances, so that we can support character-level time traveling.

- ## I would say that BlockSuite works very differently from traditional rich text editors_202301
- https://discord.com/channels/959027316334407691/1006208074316521573/1062287261724577822
- For rich text editing, multiple different nodes in the BlockSuite block tree can be connected to different rich text editing components, thus we are modeling rich text content as multiple UI components instead of a single UI container, eliminating the use of the dangerous monolith contenteditale - So for a page with hundreds of paragraphs, we can have hundreds of quill instances!
- With this design, the rich text components in BlockSuite will only contain **flat text content**, this greatly simplifies the architecture of managing rich text. 
  - That's also pretty much why we are using Quill temporally -  because its data structure is exactly modeled in this flat way, and its Delta format is natively supported by Yjs, bringing us a pretty stable experience. 
  - Based on this approach, we are actually only using a tiny feature subset of Quill, and it's also in our plan to build an alternative from the ground up.
- The thing that fascinates me about jumping out of the monolith contenteditable is to blur the boundary between the “editor” and “non-editor” part, making the tech stack of your collaborative app as regular as TodoMVC. 
- Note that this pattern requires a breakthrough in state management - for having intuitive undo/redo, we need to reconcile the state between different rich text components. Beforehand, I didn’t see any store library that supports rich text as its primitive, and that’s why we built our general-purpose store on top of Yjs since this’s what CRDT is extremely good at. Think about Redux-like time traveling that comes with zero-cost, character-wise incremental updates!
- With such a store, the view components of your blocks only need to subscribe to model updates
- This is a standard best practice, and although we are using the Lit framework (mainly for future WebComponent-based extensibility prepared for AFFiNE), I believe there is no rocket science or black magic here, and that’s how we build our AFFiNE editor just like developing yet another Dashboard app. 
- We haven’t started publicly endorsing this pattern because we are working hard on making the new AFFiNE stable and finding some best practices here. 

- This is also kind of how Notion is built if I'm not mistaken... It allows them to save each block as a row in the database as well, thus avoiding having to store a giant document with all the deltas generated by Yjs

- multiple-contentEditables design simplifies your initial implementation but prevents text selection of multiple blocks. Be careful accepting this limitation to begin with, because adding a wrapping ContentEditable later may be tricky.
