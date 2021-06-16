---
title: lib-editor-prosemirror-issues-stars
tags: [editor, issues, prosemirror]
created: '2021-06-16T14:13:01.159Z'
modified: '2021-06-16T14:13:27.162Z'
---

# lib-editor-prosemirror-issues-stars

# good-issues

- ## 

- ## 

- ## what difference between the plugin view and nodeViews and schema and decoration?
- https://discuss.prosemirror.net/t/what-can-plugin-view-do-or-what-should-it-be-used-for/3517
- a `NodeView` is used to control how a specific node is rendered (like a codeblock) but is within the editorview and semi-managed by ProseMirror
  - There are a limit set of hooks like update, destroy to control the `NodeView` similar to that of a `PluginView` (but more scoped/granular); 
  - they’re only called a change affects a node, not when a change affects the editor view.
- We tend to think about the “view” section in the same way we think about a “useEffect” hook in React. The update function can be treated like the “deps” array in useEffect and then you can use destroy to do a final clean up. It’s a really great spot to react to state changes and then perform side effects. 
  - Manipulating the dom outside of view.dom
  - Setting up global listeners and observers (like custom selectionchanges, window resizes, etc.)
  - Data fetching
  - Performing hacky workarounds to smooth over OS issues (not ideal but it’s still another tool for some stuff)
  - Notifying other parts of your application when something changes or if you have to save content (e.g. like executing a callback when the content of the Prosemirror document changes)
  - I almost think “view” should just be called “effects”

- [How can I communicate from a plugin to a custom nodeView?](https://discuss.prosemirror.net/t/how-can-i-communicate-from-a-plugin-to-a-custom-nodeview/952)
- when the node attributes of the custom nodeView change and therefore the underlying doc changes, I just replace the node and all works as expected.
  - But now I would like to communicate to the nodeView, without actually changing the node. So I tried to set from my plugin a node decoration on that nodeview (putting my payload into the spec argument). Unfortunately at my custom nodeView, the update method (where I expect to get access to the payload in the decoration spec object) never gets called.
- Is this the recommended way to communicate from a plugin to a NodeView?
  - I have a similar situation where a plugin gets external data that various NodeViews use. I need those NodeViews to update (re-render) themselves when that external data changes. So I really just need a way to tell prosemirror to re-render the NodeViews.
  - From this thread it seems possible to decorate the NodeViews and then update the decorations when the external data changes. The decoration change will then trigger prosemirror to re-render the NodeViews. It seems like a round about way to force a re-render but if its the best way then I’ll do it
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

- [Using with React](https://discuss.prosemirror.net/t/using-with-react/904)
- The issue with React-based NodeViews isn’t that it’s undoable, it is just that the interfacing & gluing between the NodeViews, Schema and Plugins (with the event dispatching and portals) is quite difficult to make.
  - So immediately if you want to create a plugin system on top of that implementation, you’ll have to start thinking how to join all the parts (normal plugins + schema + nodeviews (as the React components) + possible toolbar buttons & actions) together. 
  - What I got stuck before I got too busy doing other things was the implementing of the event-flow from the actions/key-press plugins to the plugin state, which would then notify the React components through an event-dispatcher. 
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

- ## remirror: Render ReactNodeView instance into the element of toDOM
- https://github.com/remirror/remirror/issues/271
- The difficulty in integration is that the dom node and the content dom node of the `NodeView` are consumed synchronously by ProseMirror. 
  - However, react requires a `ref` to determine where the node has been mounted and this is done asynchronously. 
  - As a result it's not possible to provide the dom `node` or `contentDOM` to ProseMirror while using pure React.
  - A workaround for this is to create both the top level `dom` node and `contentDOM` manually in a custom `ReactNodeView` . 
  - A react ref is provided as a prop to the custom React component. 
  - It's up to the creator of the custom node view to attach this ref to the part of the tree where content should be rendered to. 
  - Once the React ref is asynchronously attached, the `contentDOM` will be appended to it by the Custom `ReactNodeView` .

- ## Custom NodeView and NodeSpec.toDOM()
- https://discuss.prosemirror.net/t/custom-nodeview-and-nodespec-todom/650
  - I need some clarification about the following:
  - when defining custom `nodeViews` with its own `dom` property, I assumed I can strip away the `toDOM()` in the schema. 
  - But then things like dragging seem to be broken (and the official nodeViews example also has it not stripped out). 
  - So the schema `toDOM()` function needs to be kept, to allow a node to be serialized for special purpose such as drag and drop ?
- Yes, a node view is used when the node is displayed inside the editor, 
  - but you’ll still need some way to turn the node into semantic HTML for copy/paste and drag/drop (and possibly also export/import, if you use HTML for that) reasons.
- Suggestion: maybe prosemirror could use the dom created by the nodeView to get a default serialization of the node ?

- [Draggable and NodeViews](https://discuss.prosemirror.net/t/draggable-and-nodeviews/955)
- You’ll have to define a `toDOM` and `parseDOM` on your task node if you want it to be able to go through the clipboard or be dragged – clipboard content is represented as HTML.
- I think the toDOM should be easy as this is pretty much what the nodeView is doing using the this.buildComponent(node.attrs); but the parseDOM will be much more complicated as some of my nodeViews render complex Angular components and parsing their DOM to get the node attributes will be tricky. Or am I missing something ?
  - You’ll want your `toDOM` and `parseDOM` to describe a more or less semantic representation of the node, not some big Angular component – nobody wants angular components on their clipboard. 
  - So unless your node has lots of attributes or content, it shouldn’t be too hard to come up with a simple HTML representation.
  - You’re rendering the Angular component in a node view, right? So in your editor, your `toDOM` method is overridden by a node view, and not used for the editable display. 
  - So `toDOM` doesn’t have to involve itself with the Angular stuff at all, it can just output a single recognizeable node (say `<div data-type="mynode" data-someattribute="myvalue">`), and doesn’t need to hide anything.
- Is your node selectable? 
  - Drag-and-drop within the editor relies on the selection to remember which part it should delete when the dragged content is dropped.

- [Access editor state in node toDOM](https://discuss.prosemirror.net/t/access-editor-state-in-node-todom/2023)
- You probably shouldn’t, since the rendered node view will survive further updates to the state and thus could get out of date.
  - You can make the functions you put in nodeViews close over additional data, or even an accessor function that somehow fetches the current state, but you have to take care to take the above issue into account.

- ref
  - [Add integration tests for testing NodeViews](https://github.com/bangle-io/bangle.dev/issues/125)
