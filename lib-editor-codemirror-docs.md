---
title: lib-editor-codemirror-docs
tags: [codemirror, docs]
created: 2024-05-02T02:00:39.708Z
modified: 2024-05-02T02:00:47.318Z
---

# lib-editor-codemirror-docs

> CodeMirror is a code editor component for the web.

# guide
- codemirror的架构主要分3方面: model, view, extension
# docs

## overview

- CodeMirror is set up as a collection of separate modules that, together, provide a full-featured text and code editor. 
- Many things that you'd expect in an editor, such as the line number gutter or undo history, are implemented as extensions to the generic core, and need to be explicitly added to a configuration to be enabled. 
- To make it easy to get started, the `codemirror` package pulls in most of the things you need for a baseline editor (except a language package).

- An attitude that guides the architecture of CodeMirror is that functional (pure) code, which creates new values instead of having side effects, is much easier to work with than imperative code
- the library's state representation is strictly functional—the document and state data structures are immutable, and operations on them are pure functions, whereas the view component and command interface wrap these in an imperative interface.
  - This means that an old state value stays intact even when the editor moves on to a new state.
  - as a general rule, unless explicitly described in the docs, reassignment of properties in objects created by the library is just not supported.

- The library handles updates in a way inspired by approaches like Redux or Elm. 
  - With a few exceptions (like composition and drag-drop handling), the state of the view is entirely determined by the `EditorState` value in its `state` property.
- 💡 Changes to that state happen in functional code, by creating a transaction that describes the changes to document, selection, or other state fields. 
  - Such a transaction can then be dispatched, which tells the view to update its state, at which point it'll synchronize its DOM representation with the new state.
- The data flow during typical user interaction looks something like this:
  - ⛓️ event -> transaction -> newState -> newView
  - The view listens for events. When DOM events come in, it (or a command bound to a key, or an event handler registered by an extension) translates them into state transactions and dispatches them. This builds up a new state. When that new state is given to the view, it'll update itself.

- Since the core library is rather minimal and generic, a lot of functionality is implemented in system extensions. 
  - Extensions can do all kinds of things, from merely configuring some option, to defining new fields in the state object, to styling the editor, to injecting custom imperative components into the view. The system takes care to allow extensions to compose without unexpected conflicts.
- The set of active extensions is kept in the editor state (and can be changed by a transaction). 
  - Extensions are provided as values (usually imported from some package), or arrays of such values. They can be arbitrarily nested (an array containing more arrays is also a valid extension), and are deduplicated during the configuration process. Thus, it is okay for extensions to pull in other extensions—if the same one gets included multiple times, it'll only take effect once.
- When relevant, the precedence of extensions is determined first by explicitly set precedence category, and within that, by the position the extension has in the (flattened) collection of extensions passed to the state.

- Document Offsets
- CodeMirror uses plain numbers to address positions in the document. 
  - These represent character counts—more precisely, they count `UTF16` code units (so astral characters count as two units). 
  - Line breaks always count as a single unit (even when you configure a line separator that is longer than that).
- These offsets are used to track the selection, position changes, decorate content, and so on.
- It is sometimes necessary to figure out where a position in a start document ends up in a changed document. For this purpose, the library provides a position mapping feature, which, given a transaction (or just a change set) and a start position, can give you the corresponding new position.
- The document data structure also indexes by lines, so it is not expensive to look things up by (1-based) line number.

- Data Model
- CodeMirror, being a text editor, treats the document as a flat string. 
  - It stores this in a tree-shaped data structure to allow cheap updates anywhere in the document (and efficient indexing by line number).
- Document changes are themselves `ChangeSet` values, describing precisely which ranges of the old document are being replaced by which bits of new text. 
  - This allows extensions to track precisely what happens to the document, allowing things like an undo history and collaborative editing to be implemented outside the library core.
- When creating a change set, all changes are described in terms of the original document—they conceptually all happen at once. (If you really need to combine lists of changes where later changes refer to the document created by earlier ones, you can use the change set `compose` method.)

- Alongside the document, an editor state stores a current `selection`. 
  - Selections may consist of multiple ranges, each of which can be a cursor (empty) or cover a range between its anchor and head).
  - Overlapping ranges are automatically merged, and ranges are sorted, so that a selection's ranges property always holds a sorted, non-overlapping array of ranges.
- One of these ranges is marked as the main one. This is the one that the browser's DOM selection will reflect. The others are drawn and handled entirely by the library.
- By default a state will only accept selections with a single range. 
  - To get support for multiple selections, you have to include an extension like `drawSelection` that is able to draw them, and set an option to enable them.

