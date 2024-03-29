---
title: note-react-rfc-useMutableSource
tags: [react, rfc]
created: 2020-07-17T06:00:22.244Z
modified: 2021-01-04T17:05:20.422Z
---

# note-react-rfc-useMutableSource

# faq 

## How come this API isn't merged with useRef? (Both are used for  managing mutable, usually external data.)

- `useRef` has constraints. 
  - Essentially (with the exception of lazy initialization) you should only mutate refs during the "commit phase" (within useEffect or useLayoutEffect).
  - Refs are like instance fields on class components. They let you e.g. compare next and prev props
  - They **aren't meant for sharing values with other components**.
  - Because of their constraints, they're safe to use with concurrent rendering.

- `useMutableSource` is for reading from mutable sources that you either don't control (e.g. window.location), or sources that may be mutated anytime (e.g. a click event might dispatch a Redux action).
  - useMutableSource has nothing to do with mutating the source. 
  - It **provides a way for multiple components to read from a source without "tearing"** (rendering conflicting things).
- ref
  - [twitter: merge useMutableSource into master branch](https://twitter.com/brian_d_vaughn/status/1237829231628828672)
# discuss
- ## useMutableSource → useSyncExternalStore
- https://github.com/reactwg/react-18/discussions/86
  - Selectors no longer need to be memoized
  - Concurrent reads, synchronous updates
  - Our goal is for all subscription-based libraries to migrate their implementations to useSyncExternalStore.

- ## useMutableSource and selector stability
- https://github.com/reactwg/react-18/discussions/84
  - The React team has created the `useMutableSource` hook as a compatibility mechanism to allow external state stores like Redux to avoid issues with "tearing". 
  - some concerns were raised about the apparent need to memoize the creation of selector functions via useCallback
- The concern is that if a library migrates to using `useMutableSource` internally, all "selector" functions written by users of that library will now have to be wrapped in `useCallback` or `useMemo` to ensure that the selector functions have stable references. 
  - This appears to be necessary because `useMutableSource` relies on function reference changes as an indication that the current snapshot value needs to be recalculated
  - If a selector `fn` changes, useMutableSource() doesn’t know if it's safe to reuse a snapshot value. (A new `fn` could select a new value - either bc it closes over new props or bc the actual function is totally different). You can memoize with useCallback.
- Daishi Kato has done some experimenting with useMutableSource, and in a proof of concept concluded that unstable selector references could cause a form of infinite loop
  - A minor clarification. It's not infinite loop, but didn't work as expected.
- While this is a very understandable implementation approach, the need to memoize all selector functions appears to be a rather painful change to how libraries like React-Redux are currently used.

- We're working on a proposal 
  - The short version is: I do think we can remove the requirement that selectors need to be memoized by adding a `selector` option that separate from `getSnapshot`.
  - `useMutableSource` will be reworked to always render synchronously, including a possible rename and some other API changes
  - It's likely that an equality check will be built in because that would simplify several end-user cases
  - The React team will publish a "shim" package to allow using this with both React 17 and React 18
- Great summary, Mark! Just a caveat regarding the first bullet: updates (i.e. `dispatch`) will trigger a synchronous render, but you can still read from Redux hooks/components during some other concurrent render, like one triggered by a router or useDeferredValue. Which means Redux can work side-by-side with concurrent features.

- ## [React Context without Provider + useMutableSource](https://dev.to/aslemammad/react-context-without-provider-usemutablesource-4aph)
  - https://codesandbox.io/s/usemutablesource-react-context-spyhu
  - 自己实现了useMutableSource

- Think of tearing as something like if we have a value(state) that A and B read from it, but somehow in the rendering, the value changes. 
  - The B component is later than A, So in Rendering, the value in the A component is 0, and in the newer component (B), the value is 1. We call this tearing; 
  - it means you see two different values in the viewport from one exact source. 
  - It's a new and hard to understand implementation in React concurrent mode

- I just wonder, if I don't want to use redux, can I use this approach for any "global" state? I'm aware that react-redux uses this internally. Currently hook stores the memorized state locally under each fiber. With this approach, I wonder where the store is placed.
  - Yes, you can use this approach, And I use it in my projects. Or you can use the better version of it, which we work on, jotai.
  - The store lives in a simple object, but we attach some useStates to it basically when we use uMS, so when it changes, we call those useStates(setStates) in the components. So no wasteful renders like React Context. Just your subscribed component is going to be changed.
- couldn't this behavior be achieved with way less code using RxJs and Observables?
  - every solution has some trade-offs, I just made a vanilla fast solution with uMS, but if you can merge the observables solution with uMS, why not, it would be great. The point of this article is teaching uMS

- ## [pr: useMutableSource (merged但不推荐使用此API_202011)](https://github.com/reactjs/rfcs/pull/147)
- useMutableSource makes it so that you don’t have semantic breakages due to tearing. 
  - However it will still deopt all concurrent mode features when it happens. 
  - So it’s not compatible with new features.
  - It’s not recommended for new tooling that wants to be concurrent mode compatible. It’s for legacy compatibility.
  - We have some other ideas for mutable multi-version stores that might prove useful for systems that want to provide full future compatibility 
  - but in the current experimental releases the only way to be fully compatible is by using immutable data.
- useMutableSource if you have either mutable data structures or if you have mutable atom where that atom lives outside React.
- If you have immutable data, storing it in useState or useReducer is preferable because it will just work with everything.
# useMutableSource docs
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
# pieces
- Given a parent and a child, both calling useMutableSource with the same source: when the source updates, what order will the two components try to read the values from the source?
  - Keep in mind that `useMutableSource` is being written for concurrent mode (not legacy sync-rendering mode).
  - So I don't think I understand why the order of subscriptions matters? The resulting React work should be batched into a single React update.
  - If an update is scheduled for both the parent and child, React will render outside->in.

- Why is it getting merged into the core? Couldn’t it be an external library?
  - This particular API needed to have hooks in the reconciler. The commits are all public so you're welcome to take a look.
  - The previous stop gap useSubscription Hook was the best that could be built in user space, and it wasn't great.
- Then the action to take should have been to enable the existing hook to better integrate with React
  - Plug-in systems suck.
  - If anything, I feel like we're learning that react should have more things built-in (not necessarily "in core" but within packages owned and maintained by the core team).
  - Having things spread out majority limits what we can do and how quickly we can do it.

- Do DOM nodes and `window.methods` (eg rAF, setTimeout, etc), fall into the category of mutable external sources?
  - window methods like the ones you mentioned? No. 
  - DOM nodes are definitely mutable but this probably wouldn't be used for them.
  - `window.location` is a mutable source though.

- there's no mechanism for tracking selector equality between components. 
  - Selectors will be run (and snapshots stored) per component+hook.
