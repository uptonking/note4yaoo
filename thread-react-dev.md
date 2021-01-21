---
title: thread-react-dev
tags: [react, thread]
created: '2020-12-25T15:22:27.224Z'
modified: '2021-01-06T14:40:11.360Z'
---

# thread-react-dev

# pieces

- ## 
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
