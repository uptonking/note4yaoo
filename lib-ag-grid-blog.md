---
title: lib-ag-grid-blog
tags: [ag-grid, blog]
created: '2020-07-30T13:50:07.752Z'
modified: '2020-07-30T16:43:01.318Z'
---

# lib-ag-grid-blog

## 8 Performance Hacks for JavaScript

- [8 Performance Hacks for JavaScript_201709](https://www.ag-grid.com/ag-grid-8-performance-hacks-for-javascript/)

- Row virtualization
- Column virtualization
- Exploit Event Propagation
- Throw Away DOM
  - Good programming sense tells you to de-construct everything you construct. 
  - In the context of your framework, it means removing components from their parents when the component is disposed.
  - This hack goes as follows: if you are removing an item from the DOM (e.g. a grid cell) but you know the parent of that item is also going to be removed (e.g. a grid row) then there is no need to remove the child items individually.
- innerHTML where possible
  - What is the fastest way to populate lots of cells and rows into the browser? 
    - Should you use JavaScript (i.e. document.createElement()) to create each element, update the attributes of each element and use appendChild() to plug all the elements together? 
    - Or should you work off document fragments? 
    - Alternatively should you create all the document in a large piece of HTML and then insert it into the dom by setting the property .innerHTML?
  - We have done many tests. 
    - The answer is to use `.innerHTML` .
- Debouncing Scroll Events
- Animation Frames
- Avoid Row Order

- All of the performance hacks above are the result of years of learning. 

- 

## Inside ag-Grid: techniques to make the fastest JavaScript datagrid

- [Inside ag-Grid: techniques to make the fastest JavaScript datagrid_201910](https://indepth.dev/inside-ag-grid-techniques-to-make-the-fastest-javascript-datagrid-in-the-world-2/)

- In just 4 years we built the best JavaScript datagrid in the world.
  - We managed to do that because we first implemented a technical foundation that helped us tackle the complexity of building such a complex widget. 
  - We call this foundation “ag-stack”. 
  - This is what I want to explore in this series of articles.
- The problem stems from the amount of features that a datagrid should support and the correct interoperability between them all. 
- As we add new features, we need to ensure that all existing features continue working properly and the interoperability between them, e.g. sorting with filtering, isn’t broken. 
  - With each new feature the complexity grows.
- Another challenge is the customization of the grid. 
  - add their own logic and UI into many parts of the datagrid. 
  - We even allow customization using components from your favorite frontend framework (Angular, React and so on)

- Managing complexity in ag-Grid
  - We use a lot of low-level functional programming inside classes, however we still prefer OOP design for the higher level architecture like defining modules and setting up their interaction.
  - TypeScript significantly helps with OOP programming. 
- ag-stack describes a few pillars of grid’s internal architecture, particularly IoC Container and Component Framework, alongside some optimizations techniques that we use.
- It’s worth pointing out that we implemented all parts of ag-stack ourselves from scratch. 
  - That’s our philosophy, **if you need it, build it**. 
  - That’s why ag-Grid has zero dependencies which is a huge advantage for consumers of our datagrid.

- Row/Column virtualization
  - You can think of it as an alternative way of paging in which a datagrid gradually renders DOM nodes while a user is scrolling vertically or horizontally
  - Virtualization is achieved by only rendering rows (row virtualization) or columns (column virtualization) that are visible in content viewport. 
  - This is usually a small portion of the entire dataset. 
  - And it means that you can feed as much data as you want into the grid. 
  - The amount of data is only limited by the browser’s VM heap. 
  - If you’re using ag-Grid even that is not a problem. 
  - You can overcome this limitation by using server-side row model. 
  - To improve performance even more, we cache rendered nodes and reuse them when they are needed for next time.

- Animations using CSS transforms
  - One of the most frequently occurring animations in the datagrid are row animations.
  - We ended up using CSS transforms to run animations. 
  - This approach makes use of GPU and layering to render parts of the page involved in animations and make them as smooth as possible.
  - In CSS we’re simply using `transform` property instead of the `left` and `top` properties to animate the position of rows. 
  - One caveat though about using too much CSS transforms is that it’s possible to run out of layers with CSS translate. 
  - To avoid that problem, at ag-Grid we apply transforms to entire rows, not cells.

- Dirty checking during change detection
  - Datagrid needs to constantly update values in the DOM. 
  - The updates are triggered by changes in a dataset or through direct user input into cells. 
  - When this change happens, we need to update state of the component and render the updated value in the DOM. 
  - During change detection the grid calls `refreshCell` method for each cell. 
  - This is where DOM updates happen synchronously. 
  - There’s no asynchronous scheduling mechanism like, for example, in React fiber. 
  - While running change detection, there’s no point in updating the DOM if the value of the cell hasn’t changed. 
  - So before we do the update, we first run dirty checking — each cell stores current value and compares it to the new value it gets. 
  - Only if changes are detected or update is forced, the DOM is updated. 
  - This approach significantly reduces time required to process changes. 

## Comparison: Why ag-Grid is the best when it comes to Column Pinnin

- ref
  - [Comparison: Why ag-Grid is the best when it comes to Column Pinning](https://blog.ag-grid.com/javascript-grid-comparison-column-pinning-ag-grid/)
  - [Here's why column pinning by ag-Grid wins over competition](https://blog.ag-grid.com/heres-why-column-pinning-in-react-datagrid-by-ag-grid-wins-over-competition/)

- Column pinning is a standard feature of all datagrids. 
  - Sometimes it’s also referred to as column fixing or column freezing. 
  - This feature is useful in cases when a javascript datagrid contains many columns that cause horizontal scrolling. 
  - With column pinning you can fix a column on the left or on the right side of the grid to prevent it getting out of user view when scrolling horizontally.
- In effect, this feature splits a datagrid into two separate parts: the “frozen” one and the “scrollable” one. 
  - The “frozen” part of the datatable will be fixed, while the scrollable part will remain movable.
- Functionality overview
  - pinning a column on both left and right sides
  - pinning a column from a column menu
  - pinning a column by dragging
  - pinning an initial column dynamically
  - pinning subsequent columns dynamically
- Pinning on both sides effectively splits a grid into 3 parts with the horizontal scroll only available for the middle “non-freezed” part. 
- ag-Grid doesn’t force you to indicate an initial pinned column or the specify the number of pinned columns in the configuration. 
  - This can all be done after the grid is initialized
  - All other React datagrids either require at least one pinned column all the time or limit you by specifying the number of pinned columns in advance.

## ref

- [Testing with Jest & Enzyme - querying JSDOM vs ag-Grid API](https://blog.ag-grid.com/testing-ag-grid-react-jest-enzyme/)
  - jsdom: test user behavior
  - ag-grid api: compatible with dom virtualisation, test implementation
