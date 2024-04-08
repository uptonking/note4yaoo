---
title: lib-excel-app-list-grid-community-stars
tags: [community, grid, list, table]
created: 2021-06-29T12:45:19.734Z
modified: 2022-08-21T10:15:06.225Z
---

# lib-excel-app-list-grid-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🔢🔀 [Reorder a selected row in a table · pawelsalawa/sqlitestudio _202105](https://github.com/pawelsalawa/sqlitestudio/issues/4099)
  - Ability to order (move up and down) the selected row in a table.

- This would be against how data is stored in the database. 
  - Order is dictated by the query that you execute. 
  - If you need to modify order of query that shows you a table data, you can click on header of the column or right-click and define more complex sorting order from there.
  - Drag&drop of a row (or few rows) would have no result in the actual order in database, because - as I said above - row order is not a stored property(*), but rather property of SQL query. If such D&D would be allowed, it would give users wrong idea that rows were actually reordered and they would expect the same order after refreshing data view - which it would not be and they would come here and report bugs.
  - (*) - to be more precise, the default order IS property of stored data, but the thing is that it is insertion order and you cannot change insertion order, because - well - it is order in which you inserted data and that's it.

- ## 📡 For those following @SubsetHQ , sharing some bittersweet news today. We're changing directions away from our canvas spreadsheet 
- https://twitter.com/AJNandi/status/1757614422162649208
  - As fun as it was, we realized the bigger opportunity in the spreadsheet world is simply a high quality, local first, desktop spreadsheet. More below!
  - Over the last few years @thejasonchan and I have become obsessed with building spreadsheets, and we've gotten pretty good at it too. Which is why I'm excited to turn our learnings into a product that really scratches our own itch of a modern high-quality desktop spreadsheet.
  - We're focused on a few things initially: performance, a local-first and offline experience, desktop and web apps, and seamless import/export from xlsx / sheets files.
  - After that we want to tackle better ways to collaborate such as version control and branching. And build a community around templates, plugins, and other spreadsheet extensions.

- ## 🚀 [grid-studio: How I built a spreadsheet app with Python to make data science easier | HackerNoon_201907](https://hackernoon.com/introducing-grid-studio-a-spreadsheet-app-with-python-to-make-data-science-easier-tdup38f7)
- While this project was originally intended for commercial release, I've decided it might be better off as an open source project
- The reason for this is that during the initial development of the project I've discovered a number of projects that offer similar functionality to Grid studio.
- First, there is an open source plug-in that integrates Python directly into Microsoft Excel called xlwings. 
- Second, Python has evolved from IPython to Jupyter Notebooks to JupyterLab. 
- Overall, projects like these meant that commercializing Grid studio would mean competing with these product substitutes that are frankly available for the incredibly low price of free.

# discuss
- ## 

- ## 

- ## 

- ## A great example of where multiplayer spreadsheet sync is hard to get right. 
- https://twitter.com/AJNandi/status/1763017297785213158
  - Inserting rows needs to expand formula references that contain the index where the row was inserted. 
  - And recalculating needs to account for these new dependencies on all clients.

- Have you looked at Croquet style reflector networks as a means of implementing multiplayer spreadsheet?

- ## After working on CSV parsing for the past two months, I'm convinced that 98% of the time spent on building a CSV reader is dealing with semi-broken files.
- https://twitter.com/holanda_pe/status/1650760335823970304
- yeah, same as with html where anything remotely resembling html was rendered as well.

- Let us all promote Parquet as alternative together 
  - Non-programmers just love their CSVs
- I understand why it's popular. Portable, easy to understand, but error-prone and text-based. If we have better tools and integration into common tools, i.e. Excel, adoption would be much higher. Benefits are obvious: speed, type-safety, compression.

- ## 💥 what is the best way to implement in a @reactjs app a todo list with a huge number of items more than 10k
- https://twitter.com/sseraphini/status/1409841471491031042
  - so that when 1 todo is marked as done does not rerender the whole list of todos?
  - react-virtual + recoil?
- How will you show 10k items at once?  Each item is 1px tall?
  - You're only going to have in memory only a subset of items, & on screen a smaller subset.
  - That many items I'd require tags & date &/or priority ranges to display. Too much cognitive overload otherwise.
- React-window is a successor of react-virtualized.
- I truly advise against Recoil. I've used it in a project for testing, it is really, really immature and it has a pretty high number of bugs
- I'd say virtualize the list and `React.memo` the list items should be enough.

- ## is there a company building a meta-spreadsheet-api that abstracts around google sheets / notion / coda / airtable / etc? or a module that does that?
- https://twitter.com/tmcw/status/1599893497850757121
- Curious, what’s the end product/interface where you want to consume this?

- ## 📈🔥 [Excel as a database | Hacker News_201304](https://news.ycombinator.com/item?id=5515290)
- 
- 
- 
