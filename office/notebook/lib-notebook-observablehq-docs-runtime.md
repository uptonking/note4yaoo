---
title: lib-notebook-observablehq-docs-runtime
tags: [docs, notebook, observablehq, runtime]
created: 2021-05-14T14:44:25.385Z
modified: 2021-05-22T18:47:39.353Z
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
  - If `builtins` is specified, each property on the builtins object defines a builtin variable for the runtime. 
    - These builtins are available as named inputs to any defined variables on any module associated with this runtime. 
  - If `builtins` is not specified, it defaults to the standard library.
  - If a `global` function is specified, it will be invoked with the name of any unresolved reference, and must return the corresponding value or `undefined` (to trigger a ReferenceError); 
  - if `global` is not specified, unresolved values will be resolved from the global `window`.

- Unlike variables, ** builtins cannot depend on the value of other variables or builtins**; 
  - they are defined with no inputs
  - If a builtin is defined as a function, it will be invoked lazily to determine the value of the builtin. 
- If you wish for the value of a builtin to be a function, the builtin must be defined either as a promise that resolves to a function or as a function that returns a function. 
- Builtins may also be defined as generators for dynamic values; 

- `runtime.module([define][, observer])`
- Returns a new module for this runtime.

- `runtime.dispose()`
  - Disposes this runtime, invalidating all active variables and disabling future computation.

## Modules

- A module is a namespace for variables; 
  - within a module, variables should typically have unique names. 
  - Imports allow variables to be referenced across modules.

- `module.variable([observer])`
  - Returns a new variable for this module. The variable is initially undefined.
  - If observer is specified, the specified observer will be notified when the returned variable changes state, via the observer.pending, observer.fulfilled and observer.rejected methods. 

- `module.derive(specifiers, source)`
  - Returns a derived copy of this module, where each variable in specifiers is replaced by an import from the specified source module. 

- `module.define([name, ][inputs, ]definition)`
  - A convenience method for `variable.define`
  - 等于 `module.variable().define(name, inputs, definition)`

- `module.import(name, [alias, ]from)`
  - 等于 `module.variable().import(name, alias, from)`

- `module.redefine(name[, inputs], definition)`
  - Redefines the variable with the specified name on this module. 
  - If no such variable exists, or if more than one variable has the specified name, throws a runtime error.

- `module.value(name)`
  - Returns a promise to the next value of the variable with the specified name on this module. 

## Variable(like cell)

- A variable defines a piece of state in a reactive program, akin to a cell in a spreadsheet. 
- Variables may be named to allow the definition of derived variables: variables whose value is computed from other variables’ values. 
- Variables are scoped by a module and evaluated by a runtime.

- `variable.define([name, ][inputs, ]definition)`
  - 定义单元格对应的变量名、初始值
  - Redefines this variable to have the specified name, taking the variables with the names specified in inputs as arguments to the specified definition function.
  - If name is null or not specified, this variable is anonymous and may not be referred to by other variables.
- The `definition` function may return a promise; 
  - derived variables will be computed after the promise resolves.
  - The definition function may likewise return a generator; the runtime will pull values from the generator on every animation frame
  - When the definition is invoked, the value of this is the variable’s previous value, or undefined 
- variable names can change when a variable is redefined or deleted. 
- **Each variable corresponds to a cell** in an Observable notebook, but the cell can be redefined to have a different name or definition.
- If more than one variable has the same name at the same time in the same module, these variables’ definitions are temporarily overridden to throw a ReferenceError.

- `variable.import(name, [alias, ]module)`
- Redefines this variable as an alias of the variable with the specified name in the specified module. 

- `variable.delete()`
  - Deletes this variable’s current definition and name, if any.
  - Any variable in this module that references this variable as an input will subsequently throw a ReferenceError.

## Observers

- An observer watches a variable, being notified via asynchronous callback whenever the variable changes state.

- observer.pending()
  - Called shortly before the variable is computed.
  - For a generator variable, this occurs before the generator is constructed, but not before each subsequent value is pulled from the generator.

- observer.fulfilled(value)
  - Called shortly after the variable is fulfilled with a new value.

- observer.rejected(error)
  - Called shortly after the variable is rejected with the given error.

## re-exports stblib/inspector

- For convenience, this module re-exports the Observable standard library.

- For convenience, this module re-exports the Observable standard inspector.
