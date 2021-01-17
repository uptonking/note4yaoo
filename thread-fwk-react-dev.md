---
title: thread-fwk-react-dev
tags: [framework, react, thread]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-06T14:40:03.364Z'
---

# thread-fwk-react-dev

# pieces
 

- ## new trend in react: there's a sizeable community within react that fears state managers, and they go through hot hell to avoid one.
- https://twitter.com/0xca0a/status/1350731142480146435
  - 批判使用多个context造成wrapper hell，而不使用类似redux管理状态
- the root cause was most likely redux 
  - people think dealing with state is complex because they're facing volumes and volumes of information. 
  - and it sure piled on when they went the "zen of state" route.
- to make it clear, this isn't about libraries giving you a provider for theming and so on. 
  - they're using context as it should be used. 
  - this is merely about app-state and splitting up what normally would be fields in your state model into multiple providers to avoid re-render.
- Struggling to see what's materially wrong with this pattern? Other than deeply nested things looking unsightly. I think calling this out as a mistake is incorrect.
  - split state up, app becomes slow, rigid, hard to refactor, once state A relies on state B you get into real trouble, if B also relies on A you face an impossibility. 
- Yeah I got pretty frustrated with using context for sharing state in a performant way. Pretty happy with Zustand.
  - I just use context for delivering non-changing instances which I guess what libraries are doing too.
- Though Provider is helpful for implementing server side rendering, where it makes sense to have a store per request, rather than a singleton store

- ## But first be able to explain why you don't like passing props multiple levels
- https://twitter.com/markdalgleish/status/888213730265153538
- Also, explain why you're creating so many component layers when a single component will do just fine.
  - From experience, it's probably because their components import their own child components directly rather than accepting children as props.
  - I think it has to do with your approach. I fell into the trap at first of trying to make a neat little component for every box on the page
  - Nowadays I always start with a single component and take the top-down approach. Don't create a new component until I absolutely need to
  - Having lots of small components for page layout is amazingly expressive, they just need to be composable, accepting children as props.
    - Building out a living style guide of React components is a great way to force this architecture.
    - I've been working on something like this these last of couple months and it is an amazing workflow.
    - With well thought out component APIs, updates are a breeze. I absolutely love it.
- This is why I love the render prop on Route so much. No need for extra components just for URLs
  - I've been thinking on this angle for glamor/ the css prop/ programming workflow in general. when it's make it work -> make it right.
  - I tend to get to prod faster, but if I try to make my abstractions before making *something* work, I tend to have a bad time. 
  - Exactly. Problem with Just JavaScript is our tolerance for big classes is way less than big templates. Have to fight the abstraction urge.