- Each editor state also has a (private) reference to its configuration, which is determined by the extensions that are active for that state. During regular transactions, the configuration stays the same. 
  - But it is possible to reconfigure the state using compartments or effects that add to or replace the current configuration.

- A facet is an extension point. Different extension values can provide values for the facet. And anyone with access to the state and the facet can read its output value. 
- The idea behind facets is that most types of extension allow multiple inputs, but want to compute some coherent combined value from those. How that combining works may differ.
  - For something like tab size, you need a single output value. So that facet takes the value with the highest precedence and uses that.
  - When providing event handlers, you want the handlers as an array, sorted by precedence, so that you can try them one at a time until one of them handles the event.
  - Another common pattern is to compute the logical or of the input values (as in allowMultipleSelections) or reduce them in some other way (say, taking the maximum of the requested undo history depths).
- Facets are explicitly defined, producing a facet value. Such a value can be exported, to allow other code to provide and read it
- In a given configuration, most facets tend to be static, provided only directly as part of the configuration. 
  - But it is also possible to have facet values computed from other aspects of the state.
- Facet values are only recomputed when necessary, so you can use an object or array identity test to cheaply check whether a facet changed.

- Transactions, created with the state's `update` method, combine a number of effects (all optional):
  - It can apply document changes.
  - It can explicitly move the selection. 
  - It can have any number of annotations, which store additional metadata that describes the (entire) transaction.
  - It can have effects, which are self-contained additional effects, typically on some extension's state (such as folding code or starting an autocompletion).
  - It can influence the state's configuration, either by providing a completely new set of extensions, or by replacing specific parts of the configuration.

- To completely reset a state—for example to load a new document—it is recommended to create a new state instead of a transaction. 
  - That will make sure no unwanted state (such as undo history events) sticks around.

- The view tries to be as transparent a layer around the state as possible. 
- Unfortunately, there are some aspects of working with an editor that can't be handled purely with the data in the state.
  - When dealing with screen coordinates (to figure out where the user clicked, or to find the coordinates of a given position), you need access to the layout, and thus the browser DOM.
  - The editor takes the text direction from the surrounding document (or its own CSS style, if overridden).
  - Cursor motion can depend on layout and text direction. Thus, the view provides a number of helper methods for computing different types of motion.
  - Some state, such as focus and scroll position, isn't stored in the functional state, but left in the DOM.

- The library does not expect user code to manipulate the DOM structure it manages. When you do try that, you'll probably just see the library revert your changes right away. See the section on decorations for the proper way to affect the way the content is displayed.

- One thing to be aware of is that CodeMirror doesn't render the entire document, when that document is big. 
  - To avoid doing some work, it will, when updating, detect which part of the content is currently visible (not scrolled out of view), and only render that plus a margin around it. 
  - This is called the viewport.
- Querying coordinates for positions outside of the current viewport will not work (since they are not rendered, and thus have no layout). 
- The view does track height information (initially estimated, measured accurately when content is drawn) for the entire document, even the parts outside of the viewport.
- Long lines (when not wrapped) or chunks of folded code can still make the viewport rather huge. The editor also provides a list of visible ranges, which won't include such invisible content. This can be useful when, for example, highlighting code, where you don't want to do work for text that isn't visible anyway.

- CodeMirror's view makes a serious effort to minimize the amount of DOM reflows it causes. 
- Dispatching a transaction will generally only cause the editor to write to the DOM, without reading layout information. 
  - The reading (to check whether the viewport is still valid, whether the cursor needs to be scrolled into view, and so on) is done in a separate measure phase, scheduled using `requestAnimationFrame`. This phase will, if necessary, follow up with another write phase.
- You can schedule your own measure code using the `requestMeasure` method.

- The editor's DOM structure looks something like this:

```HTML
<div class="cm-editor [theme scope classes]">
  <div class="cm-scroller">
    <!-- 👇🏻编辑实现 -->
    <div class="cm-content" contenteditable="true">
      <div class="cm-line">Content goes here</div>
      <div class="cm-line">...</div>
    </div>
  </div>
</div>
```

- the `cm-content` element is `contenteditable`. 
  - This has a DOM mutation observer registered on it, and any changes made in there will result in the editor parsing them as document changes and redrawing the affected nodes. 
  - This container holds a line element for each line in the viewport, which in turn hold the document text (possibly decorated with styles or widgets).

