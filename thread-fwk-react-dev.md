---
title: thread-fwk-react-dev
tags: [framework, react, thread]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-06T14:40:03.364Z'
---

# thread-fwk-react-dev

# pieces

- ## 

- ## One interesting thing we found when researching my last article is that every framework's version of this React code logs different things when you click the button
- https://twitter.com/RyanCarniato/status/1353801009844240389
  - Which are more correct
  - React: "0 0 0"
  - Vue 3: "1 2 0"
  - Svelte: "1 0 0"
  - Solid: "1 2 2"
  - [5 Ways SolidJS Differs from Other JS Frameworks](https://dev.to/ryansolid/5-ways-solidjs-differs-from-other-js-frameworks-1g63)
- well a major difference between the svelte version and the react one is that with the react code everything has to pass through the whole update cycle, whereas in svelte count is just a variable and ++ mutates it in place, or rather at the next ; 
- Imho, react has made the best decision here because it takes care of the worst case scenario(Multiple state changes are batched into one state change preventing multiple rerenders).
  - Also, This behaviour is noted well in the docs and is mostly associated with event handlers.

- ## How do you decide when to split up a component? 
- https://twitter.com/MichaelThiessen/status/1165241262494167043
- TL; DR: when you need to, but not before.
- I generally split into list and listItem components so every v-for iterates over listItem components. Because there is always this moment when you need a computed value for these list items.
- When I feel a component does more things than it should, when a component gets too big (200+ lines), when a component has too many props

- ## What are some React anti-patterns that you encounter often? Why are they dangerous?
- https://twitter.com/TejasKumar_/status/1214259916376027137
  - Code mutates props.
  - Code modifies state directly.
  - props.key is read inside a component.
  - Keys duplicated among siblings.
  - Event handler returns false to prevent default.
- Putting too much logic in event handlers. This goes for any framework, though.
- Putting too many responsibilities on a single component. This is often represented by too many states, too many props, large render function, or too many instance functions.

- ## why use react for threejs?
- https://twitter.com/0xca0a/status/1282999626782650368
  - same reason you use it for the dom.
  - three arguably is even more unruly than the dom as every "thing" is wired into everything. 
  - the snapshot is from my react-europe talk, a simple search for "cube" (yellow) reveals the difference  
- threejs: cube affects *every* aspect of the app: setup, state, view, resize, events and render, it is not re-usable at that point. 32 hits. 
- react: a re-usable self-contained self-cleaning component and one invocation.
- this is not a dig at the dom or three. these are imperative systems and im glad they don't add high level features, because that's not their domain. react simply expresses sth imperative in a declarative way with a common ground that makes management and sharing much easier.
- r3f does the same for three that react-dom does for the dom, updates or not. you can write small-ish vanilla dom apps relatively clean, in three that is less likely bc a "thing" always has to reach everywhere to function.

- ## the magic of react has always been that
- https://twitter.com/0xca0a/status/1353659846202159109
  - if you eliminate the technical hinderances, then you can transfer an idea to the screen directly, you can worry about the things that actually matter, be it design or otherwise.
  - https://codesandbox.io/s/cell-fracture-forked-3rjsl
- https://twitter.com/0xca0a/status/1341811710081044483
  - a tutorial on working with @glTF3D in @threejs_org & React.
- vue/svelte/ng were made for the document object model. 
  - vue now has renderers, svelte, i don't ... think so? 
  - react saw it coming and anticipated for a future where renderers transcend(超出；胜过) platforms many years ago.

- ## Use `React.useMemo` instead of multiple `React.useCallback` s to create an object of handler functions in a custom hook. 
- https://twitter.com/kyleshevlin/status/1352639659147456512
  - [memoizedHandlers.js](https://gist.github.com/kyleshevlin/08a2deb904b79077e46966567ccabf06)
  - Makes it super simple to make a whole bunch of methods stable, preventing unnecessary rerenders

``` JS
function useBool(initialState = false) {
  const [state, setState] = React.useState(initialState)

  // Instead of individual React.useCallbacks gathered into an object.
  // Let's memoize the whole object. Then, we can destructure the
  // methods we need in our consuming component.
  const handlers = React.useMemo(() => ({
    setTrue: () => { setState(true) },
    setFalse: () => { setState(false) },
    toggle: () => { setState(s => !s) },
    reset: () => { setState(initialState) },
  }), [initialState])

  return [state, handlers]
}
```

- But why not just call setState? It's not normally getting redefined, is it?
  - The purpose of the hook is to expose an API.
  - We don’t want the consumer to be able to do just anything with setState, such as pass it a non-Boolean value in this case.
- Definitely really nice. It’s type safe and prevents inline functions to be used. I just replaced every bool state in our new project at work with that pattern 
- Nice little pattern right here, never thought about callbacks this way before. Not even sure why `useCallback` is favored over `useMemo(() => …)`. The former seems to cause more confusion than the problems it solves.
- Neat. I'd still `useCallback` for functions with non-overlapping dependencies. 
  - Otherwise, other callbacks would get recomputed unnecessarily.

- ## re: context vs redux debate
- https://twitter.com/dai_shi/status/1351351537751126018
  - If one would compare useReducer+useContextSelector vs React-Redux, it would clarify what Redux and its family offer.
  - Note use-context-selector no longer depends on any hacks, it just uses ref+subscription, like react-redux.
- By the way, we could use Redux in React without Context.
  - Just like zustand, a react hook could subscribe to a Redux store directly.
  - My reactive-react-redux v5-alpha follows this pattern with experimental useMutableSource.

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
