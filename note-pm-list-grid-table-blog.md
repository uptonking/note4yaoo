---
title: note-pm-list-grid-table-blog
tags: [blog, grid, list]
created: '2020-07-14T13:04:22.299Z'
modified: '2020-07-26T04:15:43.741Z'
---

# note-pm-list-grid-table-blog

## The complete guide to building a smart data table in React

- [The complete guide to building a smart data table in React_201911](https://blog.logrocket.com/complete-guide-building-smart-data-table-react/)

- Some common use cases for table UIs include displaying data for finance reports, sports leaderboards, and pricing and comparison pages.
- Some products that use data tables extensively include:
  - Airtable
  - Asana List View
  - Asana Timeline
  - Google Sheets
  - Notion Table
- Basic features of a data table UI include:
  - Uncompromised UX and UI. 
    - Clearly understandable - typography and custom elements inside the table UI
  - Remote data calls to load data
  - Searching the table or specific columns
  - Basic filtering and sorting options
- Advanced features in a data table UI include:
  - Custom sorting and filtering options for columns based on data types (numbers, string, boolean, select input, etc.)
  - Pagination support or infinitely long tables (performance for very large datasets)
  - Showing and hiding columns
  - Support for inline editing of data for a column
  - Support for editing a complete row of data through a modal/details panel
  - Fixed headers and fixed columns for easy viewing of data
  - Support for multiple devices (responsiveness)
  - Resizable columns to accommodate long data points inside a column (e.g., multi-line comments)
  - Horizontal and vertical scroll support
  - Expandable rows to show complete data about the row
- Common UX challenges in a table UI
  - difficult to make a table responsive without changing the layout to suit smaller screen sizes.
  - A table might need scrolling in both directions. 
    - Default browser scrollbars will work well for full-width tables, but most are of a custom width. 
    - Custom scrollbars are very tricky to support on both touch and non-touch screens.
  - Managing the width of the column based on data length is tricky. 
    - It often causes UX glitches when we load dynamic data in the table. 
    - Each time the data changes, it resizes the column width and causes an alignment glitch. 
    - We need to be careful in handling those issues while designing the UX.
- Top libraries for data tables in React
  - react-table
    - no: not support for horizontal and vertical scroll for both touch and non-touch devices
  - react-data-grid
    - use Bootstrap for styling.
    - no: not support pagination by default
  - react-datasheet
    - no: not optimized for large datasets
  - react-virtualized
    - exclusively for displaying large datasets on the UI in different formats, like grid, table, and list.
- Which React table library should you choose?
  - For a simple page with limited data, custom styles, and minimum interactivity like sorting and filtering, use react–table
  - To build a mini Google Sheets-like application, but with limited data, use react-data-grid or react-datasheet
  - For a Google Sheets- or Airtable-like application with a large dataset, use react-data-grid
  - When you’re working with a very large dataset and you need a custom UI that offers tables, grids, and many more options, choose react–virtualized
- When to build your own table UI
  - When your table is just a showcase that doesn’t have many interactions
- When you need a custom UI for the table
- When you need your table to be very lightweight without any functionality
- use cases
  - Product/marketing pages with tables for comparison
  - Pricing tables
  - Simple tables with custom styling that don’t require many interactions for the columns other than simple popover text
- Let’s start building a simple table UI with basic functionalities like sorting and searching using react-table

## Design better data tables

> The ingredients of a successful data table UI

- [Design better data tables](https://medium.com/nextux/design-better-data-tables-4ecc99d23356)

- This article presents a list of design structures, interaction patterns, and techniques to help you design better data tables.
- vertical scroll with fixed header row
- horizontal scroll with fixed header column
- sortable column
- filterable column
- resizble column
- searchable column
- add column
- customizable column fields
- row styling: zebra stripe, line divisions, free form
- row to details
- display density
- expandable rows
- inline editing
- quick view
- modal
- multi-modal
- pagination
- hover actions
- visual summary for table

## How to design data tables 
- the 20 rules guide

- [How to design data tables - the 20 rules guide](https://www.mobilespoon.net/2019/11/design-ui-tables-20-rules-guide.html)

- **Functionality**
- Start with Sort and Filters
- Make sure your columns are resizable
- Allow columns reorder 
- Inline editing

- **Design**
- Design for small screens
- Color alternating rows 
- Anchor some identifiers with fixed headers and “frozen” columns
- Set a fixed row height
  - Tables and grids are about structured information, but when a table has too many column widths and different row heights - things become messy and the information feels less structured.
  - While I believe the resizable columns are a must - having resizable rows is a different story: it adds another dimension and might confuse the users more than it's helpful.
  - So for the sake of overall usability and aesthetics, I believe all the rows should have the exact same height, regardless of the content.
  - To better support multiline text chunks consider the following:
    - Replace newlines with space and turn the whole text into one line (that can be viewed by resizing the column width).
    - Turn the row height (of all the rows) to be 2 lines instead of 1 (will only solve some of the scenarios).
    - Use tooltips (no, forget that. Tooltips are lame).
    - Consider an option to expand/collapse a row by clicking it (which might be a needed functionality anyway).
    - Consider an option to show the details of the selected row using a floating side view as mentioned in rule number 4.

- **Aesthetics**
- Increase cell padding 
- Get rid of unnecessary borders
  - get rid of those redundant borders or at least make them super thin and with light colors
- Turn black into dark gray
- Text should be vertically aligned to the top
- Text should be horizontally aligned to the left
- Numbers should be horizontally aligned to the right
- Special fields should be horizontally aligned to the middle
- Use consistent string formatting 
- Avoid using too many colors
- Avoid using too many font styles, or font weights
- Do not bloat your table with too many status icons or buttons 
- Support multiple selections for bulk actions

- **Bonus Tip**
  - I recommend having an “export to CSV” button that will allow users to manipulate the data in Microsoft Excel or Google Sheets (I, for one, care deeply about pivots).

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

## list-blog-collection

- [Testing with Jest & Enzyme - querying JSDOM vs ag-Grid API](https://blog.ag-grid.com/testing-ag-grid-react-jest-enzyme/)
  - jsdom: test user behavior
  - ag-grid api: compatible with dom virtualisation, test implementation
