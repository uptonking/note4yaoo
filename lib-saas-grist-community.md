---
title: lib-saas-grist-community
tags: [community, excel, grist, lowcode, pivot-table]
created: 2024-02-04T17:53:51.483Z
modified: 2024-02-04T20:54:34.896Z
---

# lib-saas-grist-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-not-yet
- ## 

- ## 

- ## [Offline first support _202212](https://github.com/gristlabs/grist-core/issues/380)
- Grist's origin was as a standalone, downloaded program. Then, work was done to network it in an end-to-end encrypted way, between individual devices, via a dumb hub. This idea excited people, but no-one seemed willing to actually install and pay for it. So we tried Grist as a conventional SaaS app, and that is when we started accumulating users.
  - There's definitely a case for using an offline first approach. It would be an engineering challenge, but not insurmountable.
  - Grist has two levels. There's a "home" database, which keeps track of users/sites/workspaces/documents, and that uses postgresql/sqlite via typeorm. Then, each individual document has its own database, which is sqlite accessed directly via node-sqlite3.
  - For offline first use, you could get good mileage by focusing on the individual document level. Grist has features at this level that are quite compatible with working offline, due to its history.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [(Automatically) (re)load external changes to SQLite database](https://github.com/gristlabs/grist-core/issues/836)
- I now have something that works for me, but perhaps it would be nice to also have some way to force reload the Electron app from the UI.

- ## [Lost all tables after removing snapshot bucket _202311](https://github.com/gristlabs/grist-core/issues/721)
- I don't know the details of what happened in the scenario you describe. The typical server setup persists documents in `/tmp/grist` . Start by checking if there is anything there. Back up anything you find. Your data may still be there. You can check any `.grist` file using sqlite3 (e.g. `sqlite3 FILENAME.grist 'SELECT tableId FROM _grist_Tables'` will show all user tables in the document; if you only see Table1, then it's probably an empty one). If you find data you care about, you can upload any document like that to any running Grist installation via the browser, by importing from your Grist home page.
- The `.grist` files have everything, including formulas! It's the complete document.

- ## [Tell HN: An experiment with natural language spreadsheet formulas | Hacker News _202211](https://news.ycombinator.com/item?id=33809111)
- We've been experimenting with AI-assisted writing of spreadsheet formulas.
  - First, Grist uses Python as its formula language. Current AI models are particularly good at writing Python code, and getting better (every day it seems like).
  - Secondly, Grist spreadsheets are relational databases with a schema that can be neatly described as part of a prompt for an AI model, helping it make inferences.
  - Source code of the experiment is at https://github.com/gristlabs/grist-core/pull/345 with a docker image for anyone who wants to play

- ## [Grist is a modern, relational spreadsheet | Hacker News _202310](https://news.ycombinator.com/item?id=38080951)
- What I love the most is that the way it's build makes it easy for anyone familiar with spreadsheets to get started while making virtually anything possible for a more technical person through custom widgets (basically a web app that integrates with any table and is displayed within Grist) and python formulas !
  - The advanced sharing and permission features sound great. We've been using Nextcloud + OpenOffice for this and apart from being able to lock certain parts of the spreadsheet with a password, it doesn't have any of this.

- ✨ What I really want is a spreadsheet that separates formulas from data as Lotus Improv did, has a native understanding of tables as Apple Numbers has, and solves circular references as Microsoft Excel does.
  - [Grist founder here] On separating formulas from data, that's always been an important part of Grist.
  - In Grist, check out the "Code View" page in the left-side panel -- it shows all the logic (i.e. formulas) of the document along with the Python data model (i.e. all the column names and types).
  - Also, you can save or download a copy of the document without the data, but keeping all the formulas. So you can get all the logic (and formatting, layouts, etc), and use it for different data.
  - (No support for solving circular references though.)

- What are the usecases for non standard spreadsheets? 
  - Grist is more like Airtable, a spreadsheet/database hybrid.
  - Regular spreadsheets give you a number of independently configured cells, which gives you maximum flexibility, but becomes inconvenient when you want tables instead: have a fixed structure, enforce column types and validations, implement row-level access control, or join them together.
- There aren't many reasons to create a freeform spreadsheet editor to compete with Excel or gsheet as standalone applications.
- The two areas where it makes sense to compete are:
  - a) Embedding a spreadsheet like (to varying levels of featurefullness) interfaces into other applications or workflows. A minimal feature set probably doesn't even involve formulas, just the UI affordances of a typical spreadsheet (ie it needs to copy and paste like a spreadsheet).
  - b) You are building something that acts like ms access (or airtable), just aiming for different blends of functionality/freeformness/end user fiddliness.
- For me I think it's just the sheer time investment, personally. Spreadsheets give a very easy programming language, no compiler, via Google sheets my phone can run it and my browser can run at and I can link it to someone

- This looks promising! I've been asked a lot about embeding google sheets into websites. Always been using a work around but this seems like it could be pretty special: "to show Grist spreadsheets on a website without any special back-end support, your options include grist-static, a fully in-browser build of Grist. "
  - That's exactly why I'm also very interested in using Grist. Embedding spreadsheets into web pages has never satisfied me and has resulted in unacceptable load times.

- Another data point to the curious case of the unreasonable effectiveness of a 2D rows-columns rectangle of data. Looks like a 2D rows-columns structure is simple enough yet sufficient to cover 1) a matrix, 2) an Excel spreadsheet, 3) an SQL table, 4) a directed graph of nodes and edges.

- A grist spreadsheet is an sqlite database

