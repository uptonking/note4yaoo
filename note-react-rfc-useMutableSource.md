---
title: note-react-rfc-useMutableSource
tags: [react, rfc]
created: '2020-07-17T06:00:22.244Z'
modified: '2021-01-04T17:05:20.422Z'
---

# note-react-rfc-useMutableSource

# faq 

- How come this API isn't merged with useRef? (Both are used for  managing mutable, usually external data.)
  - useRef has constraints. 
    - Essentially (with the exception of lazy initialization) you should only mutate refs during the "commit phase" (within useEffect or useLayoutEffect).
    - Refs are like instance fields on class components. They let you e.g. compare next and prev props
    - They aren't meant for sharing values with other components. 
    - Because of their constraints, they're safe to use with concurrent rendering.
  - useMutableSource is for reading from mutable sources that you either don't control (e.g. window.location), or sources that may be mutated anytime (e.g. a click event might dispatch a Redux action).
    - useMutableSource has nothing to do with mutating the source. 
    - It **provides a way for multiple components to read from a source without "tearing"** (rendering conflicting things).
  - ref
    - [twitter: merge useMutableSource into master branch](https://twitter.com/brian_d_vaughn/status/1237829231628828672)

# guide

- [pr: useMutableSource (不推荐使用此API_202011)](https://github.com/reactjs/rfcs/pull/147)
  - useMutableSource makes it so that you don’t have semantic breakages due to tearing. 
    - However it will still deopt all concurrent mode features when it happens. 
    - So it’s not compatible with new features.
    - It’s not recommended for new tooling that wants to be concurrent mode compatible. It’s for legacy compatibility.
    - We have some other ideas for mutable multi-version stores that might prove useful for systems that want to provide full future compatibility 
    - but in the current experimental releases the only way to be fully compatible is by using immutable data.

# useMutableSource

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
