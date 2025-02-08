---
title: web-ux2-tree
tags: [components, data-structure, tree]
created: 2021-07-29T20:40:04.309Z
modified: 2021-07-31T20:02:07.392Z
---

# web-ux2-tree

# guide

- ## tree vs accordion
- ui设计上
  - tree的折叠展开按钮常在左边，accordion的折叠按钮常在右边
- 功能上
  - tree一般支持移动节点nodes，accordion一般不移动且不删除节点
  - accordion的嵌套层数一般不深
# discuss-stars
- ## tabulator: Provide a way to lazy load tree node sub-items.
- https://github.com/olifolkerd/tabulator/issues/1801
- The table is simply not setup to load data asynchronously into child rows, and even if it were it would be a terrible user experience for users to click an element and nothing happen for a while untill the data loaded.
  - For that reason i have no intention of adding this as a feature to Tabulator.
  - That being said, if you wanted to implement something yourself it should be achievable.
  - I would recommend that you populate your rows with a dummy "loading" row that displays an ajax spinner when it is opened, that way the user is then aware that they are waiting for data.

- You don't need to load all data into a table at once. Tabulator comes with Progressive Ajax Loading to cover that scenario, 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 大家都是如何缓解这个问题的: 文件树层级过深
- https://x.com/zhdsuperman/status/1888156379715952864
- vscode会默认把一堆层级显示成一个文件夹
- 设置里开一下：减小缩进宽度 + 显示目录定位线

- 不用 nextjs
  - remix 用 . 而不是 / 符号分割，内部做转换好一点的

- 用next这种基于文件系统的路由自动配置方式就会有这个问题，但是好处也很明显，时时刻刻提醒开发者要注意URL语义化问题
  - 解决方法就是换一个更宽的带鱼屏

- ## Accordion versus TreeView and the DataGrid in the navigation data in Silverlight.__201207
- https://www.codeproject.com/Articles/415759/TreeView-vs-Accordion-vs-DataGrid
- In this application, in my opinion better is to use the Accordion. When we use only a single level hierarchical data.
- Treview control is equally attractive, but it seems that her destiny is appropriate tree structures of unknown depth or known elements, but more convenient to pass on this form above.
- In the above example shows a DataGrid worst, and not because of inadequacies. DataGrid gives great service in the structures that require a large number of items presented in a logical level.
- 

- ## Design for data tree variation of the accordion
- https://github.com/carbon-design-system/carbon/issues/2230
  - Rocket previously used an accordion as a type of data tree navigation. 
  - The v10 accordion moved the arrows to the right side which makes it more difficult to navigate and use as a data tree.
  - This issue is to design a way to navigate similar to a typical data tree.
- the primary use case would likely be for displaying any sort of hierarchical organization
  - we could likely include things like searching/filtering and selection for parts of the tree as well
- My product (Maximo) also requires this, although not strictly a tree view. It really is an accordion inside of an accordion. The accordion allows us to place the components we need at each level (not just text), but also have the entire tree collapsed on page-load.
- there is a planned variant of the tree view that requires more exploration

- ## Accordion inside accordion not working properly V10
- https://github.com/carbon-design-system/carbon/issues/4768
- The position is that generally, nested accordions should be avoided. That doesn't mean there might not be a use case where a team might "need" it. However, the accordion component in the Core/Common package is not going to be expanded to accommodate this feature. 
