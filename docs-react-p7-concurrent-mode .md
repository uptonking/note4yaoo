---
tags: [concurrent, docs, react]
title: docs-react-p7-concurrent-mode
created: '2020-06-23T07:35:14.835Z'
modified: '2020-07-05T18:55:35.555Z'
---

# docs-react-p7-concurrent-mode

## Introducing Concurrent Mode

- Concurrent Mode is a set of new features that help React apps stay responsive and gracefully adjust to the user’s device capabilities and network speed.
- This illustrates how UI libraries, including React, typically work today. 
  - Once they start rendering an update, including creating new DOM nodes and running the code inside components, they can’t interrupt this work. We’ll call this approach “blocking rendering”.
- In Concurrent Mode, rendering is not blocking. 
  - It is interruptible.
  - This improves the user experience. 
  - It also unlocks new features that weren’t possible before. 
- Both debouncing and throttling create a suboptimal user experience.
- The reason for the stutter is simple: once rendering begins, it can’t be interrupted. 
- No matter how good a UI library (such as React) might look on a benchmark, if it uses blocking rendering, a certain amount of work in your components will always cause stutter. And, often, there is no easy fix.
- **Concurrent Mode fixes this fundamental limitation by making rendering interruptible**.
  - This means when the user presses another key, React doesn’t need to block the browser from updating the text input. 
  - Instead, it can let the browser paint an update to the input, and then continue rendering the updated list in memory. 
  - When the rendering is finished, React updates the DOM, and changes are reflected on the screen.
- Conceptually, you can think of this as React preparing every update “on a branch”. 
  - Just like you can abandon work in branches or switch between them, 
  - React in Concurrent Mode can interrupt an ongoing update to do something more important, 
  - and then come back to what it was doing earlier.
- Concurrent Mode techniques reduce the need for debouncing and throttling in UI. 
  - Because rendering is interruptible, React doesn’t need to artificially delay work to avoid stutter.
  - It can start rendering right away, but interrupt this work when needed to keep the app responsive.
- In Concurrent Mode, React starts preparing the new screen in memory first — or, as our metaphor goes, “on a different branch”. 
  - So React can wait before updating the DOM so that more content can load. 
- In Concurrent Mode, we can tell React to keep showing the old screen, fully interactive, with an inline loading indicator. 
  - And when the new screen is ready, React can take us to it.
- In Concurrent Mode, React can work on several state updates concurrently — just like branches let different team members work independently
- For CPU-bound updates (such as creating DOM nodes and running component code), concurrency means that a more urgent update can “interrupt” rendering that has already started.
- For IO-bound updates (such as fetching code or data from the network), concurrency means that React can start rendering in memory even before all the data arrives, and skip showing jarring empty loading states.
- React uses a heuristic to decide how “urgent” an update is, and lets you adjust it with a few lines of code so that you can achieve the desired user experience for every interaction.

## Suspense for Data Fetching

## Concurrent UI Patterns

## Adopting Concurrent Mode

## Concurrent Mode API Reference
