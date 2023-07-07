---
title: lib-editor-prosemirror-community-stars
tags: [community, editor, prosemirror]
created: 2022-08-30T01:46:03.984Z
modified: 2022-08-30T01:46:22.149Z
---

# lib-editor-prosemirror-community-stars

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## props to plugin views__202206
- https://discuss.prosemirror.net/t/props-to-plugin-views/4672
  - What’s the best way to pass props into plugin views so that they update when props change (not only when state changes)?
  - I mean plugin view specific props. Like if user preference for accent color is stored higher up in the app, and its passed as a prop to a view for a plugin. Not editor state props, basically.
  - [Some thoughts on Prosemirror's API to improve it](https://tanishqkancharla.dev/thoughts/prosemirrorapi)

- Plugin views have their `update` method called as normal when the editor’s props change. Except when the state is reconfigured—then they are destroyed and recreated entirely.
- That sounds like a concept entirely outside ProseMirror. 
  - 👉🏻️ Put it in a state field and update it when it changes using a transaction, if you want to tie it into ProseMirror’s update cycle.

- This is Prosemirror tied into a bigger system, and the problem I’m having. 
  - I can’t pass props i.e. app state (or app services, but I didn’t show them here) into editor plugin views.
  - Like state about the theme colors, or global user font preference, etc.
- Here are four possible options to fix the problem.
- You can use a “props” plugin which goes into the editor state, and you just have to make sure to update it every time the app state changes.
- The second option is to just lift plugin views out of prosemirror and just make it your app view’s responsibility. 
  - Now you just read the plugin state through the editor state and use whatever services you need. 
  - Basically you make it the App’s responsibility to render the plugin views.
  - This is, imo, the “right” approach. 
  - In an ideal world, you shouldn’t even need the EditorView component when integrating Prosemirror into a bigger system. 
  - It gets replaced by the App view and EditorState gets rendered as part of it.
- The third approach is using observables/subscriptions like cole suggested or in my initial post. 
  - I didn’t bother to figure out how to draw this, but in mount you pass in those subscriptions as the “initial” props to the Editor View.
- The fourth approach is inventing some new concept in Prosemirror to support this. I’m not really sure what it would look like; Maybe the EditorView becomes a function of state and props where props is any object.

- Plugin views have their update method called as normal when the editor’s props change. Except when the state is reconfigured—then they are destroyed and recreated entirely.
- That sounds like a concept entirely outside ProseMirror. Put it in a state field and update it when it changes using a transaction, if you want to tie it into ProseMirror’s update cycle.

- ## I'm curious what you would consider "Prosemirror regrets" -- things that you'd do different or things you dont like about the current implementation
- https://twitter.com/moonriseTK/status/1487832468308774918
- Writing correct document-changing commands, especially schema-agnostic ones, is ridiculously hard right now. 
- Also the extension system is not as powerful as that in codemirror 6.

- Can you talk more about the formalisms(形式(的实例)) ProseMirror adopts that you admire?
  - I'm still discovering it but mostly the transaction and NodeView systems. Make it really easy to add custom behaviour. I just added checkbox support for my notetaking app in a few lines of code.

- ## Remove contenteditable completely?
- https://discuss.prosemirror.net/t/remove-contenteditable-completely/1766
- using contenteditable for rendering/cursor tracking reduces complexity by avoiding the need to implement layout. 
  - However, this means **ProseMirror is not aware of where things are rendered on the screen**.
  - For most use cases, this is not a problem. 
  - However, this makes implementing certain features that rely on knowing where things are rendered more difficult. 
  - From what I’ve seen, commercial close-sourced word processors such as Google Docs and MS Word Online handle rendering/cursor tracking instead of delegating to contenteditable.

- Some example use cases:
- Break up document to fixed-size pages
  - can’t do this without knowing the height of each line being rendered
- Multiple cursor placement in collaborative editing
  - the browser can only render one cursor, to render multiple cursors we need to be able to project document position to screen coordinates, expensive to do without having rendered layout information cached
- More sophisticated marks such as inline highlighting and commenting 
  - as far as I know, marks in ProseMirror are rendered by wrapping inline text with spans and decorating the wrapper spans, 
  - if you want to render more complex structures, such as a popover comment box centered/above the highlighted text, you’d have to render the highlight as a span, and then determine the wrapper span bounding box position after the mark is rendered and append the popover comment box, which I think is a workaround to the system

- I have been exploring the possibility of handling layout/rendering instead of delegating to contenteditable. 
  - It seems this involves breaking up the document into boxes that cannot be broken up further and laying them out as lines with the document’s size constraints, before finally rendering them. 
  - I don’t think this can fit with the current APIs of ProseMirror, since the concept of box and layout are missing and model toDOM simplify returns DOM specifications with no layout information.
  - Is there any recommendation for bridging the gap here? I’d love to use ProseMirror for its beautiful model and state implementation, but I’d also like to have more control over the view layer.
- I was hoping there might be a way to implement a custom view layer that deals with layout. But if not, I’ll take a stab at implementing this as a different project.
  - https://github.com/yuzhenmi/taleweaver
  - I’ve been experimenting with this, now I can better appreciate why you’re using contenteditable, it does greatly simplify capture of inputs, especially for mobile.
  - My requirement is to be aware of where things are rendered, so that there is more flexibility with fixing the page height and rendering complex UI overlays on top of the document. 
  - I no longer think it conflicts with adopting contenteditable.
  - I’m starting to experiment with determining the document layout (words + lines + pages) myself but have them inside a contenteditable, and expose an API that allows convenient/efficient conversion of document position to screen coordinates (and vice-versa). Any thoughts on this approach? 
- I’m curious how you’re planning to do the positioning, and how you’ll address the potential disruptive effect on the editing experience this may have. 
  - You might be able to get quite far with decorations adding CSS (or even break nodes) to specific elements in the document.
  - I don’t expect the core library will be doing things like this, but if you find a promising approach and run into problems caused by the library, we can certainly discuss them.
- I’ve been experimenting in a new project without prosemirror as a dependency.
  - So far, the same model implementation seems to work - I’m using the same flat token model for applying transformations, and I’m constructing a tree model from the tokens for convenient access to nodes.
  - When it comes to the view layer, things start to diverge. I’m introducing the concept of “words” - a range of tokens that cannot be split for line wrapping. A list of “words” is constructed for each block-level node, and each word may reference multiple inline nodes (if, say, the first half of a word is bolded and the second half is not). The screen size of each word is then computed. Knowing the width of each word and the width of the document, I group them into lines.
  - I’m also playing around with adding “pages” to the document. With lines built from words, I then group lines into pages, based on the height of each line and the height of each page.
  - I haven’t looked into performance optimization yet, but the screen size of each word is cached. With this information, I’m able to map document position to screen coordinates and vice-versa without repeatedly calling getBoundingClientRect.
  - As for cursor handling, I’m still experimenting, but it seems it’s better to let the browser capture cursor-related events and we can map it to changes to the cursor state. 
  - And for rendering the cursor, I think it’s more useful to do it ourselves, since there is little cross-browser/device concerns. 
  - This is assuming there is only one editing cursor that we need to listen to events for, which I think is a fair assumption for WYSIWYG. 
  - For collaborative editing, additional observing cursors can be easily rendered the same way as the editing cursor.
  - Not sure how exactly this can fit with prosemirror yet. The view module would have to be completely replaced. The Node class will probably also have to be modified, since right now it defines to-DOM for the node. I don’t think there is much conflict with the other modules.

- All the editing apps need to use contenteditable to some extent because certain text editing features (IME, etc.) don’t really work without it. 
  - It is true that some hide contenteditable a lot more than others, but as of today, one cannot live completely without it. 
  - There have been some early proposals by some of the major vendors to add more basic level support for editing in browsers over the last few years, but so far it has all been at an early draft stage and it did not develop beyond that.

- Honestly, I wish the specification for contenteditable would better handle primitive positioning and selection problems, 
  - you wouldn’t believe the amount of CSS & decoration stuff I had to code to get something even-approaching word-style selection behaviour.
  - In terms of complex UI overlays, inline highlighting/commenting, etc. I thought I’d pipe in, you can quite nicely implement sophisticated overlays with decorations and Vue.js where that’s concerned.
  - Obviously, you can switch out Vue and implement reactivity with a different framework
