---
title: docs-ag-grid-api
tags: [ag-grid, api, docs]
created: '2020-08-24T09:15:27.178Z'
modified: '2020-08-24T09:16:38.313Z'
---

# docs-ag-grid-api

## Grid Interface

- The grid interface is the combination of the following items:
- Grid Properties
  - properties used to configure the grid, e.g. `pagination = true` .
- Grid API
  - methods used to interact with the grid after it's created, e.g. `api.getSelectedRows()` .
- Events
  - events published by the grid to inform applications of changes in state, e.g. `rowSelected` .
- Grid Callbacks
  - callbacks are used by the grid to retrieve required information from your application, e.g. `getRowHeight()` .
- Row Node
  - each row in the grid is represented by a Row Node object, which in turn has a reference to the piece of row data provided by the application. 
  - The Row Node wraps the row data item. 
  - The Row Node has attributes, methods and events for interacting with the specific row e.g. `rowNode.setSelected(true)` .

### Grid Options

## Grid Properties

## Grid API

## Grid Events

## Grid Callbacks

## Grid Object
