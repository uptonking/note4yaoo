---
title: lib-editor-prosemirror-issues-stars
tags: [editor, issues, prosemirror]
created: 2021-06-16T14:13:01.159Z
modified: 2021-06-16T14:13:27.162Z
---

# lib-editor-prosemirror-issues-stars

# issues-not-yet
- plugin props vs editorView props
  - editorView props多两个参数
    - ~~state~~, dispatchTransaction
  - plugin props
    - Props that are functions will be bound to have the plugin instance as their `this` binding.

- plugin state vs editor state
- ？？？ update

- [editable islands](https://github.com/ProseMirror/prosemirror/issues/745)
  - I think I am going to consider this kind of DOM structure (editable islands) unsupported. 
  - Even if you can sort of make it work with kludges, I expect it to break in all kinds of interesting ways in corner cases. 
  - Usually, the structure of the node view can easily be adjusted to put the uneditable content in a node that's not a parent of the editable content, 
  - and in cases where that is really impossible, I recommend nesting a separate ProseMirror instance for the content and broadcasting the steps to the parent document (as in the footnote demo).
- [Replicating Typora’s Inline/Display Math Editing](https://discuss.prosemirror.net/t/replicating-typoras-inline-display-math-editing/2906)
  - https://codesandbox.io/s/prosemirror-katex-toggle-y25u4
  - 能切换渲染和编辑状态
- 如何实现不可编辑
  - filter transform actions, reset to old state
  - custom NodeView
  - nested editor like footnote
# issues-good
- ## 

- ## 

- ## 

- ## 

- ## The content of non-editable node is still editable
- https://discuss.prosemirror.net/t/the-content-of-non-editable-node-is-still-editable/2154
  - contenteditable is set to false.
  - However, when you select part of the text in a label by mouse and hit delete key, this part of text is removed.

```JS
label: {
  content: 'text*',
  defining: true,
  atom: true,
  selectable: false,
  parseDOM: [{ tag: 'label' }],
  toDOM() { return ['label', { contenteditable: false }, 0] }
}
```

- You could make the label text an attribute, rather than content.
  - That would prevent ProseMirror from trying to manage it.
  - But when you select across a node and press delete, the selected range is going to be deleted—whether individual nodes in the range are editable isn’t relevant there. 
  - The only way to prevent that is to filter transactions.
  - simply filter out transactions that delete such a node (though then the delete won’t have any effect at all).

- ## ProseMirror and Uneditable content in the document
- https://discuss.prosemirror.net/t/prosemirror-and-uneditable-content-in-the-document/1916
  - I'm trying to build a text editor that has fixed input structures for contextual sections
  - I tried “contenteditable=false” attribute with unconvincing results.
  - Second, I tried doing a plugin and Filter transaction: I could potentially filter transactions that try to delete the node, but many operations like selecting big chunks give some complex transaction data to filter.
  - Third approach would be to use css pseudo selectors and make the tags and titles outside the document model, or use decorators, but ultimately It’s unconvincingly complicated to do it that way
- I think a more promising approach would be to **have the schema just express the editable parts of the document**, using node types and attributes for the fixed parts (which seem to follow from the document structure), 
  - and then rendering them as part of the wrapper nodes for those node types (i.e. an `item` node with an attribute `type` that holds the strings like `"HARDDRIVE"` , which renders to something like `["div", {class: "item"}, ["div", {contenteditable: false, class: "itemtype", "HARDDRIVE"], ["div", 0]]` .

- ## Scan the document to find links in paragraphs and mark them
- https://discuss.prosemirror.net/t/scan-the-document-to-find-links-in-paragraphs-and-mark-them/2764
- how can I scan a document to find unmarked URLs in nodes.
- two ways of tackling the problem:
  - Going through the document tree myself and scanning the `textContent` value of Text nodes to find URLs and then splitting them up. This would be my last resort as I believe there’s probably a better way of achieving this through prosemirror transactions or the transform package
  - Listen for spaces and check if the last word is URL. If so, mark it as a link. It’s a little different from the actual request but it achieves a similar result and if that’s easier to do I would go this route. Similar behaviour can be found on Bitbucket that uses prosemirror

- To do this for an entire document, you could call `doc.descendants`, and for every text node that’s not already a link, scan for URLs and build up a transaction with `addMark` changes whenever you find any.
  - You could also express the update-on-space behavior as an input rule, but that’s a bit trickier, since it’s not a plain text replacement, and writing such rules that create their own transaction requires some non-obvious code. 
  - And this won’t catch pasted or dropped URLs, or those that don’t have a space typed after them (because they are inserted before an existing space, at the end of a paragraph, etc), so that’s probably not the best way to do this.

- ## I want to put a Handsontable widget in prosemirror, can you give me a hint about the schema and how?
- https://discuss.prosemirror.net/t/handsontable-widget/3872
- There’s roughly two approaches here. Both would involve a node view that renders your table nodes using Handsontable.
  - You can **model the whole table in your ProseMirror schema**, and carefully map changes in the table control to the proper ProseMirror steps (and vice versa, sync the table when its ProseMirror representation changes). This would make it possible to do collaborative editing inside the table.
  - You can treat the table as an opaque blob, and **either store it elsewhere or put a representation of its content in a node attribute**. Syncing would be all-or-nothing, which may require some additional logic to keep the selection inside the table intact.

- ## ProseMirror + Math at Desmos
- https://discuss.prosemirror.net/t/prosemirror-math-at-desmos/707
  - https://www.desmos.com/calculator
  - 可直接输入 `y = sin(x)` 查看效果
  - To move from the math node to prosemirror, we hook into `MathQuill` handlers and trigger a selection transaction and a `view.focus` . 
  - To go the other direction, we need to know whether we are entering the node from the left or the right. 
  - **In each math node, we listen for state selection changes (via a plugin)**, and remember whether on the last transaction the cursor was ahead of the node or behind. 
  - Then we use that info in the `selectNode` callback.
- Very nice! The crossing of the border between the formula and the other text feels entirely natural.
- I’m curious about your final design choices for the Desmos node. Did you end up converting it to a leaf node, and run into issues with cursor boundaries? 
  - We ended up making it a non-leaf node with `text*` content. 
  - It has a custom `NodeView` , which is controlled by MathQuill.
  - Transitioning the cursor was tricky. We ended up having to **monitor every transaction on the PM view**, and monitoring whether the cursor was before or after a given MathQuill node. Then, when focus entered the MathQuill node we knew whether to place the (internal, MathQuill) cursor at the beginning or the end of the content. From PM’s point of view, the whole node is selected the entire time we are editing the node.

- ## Replicating Typora’s Inline/Display Math Editing
- https://discuss.prosemirror.net/t/replicating-typoras-inline-display-math-editing/2906
  - https://codesandbox.io/s/prosemirror-katex-toggle-y25u4
  - A: Show math as LaTeX code while the cursor is inside the math node. As soon as the cursor leaves the node, render using KaTeX
  - B: Changing the cursor position by clicking/arrow keys should seamlessly transition between these two modes.
  - it seems like NodeViews are the right tool to use. I have tried two approaches
- Attempt #1: Using contentDOM
  - Set a contentDOM in the NodeView, so that ProseMirror is responsible for managing the appearance/editing of the NodeView
  - This successfully achieves Property B (cursor movement with arrow keys behaves as expected), but I cannot get Property A to work (toggling katex/code views).
  - The reason seems to be that NodeViews with a `contentDOM` have no way of knowing when the editing cursor has left the NodeView. (they only receive `setSelection` events, not selectNode and deselectNode).
- Attempt #2: Without contentDOM
  - Without contentDOM, the NodeView is responsible for its own rendering/editing, as in the footnotes example
  - this approach succeeds at Property A (toggle math editor), but unfortunately I am struggling to implement Property B, as the cursor is always set to the first position in the NodeView
- Attempt #3: Plugin with arrowHandler
  - I have also tried adapting the arrowHandler from the CodeMirror example 4 to detect from which side the cursor enters / leaves the NodeView. However, I’m not sure how to pass this information along to the NodeView. 
- This was an issue that I ran into when developing the math+text feature for Desmos. 
  - we do not use contentDom in our implementation, but use MathQuill for WYSIWYG latex editing
  - The solution for us was to listen to PM transactions using the `EditorView.dispatchTransaction` property. 
  - On every transaction, we look at the new selection in the EditorState, and save a piece of state on each NodeView, telling it whether the current selection is before or after the NodeView.
  - Then, when `selectNode` is triggered, we know which direction we approached the node from.
- The best I could come up with was below, where I maintain my own list of NodeViews that I create.
  - However, passing around these closures feels dirty to me
  - This method also updates every NodeView in the document every time the selection changes, which may cause performance issues if there are hundreds or thousands of math blocks. 
  - However, we can probably avoid calling updateCursorPos() on each one by e.g. keeping them sorted by position and calling it only on the ones we know have changed after each transaction.
- The reason seems to be that NodeViews with a `contentDOM` have no way of knowing when the editing cursor has left the NodeView.
  - They don’t, but they do know which node decorations are active on their node. So you could have a plugin that maintains a “the cursor is in this math node” **decoration**, and respond to that in the node view.
- ProseMirror relies on native browser cursor motion in most cases. Setting the math block to `contenteditable=false` might help a bit, though I’m not sure.

- ## ContentEditable=false with NodeViews causing weird selection behavior
- https://github.com/ProseMirror/prosemirror/issues/553
- When you create a custom node view without a `contentDOM` property, you're declaring that that node isn't edited in the regular `contentEditable` way, so having its `contentEditable` attribute set to `false` is intentional.
  - Having a cursor in non-editable content is not supported (and probably not a good idea in general).
- That is pretty much what happens here -- the non-editable node is a block node, so if you can't put the cursor inside it, the cursor will skip it. That's how `contentEditable` deals with uneditable block nodes, and I think it is appropriate.
- Selecting the whole element when you arrow onto it is definitely doable with a plugin. 
  - This is the default behavior for leaf nodes, but since yours has content, that logic doesn't apply to it. 
  - It might be worthwhile to have another flag, `directlySelectable` or so, for cases like this. 
  - If you, as a test, remove the `nearestDesc.node.isLeaf` test from the `readFromDOM` method in `prosemirror-view/dist/selection.js` , is the resulting behavior what you want?
- I've made a bunch of changes (not released yet) which allow you to set an `atom` property on a node spec, which makes the node count as an atom (which leaf nodes do by default), and changed the selection logic over to using that property, rather than `isLeaf` . With that feature, you should be able to simply mark nodes that will render as uneditable as atoms, and have them be selectable with the default selection logic.

- ## Invalid position when calling coordsAtPos()
- https://discuss.prosemirror.net/t/invalid-position-when-calling-coordsatpos/628
- When you (or the default `dispatchTransaction` method) calls updateState, the view is updated synchronously, except when `if (this.view.inDOMChange) {}`

- ## NodeView reconstruction
- https://github.com/ProseMirror/prosemirror/issues/851
  - I use this example nodeview
  - https://codesandbox.io/s/3y75x47jxp
  - https://codesandbox.io/s/pm-nodeview-tender-frost-3ewu8?file=/src/index.js
- Seems to work now, we didn't notice the change because of another performance issues caused by prosemirror-dev-tools. It slows down the dispatch. NodeView updating and deleting seems to work fine now

- ## What’s the best way to do an editable caption inside an element (like an image or figure) in terms of the schema and dom structure?
- https://discuss.prosemirror.net/t/figure-and-editable-caption/462
- https://glitch.com/edit/#!/pet-figcaption

- ## what difference between the plugin view and nodeViews and schema and decoration?
- https://discuss.prosemirror.net/t/what-can-plugin-view-do-or-what-should-it-be-used-for/3517
- `NodeView` is used to control how a specific node is rendered (like a codeblock) but is within the editorview and semi-managed by ProseMirror
  - There are a limit set of hooks like `update` , `destroy` to control the `NodeView` similar to that of a `PluginView` (but more scoped/granular); 
  - they’re only called a change affects a node, not when a change affects the editor view.
- We tend to think about the “view” section in the same way we think about a “useEffect” hook in React. The update function can be treated like the “deps” array in useEffect and then you can use destroy to do a final clean up. It’s a really great spot to react to state changes and then perform side effects. 
  - Manipulating the dom outside of view.dom
  - Setting up global listeners and observers (like custom selectionchanges, window resizes, etc.)
  - Data fetching
  - Performing hacky workarounds to smooth over OS issues (not ideal but it’s still another tool for some stuff)
  - Notifying other parts of your application when something changes or if you have to save content (e.g. like executing a callback when the content of the Prosemirror document changes)
  - I almost think “view” should just be called “effects”

- ## [How can I communicate from a plugin to a custom nodeView?](https://discuss.prosemirror.net/t/how-can-i-communicate-from-a-plugin-to-a-custom-nodeview/952)
  - when the node attributes of the custom nodeView change and therefore the underlying doc changes, I just replace the node and all works as expected.
  - But now I would like to communicate to the nodeView, without actually changing the node. So I tried to set from my plugin a node decoration on that nodeview (putting my payload into the spec argument). 
  - Unfortunately at my custom nodeView, the `update` method (where I expect to get access to the payload in the decoration spec object) never gets called.
- **Is this the recommended way to communicate from a plugin to a NodeView**?
  - I have a similar situation where a plugin gets external data that various NodeViews use. 
  - I need those NodeViews to update (re-render) themselves when that external data changes. 
  - So I really just need a way to tell prosemirror to re-render the NodeViews.
  - From this thread it seems possible to decorate the NodeViews and then update the decorations when the external data changes. 
  - The decoration change will then trigger prosemirror to re-render the NodeViews. 
  - It seems like a round about way to force a re-render but if its the best way then I’ll do it
  - Yes. it's recommended

- ## [How can i insert a react component as a node](https://discuss.prosemirror.net/t/how-can-i-insert-a-react-component-as-a-node/2455)
- we eventually decided to go the route of using portals as well. 
  - In our implementation, we had to re-register the portals in the NodeView’s update function in order for the portals to re-render given a change to the NodeView’s underlying node’s attributes.
- Is using portals like that actually performant?
  - We haven’t actually rigorously tested our implementation on a long doc with a ton of node views, but just thinking through it, it’s performant insofar as prosemirror doesn’t unexpectedly destroy/recreate your NodeViews. 
  - We did have to pass in a custom ignoreMutations function to prevent this, but otherwise the rendering logic is akin to react rendering children into a react tree.
- what’s the reason behind not doing the NodeViews it in plain JS? Is it because they need to interact with the rest of the app which is React (Context and stuff like that)?
  - Yep, I’d say being able to share contexts with the rest of the application is the main benefit to having the node view components be rendered within the same react tree.
- Unfortunately I can’t share our version of the code, 
  - but I’d follow pretty much what @johnkueh has implemented and then make any necessary tweaks.
  - The main addition we made in order for the component to be properly updated when the node view’s underlying node updates was a way to update the node view context from the NodeView’s `update` method.
  - Edit: Just realized I mentioned recreating the portal in the update method in my old comment. That actually isn’t necessary. Like I mentioned above, you just need some way to update the node view context that your providing to the node view component. I’d recommend looking into something like storing the node view context in a `useState` hook and then calling the state update function from the NodeView `update` function.

- ## prosemirror: react integration

- ### [Using with React](https://discuss.prosemirror.net/t/using-with-react/904)
- The issue with React-based NodeViews isn’t that it’s undoable, it is just that the interfacing & gluing between the NodeViews, Schema and Plugins (with the event dispatching and portals) is quite difficult to make.
  - So immediately if you want to create a plugin system on top of that implementation, you’ll have to start thinking how to join all the parts (normal plugins + schema + nodeviews (as the React components) + possible toolbar buttons & actions) together. 
  - What I got stuck before I got too busy doing other things was the **implementing of the event-flow from the actions/key-press plugins to the plugin state, which would then notify the React components through an event-dispatcher**. 
  - There’s an example in the Atlassian repo if you want to a crack at it.
- @johnkueh you’ve done quite a decent starter for the React + PM combo. Very impressive. You got the whole plumbing into a simple React hook
  - If you want to hear my opinion/feedback, I would maybe separate some stuff from the `ReactNodeView` as it seems a bit cluttered(杂乱的). 
  - Also I’m curious about how you use the `ReactDOM.createPortal`, will the React components be unmounted correctly when they are destroyed? There’s no `unmountComponentAtNode()` call so I’m not sure does it cause a memory leak.
  - **How in Atlassian’s editor they made it was using a separate `portalProvider` that was passed down to the `ReactNodeView`**. 
  - if you want to have the React NodeViews be notified of the plugin state changes you need some sort of event-dispatcher.
  - I was in the middle of devising(设计，想出) a react-redux type of `addStateToProps` HOC, but I was too busy with other stuff. 
  - If you have time and interest, you could try that or even create it as a hook. That would be amazing! Eg `usePluginState(PLUGIN_KEY)`.
  - Also does using React’s context add some benefit compared to just passing the NodeView’s attributes down as props to the component? 
  - Atlassian’s editor, at some point at least, used extensively `context` which made the resulting React component tree become like 100 components deep, it seemed like a design mistake.
- That’s a good question about the portals. 
  - I guess with portals the React nodes will remain in one same React tree, so they can share/use the same React context. And maybe some other advantages, 
  - I’m not sure really. I myself noted that Atlassian’s editor used it and it seemed like a use-case that was fit for it.
  - Yes I agree totally the plugin system shouldn’t React-based per say. It’s just that if you want to have modular plugins that include all those aspects I mentioned, you have to combine them yourself into one custom plugin, as the way you pass nodeviews, plugins etc to PM is through several different APIs.
  - Eg schema and plugins are provided through editorState yet nodeviews through editorView. Then because editorState is instantiated before the editorView, your plugins won’t have access to it until it is created. 
  - So if you are using something like Mobx stores with both the state and the action dispatchers, you need a separate init(editorView) to add the view afterwards. 
  - Which is I guess fine but it’s bit awkward. And well I switched from Mobx to Redux since PM kinda forces you to use Redux type application logic.
  - And oh you also got that problem. In my case I was using lot of inline nodes, so I had to modify the delete functionality to account for the extra offsets with positions. 
  - It’s been a long time since I solved it, like over a half of year, so I don’t really remember to exact details.
  -  Use the ProseMirror devtools to at least see how the elements behave, and maybe @marijn will tell you how it’s done.

- ref
  - [Lightweight React integration example](https://discuss.prosemirror.net/t/lightweight-react-integration-example/2680)
  - [How can a react element be rendered as a block or mark?](https://github.com/remirror/remirror/issues/129)
  - [Rendering a React component inside a node_201606](https://discuss.prosemirror.net/t/rendering-a-react-component-inside-a-node/349/11)
  - [How the heck do I use this with React?](https://discuss.prosemirror.net/t/how-the-heck-do-i-use-this-with-react/3437)

- ## remirror: Render ReactNodeView instance into the element of toDOM
- https://github.com/remirror/remirror/issues/271
- The difficulty in integration is that the dom node and the content dom node of the `NodeView` are consumed synchronously by ProseMirror. 
  - However, react requires a `ref` to determine where the node has been mounted and this is done asynchronously. 
  - As a result it's not possible to provide the dom `node` or `contentDOM` to ProseMirror while using pure React.
  - A workaround for this is to create both the top level `dom` node and `contentDOM` manually in a custom `ReactNodeView` . 
  - A react ref is provided as a prop to the custom React component. 
  - It's up to the creator of the custom node view to attach this ref to the part of the tree where content should be rendered to. 
  - Once the React ref is asynchronously attached, the `contentDOM` will be appended to it by the Custom `ReactNodeView` .

- ## NodeView with managed contentDOM does not get attributes applied
- https://discuss.prosemirror.net/t/nodeview-with-managed-contentdom-does-not-get-attributes-applied/1968
- The ** `toDOM` function from the schema’s node spec is completely ignored when you create a node view for that node type**
  - the node view is responsible for rendering it (and could, if it wanted, use `node.type.spec.toDOM` in the process).
- Thanks for the quick clarification, I’ve added a bit of logic to keep the attributes in-sync when updating. 
  - For future readers take a look at `(prosemirror-model.)renderSpec` to figure out how prosemirror turns `toDOM` into a usable element.

- ## Custom NodeView and NodeSpec.toDOM()
- https://discuss.prosemirror.net/t/custom-nodeview-and-nodespec-todom/650
- I need some clarification about the following:
  - when defining custom `nodeViews` with its own `dom` property, I assumed I can strip away the `toDOM()` in the schema. 
  - But then things like dragging seem to be broken (and the official nodeViews example also has it not stripped out). 
  - So the schema `toDOM()` function needs to be kept, to allow a node to be serialized for special purpose such as drag and drop ?
- Yes, a **node view is used when the node is displayed inside the editor**, 
  - but **you’ll still need some way to turn the node into semantic HTML for `copy/paste` and `drag/drop` ** (and possibly also `export/import` , if you use HTML for that) reasons.
- Suggestion: maybe prosemirror could use the dom created by the nodeView to get a default serialization of the node ?

- ## [Draggable and NodeViews](https://discuss.prosemirror.net/t/draggable-and-nodeviews/955)
- You’ll have to define a `toDOM` and `parseDOM` on your task node if you want it to be able to go through the clipboard or be dragged – clipboard content is represented as HTML.
- I think the `toDOM` should be easy as this is pretty much what the nodeView is doing using the this.buildComponent(node.attrs); but the `parseDOM` will be much more complicated as some of my nodeViews render complex Angular components and parsing their DOM to get the node attributes will be tricky. Or am I missing something ?
  - You’ll want your `toDOM` and `parseDOM` to describe a more or less semantic representation of the node, not some big Angular component – nobody wants angular components on their clipboard. 
  - So unless your node has lots of attributes or content, it shouldn’t be too hard to come up with a simple HTML representation.
  - You’re rendering the Angular component in a node view, right? So in your editor, your `toDOM` method is overridden by a node view, and not used for the editable display. 
  - So `toDOM` doesn’t have to involve itself with the Angular stuff at all, it can just output a single recognizeable node (say `<div data-type="mynode" data-someattribute="myvalue">` ), and doesn’t need to hide anything.
- With this, when I am not using a nodeView for task node it works perfectly. When I use the nodeView I am able to drag and drop a task but instead of moving it the task is duplicated.
  - Is your node selectable?  Drag-and-drop within the editor relies on the selection to remember which part it should delete when the dragged content is dropped.
  - Okay, it seems that the problem is that in order for drag and drop to work correctly it needs to let `mousedown` events pass. I need to block `mousedown` so I can click on the form when editing an image without the selection being set to the entire image node. The solution then is to make `stopEvent` let through `mousedown` events that occur on the image, but not on the form.
- Another interesting thing is that if I am using a nodeView, I can have a schema node that does not implements `parseDOM` and with a `toDOM` that returns an empty array and it works normally.

- [Access editor state in node toDOM](https://discuss.prosemirror.net/t/access-editor-state-in-node-todom/2023)
- You probably shouldn’t, since the rendered node view will survive further updates to the state and thus could get out of date.
  - You can make the functions you put in nodeViews close over additional data, or even an accessor function that somehow fetches the current state, but you have to take care to take the above issue into account.

- ref
  - [Add integration tests for testing NodeViews](https://github.com/bangle-io/bangle.dev/issues/125)
