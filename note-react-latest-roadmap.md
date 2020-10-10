---
tags: [react, roadmap]
title: note-react-latest-roadmap
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-08T03:17:23.369Z'
---

# note-react-latest-roadmap

## warning

- 不建议使用defaultProps，即将deprecate
  - 可以使用es6参数默认值
- 不建议使用forwardRef，未来ref会作为props中的属性
  - 可以使用callbackRef

## guide

- React Fast Refresh: hot reloading for React
  - https://github.com/facebook/react/issues/16604
- React Fire: Modernizing React DOM
- React Flare: new React Events
  - build UIs that feel great on desktop and mobile, with mouse and touch
- concurrent mode and suspense (stable-17)
- ref
  - [react-rfc](https://github.com/reactjs/rfcs/pulls)
  - [bigIssues](https://github.com/facebook/react/issues?q=is:open+is:issue+label:%22Type:+Big+Picture%22)
  - [React.js有哪些设计缺陷？](https://www.zhihu.com/question/316425133)
  - [React v16.9.0 and the Roadmap Update_20190808](https://reactjs.org/blog/2019/08/08/react-v16.9.0.html)

## roadmap

- ### [React v16.9.0 and the Roadmap Update](https://reactjs.org/blog/2019/08/08/react-v16.9.0.html)
- Here’s what we plan to do next
- One Release Instead of Two
  - Concurrent Mode and Suspense power the new Facebook website that’s in active development, so we are confident that they’re close to a stable state technically.
- An Update on Data Fetching
  - While React is not opinionated about how you fetch data, the first release of Suspense for Data Fetching will likely focus on integrating with opinionated data fetching libraries. 
  - In the first release, we don’t intend to focus on the ad-hoc “fire an HTTP request” solution we used in earlier demos (also known as “React Cache”). 
  - However, we expect that both we and the React community will be exploring that space in the months after the initial release.
- An Update on Server Rendering
  - We have started the work on the new Suspense-capable server renderer

- ### [React 16.x Roadmap_20181127](https://reactjs.org/blog/2018/11/27/react-16-roadmap.html)

- We shipped Hooks on time, but we’re regrouping Concurrent Mode and Suspense for Data Fetching into a single release that we intend to release later 
- We (2018) plan to split the rollout of new React features into the following milestones:
  - React 16.6 with Suspense for Code Splitting (already shipped)
  - A minor 16.x release with React Hooks (~Q1 2019)
  - A minor 16.x release with Concurrent Mode (~Q2 2019)
  - A minor 16.x release with Suspense for Data Fetching (~mid 2019)
- React 16.6 (shipped): The One with Suspense for Code Splitting
  - Suspense refers to React’s new ability to “suspend” rendering while components are waiting for something, and display a loading indicator. 
  - In React 16.6, Suspense supports only one use case: lazy loading components with `React.lazy()` and `<React.Suspense>` .
- React 16.x (~Q1 2019): The One with Hooks
- React 16.x (~Q2 2019): The One with Concurrent Mode
  - Concurrent Mode lets React apps be more responsive by rendering component trees without blocking the main thread. 
  - It is opt-in and allows React to interrupt a long-running render (for example, rendering a news feed story) to handle a high-priority event (for example, text input or hover). 
  - Concurrent Mode also improves the user experience of Suspense by skipping unnecessary loading states on fast connections.
  - You might have previously heard Concurrent Mode being referred to as “async mode”. We’ve changed the name to Concurrent Mode to highlight React’s ability to perform work on different priority levels. This sets it apart from other approaches to async rendering.
- React 16.x (~mid 2019): The One with Suspense for Data Fetching
  - The only supported use case for Suspense is code splitting
  - In this future minor release, we’d like to provide officially supported ways to use it for data fetching too. 
  - We’ll provide a reference implementation of a basic “React Cache” that’s compatible with Suspense, but you can also write your own. 
  - Data fetching libraries like Apollo and Relay will be able to integrate with Suspense by following a simple specification that we’ll document.
  - The low-level Suspense mechanism (suspending rendering and showing a fallback) is expected to be stable even in React 16.6. 
  - We’ve used it for code splitting in production for months. 
  - However, the higher-level APIs for data fetching are very unstable. 
  - React Cache is rapidly changing, and will change at least a few more times. 
  - There are some low-level APIs that are missing for a good higher-level API to be possible. 
  - We don’t recommend using React Cache anywhere except very early experiments. 
  - Note that React Cache itself isn’t strictly tied to React releases, but the current alphas lack basic features as cache invalidation, and you’ll run into a wall very soon. We expect to have something usable with this React release.
- Other Projects
  - Modernizing React DOM
  - Suspense for Server Rendering

## discussion

- time-slicing

### React Flare 

- ref
  - [React Flare](https://github.com/facebook/react/issues/15257)

- The idea is to extend React's event system to include high-level events that allow for consistent cross-device and cross-platform behavior.
- The goal of React Flare is to make it easy to build UIs that feel great on desktop and mobile, with mouse and touch, and that are accessible. 
- It includes declarative APIs for managing interactions like Press, Hover, and Focus. 
- Unlike with the current React event system, the Flare design doesn't inflate the bundle for events you don't use — and it should allow to cut down the amount of code in UI libraries that deal with mouse and touch events.
- Every user-facing event should have a timeStamp.
- Investigate native pointer capture for retargeting events
- Limit all event components to have a single host node as child? If not enforced for all components, we might need this for Hover/Focus/Press at least.
- Stop propagation by default but scope to event module types.
- Investigate ways to listen to root events without first needing to wait for a target event to be dispatched to the event component.
- Remove listener from event object passed to callbacks like onPress
- Ensure discrete events do not unnecessarily force flush previous non-discrete events.
- Ensure event responder get unmounted correctly and pending events (e.g. long press) properly get removed when doing so. 
- Create a new synthetic event and dispatch mechanism that relies on the event being generated in the event responder module, rather than from React.
- We're not longer working on this particular approach and will be exploring other ways to work with the DOM event system in the future. 
  - We've concluded that the "Flare" event system is too high-level an abstraction and we'd like to explore something that is a bit more familiar to developers familiar with the DOM (e.g., addEventListener) and React's existing tools (e.g., hooks). 
  - Our goal is still to make it possible for library authors to work with passive events, capture/bubble phase, custom events, and events occurring on the document from within a React function component...while reducing the amount of event-related code needed in ReactDOM. 
  - Ultimately building both intermediate abstractions like the Responder Event system and high-level abstractions like useTap (which we prototyped in Flare) should be possible in user-space

### React Fire: Modernizing React DOM

- ref
  - [React Fire](https://github.com/facebook/react/issues/13525)

- Our goal is to make React better aligned with how the DOM works, revisit some controversial past decisions that led to problems, and make React smaller and faster.

- Stop reflecting input values in the `value` attribute
  - But that's not how the DOM works.
- Attach events at the React root rather than the document
- Migrate from `onChange` to `onInput` and don’t polyfill it for uncontrolled components
- Drastically simplify the event system
- className → class

## api-experimental

### [react-cache](https://github.com/facebook/react/tree/master/packages/react-cache)

- This package is meant to be used alongside yet-to-be-released

- A basic cache for React applications. 
- It also serves as a reference for more advanced caching implementations.

### [react-fetch](https://github.com/facebook/react/tree/master/packages/react-fetch)

- This package is meant to be used alongside yet-to-be-released

### [use-subscription](https://github.com/facebook/react/tree/master/packages/use-subscription) (since 2019)

- [useSubscription hook PR](https://github.com/facebook/react/pull/15022)

- This hook safely manages subscriptions in concurrent mode.
- This utility can be used for subscriptions to a single value that are typically only read in one place and may update frequently (e.g. a component that subscribes to a geolocation API to show a dot on a map).

- When should you NOT use this? Most other cases have better long-term solutions
  - **Redux stores should use the context API** instead.
  - I/O subscriptions (e.g. notifications) that update infrequently should use a mechanism like `react-cache` instead.
  - Complex libraries like Relay/Apollo should manage subscriptions manually with the same techniques which this library uses under the hood in a way that is most optimized for their library usage.

- **Limitations in concurrent mode**
- use-subscription is safe to use in concurrent mode. 
- However, it achieves correctness by sometimes de-opting to synchronous mode, obviating the benefits of concurrent rendering. 
- This is an inherent limitation of storing state outside of React's managed state queue and rendering in response to a change event.

- Sources that frequently change like Redux would likely deopt to sync mode often and you'd lose a lot of the potential benefits of concurrent mode.
- Just ignore the "change frequently" bit in my previous message. 
- I didn't mean to focus on that aspect so much as the fact that using this approach for Redux would likely cause a lot of the de-optimized, sync re-renders for your app since Redux apps generally have a lot of components listening to the Redux store. (How much you care about this depends on whether you're using concurrent mode in the first place, but it would be sad if that turned out to be the only thing preventing you from using it down the road.)

### [create-subscription](https://github.com/facebook/react/tree/master/packages/create-subscription) (since 2018)

- This is a utility for subscribing to external data sources inside React components. 
- It is officially supported and maintained by the React team.

- When should you NOT use this? Most other cases have better long-term solutions
  - same as useSubscription

- This utility should be used for subscriptions to a single value that are typically only read in one place and may update frequently (e.g. a component that subscribes to a geolocation API to show a dot on a map).

- The main motivation for create-subscription is to provide a way for library authors to ensure compatibility with React's upcoming asynchronous rendering mode. 
- create-subscription guarantees correctness in async mode, accounting for the subtle bugs and edge cases that a library author might otherwise miss.

- **Limitations in async mode**
- However, it achieves correctness by sometimes de-opting to synchronous mode, obviating the benefits of async rendering. 
- This is an inherent limitation of storing state outside of React's managed state queue and rendering in response to a change event.
- The effect of de-opting to sync mode is that the main thread may periodically be blocked (in the case of CPU-bound work), and placeholders may appear earlier than desired (in the case of IO-bound work).
- For full compatibility with asynchronous rendering, including both time-slicing and React Suspense, the suggested longer-term solution is to move to one of the patterns described in the previous section.

## rfc

- [rfcs-open](https://github.com/reactjs/rfcs/pulls?q=is%3Apr+is%3Aopen+sort%3Aupdated-desc)
  - [RFC: createElement changes PR](https://github.com/reactjs/rfcs/pull/107)
    - [rfc text](https://github.com/reactjs/rfcs/blob/createlement-rfc/text/0000-create-element-changes.md)
  - [RFC: Context selectors PR](https://github.com/reactjs/rfcs/pull/119)
    - [rfc text](https://github.com/gnoff/rfcs/blob/context-selectors/text/0000-context-selectors.md)
  - [RFC: Speculative Mode PR](https://github.com/reactjs/rfcs/pull/150)
    - [RFC Implementation: Speculative work PR](https://github.com/facebook/react/pull/18262)
  - [Reparenting API](https://github.com/reactjs/rfcs/pull/34)
  - [RFC: Focus Management API](https://github.com/reactjs/rfcs/pull/109)
  - [Introducing an RFC for isomorphic IDs](https://github.com/reactjs/rfcs/pull/32)  
  - [RFC: Signals and Slots Hooks](https://github.com/reactjs/rfcs/pull/135)
  - [RFC: Unified state](https://github.com/reactjs/rfcs/pull/179)
    - suggest a unify API for creating a global, contextual and local states.

- [rfcs-merged](https://github.com/reactjs/rfcs/pulls?q=is%3Apr+sort%3Aupdated-desc+is%3Amerged)
  - [RFC: useMutableSource PR](https://github.com/reactjs/rfcs/pull/147)
    - [rfc text](https://github.com/bvaughn/rfcs/blob/useMutableSource/text/0000-use-mutable-source.md)
    - [rfc implementation PR](https://github.com/facebook/react/pull/18000)
  - [RFC: React Hooks PR](https://github.com/reactjs/rfcs/pull/68)
  - [Profiler RFC](https://github.com/reactjs/rfcs/pull/51)
    - [Profiler should measure commit phase durations](https://github.com/reactjs/rfcs/pull/139)
  - [New commit phase lifecycle getSnapshotBeforeUpdate](https://github.com/reactjs/rfcs/pull/33)
  - React.lazy
  - React.memo
  - React.createRef
  - [ref-forwarding API](https://github.com/reactjs/rfcs/pull/30)
  - New version of context

- [rfcs-closed](https://github.com/reactjs/rfcs/pulls?q=is%3Apr+sort%3Aupdated-desc+is%3Aclosed)
  - [Add React Hooks in Classes RFC](https://github.com/reactjs/rfcs/pull/124)
  - [RFC: suspendable subscriptions](https://github.com/reactjs/rfcs/pull/127)
  - Fragment refs RFC
  - Accept calculateChangedBits as a prop on Context. Providers 
    - closed in favor of context-selectors

- react-future
  - [RFC: Plan for custom element attributes/properties in React 17](https://github.com/facebook/react/issues/11347)
  - [Externalize the State Tree (or alternatives)](https://github.com/facebook/react/issues/4595)
  - [Support Passive Event Listeners](https://github.com/facebook/react/issues/6436)
  - [Play Nicely with The DOM Event System (because it's legacy anyway)](https://github.com/facebook/react/issues/4751)
  - [Support cross-renderer portals](https://github.com/facebook/react/issues/13332)
  - [Hibernating State (Not Necessarily Serialized)](https://github.com/facebook/react/issues/4594)
