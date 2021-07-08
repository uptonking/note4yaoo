---
title: lib-editor-prosemirror-dev-nodeview
tags: [editor, lib, prosemirror]
created: '2021-07-02T18:23:48.398Z'
modified: '2021-07-02T18:24:12.955Z'
---

# lib-editor-prosemirror-dev-nodeview

# guide

- 基于react组件实现NodeView要注意区分两处逻辑
  - 一般在NodeView class的constructor()方法中创建react VDOM
  - 然后在NodeView class的update()方法中更新vdom
  - 更新时常使用基于pubsub的事件管理器模式

- nodeViews作为一个props的定义
  - `image(node, view, getPos) { return new ImageView(node, view, getPos) }`本身是一个方法，只是返回值经常创建类的实例
  - NodeView本身是一个Interface而不是class，所以可以像guardian-pm-elements一样定义一个工厂方法，返回值就是实现了NodeView接口的对象

- problems
  - how to manage a list of NodeViews
  - complicated/big nodeview
  - nodeview partially editable like textarea

## NodeView vs decoration

- 渲染PMNode的控制权不同
  - NodeView可完全自己控制
    - By default, document nodes are rendered using the result of the `toDOM` method of their spec, and managed entirely by the editor.
    - If you provide a `contentDOM` property, the library will render the node's content into that, and handle content updates. 
    - If you don't, the content becomes a black box to the editor, and how you display it and let the user interact with it is entirely up to you.
  - Decorations make it possible to influence the way the document is drawn, without actually changing the document.
    - 在plugin的apply()方法中可以add/remove decorations
    - 一般用来装饰样式，而不是加减内容组件

- NodeView需要自己定制toDOM/parseDOM
  - decoration一般不修改doc

- 可以通过修改更新decoration来触发NodeView更新
# discuss-stars
- ## Selection in nodeViews outside of contentDOM
- https://discuss.prosemirror.net/t/selection-in-nodeviews-outside-of-contentdom/2282
- If you have a nodeview for a node with content and you don’t want to let the user modify the DOM of the nodeview’s shell but do allow the user to modify the content via prosemirror, is it recommended that you add a `contenteditable=false` attribute on the nodeview’s `dom` and `contenteditable=true` on the nodeview’s `contentDOM`?
  - No, that is usually a bad idea (you won’t be able to select from inside the node to outside it anymore). Sometimes you can get somewhere by wrapping the uneditable parts in an uneditable node (but there’s lot of weird browser behavior that can still trip you up there).
- I currently create a CSS sheet dynamically and add it to the document head. In that stylesheet I then add the text that should not be editable using the `::before` selector and the `content` property. The native selection doesn’t recognize CSS text that was added using CSS. It’s a bit of a hack, btu it also seems to be working.

- ## nodeView let user inserts text before contentDOM 
- https://github.com/ProseMirror/prosemirror/issues/741
- It's hard to automatically determine what is supposed to be editable and what isn't, so yes, the library relies on explicit use of the `contentEditable` attribute there.
- There might be editable information encoded in nodes besides contentDOM. Also, creating 'islands' of editable content inside uneditable nodes makes selecting from the outside to the inside or vice-versa impossible, which isn't great for use experience.
- The browser won't put the cursor in non-inline contexts, so assuming that `<div>` is `display: block`, the user won't be able to put a selection directly in the outer `<div>`

- ## NodeView inside document selection
- https://discuss.prosemirror.net/t/nodeview-inside-document-selection/1322
  - I’m using NodeView 1 and would like it to apply a style (e.g. blue overlay) to indicate when its node is inside a selection (e.g. an enclosing TextSelection / AllSelection / CellSelection / etc).
- I’ve considered and ruled out:
  - Applying an inline decoration over the range of the selection (not supported — NodeView is only notified of node decorations)
  - Using a NodeView API that is called when document selection changes (doesn’t exist)
  - Using a CSS property/pseudo selector based on DOM selection (couldn’t find anything appropriate)
