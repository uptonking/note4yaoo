---
title: pm-list-grid-blog
tags: [blog, grid, list]
created: 2020-07-14T13:04:22.299Z
modified: 2021-05-23T16:34:32.755Z
---

# pm-list-grid-blog

# guide

# blogs

## [Diffing and patching tabular data _201308](https://okfnlabs.org/blog/2013/08/08/diffing-and-patching-data.html)

- I’ve tried two methods to build revision control with all this:
  - Modifying fossil, a distributed revision control system with beautifully compact and hackable source code, to use tabular diffs and merges natively. The result is ssfossil (“spreadsheet fossil”) in the Coopy toolbox.
  - Using custom diff and merge drivers with git, to achieve a similar result. 
- Until making more radical changes to the SCM, it definitely makes sense to store tables in a text format. Formats I’ve experimented with are:
  - CSV. Simple, globally understood. But just a table.
  - CSVS. I made this up. It is an extension to CSV with multiple tables, an unambiguous spot for column names, and a place for table names. 
  - Sqlitext, pronounced “Sqlite Text”. I made this up. This is a text dump of an Sqlite database, with consistent ordering of rows. 
  - SocialCalc. A text format for representing spreadsheets used by SocialCalc and inherited by Audrey Tang’s http://ethercalc.org. Stores table formatting and other good stuff.

## [React Data Grid vs. React Data Table vs. React Grid](https://blog.ag-grid.com/react-data-grid-vs-react-data-table-vs-react-grid/)

- When describing components in English, we might use the terms "Data Grid", "Data Table", "Table" and "Grid" interchangeably. 
- When describing web components, the words can often be confused because of their overlap with existing web technology terms.
  - Grid provides functionality for page layout vs.
  - Data Table which provides data rendering and some interactivity vs.
  - Data Grid which provides a data-driven spreadsheet-like level of interactivity.

- A React Grid refers typically to a layout control to create a responsive grid layout to organise child components.
- A React Table, React Data Table or React Data Grid refers to a component that can render rows and columns of data and allow the user to interact with the data, e.g. sorting and filtering data, exporting data, and in-cell editing.
- AG Grid is a Data Grid for data-driven tabular rendering. 
  - Configuration based to offer a rich user experience out of the box with minimal programming. 

- HTML tables:
  - Render all their data at the same time, so they may not be the best mechanism to display thousands of records.
  - Size to fit the data. The length of the table increases as more data is displayed, they rely on the page scroll bar to navigate, so they may not be the best option for a tightly controlled screen layout.

- CSS Grids are used to layout all the page elements, whereas Data Grids automatically render configured data in a tabular format.

- An HTML table is a way to display data for a user but offers no way for the user to interact with the data.
- Data Grids and Data Tables offer more interaction to the user: sorting columns, re-ordering rows, drag and drop columns, filtering, and in-cell editing.
- React Data Table controls often use a` <table>` element as their underlying DOM representation and then enhance the table to provide the user with functionality to interact with the data.
- When looking at descriptions and examples for Data Grids compared to Data Tables, you may notice that Data Grids tend to be more self-contained.
  - Data Tables often require additional dependencies to handle virtualised rows to only render visible data.
  - AG Grid requires no additional dependencies.
# more
- [Building abstractions on spreadsheets - The cost of flexibility and potential solutions](https://subset.so/blog/building-abstractions-on-spreadsheets)
