---
title: lib-excel-ospreadsheet-docs
tags: [docs, excel, ospreadsheet]
created: 2023-06-07T22:37:51.236Z
modified: 2023-06-07T22:38:05.075Z
---

# lib-excel-ospreadsheet-docs

# guide

# overview

# [Architecture](https://github.com/odoo/o-spreadsheet/blob/saas-16.3/doc/extending/architecture.md)

- o-spreadsheet is architected in two main parts: the model and the spreadsheet rendering in the DOM.

- Model: commands and getters
- It directly manages the data, logic and business rules.
- The model architectural pattern is command query separation.
- You can interact with the model by two means:
  - getter functions allows to read the current state.
  - commands can update the spreadsheet state. Commands are handled internally by plugins.

- A plugin can:
  - have its own private state
  - introduce new getters to make parts of its state available for other plugins or the user interface.
  - react to any dispatched command
- Plugins are decomposed in two parts: core and UI.
- Core plugins are responsible to manage the data persistence and all associated business rules (cell content, user-defined style, chart definitions, ...). 
  - Each plugin is responsible of one data structure.
- UI plugins are separated in three different categories
  - Manage the ui state (active sheet, current selection, ...)
  - Manage the derived state from the core part (cell evaluation, computed style, ...)
  - Handle high-level features that could be described with lower-level features (Sort a zone can be described with different cell updates)

- The grid itself is rendered on an HTML canvas.
  - All other elements are rendered with the owl UI framework. 
  - The UI is rendered after each command dispatched on the model with the help of the getters.
# [Plugins](https://github.com/odoo/o-spreadsheet/blob/saas-16.3/doc/extending/plugin.md)
- A plugin is a way for o-spreadsheet to organize features in order not to interfere with one another.
- All plugins can :
  - have its own state
  - add new getters to make parts of its state available for other plugins, for the user interface or to use in formula functions
  - react to any existing command
- There is 2 different kind of plugins: CorePlugin and UIPlugin.
- UIPlugin manages transient state, user specific state and everything that is needed to display the spreadsheet without changing the persistent data (like evaluation)
- UI plugins are separated in three different categories:
- Stateful Plugins
  - Plugins which have a state, but which should not be shared in collaborative
- Core views Plugins
  - Plugins which have a derived state from core data
- Feature plugins
  - Plugins which handle a specific feature, without handling any core commands

- For processing all commands, command will go through the functions on the plugins in this order:
  - allowDispatch
  - beforeHandle
  - handle
  - finalize. 
    - In finalize, you cannot dispatch new commands
    - After all the finalize functions have been executed, the spreadsheet component will be re-rendered.

- Changes to the state that must be restored by Undo must be done through the function this.history.update()
  - this.history can be used with multiple level of depth
- Custom external dependency
  - You can provide any custom dependencies to your plugin in the Model's config.

- to reflect this state in the UI. This can be done with mainly two different ways:
  - Using the `drawGrid` method on UIPlugin
  - Using a getter in a new component (Side panels, menu item, ...)
# Commands
- Commands are the way to make changes to the state. 
  - They are dispatched to the model, which relay them to each plugins.
- There are two kinds of commands: CoreCommands and LocalCommands.
- CoreCommands are commands that
  - manipulate the imported/exported spreadsheet state
  - are shared in collaborative environment
- LocalCommands: every other command
  - manipulate the local state
  - can be converted into CoreCommands
  - are not shared in collaborative environment
- CoreCommands should be "device agnostic". 
  - This means that they should contain all the information necessary to perform their job. 
- Local commands can use inferred information from the local internal state, such as the active sheet.
- Some commands can be repeated. 
  - A command will be repeated if the user tries to REDO while the redo stack is empty. 
  - In this case, the history plugin will check if the last command locally dispatched is repeatable. If this is the case, the command will be adapted to the current selection and the current active sheet before being dispatched again.
# [collab](https://github.com/odoo/o-spreadsheet/blob/saas-16.3/doc/integrating/collaborative/collaborative_choices.md)
- Realtime collaboration is enabled by providing  transport service
  - The TransportService is responsible for sending and receiving messages between the clients with the help of central server.
