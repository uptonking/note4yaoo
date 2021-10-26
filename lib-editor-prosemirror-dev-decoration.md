---
title: lib-editor-prosemirror-dev-decoration
tags: [editor, prosemirror, text-editor]
created: '2021-07-09T18:08:03.459Z'
modified: '2021-07-09T18:08:34.957Z'
---

# lib-editor-prosemirror-dev-decoration

# guide

# discuss
- ## 

- ## 

- ## 

- ## The Grid Ed: Overlay widgets
- https://discuss.prosemirror.net/t/the-grid-ed-overlay-widgets/150
  - https://github.com/the-grid/ed
- Maybe all of this overlay hackery wouldn’t be needed if PM had examples with contenteditable=false divs in the flow. Is anything like that in the works?
  - Nodes without content are automatically set to contenteditable=false when rendered. So it seems like the right thing just happens, as seen in the most basic form in the horizontal_rule node, but you can create a node like that that renders its content in a more complicated way. (Just be aware that ProseMirror might occasionally decide to redraw the node when its surroundings change.)
- the Grid’s Ed v2 has hit master, updated for PM 0.17.x. 
  - Widgets are no longer overlaid & synced. 
  - Now there is an inline representation that is rendered as a `NodeView` and and editor representation that is rendered as a modal.

- ## Prosemirror-view upgrade caused Chinese to be affected by Decoration widget during input
- https://discuss.prosemirror.net/t/prosemirror-view-upgrade-caused-chinese-to-be-affected-by-decoration-widget-during-input/2452
- updating the view during composition is something the editor does by-design now.
  - You can make your problem a lot less severe (and make things more efficient to boot) by using the `key` option to `Decoration.widget` to avoid redrawing. 
  - Still looking into why it is disrupting compositions in the first place, since changes to those decorations shouldn’t really cause the content around them to be redrawn.

- ## Widget made with react is being redrawn every time
- https://discuss.prosemirror.net/t/widget-made-with-react-is-being-redrawn-every-time/1913
- if you directly call `createControlsWidget` and that function creates a React root, that will happen a lot, obviously. 
  - But note that you can also pass a function as second argument to `Decoration.widget` . 
  - If you do that and provide a `key` that identifies the type of widget, the view will be able to avoid redrawing the widget most of the time, and will only call the DOM creation function when actually necessary.

- ## Unmounting a Decoration Widget created with React
- https://discuss.prosemirror.net/t/unmounting-a-decoration-widget-created-with-react/3050
  - I am using the `(view, getPos) => … ` form of the toDOM param in `Decoration.widget()` . 
  - In that function, I am using `ReactDOM. Render()` . 
  - It all works great, except it doesn’t clean up when destroyed. 
  - What would be the proper way to detect widget destruction in such a case in order to call `react-dom’s unmountComponentAtNode()` to clean up?
  - For now, I am going to see about solving this feature with a `NodeView` which gives a bit more fidelity(忠实、忠诚；准确性) to the DOM lifecycle than does a widget.
- I had the same problem and I solved it by keeping the container of the react component in the plugin state and calling `ReactDOM.unmountComponentAtNode(container)` every time the decoration is created and re-rendering the widget again in the same container.
