---
title: lib-excel-tabulator-dev
tags: [docs, grid, tabulator]
created: 2020-10-21T12:46:30.133Z
modified: 2022-08-21T09:59:36.457Z
---

# lib-excel-tabulator-dev

# roadmap

# changelog

## [v5.0 Released_202110](https://github.com/olifolkerd/tabulator/issues/3403)

- [5.0 Alpha Release Now Available_202104](https://github.com/olifolkerd/tabulator/issues/3286)

- Tabulator has undergone a complete rebuild of the codebase.

- you now use ESM importing to import the Tabulator core library, and then only the modules you want to use
- Modules are where Tabulator stores functionality that is outside of the core library, such as sorting, filtering, grouping etc.

- The table rendering functionality has now been broken out into a series of different renders, that handle functions like Virtual DOM and classic render modes.

- Tabulator now has internal and external event buses instead of callbacks to allow for more flexibility in how and when you get notified about actions in the table

## [v4.9 Released - Performance Improvements(and some info on v5.0)](https://github.com/olifolkerd/tabulator/issues/3085)

- This is going to involve a wholesale refactor of the codebase to take advantage of the tree shaking functionality of ESM to improve package size and to make way for the implementation of unit testing across the library.
- This is no small update, there will be wide ranging efficiency improvements across the system as well as a range of new features and functionality
- I am currently aiming to have version 5.0 release in either Feb or March 2021
# blogging

## [Release 5.0-alpha (Technology Preview)](http://tabulator.info/docs/5.0/release)

- With the release of version 5.0 Tabulator has undergone a complete rebuild of the codebase.
- Codebase Restructure
- Class Structures
  - switched from the old prototypical design paradigm to using the cleaner ES6 Class structure.
- ESM Importing
  - Tabulator has moved to using ESM importing of the library as standard 
  - by default will now only import the minimal core library, that provides basic table layout functionality.
  - there is still an option for importing a complete version of Tabulator with all the modules pre loaded
- Communication & Event Bus
  - Communication throughout the table is now managed through a central event bus that decouples each area of the system from each other, helps isolate code, improve testing and increase communication efficiency
  - A second event bus now manages all external communication outside of the table, with old style callbacks on the table now being replaced with events that you can subscribe to
- Module Isolation
  - modules have been completely restructured to totally isolate their functionality from each other and the rest of the table
- Data Loader
  - A central data loader now manages all data as it is loaded into the table, this handles all local data, as well as triggering internal events on the event bus that allow modules to subscribe and provide data from remote sources such as ajax and databases
- Data Management Pipeline
  - The data and row management pipelines have been overhauled to allow modules to register themselves as a pipeline state, allowing modules to directly alter the rows displaying in the table as they are rendered
- Event Listeners
  - A new interaction manager has been added to the core of Tabulator that listens to all standard table events (click, tap, mouse etc) through the main table element
- Table Renderers
  - Renderers (eg virtual DOM / basic) have been separated from the row management logic to make managing the render of the table simpler 
  - The table renderers have been optimized to reduce redrawing during scroll, improving table load times and scroll efficiency, resulting in a smoother experience for end users.
