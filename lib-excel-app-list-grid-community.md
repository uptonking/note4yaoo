---
title: lib-excel-app-list-grid-community
tags: [community, grid, list, table]
created: 2021-06-24T08:48:24.911Z
modified: 2022-08-21T10:15:01.987Z
---

# lib-excel-app-list-grid-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## [Spreadsheets Are Hot–and Cranking Out Complex Code | Hacker News _202204](https://news.ycombinator.com/item?id=30955940)
- 
- 
- 

- ## 🧮 [Representing and Editing JSON with Spreadsheets (2018) | Hacker News_201910](https://news.ycombinator.com/item?id=21109798)
- I made a Google spreadsheet add-on that contains 3 built-in options for converting nested JSON to tabular format.
  - Method 1: drills into nested json objects and arrays and returns the key names as headers, key values as rows. In cases with multiple nested values, they get returned into multiple columns, differentiated by a number, e.g. orders > products > 1, orders > products > 2.
  - Method 2: same as above but returns all nested data into a single column, e.g. a single column named orders > products. This can break the association between JSON elements, but is more convenient for certain types of analysis.
  - Method 3: concatenates all the elements of each nested object into a single cell, separated with pipes.
  - In some cases (e.g. when the primary object of interest is nested inside another object) there are still problems recognizing what keys should represent rows vs columns, but in my tests the above 3 algorithms cover most of the use cases for spreadsheets.
- You could put the nested data into a separate sheet with a unique identifier for the row. Then include a foreign key back to the original sheet's primary id.
- Interesting idea, thanks. There's often multiple levels of nested data, would you want to see each level in a new sheet?
  - Absolutely! It's relational data that could map to a defined relational schema, so why not?

- ## [Use Spreadsheets Everywhere | Hacker News_202108](https://news.ycombinator.com/item?id=28049255)
- 
- 

- ## [Excel Never Dies | Hacker News_202103](https://news.ycombinator.com/item?id=26386419)
- 
- 

- ## [Ask HN: Easiest low-code way to convert spreadsheet to app? | Hacker News_202208](https://news.ycombinator.com/item?id=32331063)
- 
- 

- ## Interesting side effect of the FLIP animation technique when applied to table rows: it looks as if its not the rows themselves that change position, but the cells within them. I'm not sure if I like I better or not
- https://twitter.com/fabiospampinato/status/1718398614983078040
  - 插入删除row的动画设计

- ## What would a programming language based on unstructured data look like?
- https://twitter.com/JungleSilicon/status/1632519196751069184
  - There are many unstructured mediums such as documents, images, etc. They have a basic set of characters that can be placed in different locations but all of the data is "valid".
  - TLDR: Create unstructured data, analyse unstructured data to find patterns & structure within it, allow applications to query and interpret it.
  - Applications could then expose part of this process to the end-user so that they can make their own interpretations.
- This is Notion. or airtable or excel or any of them with end-user programmability of unstructured data. Not a language but an environment.
  - However: there is a crucial limitation of these tools (rn!). They cannot create arbitrary apps, because they cannot express interaction. You cannot create a counter in excel without VBA.
  - In my eyes, this is the last building block for users to be able to build arbitrarily complex blocks. But we’ve been dancing around Excel for a long time bc how to do that with a good UX is a really hard problem.

- ## got @stackblitz WebContainer running inside natto after a day of fighting with CORS. 
- https://twitter.com/_paulshen/status/1625756158278668289
  - not sure what this enables yet but having node and npm running in the browser is wild!
- without stackblitz, what Natto uses to execute js code locally?
  - good ol' eval - more specifically the `Function` constructor
- how do you protect sensible stuff from malicious code, such as cookie, etc?
  - iframe sandboxing on a different domain

- ## The new GitHub Issues project tables is built on @tannerlinsley ’s React Table library. 
- https://twitter.com/_clem/status/1407754748799995908
  - It has been an excellent tool in enabling fast iteration and a high level of control with *just enough* free stuff out of the box.
