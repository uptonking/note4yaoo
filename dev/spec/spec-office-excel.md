---
title: spec-office-excel
tags: [excel, format, office]
created: 2019-12-24T12:54:32.612Z
modified: 2021-09-30T07:44:25.136Z
---

# spec-office-excel

# spec

- 

# faq

- 

# guide
- features
  - csv based sheet, like mdx based doc, 简单读写无需借助专业软件
# resources
- data
  - [Sample Sales Data Excel Download – 5 Free Datasets | Excelx.com](https://excelx.com/practice-data/sales-retail/)

## tutorials

- [#1 Excel Tutorial on the Net - Excel Easy](https://www.excel-easy.com/)
  - 300 Examples to Excel like a Pro

- [ExcelChamp](https://excelchamp.com/)
  - Join our Excel courses, improve your knowledge and skills
  - [ExcelChamp | Solving Everyday Problems With Excel](https://www.excelchamp.net/)
    -  Excel Tips and Tricks, Formulas and shortcuts
# more

# discuss
- ## a standard that extends CSV files to have formulas, 
- https://twitter.com/andrestaltz/status/1344320355960299520 
  - and to slice huge CSVs into multiple files so to allow scalability, 
  - and then an ecosystem of tools to read/write them. 
  - Alternative to Excel.
- Why tho. Grid spreadsheets suck, something like @InflexHQ is the way
  - All the excel and google spreadsheet users disagree with you, so no, it doesn't suck
  - excel users routinely use CSV
- There are open-source alternatives to Excel. 
  - Yes, they have bunch of bells and whistles, much more than needed for just formulas, 
    - but you still want another ???:xls = rtf:doc?
  - I want an ecosystem of tools. 
    - Not a monolith program like LibreOffice Calc, but more like an ecosystem of plugins. 
    - Think Webpack plugins or Callbag operators
  - If we have web word processors with plugins (both CKEditor and tinyMCE are nice in that respect), there should be some spreadsheet tables as well.
- the thing is that CSV files are mostly static. 
  - Formulas are intended to work with dynamic data IMHO.
    - The standard would work on things like line-breaks, dot vs comma in numbers, currencies, etc
  - In the file, the formulas would obviously be static, 
    - but any renderer that can read this extended format would automatically calculate the formulas
- What about just files with key-value pairs (or the KV pairs could be in databases or HTTP APIs) 
  - and then you can compute on these, create new KV pairs with formulas, 
    - and finally there could be GUIs that would display these values in customized combinations lines and columns.
  - I think the easiness of reading and writing CSV is appealing and good to preserve
- Maybe not actually CSV though. 
  - Maybe some other delimiter or something slightly more structured. 
    - Alternatively, be very rigid in the format specification for this CSV variant.
    - I can see quoting in formulas getting really complicated really fast.
  - Also fun fact: Excel will parse and execute formulas from a CSV file.
- Is this distributed excel?
  - not directly. But you could put these CSVs in a hyperdrive and there you go
- Sounds similar to using SQLite files where the formulas are functions in a language with a SQLite C FFI

- I do wonder, how far with justabusing sqlite would get you:  https://sqlite.org/csv.html
# solutions

## [Inflex](https ://inflex.io/)

- Inflex® is an upcoming spreadsheet alternative: 
  - static types
  - powerful functional language (Haskell-inspired)
  - rich data structures (no grid!)
  - browser-based

- Familiar formulas like in spreadsheets
  - Cells are boxes that compute things, like arithmetic. 
  - You can click them to change the formula and hit Enter to see the result again.
  - Where's the grid? There is no grid. We use cells on an as-needed basis.

- Built-in records
  - Inflex natively understands records with built-in syntax. 
  - Records model the idea of a single thing, like a person or a stock item.
  - Records can be worked with either as code or as structured elements in the interface.

- Lists
  - Lists are also built-in with special syntax, which can be edited either graphically or as a formula.
  - They contain one value inside, and each item in the list has the same type, so it's always safe to apply transformations or filters on them.

- Tables
  - We can create a table in the graphical interface piece by piece.
  - In Inflex, tables are simply lists of records! 
  - That means you can re-use the same intuitions and concepts, a filter on a table is just a filter on a list.

- Functions
  - Functions let us specify computations to be done on some input. 

- Re-using functions
  - Functions are normal values like numbers or text, so they can be put in a cell and passed around.
  - Here we put the function in another cell and then use it in our original filter. 
  - This way, we separated concerns and gained re-use.

- Type system to prevent mistakes
- Use blanks when you're not done
- Nest data inside other data freely

## [Stencila](https://stenci.la/)

- Executable document pipelines
  - Author, collaborate, execute, and publish beautiful interactive documents on an open source web platform
- Integrates with existing workflows
- Collaborate
- Reproducible Environments

## [Frictionless Data](https://frictionlessdata.io/)

- Frictionless Data is a progressive, incrementally adoptable open-source toolkit 
  - that brings simplicity and gracefulness to the data experience
  - whether you're wrangling a CSV or engineering complex pipelines with gigabytes.
