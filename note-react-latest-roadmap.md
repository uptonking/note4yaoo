---
tags: [react, roadmap]
title: note-react-latest-roadmap
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-08T03:17:23.369Z'
---

# note-react-latest-roadmap

## guide

- React Fast Refresh: hot reloading for React
  - https://github.com/facebook/react/issues/16604
- React Fire: Modernizing React DOM
- React Flare: new React Events
  - build UIs that feel great on desktop and mobile, with mouse and touch
- concurrent mode and suspense (stable-17)
- ref
  - [bigIssues](https://github.com/facebook/react/issues?q=is:open+is:issue+label:%22Type:+Big+Picture%22)
  - [React.js有哪些设计缺陷？](https://www.zhihu.com/question/316425133)
  - [React Fire](https://github.com/facebook/react/issues/13525)
  - [React Flare](https://github.com/facebook/react/issues/15257)
  - [React 16.x Roadmap_20181127](https://reactjs.org/blog/2018/11/27/react-16-roadmap.html)
  - [React v16.9.0 and the Roadmap Update_20190808](https://reactjs.org/blog/2019/08/08/react-v16.9.0.html)

## roadmap

- We shipped Hooks on time, but we’re regrouping Concurrent Mode and Suspense for Data Fetching into a single release that we intend to release later this year
- We (2018) plan to split the rollout of new React features into the following milestones:
  - React 16.6 with Suspense for Code Splitting (already shipped)
  - A minor 16.x release with React Hooks (~Q1 2019)
  - A minor 16.x release with Concurrent Mode (~Q2 2019)
  - A minor 16.x release with Suspense for Data Fetching (~mid 2019)

## time-slicing

## api-experimental

### [react-cache](https://github.com/facebook/react/tree/master/packages/react-cache)

- This package is meant to be used alongside yet-to-be-released

- A basic cache for React applications. 
- It also serves as a reference for more advanced caching implementations.

### [react-fetch](https://github.com/facebook/react/tree/master/packages/react-fetch)

- This package is meant to be used alongside yet-to-be-released

### useMutableSource

- This hook is primarily intended for use by libraries like Redux (and possibly Relay). 
  - Work with the maintainers of those libraries to integrate with the hook.

- `useMutableSource()` enables React components to safely and efficiently read from a mutable external source in Concurrent Mode. 
- The API will detect mutations that occur during a render to avoid tearing and it will automatically schedule updates when the source is mutated.
- This hook is designed to support a variety of mutable sources.
- Redux users would likely never use the useMutableSource hook directly. 
  - They would use a hook provided by Redux that uses useMutableSource internally.
- The current best "alternates" to this API are the Context API and useSubscription hook
- The Context API is not currently suited for sources that are used by many components throughout the tree, as changes to the context result in updates that are very heavy (for example, see Redux v6 performance challenges). 
- Advantages of `useMutableSource` over `useSubscription`
  - No temporary tearing will occur during render (even before the initial subscription).
  - Subscriptions can be "scoped" so that updates to parts of a mutable source only impact the relevant components (and not all components reading from the source). 
    - This means that in the common case, this hook should perform much better.
- useMutableSource is similar to useSubscription
  - Both require a memoized “config” object with callbacks to read values from an external “source”.
  - Both require a way to subscribe and unsubscribe to the source.
- There are some differences though:
  - useMutableSource requires the source as an explicit parameter. 
    - (React uses this value to protect against "tearing" and ensure that all components reading from a particular source render with the same version of data.)
  - useMutableSource requires values read from the source to be immutable snapshots. 
    - This enables values to be reused during high priority render, allowing more expensive re-renders to be deferred when needed.
- Version number
  - Tracking a source's version allows us to avoid tearing when reading from a source that a component has not yet subscribed to.
- Pending update expiration times
  - Tracking pending updates per source enables newly-mounting components to read without potentially conflicting with components that read from the same source during a previous render.
- Scenarios to handle
  - Reading from a source before subscribing
  - Reading from a source after subscription
- Unresolved questions
  - Are there any common/important types of mutable sources that this proposal will not be able to support?

- Given a parent and a child, both calling useMutableSource with the same source: when the source updates, what order will the two components try to read the values from the source?
  - Keep in mind that `useMutableSource` is being written for concurrent mode (not legacy sync-rendering mode).
  - So I don't think I understand why the order of subscriptions matters? The resulting React work should be batched into a single React update.
  - If an update is scheduled for both the parent and child, React will render outside->in.

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

- [rfcs-merged](https://github.com/reactjs/rfcs/pulls?q=is%3Apr+sort%3Aupdated-desc+is%3Amerged)
  - [RFC: useMutableSource PR](https://github.com/reactjs/rfcs/pull/147)
    - [rfc text](https://github.com/bvaughn/rfcs/blob/useMutableSource/text/0000-use-mutable-source.md)
    - [rfc implementation PR](https://github.com/facebook/react/pull/18000)
  - [RFC: React Hooks PR](https://github.com/reactjs/rfcs/pull/68)

- [rfcs-closed](https://github.com/reactjs/rfcs/pulls?q=is%3Apr+sort%3Aupdated-desc+is%3Aclosed)
  - [Add React Hooks in Classes RFC](https://github.com/reactjs/rfcs/pull/124)
