---
title: lib-ag-grid-codebase-design
tags: [ag-grid, codebase, lib]
created: '2020-08-21T09:00:56.176Z'
modified: '2020-08-21T09:01:26.000Z'
---

# lib-ag-grid-codebase-design

## overview

- ag-grid-packages
  - ag-grid-community: All Community Features
    - community-modules: 主要4部分
      - core
      - client-side-row-model 
      - infinite-row-model
      - csv-export 
      - 框架相关: react,vue,angular,polymer
  - ag-grid-enterprise: All Enterprise Features
    - enterprise-modules
      - core
      - row-grouping
      - rich-select
      - column-tool-panel
      - range-selection
      - date-time-cell-editor
      - filter-tool-panel
      - clipboard
      - excel-export
      - master-detail
      - menu
      - server-side-row-model 
      - set-filter
      - side-bar
      - status-bar
      - viewport-row-model
  - ag-grid-react: React Support
  - ag-grid-vue: Vue Support
  - ag-grid-angular: Angular Support
  - ag-grid-polymer: Polymer Support
  - examples-grid/charts
  - charts-packages
    - 也是4种实现: community, react, vue, angular

- There are two main ways to install ag-Grid - either by using `packages` , or by using `modules` .
  - packages are the easiest way to use ag-Grid, but by default include all code specific to each package, 
  - whereas modules allow you to cherry pick what functionality you want, which will allow for a reduced overall bundle size.
  - If you're unsure whether to use packages or modules, then we'd recommend starting with packages and migrate to modules if you wish to reduce overall bundle size.
- When using `packages` , you get all of the code within that package and cannot pick and choose which features you require. 
  - You also don't need to register these packages in the same way you do with `modules` .
  - This means that it is easier to use packages, but the trade-off will be you'll end up with a larger bundle size if you don't require all features within a given package.

- ag-Grid `modules` allow you to pick and choose which features you require, resulting in a smaller application size overall, with the trade-off being that you need to register the modules you require.
  - @ag-grid-community/all-modules: All Community Modules
  - @ag-grid-community/core: Core Grid Components, GridOptions, ColDef etc
  - @ag-grid-community/client-side-row-model: ClientSideRowModelModule
  - @ag-grid-community/infinite-row-model: InfiniteRowModelModule
  - @ag-grid-community/csv-export: CsvExportModule

- `@ag-grid-community/all-module` s can be considered to be equivalent to `ag-grid-community` , but with the additional need to register modules within.
- `@ag-grid-enterprise/all-modules` will contain all Community modules.
- Note that neither `@ag-grid-community/all-module` s nor `@ag-grid-enterprise/all-modules` contain framework support 
  - if you require framework support you need to explicitly specify it, like `@ag-grid-community/react`
  - You do not need to register framework modules (ie. `@ag-grid-community/angular` etc).
- If you choose to select individual modules, then at a minimum the a Row Model need to be specified. 
  - After that all other modules are optional depending on your requirements.
- Providing Modules Globally
  - You can import and provide all modules to the Grid globally if you so desire, but you need to ensure that this is done before any Grids are instantiated.
- Providing Modules To Individual Grids
  - use `modules` prop
- If you specify any Community or Enterprise dependency, then the corresponding `core` module will also be pulled in and be made available to you.
- `@ag-grid-community/core`
  - This module contains the core code required by the Grid and all modules (Enterprise or Community) depend on it. 
  - As such `@ag-grid-community/core` will always be available no matter what module you specify in your `package.json` .
