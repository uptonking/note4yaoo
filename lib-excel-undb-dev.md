---
title: lib-excel-undb-dev
tags: [excel, undb]
created: 2023-05-17T07:35:48.070Z
modified: 2023-05-17T07:36:07.757Z
---

# lib-excel-undb-dev

# guide

- features
  - private-first / self-hostable
  - multiple built-in field types
  - multiple views, including grid, kanban, tree, calendar and more
# dev-to
- 去掉table概念，将field作为最底层基础block
  - 将table只视为field的一种具体组合，field还可以组合为kanban/tree

- 去掉loadable-component
# codebase
- undb底层数据库设计包括 table/field/view/attachment


- 
# dev

# docs

- Undb tables function like spreadsheets in that you can sort, filter, aggregate your data and modify many other table features. 
  - In contrast to standard spreadsheets, Undb lets you see tables in several ways as a grid of rows and columns, Tree diagram, form, calendar, or kanban boards.

- A table consists of rows and fields (columns).
  - In a table, a field is a collection of values of the same data type. 
  - Each field is a data structure that holds a defined data type.

- Basic table field types are the different data types that can be stored in a table, such as text, numbers, and dates, and are used to classify and manage data effectively.

- The system field are used to record system information, including the creation and modification times, the creator and modifier’s names, etc. 

- Reference Field
  - 1-1: 比如商品-二维码
  - 1-N: hasMany，比如店铺-商品二维码
  - N-N: 比如商品-类别标签
- Relationships between table records can be established by using `LinkToAnotherRecord` column type.

- Lookup Field
  - Lookup fields are read-only fields. 
  - When creating a lookup field you can choose a ‘Link to table’ field in the same table and a field in the related table.
  - Start by creating a link to table field before using a lookup field.
- The Count field is used to count the number of matching entries in the referenced table for the unique key (foreign key) referenced by the current row. 
# more
