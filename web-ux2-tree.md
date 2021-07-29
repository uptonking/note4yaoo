---
title: web-ux2-tree
created: '2021-07-29T20:40:04.309Z'
modified: '2021-07-29T20:40:10.336Z'
---

# web-ux2-tree

# guide

- ## tree vs accordion
- ui设计上
  - tree的折叠展开按钮常在左边，accordion的折叠按钮常在右边
- 功能上
  - tree一般支持移动节点nodes，accordion一般不移动且不删除节点
  - accordion的嵌套层数一般不深
# discuss

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
