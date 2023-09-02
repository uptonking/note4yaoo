---
title: lib-editor-prosemirror-community-showcase
tags: [community, editor, prossemirror, showcase]
created: 2023-06-11T07:07:28.594Z
modified: 2023-06-11T07:07:55.724Z
---

# lib-editor-prosemirror-community-showcase

# guide

# discuss
- ## 

- ## 

- ## 

- ## linear: editor improvements to come. I’m excited for this and the ones that follow.
- https://twitter.com/artman/status/1697266389814243396
  - Our editor is based on Prosemirror.
  - We’re using Prosemirror at the core, with a lot of in-house functionality added (+ lots more really cool stuff still coming)

- ## [Announcing React ProseMirror_202303](https://discuss.prosemirror.net/t/announcing-react-prosemirror/5328)
- It looks like Tiptap takes the same approach we did wherein React node views register themselves to be rendered as portals.
  - Compared with Tiptap, I think our approach is lighter touch, sticking closer to the ProseMirror API and trying to not have too much API surface of its own. Whether that’s good or bad is probably a matter of preference.
- Our main contribution is probably the `useEditorEvent` and `useEditorEffect` hooks, which ensure that React node views can access the whole editor view safely from the React lifecycle in order to call methods like `coordsAtPos` . 
  - We found this to be particularly important when the editor state itself is stored in another state management system like Redux and you want to make Redux-connected node view components that see a consistent view of the editor state.

- Last time I dug into the TipTap integration with React, I noticed something a bit hacky which was the use of a `forceUpdate` to get React to re-render
  - There was a PR that tried to get fix this using the new `useSyncExternalStore` hook
- The `forceUpdate` is necessary in our case for the `LayoutGroup` implementation, which relies on the `useLayoutEffect` hook to update a Set stored in a Ref. Since Ref updates don’t result in re-renders, we have to separately force a re-render by bumping some state!

- It looks like TipTap uses it to force a re-rendering in React in response to a transaction on the editor. The possibility for useSyncExternalStore may have been if TipTop treats the Editor View as a source of external state.

- In react-prosemirror, we don’t attempt to treat the Editor View as a source of external state, because the expectation is that **React is actually the source of the state for the Editor View**
  - Any dispatching of a transaction should result in changing React state, and the state flows back to the Editor VIew through React, without any need for a forced update.
  - React Node Views that get updated by ProseMirror will also call setState on their components in response to the Node View update method getting called by ProseMirror. 
  - Since this happens during the creation of a layout effect of the editor component, React flushes these updates synchronously.
- Where react-prosemirror uses forceUpdate is a bit different from TipTap. 
  - Since state comes from React and only flows to the Editor View during a layout effect, we wanted to discourage use of the Editor View from outside effects and events, in order to prevent code from observing React state that is out of sync with Editor View state. 
  - We provide the useEditorEffect hook to let components get access to the editor view.
- React has layout effects that run synchronously after an update, bottom-to-top. 

- Remirror is a much heavier framework. We had an existing, non-trivial application that was using ProseMirror directly, with many ProseMirror plugins and many existing components. We wanted something light and close to the ProseMirror API to migrate to that focused only on state and rendering integration.

- ## [Socalled "Tracked changes" using ProseMirror_201806](https://discuss.prosemirror.net/t/socalled-tracked-changes-using-prosemirror/1365)
- https://github.com/fiduswriter/fiduswriter/blob/main/fiduswriter/document/static/js/modules/editor/track/accept.js
