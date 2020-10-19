---
title: lib-react-table-latest-roadmap
tags: [react-table, roadmap]
created: '2020-07-14T06:59:25.968Z'
modified: '2020-07-14T12:07:15.486Z'
---

# lib-react-table-latest-roadmap

## ref

- [[Umbrella] v7 Stable Release ](https://github.com/tannerlinsley/react-table/issues/1964)
  - Fix row-selection bug (#1900)
  - Consider Col/Row-span plugin requirements (not the actual plugin) (#1342, #1933) (Non v7 release, but soon after hopefully)
  - Ensure no infinite rendering loops like in #1911
  - Ensure prop getter utilities and column decorators can and will generate stable callbacks and values (#1936)

## work-in-progress

- 20200923
  - I'm currently planning React Table v8 and an entire dedicated course for it.
  - It's possible that when v8 becomes available, I might only allow my Github Sponsors access at first and even give away free courses to all of my sponsors similar to React Query Essentials.

## react-table v8

- [WIP v8 pr 2335](https://github.com/tannerlinsley/react-table/pull/2335)
- The external API in v8 will be almost identical (with breaking changes for only a couple of apis, mostly around controlled state).  
- Other breaking changes will be focused around the plugin system as well, but only in boilerplate structure and types.

- [WIP v8 pr 2166](https://github.com/tannerlinsley/react-table/pull/2166)
- This PR is likely v8. It's been refactored to something that is much easier to understand and maintain. 
- More notable **differences**:
  - What were "core" plugins are now native to the useTable hook
  - All of the new core functionality is now more tightly integrated, way more predictable. 
    - All core features are "always on", but not always active, making them easier to test and type together
  - A new plugin-system style is being born, but is not yet complete. 
    - It will likely involve simply extending and composing the options object that is passed to the useTable hook
  - The table instance has a much better and fully-formed api that should allow full control over most features of the table, including column, row, and even cell-level operations
  - State is now much easier to control from fully-automatic, to partial opt-in, all the way up to fully controlled. 
    - Some things are still not controllable, but the system would be much easier to extend to make that happen now.
  - Better support for building dedicated expander and row selection columns
  - Much of the API has been rearchitected to be lazy (but still memoized), meaning that basically everywhere, you'll see a lot of getter functions. 
    - This actually ends up improving render performance quite a bit, since we can set the getter functions really early on when we build the row/cell model even though the final state those getters will return isn't ready yet. 
    - That also means we don't have to re-loop over the rows and cells later on (which is a ton of extra wasted looping) to do it then.
- react-table was using setState pattern earlier and migrated to useReducer, and back to useState again in v8
- It is easy to set state using setState pattern more in imperative style. 
- And with useReducer pattern it is easy to define different actions and is useful in collecting feature usage stats/analytics.
- The main benefits actually haven't been shown yet as this is still a WIP. But for starters:
  - Much less code, at least for our case. If you look at the migration, the logic inside of useState is exactly the same as useReducer in most cases, and also, since it lives inside of the context which it is in, the access to the instance (or getInstance makes more sense here.
  - It's very probable that the concept of updating table state is about to change internally as we externalize some or most of the table's core to a non-react instance factory.
  - Even though it's setState, it's a special flavor, one that is able to pass action types, action meta, etc, so aside from the syntax, the benefits at the end of the day are the same as a reducer, except it's more ad-hoc, which is perfectly suited for plugins and users IMO.
  - Yes, we could expose an action that replicates useState in the reducer, but if you noticed, for every action we had, we were also exporting a companion proxy method on the instance that does the same thing and most times is way more reliable than calling the action itself. Getting rid of that layer makes things way more direct
  - Again, this is all subject to change. This is the stage we're in...
