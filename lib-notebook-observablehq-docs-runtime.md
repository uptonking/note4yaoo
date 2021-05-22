---
title: lib-notebook-observablehq-docs-runtime
tags: [docs, notebook, observablehq, runtime]
created: '2021-05-14T14:44:25.385Z'
modified: '2021-05-22T18:47:39.353Z'
---

# lib-notebook-observablehq-docs-runtime

# guide

# docs

- https://github.com/observablehq/runtime
  - The Observable dataflow runtime.
  - an open-source runtime which stitches together a notebook’s cells into a dependency graph and brings them to life through evaluation

- The Observable runtime lets you run Observable notebooks as true reactive programs in any JavaScript environment: on your personal website, integrated into your web application or interactive dashboard. 

## Runtimes

- `new Runtime(builtins = new Library[, global])`

- Returns a new runtime. 
  - If builtins is specified, each property on the builtins object defines a builtin variable for the runtime. 
  - These builtins are available as named inputs to any defined variables on any module associated with this runtime. 
  - If builtins is not specified, it defaults to the standard library.
- Unlike variables, builtins cannot depend on the value of other variables or builtins; 

## Variables

- A variable defines a piece of state in a reactive program, akin to a cell in a spreadsheet. 
- Variables may be named to allow the definition of derived variables: variables whose value is computed from other variables’ values. 
- Variables are scoped by a module and evaluated by a runtime.

## Modules

- A module is a namespace for variables; 
  - within a module, variables should typically have unique names. 
  - Imports allow variables to be referenced across modules.

## Observers

- An observer watches a variable, being notified via asynchronous callback whenever the variable changes state.

## re-exports

- For convenience, this module re-exports the Observable standard library.

- For convenience, this module re-exports the Observable standard inspector.
