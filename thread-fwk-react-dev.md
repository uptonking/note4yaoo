---
title: thread-fwk-react-dev
tags: [framework, react, thread]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-06T14:40:03.364Z'
---

# thread-fwk-react-dev

- 关于react的特殊用法、架构设计、与其他框架的联系区别

# pieces

- ## 


- ## can I virtualize an array of @reactjs components?
- https://twitter.com/sseraphini/status/1362502418781642755
  - I'd like an API like this:
  - `<Virtualize> {arr.map(a => <Item key={a.id} a={a} /> </Virtualize>`
- What do you mean by virtualize?
  - I’d like to stop rendering them on DOM to make the page light
  - For offscreen elements? Or something else?
  - Yep, offscreen ones
  - Offscreen elements are deprioritized in React. But that would be a great challenge, since you'd end up destroying and recreating elements every time it left the viewport.
  - But that would be a interesting feature for React.
  - We could check for an element position in the viewport, and check if it's inside it. And not render elements outside that viewport. But that would make the components mount/remount every time.
- replace react-window/virtualized with react-virtuoso
  - removed a lot of boilerplate code!


- ## Does anyone else add `console.log()` or `debugger;` to their components in the middle of a debugging session so that Fast Refresh picks it up?
- https://twitter.com/dan_abramov/status/1362549600511483917
- I sometimes add a console log so I can look at it's arguments in the debugger because it's easier than looking at a massive list of props

- ## One of the challenges of building React component libraries is to not impose any specific styling solution to the App code.
- https://twitter.com/pomber/status/1362125599607820290
  - My approach is to use a `classes` prop
  - That makes the component interoperable with almost all styling solutions.
  - 本已有10种方案，作者又提出了一种，于是有了11种方案；更应该参考大公司方案
- I like this approach a lot, I have this same problem with my company’s component library used in multiple apps with different styling solutions, 
  - I initially used Tailwind but ended up ditching it and providing behavior only components without styles

- ## I envy the mental capacity of folks who can be productive prototyping with single-file components.
- https://twitter.com/dan_abramov/status/1361792509601607685
  - React lets me write garbage code (for prototyping) and I love that. 
  - Got a single 1K line file, ~10 components, changing their names/structure all the time. 
- I'm not sure what the difference is here. At least in Vue, single-file components allow you to do the very thing that you describe for prototyping:
  - Everything in one file? Check.
  - Define multiple components in the same file? Check.
  - As a React and Vue user I can relate
  - With Vue SFC I really have to plan the components in advance; 
  - sometimes I get it right, sometimes I get it wrong, 
  - but refactoring them is painful. 
  - Meanwhile with React I can just refactor them like normal functions
- It's exactly the opposite for me - I split into smaller files to navigate more easily. 
  - I envy the technical skills of people who are able to navigate 1K line file productively
- A big file doesn't mean your code is garbage. 
  - You will know its boundaries better after a while and you can split it up and give it good names. 
  - But that's usually the path towards good code. 
  - Premature organization by arbitrary rules can make it harder to see better patterns.
- I prefer react style allowing me to compose multiple components in one file, especially when it's something like a drop-down component, or something where I may not reuse some of the other components.
  - I like embers conventions for structures and uniformity, and then I like svelte for the simple and fast dev process.

- ## how to debug @reactjs components?
- https://twitter.com/sseraphini/status/1361300393544855554
  - console.log props and state
  - console.log inside useEffect
  - console.log
- How to debbug JS:
  - Old school - alert
  - New Kids on The Block - console.log
  - Bonkers - debbuger; 
  - Noobs - Dev tools
- I prefer debugger, or debugger statements, which is basically flexible console.log
- Break points (debugger) is the only way I debug anything in any language.
- Devtools. Breakpoints
- useDebugValue to custom hooks

- ## I smell an antipattern.
- https://twitter.com/erikras/status/1361606811971952641
  - I’ve got two third party custom hooks that want to give me a ref to give to an element so that it can do fun stuff to the element.
  - The problem is I want to give both refs to the same element. 
