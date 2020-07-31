---
title: note-pm-list-grid-table-design
tags: [grid, table, ux]
created: '2020-07-30T16:42:11.432Z'
modified: '2020-07-30T16:42:38.231Z'
---

# note-pm-list-grid-table-design

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

## 5 Practical Solutions to Make Responsive Data Tables

- [5 Practical Solutions to Make Responsive Data Tables](https://medium.com/appnroll-publication/5-practical-solutions-to-make-responsive-data-tables-ff031c48b122)

- Shorten
  - cutout unnecessary columns and keep the table concise by leaving the crucial data only
- Moveable
  - use swipe gestures to scroll through the whole table horizontally.
- Collapsed
  - everything is visible without scrolling and columns are navigated using swipe gestures
  - The primary column (legend) can be fixed in one place so we don’t lose the context of data.
- Transformed
  - The main rule is a collapsing of the table rows into separate cards.
- Comparing
  - It’s also a similar to the Collapsed one I described above but it is ready for a larger amount of data.
  - All we need to add is easy navigation through the whole table, displaying only two columns at a time.

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

## How to design data tables - the 20 rules guide

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

## Tables UI design in Figma: data grid by a single component

- [Tables UI design in Figma](https://uxdesign.cc/tables-ui-design-in-figma-data-grid-by-a-single-component-5d2c76c16f8)

- There are three approaches to table design to create a data grid with a flexible architecture. 
- In each case, either a row component, a column component or a cell component is used.
- Table styles
  - classic
  - contrast heading
  - material table
  - patch work
  - minimal
- All 5 styles I've shown above are collected from one cell-component, the difference is only in content and all they will refer on one and the only chief component. I consider this method to be the most flexible
- Use a row with cells of a predefined quantity. 
  - Thus, the table is quickly made by simply cloning from top to bottom. 
  - Then the width and height of each row are adjusted.
  - low degree of flexibility, the cells are always proportionally scaled.
- make the table from the component-columns, inside of which the number of rows is predetermined and multiplied, and all the extra ones would be cut off outside the frame through the Clip Content option. 
  - Then it would be enough to pull the frame down by the bottom border to show more additional cells in the column
  - inside a component, you cannot adjust the height of each cell
- The use of a cell-component gives maximum flexibility in styling the table.
  - Cons: there are almost none, except that this approach requires more time and system design skills
  - Pros: maximum flexibility, ability to control the grid with a single component, adjust separators, background, nested icons and more.

## Why You Will Never Give Up Spreadsheets

- [Why You Will Never Give Up Spreadsheets_2016](https://handsontable.com/blog/articles/2016/7/why-you-will-never-give-up-spreadsheets)

- The Positives
  - As the tools we use to create spreadsheets evolved, they have added features that allow for more than simply working with numbers and text. 
    - Users can now integrate charts, animation, and images, while using filtering, sorting and pivot tables to rapidly change the type of information displayed.
  - The fact that – at entry level – it requires very little training to use.
  - It is cost effective, with open-source and commercial versions available for all operating systems, without the need for high-end hardware.
  - In many instances, spreadsheets created on one platform can still be opened and edited on a completely different platform.
  - It is a very powerful tool for editing, reading, reporting and analyzing data.

- The Flaws
  - Detecting errors with strict policies in place
    - the protection, validation and testing of formulas and macros
    - change control
    - version control
  - errors will still creep in because these measures are all manual, and subject to the fallibility of man
  - Poor – or non-existent – audit trail functionality.
  - The inability to generate real-time reports – with read-only rights – across the organization.
  - Producing ad-hoc reports and analysis is often difficult and onerous.
  - Managing and sharing large files is prone to problems.
  - They lack effective processes for enforcing data ownership.
  - They don’t offer a system for seamless, automatic back-ups, influencing data integrity concerns.

- The Outlook
  - Is comfortably able to handle big data.
  - Loads data dynamically, from a variety of data sources, and integrates easily with other cloud-computing solutions.
  - Is more modular, with add-ons that extend the functionality even further.
  - Has error checking and version control built-in.
  - Retains the ease-of-use and intuitiveness of traditional spreadsheet software, but offers better security.
  - Offers automated back-ups, with effortless restoration.
  - Apply a common standard in the design and development of spreadsheets, addressing things such as cell formatting.
  - Ensure that everyone who works with spreadsheets has had suitable training. 
    - Although basic spreadsheet work requires minimal training, more complex operations, including how to check the results of functions, can only be properly done with appropriate training.
  - Implement best practices for collaborative work, including a peer review system, to help minimize errors.
  - Add an About sheet to all complex spreadsheets, documenting the author, the purpose of the document, the version number, and any formatting conventions.
  - Ensure that everyone is always using the same software version.
