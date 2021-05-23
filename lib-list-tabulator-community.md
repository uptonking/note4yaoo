---
title: lib-list-tabulator-community
tags: [community, tabulator]
created: '2021-05-06T09:50:36.167Z'
modified: '2021-05-13T02:55:29.807Z'
---

# lib-list-tabulator-community

# guide

# discuss-stars

- ## Tabulator – Easy-to-use JavaScript library for interactive tables_201811
- https://news.ycombinator.com/item?id=18568072
- It seems standard that all of these JS table libraries are rendering using `<div>` elements instead of a `<table>` element. Why? As far as I can tell, all of the features could be implemented using the correct HTML element rather than using `<div>` to mimic a table.

- Let me preface my answer by saying im the chap(对男子的友好称呼，家伙，伙计) that built Tabulator
- This is because the `<table>` element introduces a lot of design constraints.
  - There is a lot of inherent styling that would have to be overridden if a `table` element was to be used. 
  - It could also mess with the standard behaviour of other table elements that have been generically styled.
- Importantly when you start building interactive complex tables, there are 100's of different types of elements needed to make the table function correctly that a standard HTML element simple isn't designed to handle, event making the header and the body scroll separately requirements more elements that a standard table can handle 
  - and it would invalid HTML to use the tags inside the table that would be needed to achieve it.
  - Especially when you move into the world of the virtual DOM, a standard table element simply wont cut it
  - With the inclusion of aria tags, there are no accessibility issues as screen readers treat them just as any other tables.
- For Tabulator the virtual DOM is essential. 
  - If you try and load 10, 000 rows into a table either the browser will slow down and become almost unusable or crash entirely.
  - For large data sets it makes the table work regardless of the number of rows
- What if you just chunk your DOM writes into small batches, and then put them into a queue, which is then consumed within a requestAnimationFrame() handler?
  - A bit of indirection, but not nearly as much as a complete virtual DOM. (I assume this would result in the table "slowly" populating, but the browser and the page should both remain responsive.)
  - You can can do this but for large data sets it would take ages and doesnt over come the main issue.
  - Yes loading that many elements into the DOM is slow and your approach would stop it blocking, however what it doesnt do is stop the sheer(大量的，陡峭的) number of elements from overloading the DOM.
  - Most browsers simply cant handle that many elements in the DOM, if you try and scroll a div containing that may elements at best it will be sluggish and at worst it will simply crash the browser. 
  - on devices without much memory it is very likely that the whole DOM will freeze up and make the site unusable.
- By adding and deleting the elements as they become visible/hidden, it keeps the number of elements in the DOM to a minimum, while improving load time and adding only a bit of extra processing to the scroll event, which modern browsers can handle with ease. giving all round the best solution

- Olifolkerd, I would love to know more about Tabulator's approach to supporting multiple frameworks, please.
  - on the whole the key is to stick to vanilla JS and avoid trying to use to forcible a design paradigm that could conflict with other frameworks.
  - Removing dependencies on other libraries was key to making it interoperable.
  - Everything in Tabulator is built to be extensible so where an incompatibility exists it is easy to build a solution for a particular framework.
  - Tabulator still has one hangup in the way it works, in that it doesnt use reactive data (changing the array you passed into the table, does not automatically update the table, unlike react and view, you have to bind watchers at the moment) but this will be coming in the next release. at which point they should all work harmoniously
  - The biggest challenge is to ensure that things are drawn correctly at the correct time. 
  - Because Tabulator uses a virtual DOM it makes it a since to redraw parts of the table when needed
  - I wrote my own VDOM library, Tabulator has zero dependencies for its core functionality

- Author of Handsontable, here. We actually use `<table>` , but there are many things that are easier with `<div>` :
  - With `<div>` , you have complete control over the positioning of the cells. 
    - With `<table>` , you delegate(v,委托，选派) the layout to the browser engine. 
  - `<table>` has lots of semantic meaning, which makes it slower to render than a `<div>` , because the browser engine needs to make a sense of it. 
    - There are differences in how `<table>` s are rendered in various browsers. 
    - This is especially a problem with old browsers such as IE6. 
    - `<table>` element is much more complex to process than a `<div>` .
    - Is this really slower overall? 
    - `<table>` is one of the few elements that actually have a dedicated "Processing model" section in the spec
    - It is not neccessarily a bottleneck, as long as your datagrid library uses the browser's ability to render the table. 
    - But if you want a custom look and feel, such as overlapping cells, irregular shaped cells, animated cells, it's far better to do it based on `<div>` s instead of fighting the browser engine.
    - This is why you need to use a virtual DOM to prevent the DOM from being filled with elements that consume memory and slow it down
    - it’s a real technique to render only a subset of elements that fit on ~2 screen lengths and swap them out as the user scrolls for arbitrarily large tables. Just using virtual dom doesn’t magically solve this but it does make doing things like this parlor trick easier IMO.
  - It is trickier to implement things like floating headers, virtual scrolling with `<table>`
  - Still, Handsontable uses `<table>` because you can overcome these problems if you're motivated enough. 
    - The biggest benefit is that `<table>` gives you enhanced semantics, which are good for Accessibility, SEO or any other form of code processing.
    - In addition to that, using `<table>` gives you out-of-the-box Excel file export because `.xlsx` files (which are basically zipped XML files) support HTML tables.
  - Could use use `<table>` for the semantics but set `display:block` to get `<div>` style layout?
    - the problem is it isnt just the table element, it is the thead,tbody,td,th elements as well
    - Complex interactive tables need a great number of elements to make them run and these wont conform(v,遵守，服从) to the standards of using a table (you cant just put a div inside a tbody element) but that is exactly what you would need to get a table with a virtual DOM to work correctly.
    - There are a lot of different styling tweaks that would need to be overriden for each element, some of which arent consistent across each browser.
    - Also people have a tendency to put styles on the generic table tab to style tables across the site. if Tabulator was to then be used on the page, it could have any number of unknown CSS properties set on it, so would essentially have to look at overriding all possible style properties.
    - where as no one generically styles divs or spans and they come with very little built in styling making them the ideal choice for a library that wants to keeps its functionality isolated from the rest of the site
  - table libraries using table tags:
    - handsontable, datatables.net(for jQuery)

# discuss
