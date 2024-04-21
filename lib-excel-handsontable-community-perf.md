---
title: lib-excel-handsontable-community-perf
tags: [community, handsontable, performance]
created: 2024-04-21T15:16:42.875Z
modified: 2024-04-21T15:16:57.106Z
---

# lib-excel-handsontable-community-perf

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-stars
- ## 

- ## 

- ## 

- ## 🌰 [Rendering 400k rows _202009](https://forum.handsontable.com/t/rendering-400k-rows/4688/7)
- There is not official paging plugin yet.
  - you can load all the data for a split of second and page it again when the export plugin finishes its job.
  - You can also check this PR https://github.com/handsontable/handsontable/pull/6837/files where we create a POC for pagination. 

- ## 💡 [[POC] Paging plugin _202004](https://github.com/handsontable/handsontable/pull/6837)
  - I wanted to check how hard it would be to implement paging with IndexMap. The answer is around 20 loc
  - POC is using hidden rows for paging so the option `exportHiddenRows` of `exportFile` plugin should work. But using both, hiding some rows and paging, would create a problem to export all pages without the hidden ones. 
  - There were so many changes to develop, moving files around and CI tests that this PR no longer is applicable to current source, nor meet the requirements of code quality. It has to be adapted and created from scratch, this draft has to be closed.

- ## [Improving performance of row and column calculators _202103](https://github.com/handsontable/handsontable/issues/7674)
  - change in number of columns added as offset to calculator may result in performance boost. There is possibility that we can do even more improvements.

- ## 💡 [Handsontable scrolling performance with lots of rows _202207](https://forum.handsontable.com/t/handsontable-scrolling-performance-with-lots-of-rows/6270)
- We are aware that handling such amount of data might be problematic performance wise. 
  - The solution that I can propose is to use `pagination` to divide the data into smaller chunks (it depends on data volume you have). 
  - However, there are some disadvantages. For example you won’t be able to use such features as column sorting on the whole table. It will work only in the current page. 
  - Here’s an one of the examples of how it can be done: 
  - https://jsfiddle.net/aszymanski/7arygep2/

- pagination isn’t a great option for us. From profiling and looking at the code it appears that Handsontable should be able to render a large number of rows (eg. 1M+), since virtualisation means that it’s only rendering the visible rows, but there are a few places in the code that cause the performance issues (eg. the `ViewportRowsCalculator`). We were hoping for a solution where we could bypass/override this behaviour.
- We’re currently evaluating HoT (a fantastic product, btw!) as the “engine” for our table editing in our data viz, analysis and editing product, where users commonly work with datasets well beyond 100, 000 records. We’re aiming to create a seamless experience working with tables of large and small data, without resorting to pagination.
  - We are currently experimenting with creating a sparse array with (say) 1 million rows, but only populating data for the visible screen plus some buffer. This is great, and allows us to data-load only a small volume across the network, without any significant memory use in the JS runtime.
  - However, HoT performance degrades linearly with row count. Much beyond 100, 000 it becomes a problem. Comparing with both online spreadsheets and Excel, 1 million rows seems like a reasonable expectation (and beyond is theoretically possible).
- 🐛 re-calculating rows and columns is the main issue here 
  - It is fired on each scroll (that’s the designed behavior) and the greater the amount of rows or columns the more calculation are needed to be done.
  - It is fired on each scroll (that’s the designed behavior) and the greater the amount of rows or columns the more calculation are needed to be done.

- ## [Alternative of setDataAtCell  _202008](https://forum.handsontable.com/t/alternative-of-setdataatcell/4641)
- If you are running the `setDataAtCell` method 1000 times in the run I recommend changing the source data and use `loadData()` afterwards. It will result in 1 call to Handsontable instead of 1000.

- ## [Performance issue: splicing source data with observeChanges/columnSorting triggers "observe change" on all data that comes after the spliced index ](https://github.com/handsontable/handsontable/issues/5274)
- It looks like the `observeChanges` is used to perform proper sorting after adding or removing rows. It fires for `afterCreateRow` and `afterRemoveRow` hooks.

# discuss-lazy
- ## 

- ## 

- ## 

- ## [Handson table Infinite Scroll to load data _201509](https://github.com/handsontable/handsontable/issues/2784)
- https://jsfiddle.net/ke60pzbd/
  - Please treat this as a rough idea and officially we do not support infinite scroll. It should add new rows, while the code above after scroll reloads the data to load a bigger set of rows.
  - [[New feature request] Infinite scroll  ](https://github.com/handsontable/handsontable/discussions/7866)

- 🌰 [Infinite Scrolling (2022) ](https://forum.handsontable.com/t/infinite-scrolling-2022/5936)
  - 202202: Infinite scroll isn’t implemented yet, neither it is on our current road map. If you’re looking for workarounds, the one that you showed seems to be a pretty good option for now.

- ## [[GH #5769] Is there a way to make faster appending new data to already-loaded data? _202007](https://forum.handsontable.com/t/gh-5769-is-there-a-way-to-make-faster-appending-new-data-to-already-loaded-data/4516/3)
- Handsontable does not have a built-in infinite scroll and if something is out of the viewport it has to be loaded and all the rows in the table rerender.
  - We are planning to change this behavior by introducing eco-renderers

- ## 🌰 [How to implement a lazy loading algorithm _201802](https://forum.handsontable.com/t/how-to-implement-a-lazy-loading-algorithm/1828)
  - I’m trying to implement a lazy loading algorithm and my current approach is to use an `afterScrollVertically` handler. In this handler I have problems to determine the current visible rows. Have you an idea how I could solve the problem?

- I think that `getLastVisibleRow` (a part of `AutoRowSize` plugin) should be what you are looking for.

- ## 🌰 [Lazy loading from a server _202310](https://forum.handsontable.com/t/lazy-loading-from-a-server/7171)
  - What is the best practice on how to deal with a lazy loading from a server today?
  - Sorting on a server’s side I believe is still problematic, right?

- I kinda figured out

- ## [Virtualisation - lazy loading data when it becomes visible in the grid _202212](https://forum.handsontable.com/t/virtualisation-lazy-loading-data-when-it-becomes-visible-in-the-grid/6643)
  - What is the best practise to implement a “hot data load”?

- We have an option that allows not to render all of the rows at initialization, but along with the user’s scrolling. There are also other performance tips that might be useful for you.
  - We don’t have any kind of loading animation solution available out of the box currently.
