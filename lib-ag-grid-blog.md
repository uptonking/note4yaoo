---
title: lib-ag-grid-blog
tags: [ag-grid, blog]
created: '2020-07-30T13:50:07.752Z'
modified: '2020-08-10T06:01:15.443Z'
---

# lib-ag-grid-blog

## guide

- [Niall Crosby articles](https://medium.com/@niall.crosby)
  - [Why The World Needed Another Angular Grid - The Story of ag-Grid](https://medium.com/ag-grid/why-the-world-needed-another-angularjs-1-x-grid-17e522a53bc8)
  - [8 reasons to choose ag-Grid as your JavaScript Datagrid](https://medium.com/ag-grid/8-reasons-to-choose-ag-grid-as-your-javascript-datagrid-eb4a767a351f)
    1. The `ag` in ag-Grid stands for `AGnostic`
    2. Enterprise Foundations
    3. Integrating, not Wrapping
    4. Features Above and Beyond
    5. Open Source
    6. Free and Commercial
    7. Pure Open Source is Risky
    8. You Ain't Seen Nothing Yet in the market
  - [JavaScript Big Data in a Small Browser](https://medium.com/@niall.crosby/javascript-big-data-in-a-small-browser-3b19c01e2132)
  - [Delivering Big Data in the Small Browser](https://medium.com/ag-grid/delivering-big-data-in-the-small-browser-41704f1058f0)
- [Max Koretskyi articles](https://indepth.dev/author/maxkoretskyi/)

## 8 Performance Hacks for JavaScript in ag-grid

- [8 Performance Hacks for JavaScript_Niall Crosby_201709](https://www.ag-grid.com/ag-grid-8-performance-hacks-for-javascript/)

- This blog presents performance patterns, or performance hacks, that we used to put our grid on steroids.

- ### Row virtualization
  - Row virtualisation means that we only render rows that are visible on the screen. 
  - For example, if the grid has 10, 000 rows but only 40 can fit inside the screen, the grid will only render 40 rows (each row represented by a DIV element). 
  - As the user scrolls up and down, the grid will create new DIV elements for the newly visible rows on the fly.
  - If the grid was to render 10, 000 rows, it would probably crash the browser as too many DOM elements are getting created. 
  - Row virtualisation allows the display of a very large number of rows by only rendering what is currently visible to the user.
  - is virtualization basically lazy loading, right?
    - no, the data is all present in the browser, it only renders what it needs due to scrolling position. 
    - lazy loading in ag-grid is achieved using either pagination, or the additional row models (viewport, infinite scrolling or enterprise row model) - which you can read about in the ag-grid docs.

- ### Column virtualization
  - Column virtualisation does for columns what row virtualisation does for rows.

- ### Exploit Event Propagation
  - The grid needs to have mouse and keyboard listeners on all the cells so that the grid can fire events such as 'cellClicked' and so that the grid can perform grid operations such as selection, range selection, keyboard navigation etc. 
  - In all there are 8 events that the grid requires at the cell level which are click, dblclick, mousedown, mouseover, mouseout, mouseenter, mouseleave, contextmenu.
  - Adding event listeners to the DOM results in a performance hit. 
  - A grid would naturally add thousands of such listeners as even 20 visible columns and 50 visible rows means 20 (columns) x 50 (rows) x 8 (events) = 8, 000 event listeners. 
  - As the user scrolls our row and column virtualisation kicks in and these listeners are getting constantly added and removed which adds a lag to scrolling.
  - Solution - Event Propagation
    - 6 of these 8 events propagate (the exceptions are mouseenter and mouseleave). 
    - So instead of adding listeners to each cell, we add each listener once to the container that contains the cells. 
    - That way the listeners are added once when the grid initializes and not to each individual cell.
    - The challenge is then working out which cell caused the event.
  - This is a similar pattern used by React using React's Synthetic Events. 
    - React uses event delegation and listens for events at the root of the application. 
    - React keeps track of which rendered nodes have listeners. 
    - The synthetic event system implements its own bubbling and calls the appropriate handlers.

- ### Throw Away DOM
  - Good programming sense tells you to de-construct everything you construct. 
  - In the context of your framework, it means removing components from their parents when the component is disposed.
  - This hack goes as follows: 
    - if you are removing an item from the DOM (e.g. a grid cell) but you know the parent of that item is also going to be removed (e.g. a grid row) ,then there is no need to remove the child items individually.
  - So in ag-Grid, as rows are created, we use composition to build the complex structure into the DOM. 
    - However when removing the rows, we do not remove the cells individually from the DOM, instead we remove the entire row in one quick DOM hit.

- ### innerHTML where possible
  - What is the fastest way to populate lots of cells and rows into the browser? 
    - Should you use JavaScript (i.e. `document.createElement()` ) to create each element, update the attributes of each element and use `appendChild()` to plug all the elements together? 
    - Or should you work off document fragments? 
    - Alternatively should you create all the document in a large piece of HTML and then insert it into the dom by setting the property `.innerHTML` ?
  - We have done many tests. 
  - The answer is to use `.innerHTML` .
  - So ag-Grid leverages the speed of `.innerHTML` by creating the HTML in one big string and then inserting it into the DOM using the method `element.insertAdjacentHTML()` . 
    - The method `element.insertAdjacentHTML()` is similar but slightly less well known equivalent of the property `.innerHTM` L. 
    - The difference is that `insertAdjacentHTML()` appends to existing HTML where as `.innerHTML()` replacing the current content. 
    - Both work just as fast.
  - This works well when there are no custom cell renderers. 
    - So for all cells that do not use cell renderers, the grid will inject the whole row in one HTML string which is the quickest way to render HTML. 
    - When a component is used, the grid will then go back and inject the components into the HTML after the row is created.
  - However, in ag-Grid, we want the fastest grid possible, so it's best to avoid the use of cell renderer components to leverage the power of `innerHTML` for the fastest rendering of rows.
  - `.innerHTML` and `insertAdjacentHTML()` execute at the same speed, they both provide a string a html to the browser which then creates the DOM in one go. 
    - the difference is one replaced the content (innerHTML), the other appends to the content (insertAdjacentHTML).
    - So the hack is to add to the DOM using HTML strings, not by creating new DOM elements. And it doesn't matter much if one uses innerHTML or insertAdjacentHTML(), as long as they don't do something like `innerHTML += myHtml` . Is that correct?
    - yes, that's correct. however be aware, this worked for ag-Grid, in your application, do your own performance tests to see if worth it. in IE we found 50% improvement. in chrome it was more marginal (if the world was on chrome, we wouldn't of not bothered with this bit, however lots of our customers work in banks which implies IE a lot of the time).

- ### Debouncing Scroll Events
  - When you scroll in ag-Grid, the grid is doing row and column virtualisation, which means the DOM is getting trashed. 
  - This trashing is time consuming and if processed within the event listener will make the scroll experience 'rough'.
  - To get around this, the grid uses debouncing of scroll events with animation frames.

- ### Animation Frames
  - The next performance hack was to break the rendering of the rows into different tasks using animation frames. 
  - When the user scrolls vertically to show different rows, the following tasks are set up in a task queue:
    - 1 task, if pinning then scroll the pinned panels.
    - n tasks to insert each rows container (results in drawing the row background colour).
    - n tasks to insert the cells using string building and innerHTML.
    - n tasks to insert the cells using cell renderers where applicable.
    - n tasks to add mouseenter and mouseleave listeners to all rows (for adding and removing hover class).
    - n tasks to remove the old rows (do not deconstruct cells, just rip the rows out).
  - The grid then uses animation frames (or timeouts if the browser does not support animation frames) to execute the tasks using a priority order. 
    - Scrolling will get done first, best efforts are made to keep pinned sections in line.
    - Row containers are second, the first thing the user will see is the outline of the rows.
    - Cells are drawn in stages, as quickly as the browser will allow while giving visual feedback to the user.
    - Removing of old rows is left till last, as that has no visual impact.
    - If a new scroll event comes in, then this gets priority again over older tasks of lower priority, keeping all pinned areas in sync as a priority.
    - Tasks that are old are cancelled i.e. the user has scrolled past by the the time the row is to be rendered.
  - Having this many tasks should result in a lot of animation frames. 
  - To avoid this, the grid does not put each individual task into an animation frame. 
  - This would be overkill as then the create, destroy and schedule of animations frames would add their own overhead. 
  - Instead the grid requests one animation frame and executes as many tasks as it can within 60ms.
  - If the grid does not exhaust the task queue, it requests another animation frame and tries again, and keeps trying until the task queue is emptied.
  - Fast browsers such as Chrome can get everything done in one animation frame and produces zero flicker. 
  - Slower browsers such as Internet Explorer can take 10+ animation frames to process the task queue for a standard scroll. 
  - As we move through these improvements, you will notice we are using animation frames to add mouseenter and mouseleave. 
    - This is different to the other events where we use event propagation to listen for all other events at the parent level. 
    - mouseenter and mouseleave do not propagate, so instead we add these in an animation frame after the rows are rendered. 
    - This has minimal impact to the user. They are not waiting for these events to be added before they see the row on the screen.
  - The grid uses similar task priority queuing for horizontal scrolling. 
  - When the user scrolls to show more columns, the header gets scrolled first and the cells are updated next. 
  - This is all done using the same task queue and animation frames.

- ### Avoid Row Order
  - By default, the DOM created by the grid will have the rows appear in the order they were created. 
  - This can get out of sync with the rows on the screen as the user scrolls, sorts and filters. 
  - The row virtualisation trashing adds and removes rows as the user scrolls.
  - Screen readers and other tools for accessibility require the row order to be the same in the DOM as on the screen. 
  - Having the row order consistent with the screen causes a performance hit, as it stops the grid from adding rows in bulk.
  - So there is a trade-off. 
    - By default, the grid does not order the rows. 
    - If the user wants the row order, they can use the property `ensureDomOrder=true` . 
    - The grid works a bit slower but is compatible with screen readers.

- ### Summary
  - All of the performance hacks above are the result of years of learning.
  - They are tried and tested approaches for squeezing performance out of the browser. 
  - One lasting note - these are performance hacks that worked for us in ag-Grid. 
  - They may not be suitable to your application (an application has different concerns to a data grid).

## Inside ag-Grid: techniques to make the fastest JavaScript datagrid

- [Inside ag-Grid: techniques to make the fastest JavaScript datagrid_201910](https://indepth.dev/inside-ag-grid-techniques-to-make-the-fastest-javascript-datagrid-in-the-world-2/)

- In just 4 years we built the best JavaScript datagrid in the world.
  - We managed to do that because we first implemented a technical foundation that helped us tackle the complexity of building such a complex widget. 
  - We call this foundation “ag-stack”.
  - This is what I want to explore in this series of articles.
- The main idea is to review patterns and techniques that we use under the hood to build the fastest datagrid while also providing ample customization opportunities. 

- The problem stems from the amount of features that a datagrid should support and the correct interoperability between them all. 
  - As we add new features, we need to ensure that all existing features continue working properly and the interoperability between them, e.g. sorting with filtering, isn’t broken. 
  - With each new feature, the complexity grows.
- Another challenge is the customization of the grid. 
  - add their own logic and UI into many parts of the datagrid. 
  - We even allow customization using components from your favorite frontend framework (Angular, React and so on)
  - But to make it possible, we needed to implement a lot of bridges to connect grid internals and customization layers. 
  - It’s quite a big chunk of infrastructure code that needs to be checked every time we make changes to the architecture.

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

## [Why do we have Dependency Injection in web development](https://indepth.dev/why-do-we-have-dependency-injection-in-web-development/)

- Dependency Injection (DI) software design pattern has long been part of native client and server-side applications that use OOP languages. 
- In essence it’s a technique for achieving Inversion of Control (IoC) between classes and their dependencies. 
- The content mostly discusses cases related to architecture of native applications that use OOP languages like Java or C#. 
- If you want to know the reasons for using DI in web applications, there’s almost no information available. 
  - Most of the explanations you’d find would be about how DI makes unit-tests easier. 
  - Yet, it’s important to realize that the purpose of DI is much broader than just enabling unit testing.
- I’ve read many articles about DI and most of them define two major benefits of using DI: 
  - enabling loose coupling of code (decoupling)
  - simplifying testing setup. 
- when two blocks of code are loosely coupled, it means that a change in one usually doesn’t require a change in the other. 
  - advantage of loose coupling is that it increases maintainability of the overall solution.

## JavaScript GPU Animation with Transform and Translate

- [JavaScript GPU Animation with Transform and Translate](https://www.ag-grid.com/ag-grid-gpu-animation-transform-translate/)

## Comparison: Why ag-Grid is the best when it comes to Column Pinning

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
