---
title: lib-notebook-observablehq-docs-runtime-inspector
tags: [docs, observablehq]
created: '2021-05-14T14:44:25.385Z'
modified: '2021-05-14T14:51:47.612Z'
---

# lib-notebook-observablehq-docs-runtime-inspector

# runtime

- https://github.com/observablehq/runtime
  - The Observable dataflow runtime.

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
# inspector

- https://github.com/observablehq/inspector


- This library implements the default value renderer for Observable programs. 
- When used with the Observable runtime as observers, inspectors can insert elements into the DOM and render interactive displays for arbitrary values.
- An inspector implements the Observable runtime’s Observer interface by rendering the current value of its associated variable to a given DOM element. 
- Inspectors display DOM elements “as-is”, and create interactive “devtools”-style inspectors for other arbitrary values such as numbers and objects.


