---
title: lib-editor-slate-latest-changelog
tags: [changelog, slate-editor]
created: 2022-05-15T18:43:48.811Z
modified: 2023-02-05T19:03:12.723Z
---

# lib-editor-slate-latest-changelog

# guide
- resources
  - [changelog list](https://docs.slatejs.org/general/changelog)
# changelog

## v

## [v0.100.0__20231021](https://github.com/ianstormtaylor/slate/releases/tag/slate-react%400.100.0)

- Add `onSelectionChange` and `onValueChange` in Slate React component

## v0.90.0__20230201

- Revert to using inline styles for default editor styles

## v0.80.0__20220526

- update insertText logic when selection is not collapsed
- Revert to previous position behavior around inline voids
- Revert #4876 & #4910 to restore original decorations behavior

## [v0.76.0__20220325](https://github.com/ianstormtaylor/slate/releases/tag/slate%400.76.0)

- adds a separate `insertSoftBreak` method on the editor instance that gets called when a soft break is inserted. 
- toSlatePoint should not consider a selection within a void node if the void node isn't in the editor itself.

## [v0.67.0__20211019](https://github.com/ianstormtaylor/slate/releases/tag/slate-react%400.67.0)

- The Slate Provider's `"value"` prop is now only used as initial state for `editor.children` as was intended before. 
  - If your code relies on replacing `editor.children` you should do so by replacing it directly instead of relying on the "value" prop to do this for you.

- 0.6x版本早期大多关于修复typescript

## 0.57.0__20191218

- Overridable commands now live directly on the editor object.
  - now the core actions that can be overridden are implemented as individual functions on the editor (eg. editor.insertText) and they can be overridden just like any other function (eg. isVoid).

## [v0.54.0__20191212](https://docs.slatejs.org/general/changelog#0.54-december-12-2019)

- The `<Slate>` `onChange` handler no longer receives the `selection` argument. 
  - Previously it received `(value, selection)`, now it receives simply `(value)`. 
  - Instead, you can access any property of the editor directly (including the value as `editor.children`). 
  - The value/onChange convention is provided purely for form-related use cases that expect it. This is along with the change to how extra props are "controlled". By default they are uncontrolled, but you can pass in any of the other top-level editor properties to take control of them

- The `<Slate>` component is now pseudo-controlled. It requires a value= prop to be passed in which is controlled. 
  - However, the selection, marks, history, or any other props are not required to be controlled. They default to being uncontrolled. 
  - If your use case requires controlling these extra props you can pass them in and they will start being controlled again. 
  - This change was made to make using Slate easier, while still allowing for more complex state to be controlled by core or plugins going forward—state that users don't need to concern themselves with most of time.
- The Editor now has a `marks` property. 
  - This property represents text-level formatting that will be applied to the next character that is inserted.
  - This is a common richtext editor behavior, where pressing a Bold button with a collapsed selection turns on "bold" formatting mode, and then typing a character becomes bold. 
  - This state isn't stored in the document, and is instead stored as an extra property on the editor itself.

## 🚀 [v0.50.0__20191128](https://github.com/ianstormtaylor/slate/tags?after=slate-history%400.50.0)

- [Migrating](https://docs.slatejs.org/concepts/xx-migrating)
- Migrating from earlier versions of Slate to the 0.50.x versions is not a simple task. 
  - The entire framework was re-considered from the ground up.
- Here's an overview of the major differences in the 0.50.x version of Slate from an architectural point of view.
- The data model is now comprised of simple JSON objects. 
  - Previously, it used Immutable.js data structures. 
  - This is a huge change, and one that unlocks many other things. 
- The data model is interface-based. 
  - Previously each model was an instance of a class. 
  - Now, not only is the data plain objects, but Slate only expects that the objects implement an interface. 
  - So custom properties that used to live in node.data can now live at the top-level of the nodes.
- A lot of helper functions are exposed as a collection of helper functions on a namespace. 
  - For example, Node.get(root, path) or Range.isCollapsed(range). This ends up making code much clearer 
- The codebase now uses TypeScript. 
- The number of interfaces and commands has been reduced. 
  - Previously Selection, Annotation, and Decoration used to all be separate classes. 
  - Now they are simply objects that implement the Range interface. 
  - Previously Block and Inline were separate; 
  - now they are objects that implement the Element interface. 
  - Previously there was a Document and Value, but now the top-level Editor contains the children nodes of the document itself.
- The number of commands has been reduced too. 
  - Previously we had commands for every type of input, like insertText, insertTextAtRange, insertTextAtPath. 
  - These have been merged into a smaller set of more customizable commands, eg. insertText which can take at: Path | Range | Point.
- A new "command" concept has been introduced. 
  - (The old "commands" are now called "transforms".) 
  - Commands are triggered by calling the editor.* core functions. And they travel through a middleware-like stack, but built from composed functions. Any plugin can override the behaviors to augment an editor.
- Plugins are now plain functions that augment the Editor object they receive and return it again
  - Previously they relied on a custom middleware stack, and they were just bags of handlers that got merged onto an editor. Now we're using plain old function composition (aka wrapping) instead.
- Block-ness and inline-ness is now a runtime choice. 
  - Previously it was baked into the data model with the object: 'block' or object: 'inline' attributes. 
  - Now, it checks whether an "element" is inline or not at runtime. 
- Rendering and event-handling are no longer a plugin's concern. 
  - Previously plugins had full control over the rendering and event-handling logic in the editor. 
  - This creates a bad incentive to start putting all rendering logic in plugins
  - the new architecture has plugins focused purely on the richtext aspects, and leaves the rendering and event handling aspects to React.
- we're now using the standardized `beforeinput` event as our baseline. It is fully supported in Safari and Chrome
- The core history logic has now finally been extracted into a standalone plugin. 
- Marks have been removed from the Slate data model. 
  - Now that we have the ability to define custom properties right on the nodes themselves, you can model marks as custom properties of text nodes. 
- annotations have been removed from Slate's core. 
  - They can be fully implemented now in userland by defining custom operations and rendering annotated ranges using decorations.
  - But most cases should be using custom text node properties or decorations anyways. 

## [0.47.0__20190508](https://docs.slatejs.org/general/changelog#0.47-may-8-2019)

- Introducing `Annotation`.
  - The value.decorations property is now value.annotations.
  - similar to what used to be stored in `value.decorations`, except they also contain a unique "key" to be identified by. 
  - They can be used for things like comments, suggestions, collaborative cursors
- Introducing "iterable" model methods.

- v0.47.9__20191110

## [0.35.0__20180727](https://docs.slatejs.org/general/changelog#0.35-july-27-2018)

- `Range` now keep track of paths, in addition to keys. 
  - Previously ranges only stored their points as keys. 
  - Now both paths and keys are used, which allows you to choose which one is the most convenient or most performant for your use case. 
  - They are kept in sync by Slate under the covers.
- A new set of `*ByPath` change methods have been added. 
  - All of the changes you could previously do with a `*ByKey` change are now also supported with a *ByPath change of the same name. 
  - The path-based changes are often more performant than the key-based ones.