- To manage editor-related styles, CodeMirror uses a `style-mod` system to inject styles from JavaScript. Styles can be registered with a facet, which will cause the view to make sure they are available.
- A theme declaration defines any number of CSS rules using style-mod notation. 

- Commands are functions with a specific signature. 
  - Their main use is key bindings, but they could also be used for things like menu items or command palettes. 
- A command function represents a user action. 
  - It takes a `view` and returns a boolean,  `false` to indicate it doesn't apply in the current situation, and `true` to indicate that it successfully executed. 
  - The effect of the command is produced imperatively, usually by dispatching a transaction.
- When multiple commands are bound to a given key, they are tried one at a time, in order of precedence, until one of them returns true.
- Commands that only act on the state, not the entire view, can use the `StateCommand` type instead, which is a subtype of `Command` that just expects its argument to have `state` and `dispatch` properties. 
  - This is mostly useful for being able to test such commands without creating a view.

- There are a number of different ways to extend CodeMirror, and picking the proper way for a given use case isn't always obvious. 
- State Fields
  - Extensions often need to store additional information in the state. The undo history needs to store undoable changes, the code folding extension needs to track what has been folded, and so on.
  - For this purpose, extensions can define additional state fields. State fields, living inside the purely functional state data structure, must store immutable values.
  - State fields are kept in sync with the rest of the state using something like a reducer. Every time the state updates, a function is called with the field's current value and the transaction, which should return the field's new value.
- in almost all cases, it is a really good idea to tie your state into the editor-wide state update cycle, because it makes it a lot easier to keep everything in sync.

- View plugins
- View plugins provide a way for extensions to run an imperative component inside the view. 
- This is useful for things like event handlers, adding and managing DOM elements, and doing things that depend on the current viewport.
- View plugins should generally not hold (non-derived) state. They work best as shallow views over the data kept in the editor state.
- When the state is reconfigured, view plugins that aren't part of the new configuration will be destroyed

- Decorating the Document
- When not told otherwise, CodeMirror will draw the document as plain text. 
- Decorations are the mechanism through which extensions can influence what the document looks like. 
- They come in four types:
  - Mark decorations add style or DOM attributes to the text in a given range.
  - Widget decorations insert a DOM element at a given position in the document.
  - Replace decorations hide part of the document or replace it with a given DOM node.
  - Line decorations can add attributes to a line's wrapping element.
- Decorations are provided through a facet. Every time the view is updated, the content of this facet is used to style the visible content.
- Decorations are kept in sets, which are again immutable data structures. 
  - Such sets can be mapped across changes (adjusting the positions of their content to compensate for the change) or rebuilt on updates, depending on the use case.

- Extension Architecture
- To create a given piece of editor functionality you often need to combine different kinds of extension: a state field to keep state, a base theme to provide styling, a view plugin to manage in- and output, some commands, maybe a facet for configuration.
- A common pattern is to export a function that returns the extension values necessary for your feature to work. 
  - Making this a function, even if it doesn't (yet) take parameters is a good idea—it makes it possible to add configuration options later, without breaking backwards compatiblity.
- Since extensions can pull in other extensions, it can be useful to consider what happens when your extension is included multiple times. 
- It is usually possible to make multiple uses of an extension just do the right thing by relying on the deduplication of identical extension values—if you make sure you create your static extension values (themes, state fields, view plugins, etc) only once, and always return the same instance from your extension constructor function, you'll only get one copy of them in the editor.
- what do you do when the different instances of the extension got different configurations?
  - Sometimes, that's just an error. But often, it is possible to define a strategy for reconciling them. Facets work well for this. You can put the configuration in a module-private facet, and have its combining function either reconcile configurations or thow an error when this is impossible. Then code that needs access to the current configuration can read that facet.
  - See the `zebra` stripes example for an illustration of this approach.
# api
- Annotations are tagged values that are used to add metadata to transactions in an extensible way. 
  - They should be used to model things that effect the entire transaction (such as its time stamp or information about its origin). 
  - For effects that happen alongside the other changes made by the transaction, state effects are more appropriate.
- State effects can be used to represent additional effects associated with a transaction. 
  - They are often useful to model changes to custom state fields, when those changes aren't implicit in document or selection changes.

- 
- 
- 

# v5
- [CodeMirror 5](https://int-heuristweb-prod.intersect.org.au/HEURIST/HEURIST_SUPPORT/external_h7/codemirror-5.61.0/)
# more
