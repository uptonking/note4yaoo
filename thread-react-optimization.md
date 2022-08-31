---
title: thread-react-optimization
tags: [job, optimization, react, thread]
created: 2021-09-24T06:50:13.642Z
modified: 2021-09-24T06:50:31.330Z
---

# thread-react-optimization

# discuss
- ## 

- ## React tip: when conditionally rendering component based on some string enum (like a role), use an object to map enum values to components.
- https://twitter.com/DavidKPiano/status/1564950527477252098
  - This can be cleaner than using conditional operators, and it keeps the logic organized & clear.
- Honestly, I like to use objects instead of the switch statement, it's more clear and easy to add new options
  - Surprisingly, it's faster too! JS doesn't optimize for switch statements I believe (O(n) instead of O(1)), so many case statements can have a noticeable performance impact.
  - [Is a hash faster than a Switch in JavaScript?](https://www.davidbcalhoun.com/2010/is-a-hash-faster-than-a-switch-in-javascript/)
  - It comes down to the fact that switch statements in JS don't use jump tables (AFAIK).

- the "object map lookup" pattern (whatever you want to call it) is extremely useful and more concise than switch/ternary/if-statements IMO

- Relevant not only for React, but for any switch/case or if/else logic in JS, when you're mapping one set of values to another
  - This should not just be a react tip but a programming tip. Use clear mappings vs long conditional statements. #developer
  - I believe this is called the “Strategy Pattern” 

- This is a great pattern, and works really well with dynamic imports which reduce the bundled JS size and load time. 
  - Why bother loading the views for the roles that cannot access those components?

- I'm hoping https://github.com/tc39/proposal-pattern-matching happens soon enough for the more complex cases where you can't express as key+value map.

- I think this works for RBAC, but in general for more complex apps (especially B2B apps) I wouldn't recommend using roles this way.
  - Instead, you often look at permissions — e.g., if `hasPermission(user, EDIT, Product)`, you get `EditorView`; otherwise you get `DefaultView`.

- A functional alternative. It is possible to extend the "when" function with lazy imports (dynamic imports).

- ## helping someone debug react perf got me thinking about a generic high-level approach
- https://twitter.com/_paulshen/status/1441177985512468485
- 👉🏻️ Identify the cause of react rendering. 
  - This is usually some form of `setState` - could be in a lib (eg react-redux). 
  - React isn't going to rerender your app just because it feels like it
- 👉🏻️ Identify why the update is needed. 
  - What state is changing (if any)? 
  - What in the app cares about this change? 
  - How does the UI change and what are the side effects?
- 👉🏻️ Use profiler (or console.log) to see what code is actually running..
  - What components are rendering? Where is time being spent? (use react devtools/chrome perf)
  - What is diff between what needs to run vs what actually runs? 
  - If only parent component reads the state, do its children need to update? Most optimization is making this diff smaller..
- 👉🏻️ Change the code so that less code is running on state updates. 
  - There are a lot of strategies I won't dive into here - memoizing, React.memo, restructuring children, creating smaller global stores (eg redux), moving state outside react's purview, etc..
- 👉🏻️ There are also optimizations around reducing number of React updates. Strategies include throttling and batching (upgrade to React 18 or `unstable_batchedUpdates` )