- It seems like I need to write a plugin that applies a node decoration to each node (that I want styled) and then use the `update` hook to apply the styling. 
  - Doing this inefficiently seems simple — after each transaction traverse the document between the current selection `Node#nodesBetween` . 
  - To do this efficiently I think I’d need to track positions of node insertions/deletions/shifts in the plugin, and then find positions falling within the selection bounds during selection changes.
  - is this the best way to solve the problem? 
- I ended up implementing an alternative approach, which is to create an observable of the editor selection in a plugin (fed by the `plugin.view.update` hook), and pass it down to the node view. 
  - The node view then subscribes to selection changes, and uses `getPos()` to check if it’s in bounds, and updates itself based on that. 
  - Thanks @rifat for the suggestion from Atlassian’s editor

- ## Can a MarkView know when selection is inside their node?
- https://discuss.prosemirror.net/t/can-a-markview-know-when-selection-is-inside-their-node/1956
- You didn’t really ask a very clear question, but the problem may revolve around the fact that **a node view doesn’t really get to see arbitrary updates to the document**, so there’s no good point to run the code you pasted. It might be easier to drive this panel from a plugin, which can test whether the selection is inside a node of the relevant type, and adds or removes the panel (either overlaid on the editor or via a widget decoration) as appropriate.
- I would also like to know why there is no getPos function for MarkViews. Is this a technical limitation or just a missing feature?
  - Marks aren’t ‘objects’, in that they are metadata applied to groups of other nodes, but their actual start and end isn’t really meaningful, and they may be split or merged at arbitrary points in time. As such, making them behave like stateful objects in the view is tricky and doesn’t seem like a good conceptual fit to begin with.
- Okay I found a basic way to calculate a mark view range. I can get the start position with `posAtDOM` and the dom element. After that I have to get the full mark range within the parent node.
- I’ll go with building a plugin that displays the overlay if the selection is inside a link mark. Could you explain what the purpose of a MarkView is then? Is it only to vary how the mark is rendered?
  - Yes, it’s just a hook that you can use to change the rendering in the editor.

- ## NodeView setSelection is insufficient
- https://discuss.prosemirror.net/t/nodeview-setselection-is-insufficient/805
  - I’m trying to use NodeViews setSelection to manually set selection inside the NodeView. 
  - My NodeView has a “dom” property and doesn’t have a “contentDOM”
  - `setSelection()` works perfect but I don’t know the moment when cursor leaves the NodeView node element. 
  - I was expecting `deselectNode()` to do this, but it doesn’t fire for this event. 
  - Can I somehow (not with a plugin) detect that cursor left the NodeView node?
- `deselectNode` is called when a node selection is removed from the node, it’s not used for other kinds of selections. 
  - There’s nothing that will notify a node view when the DOM selection is moved out of it. What are you trying to accomplish?

- ## How to make child content of a node uneditable dynamically in ProseMirror?
- https://stackoverflow.com/questions/40939898
- I can think of two ways
  - When a piece of the document is locked, filter transform actions, canceling (resetting to the old state) any that touch this region (can be determined by calling `forEach` on the elements in `action.transform.mapping.maps` ).
  - Write a custom node view for these kinds of nodes, and give them an attribute `readOnly` . Toggle it when they should become uneditable, and when it is on, render the locked content with `contenteditable=false.` But note that this does not protect against programmatic changes to the content. Also, it will make it impossible to put the cursor into them, which might not be desired.

- ## How to create non-editable text segments in the document
- https://discuss.prosemirror.net/t/how-to-create-non-editable-text-segments-in-the-document/1154
- I recommend against creating editable ‘islands’, i.e. uneditable elements with editable elements within them. 
  - Browsers kind of support that, but it has all kinds of problems. 
  - For example selections aren’t allowed cross such uneditable boundaries—you can’t have a selection that starts inside the island and continues outside of it—and focus handling in ProseMirror breaks since the focus will be on the inner element rather than on the top-level editable element.