- Messages sent through the transport service should be handled by a **centralized server**. 
  - Its goal it to coordinate messages, order them and maintain the current spreadsheet revision. 
  - For each received messages, **the server decides if it's accepted or not**. 
  - If the message is accepted, it's transmitted to all clients (including the one which sent the message).

- The solution we implement is based on Operation Transform (OT).
- To separate which commands should be shared, we introduce a separation of the commands:
  - CoreCommands: all the commands handled by a CorePlugin
  - Commands: all the CoreCommands and the Commands handled by a UIPlugin (i.e. all the commands of spreadsheet)
- For each new CoreCommand, a check should be done if transformation and inverse functions should be written (a test is present to force this check).

- Here is our thoughts and reflection about how to implement the multi user feature in o-spreadsheet.
  - Which piece of information should be shared?
  - How to have a synchronized between multiple clients
  - How to manage concurrency and conflicts (ex: update a cell in a removed sheet)
  - The spreadsheet should be reactive, i.e. the actions the user do should be immediately executed locally
  - How to handle local Undo/Redo

- last-write-wins
  - the clients send their changes to others without taking care of concurrency and conflicts. The last arrived wins. 
  - This required to send all changes, so adding a columns (which moves all the cells to the right) is quite huge. 
  - This option was quickly abandoned as it's not possible to handle conflicts and Undo/Redo.

- CRDT
  - better than OT in terms of synchronization, but is actually much more complex (in terms of code and data).

- Operational Transformation
  - The aim of operation transform is to keep the intention of the users, even when the actions are executed concurrently. 
  - This required to transform the operation which comes after with the transformation which comes before. 
  - To do that, **we need a global order**
- In order to identity and resolve conflicts, we need a way to detect two concurrent actions, and a way to order them.
- The first option we explored to resolve that is the implement a `state vector`, which allows detecting conflicts and order commands client-side. This option was quickly abandoned as it's required bi-directional transformation.
- The second option (the which we keep) was to introduce a server-based scheduling. 
  - The first command the server received is considered as the first command. 
  - To detect concurrency, we introduce a **revision log**, which is a unique identifier to indicate on which state the action is executed. 
  - Each time an action is received and accepted by the server (the revision log of the server is the same as the action), the revision log is incremented.
- When a client executes an action, it's locally executed, sent to the server and kept in the pending actions of the user. 
  - If the action is accepted by the server, the action is removed from the pending ones. 
  - In the other case, the pending actions are reverted, transformed with the action received from the server, re-applied locally and resent to the server until they are accepted.
- Local undo is implemented by keeping locally the actions of the user, revert to just before the undo-ed action, transform the next actions as if the undo-ed action was not executed and re-apply them. Local redo follow the same logic.
- To keep a synchronous state, we only need to share the commands which impacts the state of spreadsheet (columns, grid, ...) but not the local state (selection of the user, composer state, ...)

- This solution has a lot of pros, but also some cons:
  - We need to write a transformation function for each command we create, which could theoretically becomes huge. However, in practice, the transformations only concerns commands which changes the grid (add/remove columns, remove a sheet, merge).
  - Undo/Redo is synchronous, i.e. it should be accepted by the server before being executed locally.

- Undo/Redo with inverse command, but actually inverse events
  - can snapshot every time someone leaves (since we don't need the history)
  - no need to keep and apply history when joining a session
  - concurrent undo/redo are allowed
  - more work to introduce a new command => need to introduce events as well
  - more bandwidth/data. e.g. ADD_ROW becomes "row-added", "cell-updated", "cell-updated", "cell-updated", "cell-updated"...
  - need to trigger an event to change the state (same as this.history.update)

- To extend o-spreadsheet without breaking realtime collaborative edition, there are some points to keep in mind.
- There are two types of commands: CoreCommands and Commands. 
  - **Only CoreCommands are synchronized**.
  - For each new CoreCommand, a transformation function could be required for each other CoreCommands.
- In addition to a transformation, an "inverse function" is required for commands which transforms other commands
  - The inverse function takes as input a CoreCommand and should return a list of CoreCommands.
  - The inverse function is used during a selective undo to transform commands executed after the undo-ed command as if the command had never been executed.
# more