- I'm looking for a "spreadsheet as text files" solution. Something that separates the programming, the data and the visualization. Any pointers?
  - The main reason is being able to see and edit the programming / formulas as overall text, rather than the usual fragmented cell by fragmented cell view. I love named cells and "ranges". I love the concepts of replicating rows or adding a column to a calculation - that's all good. But programming (or editing data) in the small, cell by cell, just doesn't compute.
  - "Notebook"-style programming comes close. Ideally, I'd prefer if the visualization was handled independently - freely choosing the embedded capabilities if any, or the mountains of visualization software that already exists.
- A while back [this project (grid studio)](https://github.com/ricklamers/gridstudio) looked interesting but I don't think its being maintained.
- Quadratic is pretty similar to Grid studio and still being actively developed (https://www.quadratichq.com/)
- If the program-spreadsheet exports the right data, it can be rendered or GUI-ed separately - even by a program that watches for export file changes. Even by a spreadsheet viewer for the people who insist.
  - A notebook lets you use various libraries or outside programs to do the rendering.

- does this sync (in real-time) with a backend and support multi-user (with auth)? Since it stores the data in SQLite, it would be nice to integrate e.g. ElectricSQL to sync with a self-hosted central Postgres db.
  - it doesn't sync with anything but has its own data store, built around sqlite, and you can indeed download "documents", which are just sqlite files.  (I looked at how they encode summary tables, and it's not as views, so the grist<->sqlite translation is not as shallow/isomorphic as one might hope)
  - authentication is not taken care of by grist-core itself, but they provide different integration methods (saml, forwarded headers, … ?)

- Excel already does this except for the variable column width. One can select a cell inside a table-like range and click "Format as a Table" to have Excel automatically infer the range of the table (including the headers) and enhance it with database-like features. One can then refer to columns in formulas using references like so: =[@[first column]] + [@second_column]. Modifying the formula in one cell will also update all the cells in the same columns. The table object becomes accessible using labels (e.g. Table1)
- But I still can’t write joins as formulas
  - Can you do this in grist or Airtable? Building join tables with calculated fields is a missing feature in all spreadsheet-like solutions as far as I know. Also I concur with the parent that I often get frustrated by my inability to do spreadsheety things in these tools.
- In Grist, reference columns let you do a lot of what you can do with a join while still having spreadsheet-style immediate updates when underlying data changes.

- You can embed an integrated Jupyter notebook into a Grist spreadsheet
- LibreOffice already allows SQL on spreadsheets; but SQL formulae would be cool.

- Maybe I'm old-fashioned, but I do still think that SQL is a better interface to databases than excel formulas, and classical spreadsheet UIs are a better interface for, well, spreadsheets.

- ## [Grist – Open core alternative to Airtable and Google Sheets | Hacker News _202202](https://news.ycombinator.com/item?id=30392227)
- Development currently happens on a private mono-repo with all sorts of stuff in it - including for the SaaS environment yes, and bits left over from when Grist started out initially as a stand-alone desktop app, and so on. Commits are pushed to grist-core about once a week, using git subtree. If you look at commit history, you'll see plenty of features going in month after month. Since we currently develop elsewhere, you'll see few pull requests on github.

- No no, it's not an alternative to Airtable and Google Sheets, it's much more than that! Seeing the demo, coupled with the Python support, I felt like anyone could built a complex SAAS like Salesforce on it.
- I looked, but it seems to run on SQLite. Makes me a bit concerned about scalability.
  - They mention 100, 000 rows as a soft limit. SQLite is the underlying database technology and it has a maximum database size of 281 terabytes. Enough

- 🤔 why didn't this project leverage these modern technologies for UI and instead went with Backbone and Knockout?
  - Despite all the talk, there isn’t a world of difference between how apps used to be written 10 years ago and more modern frameworks. The tooling and the language have evolved, but you still manage state in similar ways, fetch data, build components, render.
  - Mainly you’ll be managing the rendering lifecycle manually in Backbone, which you’d end up doing in React anyway to get the best performance for an app like this - you’ll get molasses if you naively build a spreadsheet in react.
  - One thing I consider a huge advantage: you can read and understand the source in one afternoon. Makes debugging and optimization a lot easier.

- It's a Node app, so CPU-bound work will run linearly on a single thread unless work was done to break up work into multiple processes or worker threads.
  - It’s behavior was more suggestive of Zeno's paradox than of single-threadedness.

- 🐛 This looks good but you need to import the data into it. It would be great if it can be connected to an existing DB. From the discussion, came across https://nocodb.com/ but the authorization levels doesn't seem fine grained enough. For ex. limiting access for group of users to a particular schema in postgresql

- Does this support live updates as other users make edits (without refreshing the page)?
  - Yes it does, changes are broadcast to all connected clients and applied in place. Disclosure: I work on Grist.

- ## 🚀 [Show HN: Grist, a Hacker Friendly Spreadsheet | Hacker News _202011](https://news.ycombinator.com/item?id=25257521)
- we built Grist to be a “relational spreadsheet” — most of what a spreadsheet has, but with more structure, linking between records, and a flexible UI on top.

- So whenever a new form/table is created, is it getting stored within a sqlite table on your backend ?
  - Yes, a new table in your spreadsheet is stored as a new sqlite table, plus some metadata about it in some other administrative tables. You get all of this as a standalone, round-trippable file when you download your spreadsheet.

- Instead of me trying to put together Jupyter and this can I just use Python in Grist like use the Pandas and everything else? 
  - When running locally, you can use whatever you like, pandas or anything else, which is fun (we've experimented with some options for Jupyter integration ourselves). 
  - In our hosted service, for security we have a locked down python sandbox with white-listed libraries. Definitely on our roadmap to liberate the full power of python libraries in hosted!