- It makes sense to ask why we didn’t opt for one of the “kitchen sink” table libraries out there that give you state and UI out of the box.
  - This is an important investment for GitHub, and we knew we’d need a very high level of control over every minute aspect of the experience.
  - React Table, on the other hand, gave us enough structure to get to an MVP quick early on that has served as our foundation the whole way through, and we can still try out crazy ideas in this thing because outside of data and state, the framework doesn’t really care what we do.
  - So really the point here is that I think we’re glad we went with something in that sweet spot of some free features and full control, instead of tons of free features and just a big list of settings to tune.
- wait I thought GitHub was all web-components
  - We have a lot of web components! But we’re by no means *all* web components. For this very user-interaction-heavy and client-side-state-heavy project, React just made a lot of sense.

- ## A new GitHub Issues is coming this Fall, with better ways to plan, track, and manage projects.
- https://twitter.com/github/status/1407731478096756739
  - https://github.com/features/issues
  - github的issues依靠用户量，要超越atlassian全家桶已经势不可挡了

- ## React Aria's data table component is coming along nicely!
- https://twitter.com/devongovett/status/1407747623268671490
  - Keyboard navigation to rows, cells, and focusable elements within cells
  - Multi selection
  - ARIA selection announcements
  - Sorting
  - Tiered headings
  - Async data loading + infinite scrolling
  - Typeahead
  - And more!
- We sometimes have tables inside a table and expanding rows. Is that something you plan to implement?
  - Yeah, we will eventually support expanding rows. We would follow the ARIA treegrid pattern for that
- Does it have the "basic" features tables proposed as in react-virtualized or react-windows?
  - Yes! Our own tables in Spectrum are all virtualized. It should work with any virtualization library. We'll add some examples to the docs. Eventually we might make our own virtualizer public as well.

- ## Is it ok to use an html table in 2021 for an actual table? I am actually afraid to ask.
- https://twitter.com/oleg008/status/1417927299668889611
- Half the replies say tables should be used for semantics, the other half are saying they're horrible for responsiveness. So whats the new rule of thumb? Media queries that produce tables on desktop but cards on mobile? Anyone have a general approach?
  - TLDR: **if you need a responsive table that transforms depending on the screen, you want to use `div` with `display: table` and aria attributes, also you don't want to use table for layouts, but otherwise html table is the way to go**. 
- Yes! If it’s an actual table, you should use the table elements for better accessibility (screen readers provide useful shortcuts to navigate tables).
- react-table uses the `<table>` html element and is a wonderful library. I don't see how you can build a complex table without any JS.
- My opinion about tables for media queries is that you should make the table vertically scrollable, that simple, is the same table with the same information and I don't think you need to implement things like collapsable columns for a proper reading. Here's Wikipedia using tables.
- Problem is responsive design. You cant really layout table with lots of columns to look good on mobile screen
  - You are right but is there anyway to produce a table with lots of columns and rows that works well on mobile? I mean yeh I can make it prettier but is it still as usable?
  - Put it in a div with overflow scroll. What we do though is build ours with flex table css, and drop into cards on mobile. Or, hide non essential columns.
- Yes, as long as you're not using it for layout, but if you are, don't forget to use spacer.gifs and rowspan and colspan.
- It's a fairly common pattern to use them in email templates
- Tables will always look terrible on a mobile screen. But there is no other fast and easy way to put it without incorporating some javascript and nastily-long CSS hacks.
- If it is tabular data, absolutely! I ask this as an interview question. Never use them for layout but using the proper semantic tags for tabular data helps with accessibility and helps machines/bots infer messaging in your content.
- Yeah, you can use the table element. You might not want to use it though if you want the table to change the layout and style on smaller devices though. Another possible solution would be to use a table element on large screens and other elements on smaller screens.
- You can also trim div tags with CSS display table, table-row, table-cell etc. and make it accessible with loads of aria-xxx attributes.... or just use a table for a table
- If you need windowing, columns resizing, or other fancy features, a DIV soup may be your best bet.
- IMHO tables still make sense on desktop but are far from great on mobile. On mobile, cards are usually better.
- Many people mentioned that it's hard to make a table on mobile easy to use.
  - My take - if table is not fitting on one mobile screen, it probably shouldn't be a table at all or you have to live with  bad or suboptimal UX.
  - Sure you can scroll horizontally, but is this great?
