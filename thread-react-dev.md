---
title: thread-react-dev
tags: [react, thread]
created: '2020-12-25T15:22:27.224Z'
modified: '2021-01-06T14:40:11.360Z'
---

# thread-react-dev

# pieces

- ## 

- ## how to trace which component is suspending in React so I can put a Suspense wrapper around it?
- https://twitter.com/fakenickels/status/1364921351820181512
- tired: Suspense wrapper, wired: Suspenders
- debug stopping at every error since suspense is basically throwing a promise from a component?
- I *think* the dev tools might tell you what suspended.

- ## Once upon a time, there was discussion and PRs that tried to add a third "root state" argument to `combineReducers` , so that slice reducers could read other slices if available:
- https://twitter.com/acemarke/status/1363547923963863046
  - But, we finally gave up on that idea. Still feels potentially useful, though
  - [Feature Request: Allow reducers to consult global state](https://github.com/reduxjs/redux/pull/1768)
- There's been at least one time in the past where I wanted two reducers but went with only one because one of them would need access to the other's state. I can't honestly remember the exact situation though.

- ##  `<Context.Provider value={<SomeJSX />}> <Stuff /> </Context.Provider>` .
- https://twitter.com/dan_abramov/status/1363134687250636800
  - Haven’t used this pattern before, but it’s kind of neat? If you want to pass some piece of UI deeply down without passing props themselves. 
  - Sprinkle(撒，洒) useMemo on JSX node to avoid extra re-renders.
- We use this pattern in our design system. 
  - We have a 'linkComponent' prop on the provider so you can customise how links are rendered, e.g. wire them up to your router, add analytics, etc.
  - [BraidProvider](https://seek-oss.github.io/braid-design-system/components/BraidProvider/)
- May be the first time I've read a facebook dev acknowledge that we actually want to avoid extra re-renders.
  - I mean specifically in this situation (pass some context deep down). 
  - I am not proposing that one should micro-optimize every single component, which is how people tend to interpret this.
  - The rule of thumb is pretty simple — if it makes an interaction faster (as measured by profiling) then do it
- We use multiple vue apps, which the equivalent would be provide/inject, but using this makes components hard to reuse sometimes as they depend on data that sometimes isn't there. 
  - Best to keep this down to globals that are relevant to the entire app, not just a specific component.
- We do this at Stripe to make sure the correct legal text gets shown in our various signup flows. It's also handy (with some extra complexity) for implementing ReCAPTCHA.
- Isn't it just equivalent to container or layout component?
  - Yea, pretty much, although that’s usually done with props rather than Context
  - Yes. Basically a replacement of Container components suffering from prop drilling? But a neat pattern, not sure why I never thought it's possible 
- Interesting. Provider which instead of controlling data, controls rendering. 
  - So the client gets baked ui which is black box for him, the only think is to show it where or when we want.
- I have followed this pattern when I created a generic table component (wrapped in a provider). 
  - When using an instance of such a table, the developer can define different types of columns (column displaying a url link, checkbox column, date column...etc)
  - These different types were f columns are essentially jsx components I’m sending back to the table provider which then renders them as content of my `<td>` .
- Creating modals on demand through redux or context, including react elements, callback function etc. I really like it.

- ## Should You Use useMemo in React? A Benchmarked Analysis.
- https://twitter.com/tannerlinsley/status/1362119303793844226
- It's true that useMemo is not free, but IMO this article is somewhat misleading. 
  - The reason the slowdown for initial render gets so large is because this benchmark returns that huge object from useMemo (so it's being stored!) 
  - It's not algorithmic complexity but memory cost.
  - In the example with n = 5000, we have 10000 components, and each of them stores an array with 5000 objects in it. If you look at the Memory tab, this gets our page to 1GB memory usage! At that point it's not that surprising it would slow down.
  - If we return a primitive value from useMemo (e.g. result of an expensive calculation — which is what it's meant for), the perf gap almost disappears in my testing.
  - So yes, useMemo may slowdown because it uses computer memory, and holding onto 1GB might not be the best idea.
  - There is still a broader point about unnecessary useMemo being unnecessary, but the claim that it by itself causes such a drastic algorithmic slowdown on first render doesn't appear to be true. But holding onto large objects — and lots of them — does have a cost, useMemo or not.
- But using useMemo not just for a value or loop but to memoise the children when there's loads that rarely need to rerender would be super beneficial and not covered here? Also (not sure on this) but when fetching data from an API it would help (when not using some other lib).

- ## Is there still no answer to composing forwarded and internal refs in React?
- https://twitter.com/ryanflorence/status/1361519704821538820
- what is the core use case behind needing this? 
  - When you want to use the ref within your component but also want to allow component user to pass a ref
- I always just used callback refs like so.

- ## saw so many tweets about how cm and suspense are useless etc. 
- https://twitter.com/0xca0a/status/1358703189428752384
  - if you have ever tried R3F you know how it simplifies things that otherwise would cost you an arm and a leg. 
  - FE & forms will gets the same benefits, try it if you can, it's a paradigm shift. 

- ## Anyone ever used Preact without using internal state at all?
- https://twitter.com/_developit/status/1356068911263977472
  - Thinking about using an FSM for state management and then just calling `render(<App {state} />, el)` on state changes.
- Main issue is that you'll only ever be triggering whole-app renders. 
  - With state, only the subtree with changes re-renders. 
  - For a state machine approach I tend to subscribe components individually, even if all they do is call `setState({})` on themselves.
- And if you use a non-vdom library, whole app re-renders might even be cheap 
  - That depends on reference equality bailouts same as VDOM though. 
  - In both cases, a top-level rerender with entirely new data is worst-case perf.
  - There should be far fewer such checks in a sparse tree of template bindings than a full vdom tree. It would be less by the ratio of bindings to leaf DOM nodes.
  - true, assuming minimal composition of templates.

- ## I've come to believe that the base React Hooks should always be used inside of a custom hook 
- https://twitter.com/kyleshevlin/status/1354845869246476290
  - to provide encapsulation and context to the concern
  - IME, 2 things are true
  - there’s never a use of useEffect that couldn’t benefit from a good function name
  - Re: the other hooks, they almost always come grouped together, ie if your managing state, you have some callbacks to handle that state.
  - Put ‘em in custom hooks.

  - Don’t worry if the hooks are reusable, that can come later.
    - By putting all the elements related to a concern in a custom hook, you can focus on the API you want your component to use. 
    - You can hide implementation details your component doesn’t need to know.

  - [useEncapsulation or Why Your React Components Should Only Use Custom Hooks](https://kyleshevlin.com/use-encapsulation)
    - A custom hook is just a function and functions are structures we can use to encapsulate the related elements of a concern and expose an API to our function's consumer.
    - Take notice, our Component now only consumes custom hooks. 
    - Another benefit of this pattern is that dependencies quickly become obvious because they end up being arguments to our custom hooks.
    - By adding this layer of abstraction between our component and the standard React hooks, we can change the implementation of our custom hook's API without changing the component. 

- Something that could help writing components like this.
  - The hook can still live in the same file, declare it at the bottom rather than the top with a "function declaration", or attach it a static property to the component.
  - If it becomes reusable, move it to a separate file.
  - Yeah, I would never move it to a new file _unless_ it was intentionally reusable.

- ## Do you push a new history entry onto the stack? Replace it?
- https://twitter.com/tannerlinsley/status/1355570411803602946
  - And on top of all of this, provide an API that feels like setState, a reducer or state machine?
  - I realize that very few apps actually ever deal with this type of router state… But still, why is it so hard.
  - Which brings me to another point, after dealing with dashboard state for a very very long time now, I am very convinced that it most closely resembles a massive tree of deterministic State machines.
  - This begs the question: should the state live in a machine and get synchronized? Or should it live in the URL?
  - From experience, when the state actually lives in the URL, it becomes very difficult to rely on read and write consistency. Then add a router abstraction in the middle?
  - 描述了很多urlstate处理的经典问题，并且没有标准答案

- ## I recently had to implement a feature where the user could download a png of a div. I came across html2canvas which did the trick perfectly
- https://twitter.com/bmullan91/status/1220659214848229378
- We did something similar to download a chart back in 2015, the result was almost the same but It did broke css a bit. 
  - At the end we preserved that approved because it was way easier to do it in the frontend than moving the logic to the backend. I recommended it.
- I did something like this but for code screenshots before I know carbon existed 

- ## Am I right in thinking StrictMode’s second render swallows console.logs?
- https://twitter.com/mattgperry/status/1352000290241859590
- Yeah, I believe they added this to not pollute the console.
- Ye, this is imho actively harmful - duplicated console.logs might be confusing at first but they dont lie and actually incentivize people to think about purity, concurrent mode etc

- ## I’ve seen React libraries that return elements as objects with $$typeof, while others return them with React.createElement. 
- https://twitter.com/jon_neal/status/1351512951337967619
  - Are there performance considerations?
- If you want to be compatible with React and Preact, publish it as JSX and let people transpile your library with their JSX pragma.
- I would be wary(谨慎的，小心的) of both approaches here. 
  - The $$typeof check will fail in environments without Symbol (react uses a numeric constant), 
  - and both could change in a minor version (they're not part of the public API).
- Though I'll say, if you genuinely need to produce cross-compatible VNodes, your codepen is pretty clever. 
  - It will have a potentially large performance impact though, since property access into Virtual DOM elements will become polymorphic instead of monomorphic.
  - Another option would be for the community to standardize on a "vdom provider" package that libraries could import, which users of a library would be required to alias to their desired implementation. 
  - All of these solutions get more difficult when you factor in state/hooks/etc.

- ## Underrated JSX feature; text interpolations without any extra syntax/quotes/whatever. So good.
- https://twitter.com/threepointone/status/1350174511883300876
- I used to hate this, but looking at it from a design perspective, 
  - this makes a ton of sense and like the issue mentions is great for internationalization
- This is something I missed when I tried using Reason React
  - And the fact that I had to google for like a fucking hour to find the correct binding in order to map over my todo list

- ## the React model of All-in-JS components where HTML and CSS live inside your JavaScript module.
- https://twitter.com/horse_js/status/959908677074513921
- HTML is okay... but CSS should not be inside JS

- ## browser's built-in form validation features are surprisingly robust. 
- https://twitter.com/housecor/status/1330871889867264004
  - Declare attributes like required, min, max, minLength, maxLength, and pattern (regex) on fields.
  - Call checkValidity() to validate. 
- indeed! React devs may forget that you don't have to do this all in JS. 
  - and it turns out that it can be quite a lot less code as well!

- ## Frontend Devs, if you were writing a new UI from scratch, would you use @reactjs or @vuejs  and why?
- https://twitter.com/SENDYYeah/status/1247568314492018688
- I'm not saying @reactjs is the best, but more to personal preference. 
  - After tried both of them for some projects, I feel react project is easier to read and to maintain.
  - JSX force us to put everything in a single language, JS, CSS, HTML all in JS, the thing that scares newcomers
  - After months of grieve for the lost of directives in ReactJS, I tried vuejs and maintenance a project
  - I understand that JSX fits me better than Vue approach, 

    - JSX makes me able to read logic easier, 
    - you put everything **explicitly**, any logic, even for CSS styling on your components.

  - With ReactJS, you have to read everything in JS (or TS), no directives, no binding, nothing to hide
  - some vue solutions makes us easier, but sometimes it took longer to code

    - react be like "tell your JS to return a component with this"
    - vue "tell your component to do a JS work and return a new component with this"

- ## I almost get the perception on here that react it's like the new "jQuery" now._202008
- https://twitter.com/CerovacBogdan/status/1299308881521377280
  - Is it assumed that most FE devs know a bit?
- I was on and off and now again a bit on, 
  - but I would not dare to say that it is the new jQuery as it requires much more specific knowledge (JSX one of them). 
  - But yes - Wordpress does use it - and with it's market share - it has the potential to become new jQuery
- When I was starting out, it was the go-to once you knew some fundamentals. 
  - But, it seems people don't spend as much time with libraries now and jump straight into frameworks like React
  - Did JSX pose a hurdle(障碍；栏杆)?

    - Agree :) I try to be vanilla now, jQuery was golden for cross-browser DOM mngmt. and abundance of plugins. 
    - Maybe if we look at React in that light... I see the benefits of ALL-in-JS in complex context that needs code-reusing etc. 
    - but for simpler "doc's" I still prefer raw HTML+JS

- ## list: How do you manage API calls in react_202101
- https://twitter.com/_Adyasha8105_/status/1347978564251963392
  - Using a library like react-query 
  - or your own custom hooks 
  - or just plain fetch/Axios calls in components or inactions? 
  - What's the best way to go forward
- Short answer: react-query
  - Long answer: Axios was my base. 
  - I found state is kinda tricky when there’s too many request or components with CRUD operations (introduced xstate). 
  - then I realized a cache could help to improve UX (added react-query) 🙃. 
  - Start simple then build up
- I also created my own generic http class wrapper so if I want to swap between fetch, axios or something else, I won’t have to change in multiple places. 
  - have not tried React Query but it looks cool...
  - I just always am cautious of abstraction lib dependencies.
- I have not worked much in React But Axios did the work I needed
- I build a gateway per api 
  - so that all calls to the api go through one entity (in case the contract changes) and it extends a class that makes the actual calls with fetch. 
  - I use redux actions to call the gateway method. Will look at react-query though!

- ## JSX is an abomination(令人厌恶的事物).
- https://twitter.com/justinfagnani/status/1246514699341983744
  - You can't write a literal <, because that opens a tag, 
  - but you can't write &lt; either because JSX isn't HTML and doesn't support entities. 
  - You also can't write HTML comments, or use `<template>` .
  - JSX is clearly unsuitable as a general way to write HTML in JS.
- You can't event put a < inside of a string inside a JSX expression
- There are alternative ways of expressing DOM in JS though. For example: domz
- Recently ran into not being able to use `<template>` in React/Angular. 
  - Workaround is to use `dangerouslySetInnerHtml/[innerHTML]` . 
  - After that make sure that the sanitizer does not strip your Custom Elements
- JSX isn’t even made to “write HTML in JS”

- [My 5 Tips in Building a Design System](https://twitter.com/frostyweather/status/1087380930417840128):
  1. Build components without business logic, but hooks for data.
  2. Build UI components for/from products, not in the abstract
  3. Should be easy to onboard/understand
  4. Create code guidelines early on
  5. Strong processes involved = strong DS
  - I would add early and often 'collaboration' with the dev team to stay aligned.

- ## Unit testing a react component is a waste of time in 99% 
- https://twitter.com/oleg008/status/1235358013495676928
- here is why
  - React components are useless without React or a compatible runtime. 

    - You can see components also as "plugins" which together with the runtime make a framework and then an application.

  - React handles a lot of its side effects like hooks and rendering. 

    - Without all those things, most of the component code should be pretty dumb. 
    - If it's not, you should extract that logic into a separate function.

  - Once all your components are pretty dumb, there is no point in unit testing them, because it's like testing a configuration.

    - What you should be testing though if your component works as expected for an end-user.
    - which means you need functional or e2e tests. 
    - Depending on your use case it can be cypress and co, jest with JSDOM  or anything else that renders your component using React and validates the result same way a consumer would do.

  - Snapshot tests are rarely useful because they test only an HTML output of a component, 

    - which is ok if your user actually consumes HTML as a text, 
    - but most of the time this is not the case.
    - Your typical users in the browser see a DOM rendered presentation of your components, which includes all side effects, interactions and transitions and you are not testing those with snapshots.

- Unit tests are useless 99% of the time. It has nothing to do with react
  - I disagree with that. They are great for complicated functions.

    1. Making clear how they are supposed to be used
    2. Ensuring they work for the intended use cases.

  - Obviously no guaranties outside the unit bu thats expected. React components are a special case.