- What is the good way to track when caret is entering a this.contentDOM ?
  - Same answer as always: inspect transactions. 
  - You can add decorations to a node to send “messages” to its node view—the update method will get them as an argument. 
  - So you’d have a plugin that maintains a set of ‘active’ markup nodes and for each transaction updates that and generates the appropriate decorations.

- ## Custom NodeView containing an editable node
- https://discuss.prosemirror.net/t/custom-nodeview-containing-an-editable-node/587
  - 目标是，图片部分不可编辑，但文字部分可编辑
  - I’m trying to create this type of node in ProseMirror:(image) (text node) (select image dropdown)
  - The dropdown allows a user to select the image being shown and sets the attrs.image-uri. 
  - But I want the dropdown and the image to be completely ignored by the editor (no cursor selection, deletion, etc).
  - And I want to be able to interact with the text node as normal (ability to split, toggle mark, etc).
- I’ve tried using a custom node view but it appears that children of a `contentEditable=true` element is interact-able. 
  - I found that `::before` and `::after` elements are the exception to this and I may try to use that - 
  - but that seems limited and hacky as I would have to determine boundaries to be able to attach click/hover handlers on the dropdown.
- Another approach I’ve considered is trying to overlay the dropdown and image on top of the editor so that they aren’t children of the top-level contentEditable=true element
- In your custom Nodeview, you could set all your additional elements to `contentEditable=false` , to avoid having a visible blinking text cursor. And you just set `contentDOM` to define the children you want to interact as normal. 
- About your second question, not sure whether I understood it properly, but you could use decorations to inject your dropdowns overlays, right at the custom node, then I don’t see a need to track position changes as you described it.
  - It appears that setting the additional elements to `contentEditable=false` still allows them to be selectable and deletable…
- If you put content into a non-editable `display:block` element, the browser will mostly not interact with it during editing. 
  - Inline elements in between editable content are more problematic. 
  - They will be involved in the cursor motion in the surrounding editable element.
  - **Selecting across things is always possible when they are children of an editable node**.
- I was able to get this working by calling `coordsAtPos()` to render elements with `position: absolute` on top of the prose-mirror element.

- ## nodeView with partially non-editable content: dom reader problems
- https://github.com/ProseMirror/prosemirror/issues/745
-  Does a DOM structure like this, which doesn't create a new editable island, provide better results?
   - Editable HTML is really bad at this, and ProseMirror doesn't really have a way to paper that over. In this specific case, you could probably make the `$` a CSS `:before` element to get the behavior you want. Or make the inner element (class=text) a block (on the CSS level) element and use CSS and padding hacks to position the $ in the right place. But a general solution doesn't exist yet.
- Are there complications about adding checks in the blur/focus handlers ? Something like checking if the blur event target is actually inside an editable island of the current view.dom ?
  - Yes, there are. **Such an island is considered a separate editable element by the browser**, and events for edits inside it will fire on the island node, rather than the outer editable node.
- I think I am going to consider this kind of DOM structure (editable islands) unsupported. 
  - Even if you can sort of make it work with kludges, I expect it to break in all kinds of interesting ways in corner cases. 
  - Usually, the structure of the node view can easily be adjusted to put the uneditable content in a node that's not a parent of the editable content, 
  - and **in cases where that is really impossible, I recommend nesting a separate ProseMirror instance** for the content and broadcasting the steps to the parent document (as in the **footnote** demo).

- ## Allow focus on uneditable node view
- https://discuss.prosemirror.net/t/allow-focus-on-uneditable-node-view/1863
  - I’m trying to find a way to allow content in a node view with `contenteditable="false"` to be interacted with normally (selecting text, clicking controls, etc).
- Have you tried setting dom.tabIndex = 0 in the node view? That seems to help a lot. ProseMirror assumes that if its editable node has focus, it should control the selection. By making the inner node focusable, you allow its content to be selected without focusing the editor.