- Libraries should almost always accept, not create, refs IMO
  - How do libraries know when these refs resolve?
  - The same way we all do? In a useEffect.
- This is a good reason to stay away from react-hook-form and instead embrace the glory that is react-final-form!
- mergeRefs utility function to the rescue.

- ## What are the major changes to the ecosystem since 2018?
- https://www.reddit.com/r/reactjs/comments/lg92yi/what_are_the_major_changes_to_the_ecosystem_since/
- Biggest things:
  - React hooks changed how we write components, along with increased use of the new Context API (which has also led to confusion over when and how to use Context effectively)
  - Redux is still most widely used state management tool, but there are many other good options
  - Redux Toolkit and React-Redux hooks drastically simplified writing Redux code
  - New libraries like React-Query and Apollo that focus on "data fetching/caching" instead of "state management"
  - Next and Gatsby joining CRA as major "React distributions"
  - Switch from Enzyme to React Testing library and more "integrated" component testing
  - Widespread use of TypeScript (>50% usage in the React community at this time)

- ## 3 Rules for Keeping Components Organized
- https://www.seancdavis.com/blog/three-rules-keep-components-organized/
- Rule #1: Separate Source Files into Logical Buckets
  - I prefer to separate components by the role they play within the larger application.
  - Even though layouts, templates(container), and blocks(comp/element) are (or could be) all technically a type of component, I like keeping them separate from one another. 
  - some frameworks — Jekyll is one example — are more opinionated about where you place your components without some custom configuration. 
  - (With Jekyll, components are more like partial templates, which they call includes). 
  - In cases like this, it's usually a good idea to use the framework's defaults.
- Rule #2: The Top Level is for Shared Components Only
  - Many times a component is only used in one place, by one other component. 
  - In that case, it isn’t necessary for that component to be exposed right in the primary components directory. 
  - Instead, it could be nested within the directory of the component that uses it.
  - the top-level of a directory of components should be in use either by more than one other component or by some other type of component.
- Rule #3: Supporting Files Live Alongside their Component(s)
  - Knowing that all supporting files are in a directory along with a component saves me a lot of digging around.
  - Supporting files include stylesheets, client-side scripts (for server-side components), or utility files (like adapters and transformers).
  - I have found it much more efficient to group a component with all its supporting files rather than grouping types of files together. 
  - I've found it easier to locate pesky issues by keeping styles and scripts decentralized and closer to the thing they are affecting.
  - That said, this requires some additional diligence on your part to ensure you're scoping those supporting files in such a way that they're only affecting the necessary component(s).

- ## The browser is the source of truth when it comes to the URL. 
- https://twitter.com/mjackson/status/1356713777526263808
  -  Any time you read it and put it into memory (like Redux) you risk getting out of sync. 
  - Your Redux store is not the source of truth when it comes to the URL.
- Remember: the user can change the URL without you ever knowing about it. They can either:
  - hit the back button or
  - manipulate the address bar directly.
  - You can't stop them. Once they do, the URL has changed. If your source of truth is Redux, you're now out of sync.
  - The only thing you can do is react to a change in the URL.
  - To effectively "prevent" navigation, you must be able to undo the navigation they just did. This is not easy to do, but it's possible in most cases using histry pkg
- i think the main appeal to copying any sort of external state into redux was so that you can join it with other data already in redux (in mapStateToProps) but i don’t think this is necessary anymore given hooks. makes it much nicer to compose state at the component level
- one can also say the the url is just a side  effect of being in the current state. Kinda like saving a bookmark. Now source of truth is your app, and in state X it sets url Y and renders DOM Z

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
- I work in React almost exclusively now, but I have to admit that classes add a lot of clarity to state in components.
  - *However* having worked on the Angular team, particularly in the engine/compiler, I can tell you that classes are a double-edged sword because of inheritance.
  - People subclassing subclassed components. 
  - Class-based components in web frameworks tend to have some static traits. 
  - There's a lot of dancing around how to propagate that through inheritance in a way that makes sense.

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
