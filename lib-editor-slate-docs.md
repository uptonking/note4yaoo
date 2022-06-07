---
title: lib-editor-slate-docs
tags: [docs, slate]
created: '2022-05-15T18:41:24.616Z'
modified: '2022-05-15T18:41:39.560Z'
---

# lib-editor-slate-docs

> A completely customizable framework for building rich text editors.

# guide
- resources
  - [Deep in Slate.js —— 深入 Slate.js gitbook](https://github.com/yoyoyohamapi/book-slate-editor-design/blob/master/SUMMARY.md)
    - 这本小册基于的 Slate.js 0.44.x 版本，虽然 Slate.js 现在已经渐进到了 0.50.x 版本，但其架构编辑器的方式仍然是统一的，
    - 小册的初衷也在于借 Slate.js 分析和讨论 Web 富文本编辑器的架构方式，而不是教导怎么使用 Slate.js
# overview
- slate /18.6kStar/MIT/202009/ts
  - https://github.com/ianstormtaylor/slate
  - https://docs.slatejs.org/general/changelog
  - a completely customizable framework for building rich text editors.
  - since v0.50.0(201911), slate codebase has had a complete overhaul(彻底检修)
    - The data model is now comprised of simple JSON objects.(old: Immutable.js data structures)
    - Plugins are now plain functions that augment the Editor object they receive and return it again.
    - The codebase now uses TypeScript. 

- slate-examples
  - https://www.slatejs.org/examples/richtext
  - https://www.slatejs.org/examples/hovering-toolbar
  - https://www.slatejs.org/examples/mentions

- custom formatting的示例
  - bold, italic, strikethrough, code
- custom elements的示例
  - code block
# motivation
- ## Why create Slate?
  - Before creating Slate, I tried a lot of the other rich text libraries out there—Draft.js, Prosemirror, Quill, etc.
  - What I found was that while getting simple examples to work was easy enough, once you started trying to build something like Medium, Dropbox Paper or Google Docs, you ran into deeper issues...
- The editor's "schema" was hardcoded and hard to customize. 
  - Things like bold and italic were supported out of the box, but what about comments, or embeds, or even more domain-specific needs?
- Transforming the documents programmatically was very convoluted(复杂的，晦涩的). 
  - Writing as a user may have worked, but making programmatic changes, which is critical for building advanced behaviors, was needlessly complex.
- Serializing to HTML, Markdown, etc. seemed like an afterthought. 
  - Simple things like transforming a document to HTML or Markdown involved writing lots of boilerplate code, for what seemed like very common use cases.
- Re-inventing the view layer seemed inefficient and limiting. 
  - Most editors rolled their own views, instead of using existing technologies like React, so you had to learn a whole new system with new "gotchas".
- Collaborative editing wasn't designed for in advance. 
  - Often the editor's internal representation of data made it impossible to use for a realtime, collaborative editing use case without basically rewriting the editor.
- The repositories were monolithic, not small and reusable. 
  - The code bases for many of the editors often didn't expose the internal tooling that could have been re-used by developers, leading to having to reinvent the wheel.
- Building complex, nested documents was impossible. 
  - Many editors were designed around simplistic "flat" documents, making things like tables, embeds and captions difficult to reason about and sometimes impossible.

- ## Slate Principles
- First-class plugins. 
  - The most important part of Slate is that plugins are first-class entities. 
  - That means you can completely customize the editing experience, to build complex editors like Medium's or Dropbox's, without having to fight against the library's assumptions.
- Schema-less core. 
  - Slate's core logic assumes very little about the schema of the data you'll be editing
- Nested document model. 
  - The document model used for Slate is a nested, recursive tree, just like the DOM itself. 
  - This means that creating complex components like tables or nested block quotes are possible for advanced use cases.
- Parallel to the DOM. 
  - Slate's data model is based on the DOM—the document is a nested tree, it uses selections and ranges, and it exposes all the standard event handlers. 
  - This means that advanced behaviors like tables or nested block quotes are possible.
- Intuitive commands. 
  - Slate documents are edited using "commands"
  - This greatly increases your ability to reason about your code.
- Collaboration-ready data model. 
  - The data model Slate uses—specifically how operations are applied to the document—has been designed to allow for collaborative editing to be layered on top
- Clear "core" boundaries. 
  - With a plugin-first architecture, and a schema-less core, it becomes a lot clearer where the boundary is between "core" and "custom", which means that the core experience doesn't get bogged down in edge cases.
# usage
- We want the `editor` to be stable across renders, so we use the `useState` hook without a setter
  - const [editor] = useState(() => withReact(createEditor()))

- `<Slate>` context provider.
  - The provider component keeps track of your Slate editor, its plugins, its value, its selection, and any changes that occur. 
  - It must be rendered above any `<Editable>` components. 
  - But it can also provide the editor state to other components like toolbars, menus, etc. using the `useSlate` hook.
  - You can think of the `<Slate>` component as providing a context to every component underneath it.
    - Slate Provider's "value" prop is only used as initial state for `editor.children`. 
    - If your code relies on replacing `editor.children`, you should do so by replacing it directly instead of relying on the "value" prop to do this for you. 
  - By having a shared context, those other components can execute commands, query the editor's state, etc.

- `<Editable>` component acts like `contenteditable`.
  - Anywhere you render it will render an editable richtext document for the nearest editor context.

- What makes Slate great is how easy it is to customize. 
  - Just like other React components you're used to, Slate allows you to pass in handlers that are triggered on certain events.
- For the purposes of our example, let's implement turning all ampersand, &, keystrokes into the word and upon being typed.

- Slate lets you define any type of custom blocks you want, like block quotes, code blocks, list items, etc.
  - To make that happen, we need to define a "renderer" for `code` element nodes.
  - Slate passes attributes that should be rendered on the top-most element of your blocks, so that you don't have to build them up yourself. You must mix the attributes into your component.
  - Slate will automatically render all of the children of a block for you, and then pass them to you just like any other React component would, via props.children.
  - You must render the children as the lowest leaf in your component.

- we'll show you how to add custom formatting options, like bold, italic, code or strikethrough.
  - we'll edit the onKeyDown handler to make it so that when you press control-B, it will add a bold format to the currently selected text
  - For every format you add, Slate will break up the text content into "leaves", and you need to tell Slate how to read it, just like for elements. 

- Up until now, everything we've learned has been about how to write one-off logic for your specific Slate editor. 
  - In the previous guides we've written some useful code to handle formatting code blocks and bold marks. 
  - And we've hooked up the onKeyDown handler to invoke that code. 
  - But we've always done it using the built-in Editor helpers directly, instead of using "commands".
  - Slate lets you augment the built-in editor object to handle your own custom rich text commands.
  - And you can even use pre-packaged "plugins" which add a given set of functionality.

- if you want to save your content as plain text instead of JSON, we can write some logic to serialize and deserialize plain text values
  - Note that even though you can serialize your content however you like, there are tradeoffs. 
  - The serialization process has a cost itself, and certain formats may be harder to work with than others. 

- **If you want to update the editor's content in response to events from outside of slate**, you need to change the `children` property directly. 
  - The simplest way is to replace the value of editor.children `editor.children = newValue` and trigger a re-rendering (e.g. by calling `editor.onChange()` in the example above). Alternatively, you can use slate's internal operations to transform the value
  - Alternatively, you can use slate's internal operations to transform the value
# concepts
- Slate works with pure JSON objects. 
  - All it requires is that those JSON objects conform to certain interfaces
  - But any other custom properties are also allowed, and completely up to you. 
  - This lets you tailor your data to your specific domain and use case, adding whatever formatting logic you'd like, without Slate getting in the way.
- This interface-based approach separates Slate from most other rich text editors which require you to work with their hand-rolled "model" classes and makes it much easier to reason about. 
  - It also means that it avoids startup time penalties related to "initializing" the data model.

- All of the behaviors, content and state of a Slate editor is rolled up into a single, top-level `Editor` object.

```typescript
interface Editor {
  // Current editor state
  /** contains the document tree of nodes that make up the editor's content.*/
  children: Node[]
  /** contains the user's current selection, if any */
  selection: Range | null
  /** contains all of the operations that have been applied since the last "change" was flushed */
  operations: Operation[]
  /** stores formatting to be applied when the editor inserts text.*/
  marks: Omit<Text, 'text'> | null
  // Schema-specific node behaviors.
  isInline: (element: Element) => boolean
  isVoid: (element: Element) => boolean
  normalizeNode: (entry: NodeEntry) => void
  onChange: () => void
  // Overrideable core actions.
  addMark: (key: string, value: any) => void
  apply: (operation: Operation) => void
  deleteBackward: (unit: 'character' | 'word' | 'line' | 'block') => void
  deleteForward: (unit: 'character' | 'word' | 'line' | 'block') => void
  deleteFragment: () => void
  insertBreak: () => void
  insertSoftBreak: () => void
  insertFragment: (fragment: Node[]) => void
  insertNode: (node: Node) => void
  insertText: (text: string) => void
  removeMark: (key: string) => void
}

```

- The most important types are the `Node` objects:
  - A root-level `Editor` node that contains the entire document's content.
  - Container `Element` nodes that have semantic meaning in your domain.
  - And leaf-level `Text` nodes which contain the document's text.
  - These three interfaces are combined to form a tree—just like the DOM.
- Mirroring the DOM as much as possible is one of Slate's principles. 
- A Slate document is a nested and recursive structure. 
  - In a document, elements can have children nodes—all of which may have children nodes without limit. 
  - The nested and recursive structure enables you to model simple behaviors such as user mentions and hashtags or complex behaviors such as tables and figures with captions.

- interface Editor { children: Node[] }
  - The top-level node in a Slate document is the Editor itself. 
  - It encapsulates all of the rich text "content" of the document.

- interface Element { children: Node[] }
  - Elements are the nodes that are custom to your domain. 
  - You can define custom elements for any type of content you want.
  - It's important to note that you can use any custom properties you want. 
  - The type property in that example isn't something Slate knows or cares about. 
  - All that matters is that elements always have a children property.
- All elements default to being "block" elements. 
  - They each appear separated by vertical space, and they never run into each other.
- But in certain cases, like for links, you might want to make them "inline" flowing elements instead. That way they live at the same level as text nodes, and flow.
  - You can define which nodes are treated as inline nodes by overriding the `editor.isInline` function. (By default it always returns `false`.) 
  - Note that inline nodes cannot be the first or last child of a parent block, nor can they be next to another inline node in the children array. 
  - Slate will automatically space these with `{ text: '' }` children by default with `normalizeNode`.
- Elements can either contain block elements or inline elements intermingled with text nodes as children.
  - But elements cannot contain some children that are blocks and some that are inlined.
- Elements default to being non-void, meaning that their children are fully editable as text. 
  - But in some cases, like for images, you want to ensure that Slate doesn't treat their content as editable text, but instead as a black box.
  - This is a concept borrowed from the HTML spec
  - You can define which elements are treated as void by overriding the `editor.isVoid` function. (By default it always returns false.)

- interface Text { text: string }
  - Text nodes are the lowest-level nodes in the tree, containing the text content of the document, along with any formatting. 
  - Text nodes too can contain any custom properties you want, and that's how you implement custom formatting like bold, italic, code, etc. 
  - These custom properties are sometimes called marks.

- Locations are how you refer to specific places in the document when inserting, deleting, or doing anything else with a Slate editor. 

- type Path = number[]
  - Paths are the lowest-level way to refer to a location. 
  - Each path is a simple array of numbers that refers to a node in the document tree by its indexes in each of its ancestor nodes down the tree
  - The Editor itself has a path of []
  - For example, to select the whole contents of the editor, call Transforms.select(editor, [])

- interface Point { path: Path  offset: number }
  - Points are slightly more specific than paths, and contain an offset into a specific text node
  - It can be helpful to think of points as being "cursors" (or "carets") of a selection.
  - Points always refer to text nodes! Since they are the only ones with strings that can have cursors.

- interface Range { anchor: Point  focus: Point }
  - Ranges are a way to refer not just to a single point in the document, but to a wider span of content between two points. 
  - anchor  returns the Node in which the selection begins.
  - focus  returns the Node in which the selection ends.
  - the ordering of an anchor and selection point depend on whether the range is backwards or forwards.
  - One important distinction is that the anchor and focus points of ranges always reference the leaf-level text nodes in a document and never reference elements. 
    - This behavior is different than the DOM, but it simplifies working with ranges as there are fewer edge cases for you to handle.

- selection: { anchor: { path: [0, 0], offset: 0 }, focus: { path: [0, 0], offset: 15 }, }
  - The selection is a special range that is a property of the top-level Editor
  - Slate doesn't allow for multiple ranges inside a single selection, which makes things a lot easier to work with.

- Slate's data structure is immutable, so you can't modify or delete nodes directly. 
  - Instead, Slate comes with a collection of "transform" functions that let you change your editor's value.
- Slate's transform functions are designed to be very flexible, to make it possible to represent all kinds of changes you might need to make to your editor. 
  - Selection-related transforms are some of the simpler ones.
  - For example, it's common to need to move a cursor forwards or backwards by varying distances—by character, by word, by line.
- Text transforms act on the text content of the editor. 
- Node transforms act on the individual element and text nodes that make up the editor's value. 
- Many transforms act on a specific location in the document. 
  - By default, they will use the user's current selection. 
  - But this can be overridden with the `at` option.
- The `at` option is very versatile, and can be used to implement more complex transforms very easily. 
  - Since it is a Location it can always be either a Path, Point, or Range. 
  - And each of those types of locations will result in slightly different transformations.
  - For example, in the case of inserting text, if you specify a Range location, the range will first be deleted, collapsing to a single point where your text is then inserted.
- These location-based behaviors work for all the transforms that take an `at` option. 
  - It can be hard to wrap your head around at first, but it makes the API very powerful and capable of expressing many subtly different transforms.

- Many of the node-based transforms take a match function option, which restricts the transform to only apply to nodes for which the function returns true
  - When performing transforms, if you're ever looping over nodes and transforming them one at a time, consider seeing if match can solve your use case, and offload the complexity of managing loops to Slate instead.

- Operations are the granular, low-level actions that occur while invoking transforms. 
  - A single transform could result in many low-level operations being applied to the editor.
  - Slate's core defines all of the possible operations that can occur on a richtext document
- Under the covers Slate converts complex transforms into the low-level operations and applies them to the editor automatically. 
  - So you rarely have to think about operations unless you're implementing collaborative editing.
  - Slate's editing behaviors being defined as operations is what makes things like collaborative editing possible, because each change is easily define-able, apply-able, compose-able and even undo-able!

- While editing richtext content, your users will be doing things like inserting text, deleting text, splitting paragraphs, adding formatting, etc. 
  - Under the cover these edits are expressed using transforms and operations. 
  - But at a high level we talk about them as "commands".
- Commands are the high-level actions that represent a specific intent of the user. 
  - They are represented as helper functions on the Editor interface. 
  - A handful of helpers are included in core for common richtext behaviors
- Commands always describe an action to be taken as if the user was performing the action. 
  - For that reason, they never need to define a location to perform the command, because they always act on the user's current selection.
- Under the covers, Slate takes care of converting each command into a set of low-level "operations" that are applied to produce a new value. 
  - This is what makes collaborative editing implementations possible. 
  - When writing your own commands, you'll often make use of the Transforms helpers that ship with Slate.
- you can override any of the behaviors of an editor by overriding its function properties.
  - editor.isInline = element => { return element.type === 'link' ? true : isInline(element) }
- Whenever you override behaviors, be sure to call the existing functions as a fallback mechanism for the default behavior. 
  - Unless you really do want to completely remove the default behaviors
- The `Editor` interface, like all Slate interfaces, exposes helper functions that are useful when implementing certain behaviors. 
  - There are also many iterator-based helpers

- A plugin is simply a function that takes an `Editor` object and returns it after it has augmented it in some way.

- Slate doesn't re-invent its own view layer that you have to learn. It tries to keep everything as React-y as possible.
  - Slate gives you control over the rendering behavior of your custom nodes and properties in your richtext domain.
  - You can define these behaviors by passing "render props" to the top-level `<Editable>` component.
  - For example if you wanted to render custom element components, you'd pass in the `renderElement` prop
- Be sure to mix in props.attributes and render props.children in your custom components! 
  - The attributes must be added to the top-level DOM element inside the component, as they are required for Slate's DOM helper functions to work. 
  - And the children are the actual text content of your document which Slate manages for you automatically.

- When text-level formatting is rendered, the characters are grouped into "leaves" of text that each contain the same formatting applied to them.
  - To customize the rendering of each leaf, you use a custom renderLeaf prop
- One disadvantage of text-level formatting is that you cannot guarantee that any given format is "contiguous"(相邻的)—meaning that it stays as a single leaf.
  - 注意处理无效元素 `<em>t<strong>e</em>x</strong>t` 文本
- as long as you use text-level formatting and element-level formatting for their intended purposes
  - Text properties are for non-contiguous, character-level formatting.
  - Element properties are for contiguous, semantic elements in the document.

- Decorations are another type of text-level formatting. 
  - They are similar to regular old custom properties, except each one applies to a `Range` of the document instead of being associated with a given text node.
  - However, **decorations are computed at render-time based on the content itself**. 
  - This is helpful for dynamic formatting like syntax highlighting or search keywords, where changes to the content (or some external data) has the potential to change the formatting.
  - Decorations are different from Marks in that they are not stored on editor state.

- In addition to controlling the rendering of nodes inside Slate, you can also retrieve the current editor context from inside other components using the `useSlate` hook.
  - That way other components can execute commands, query the editor state, or anything else.
  - A common use case for this is rendering a toolbar with formatting buttons that are highlighted based on the current selection

- Slate's data model has been built with serialization in mind. 
  - Specifically, its text nodes are defined in a way that makes them easier to read at a glance, but also easy to serialize to common formats like HTML and Markdown.
  - And, because Slate uses plain JSON for its data, you can write serialization logic very easily.

- deserializing
  - This is when you have some arbitrary input and want to convert it into a Slate-compatible JSON structure. 
  - Slate has a built-in helper for this: the slate-hyperscript package.
  - slate-hyperscript isn't only for JSX. It's just a way to build trees of Slate content. Which happens to be exactly what you want to do when you're deserializing something like HTML.

- "Normalizing" is how you can ensure that your editor's content is always of a certain shape. 
  - It's similar to "validating", except instead of just determining whether the content is valid or invalid, its job is to fix the content to make it valid again.
  - Slate editors come with a few built-in constraints out of the box.
  - These constraints are there to make working with content much more predictable than standard contenteditable. 
  - All of the built-in logic in Slate depends on these constraints

- Built-in Constraints
  - These default constraints are all mandated because they make working with Slate documents much more predictable.
- All Element nodes must contain at least one Text descendant — even Void Elements.
  - If an element node does not contain any children, an empty text node will be added as its only child. 
  - This constraint exists to ensure that the selection's anchor and focus points (which rely on referencing text nodes) can always be placed inside any node. 
  - With this, empty elements (or void elements) wouldn't be selectable.
- Two adjacent texts with the same custom properties will be merged. 
  - This exists to prevent the text nodes from only ever expanding in count in the document, since both adding and removing formatting results in splitting text nodes.
- Block nodes can only contain other blocks, or inline and text nodes. 
  - **The type of children allowed is determined by the first child**, and any other non-conforming children are removed. 
  - This ensures that common richtext behaviors like "splitting a block in two" function consistently.
- Inline nodes cannot be the first or last child of a parent block, nor can it be next to another inline node in the children array. 
  - If this is the case, an empty text node will be added to correct this to be in compliance with the constraint.
- The top-level editor node can only contain block nodes. 
  - If any of the top-level children are inline or text nodes they will be removed. 
  - This ensures that there are always block nodes in the editor so that behaviors like "splitting a block in two" work as expected.
- Nodes must be JSON-serializable. 
  - For example, avoid using undefined in your data model. 
  - This ensures that operations are also JSON-serializable, a property which is assumed by collaboration libraries.
- Property values must not be `null`. 
  - Instead, you should use an optional property, e.g. `foo?: string` instead of `foo: string | null`. 
  - This limitation is due to `null` being used in operations to represent the absence of a property.

- you can also add your own constraints on top of the built-in ones that are specific to your domain.
  - extend the `normalizeNode` function on the editor. 
  - The `normalizeNode` function gets called every time an operation is applied that inserts or updates a node (or its descendants), giving you the opportunity to ensure that the changes didn't leave it in an invalid state, and correcting the node if so.
- One thing to understand about `normalizeNode` constraints is that they are multi-pass.
  - When you do call `Editor.unwrapNodes`, you're actually changing the content of the node that is currently being normalized. 
  - So even though you're ending the current normalization pass, by making a change to the node you're kicking off a new normalization pass. 
  - This results in a sort of recursive normalizing.
- This multi-pass characteristic makes it much easier to write normalizations, because you only ever have to worry about fixing a single issue at once, and not fixing every possible issue that could be putting a node in an invalid state.
  - anytime `normalizeNode` is called and you spot an invalid state, you can fix that single invalid state and trust that `normalizeNode` will be called again until the node becomes valid.
- Before any of the other normalizations can execute, Slate iterates through all Element nodes and makes sure they have at least one child. 
  - If it does not, an empty Text descendant is created.
- One pitfall to avoid is creating an infinite normalization loop.
  - This can happen if you check for a specific invalid structure, but then don't actually fix that structure with the change you make to the node.
- Sequences of Transforms may need to be wrapped in Editor.withoutNormalizing if the node tree should not be normalized between Transforms.
  - This is frequently the case when you unwrapNodes followed by wrapNodes. 
  - For example, you might write a function to change the type of a block 

- You must define CustomTypes, annotate useState, and annotate the editor's initial state when using TypeScript or Slate will display typing errors.
- While you can define types directly in the CustomTypes interface, best practice is to define and export each type separately so that you can reference individual types like a ParagraphElement.

- At the moment, Slate supports types for a single document model at a time. For example, it cannot support two different Rich Text Editor with different document schemas.
  - One workaround for supporting multiple document models is to create each editor in a separate package and then import them. This hasn't been tested but should work.
