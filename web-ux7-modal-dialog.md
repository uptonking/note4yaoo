---
title: web-ux7-modal-dialog
tags: [components, modal, ui]
created: 2021-02-09T18:33:56.949Z
modified: 2021-07-29T20:37:39.797Z
---

# web-ux7-modal-dialog

# guide

- layer管理时要考虑焦点管理 FocusTrap/Lock

- not-yet
  - router-based dialog

- [popper > floating-ui motivation](https://floating-ui.com/docs/motivation)
# blogs-modal/dialog
- [Better interfaces for dialogue ](https://thesephist.notion.site/Better-interfaces-for-dialogue-4c20a2faf16f47a5a12e090d16c99353)
  - https://twitter.com/thesephist/status/1739616441182081530
  - I've been sketching out ideas for a chat interface to language models that treat branching/multiple timelines as a first-class concept and try to make heavily branch-y threads navigable.
# discuss
- ## The Floating UI components package will largely will consist of composable effects that have a similar API to the positioning middleware. 
- https://twitter.com/atomiksdev/status/1484837373217480706
  - Written in vanilla JS and can be wrapped by any framework of choice.
  - currently it just focuses on positioning like Popper, so there's nothing related to actual user behavior/a11y
  - but there will soon be ways to actually build (accessible) behavior in tandem with positioning logic

- ## Popper v3 is now platform-agnostic, so it can run on React Native (or anything that runs JS)
- https://twitter.com/atomiksdev/status/1461340424275054593
- For React Native, this demo uses very simple/naive calls unlike the DOM version, need to dedicate some time to it!

- ## Building a Dialog component: markup, handlers, problems, solution
- https://twitter.com/peduarte/status/1440610257810571269
- The markup
  - We need to be able to open and close it
- The handlers
  -  add some state and some handlers to be able to open and close the Dialog
- The problems
  - Lack of instructions for assistive technology 
  - Lack of keyboard shortcuts 
  - Lack of control over the content in the DOM
- The solution
- The @radix_ui Dialog component is unstyled and comes with all necessary features out of the box
  · Follows the WAI-ARIA pattern
  · Implements AT instructions
  · Focus trap
  · Scroll lock
  · Keyboard shortcuts
  · Familiar API

- ## [Design Patterns for Replacing Modal Windows](https://community.appway.com/screen/kb/article/design-patterns-for-replacing-modal-windows-1482810903553)
- The problem with modal windows
  - they interrupt users and force them into doing a specific action
  - Many people simply don't read modal dialog boxes, or are confused by them.
  - Many people simply don't read modal dialog boxes, or are confused by them.
- Pattern 1: Show UI elements inline
- Pattern 2: Collapsible UI Elements
- Pattern 3: Dynamic Inline Elements
- Pattern 4: Showing a loading screen/progress bar
- Pattern 5: Error Messages icon with details in tooltip 
- Pattern 6: Warning Dialogs
- If you can't avoid modal windows
  - The modal window should have a descriptive title
  - The modal window should have a Cancel button
  - The modal window should have a Close button
  - Escape should close the window
  - Close when clicking outside the modal window
  - Add a drop shadow and a transparent background
  - Don't make the modal window too large
# ref
- [ebay: Rethink Modals Management in React](https://medium.com/ebaytech/rethink-modals-management-in-react-cf3b6804223d)
