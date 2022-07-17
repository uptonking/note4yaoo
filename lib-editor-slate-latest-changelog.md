---
title: lib-editor-slate-latest-changelog
tags: [changelog, slate]
created: 2022-05-15T18:43:48.811Z
modified: 2022-05-15T18:43:59.130Z
---

# lib-editor-slate-latest-changelog

# guide
- resources
  - [changelog list](https://docs.slatejs.org/general/changelog)
# changelog

## [v0.50.0__20191128](https://github.com/ianstormtaylor/slate/tags?after=slate-history%400.50.0)

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

## v0.47.9__20191110
