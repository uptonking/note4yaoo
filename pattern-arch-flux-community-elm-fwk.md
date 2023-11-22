---
title: pattern-arch-flux-community-elm-fwk
tags: [community, elm, hyperapp, raj]
created: 2023-11-22T17:27:23.013Z
modified: 2023-11-22T17:27:51.371Z
---

# pattern-arch-flux-community-elm-fwk

# guide
- elm-inspired: hyperapp, raj

- state + vdom
  - hyperapp

- view agnostic
  - raj
  - hydux

- model-view-update: helper functions
# discuss-stars
- ## 

- ## 

- ## [Trying to use hyperapp with JSX, using esbuild, almost working, except for text nodes. Any ideas?](https://github.com/jorgebucaran/hyperapp/issues/996)
- Hyperapp is actually a lot different from react/preact which does surprise many. 
  - Rather it is more like Elm, but implemented in javascript. Heavy on the functional programming idea (without the type-system ofc).
  - Hyperapp keeps all state in one single global store. When any state changes, the entire view gets recalculated and rerendered.
  - unlike redux, actions are not objects that get pushed in to a reducer. Rather, actions are functions which themselves define the state transformation as a simple function.

- ## hyperapp is similar to Elm, plain JavaScript, no bundlers needed_202008
- https://twitter.com/zaiste/status/1294709371818188801
- Unlike React, etc. where all you've got are declarative views and suit-yourself & good luck imperative code, Hyperapp brings you declarative effects, subscriptions, actions and views. That's Hyperapp's value proposition—everything is declarative, not just one piece of the pie
  - The benefit is in how you can create an entire app based on functional principles, using 99.99% pure & immutable code.

- ## Is time-travel/serializing actions possible to implement in hyperapp?_202103
- https://discord.com/channels/804672552348680192/805935640318705744/819411360424919060
- I was tinkering with some approaches to time-travel. I think the most straightforward way is probably to use immutable state and push changes to an array. That way, each state uses "structural sharing" and only updates references to changed values. Immer was helpful, but maybe it can be done with vanilla JS? Not sure.
- we've been experimenting with JSON Patches that describe which paths/values changed. Immer supports patches out of the box.
  - JSON Patch is handy for implementing proper undo using inverse patches. That way you can grab a specific change and restore the previous value(s).
- https://github.com/mrozbarry/hyperapp-debug I think this might be already outdated, but it shows you how you'd basically add time traveling and similar stuff

- ## 🤔🏘️ Are there any common practices on how to organize a multi-page SPA in Hyperapp?
- https://discord.com/channels/804672552348680192/804672553095528470/973843076533600336
  - I discovered Hyperapp while looking for a lightweight alternative to Svelte. Hyperapp looks like a sane version of Elm.how to organize multiple "pages" in Hyperapp...
- For the view-part it is easy: Make each page a component, that includes the other components each page needs. I usually keep pages in a folder to itself, and components that are reused in a separate folder.
- The real question is how to manage the state. Overall there are three options:
  - A) Manage the whole app in a single app call. The main view determines which page-component to render based on the url/hash, and passes the entire state to the page component it will render. There is no (technical) difference between "shared state" and "page state" in this setup
  - B) Make each page as a separate app in a separate html file. The old-scoolish approach. This is usually preferrable if the different pages don't need to share hardly any state. Small amounts of shared state can be persisted in sessionStorage.
  - C) The complicated approach: Define each page as a separate app in a js-module. The main page is also an app, which controls importing, starting and stopping the various pages' apps. It passes shared state along as initial state to each respective app. In this manner you could also have multiple parallell apps running in the main page for controlling common dynamic parts such as the header. 
  - Personally I would recommend starting with A) and if it just gets too complicated you could always start breaking apart the app into multiple apps as in the C) approach. (Bear in mind, C is complicated too! It just moves complication from State/Actions to effects/subscriptions)

- B) would solve the routing problem
  - Yes it would, and if you can get away with it, it is definitely the preferrable choice. But usually shared-state between pages is the reason you're considering an SPA in the first place. And if there's shared state I'd go with A.
- As for routing, there are basically two approaches (in general, not just hyperapp): hash based (looking at whatever comes after the # in the URL) and the history-api (pushState/popState).  Both things can be solved in hyperapp using subscriptions. So you don't technically need a routing library.
  - The history-api is usually considered the "proper" way, and it can get a little complicated 
  - The hash-based approach is much simpler and also works without special server configuration

- ## 🔥 [Hyperapp – A tiny framework for building web interfaces | Hacker News_202006](https://news.ycombinator.com/item?id=23688798)
- I have tried Hyperapp some time ago. It's usable for small apps, but the lack of ecosystem makes it unfit for anything larger -- as is usual for all niché JS frameworks.

- Hyperapp can and will work, with larger applications, but hyperapp does not have super strict "guide rails" like other more popular frameworks do, so its up to you to design

- What are the difference with Mithril.js?
  - They're similar, but Hyperapp is purely functional and more comparable to Elm.

- Now it looks like Elm
  - Exactly! And the latest version (which is not officially out yet) is even closer to Elm that the first version ever was.

- I'm familiar with Elm but i think the model of Hyperapp is better than the `[state command]` pattern. This is how i see Hyperapp, the event part of Hyperapp is not about commands, it's about transition functions, functions that takes a before state and returns an after state. Hyperapp doesn't let the user to control the state by itself.
  - But there is worst, the problem with the pattern [state command] is that it doesn't work well with async method, because at the time the command is called, the state which is passed alongside the command and the state maintained by Hyperapp may be different.
- in Hyperapp there are no async/await functions. Or Promises. Can't use functions that create side effects. Can't use setTimeout, setInterval, new Promise, fetch, add/removeEventListener, etc.
  - The state becoming stale is never an issue in Hyperapp, because you get a fresh copy of it inside actions, which is the only place where you can "update" the state.
- Thanks for taking the time to explain me how it works. So you're right that you can not use a previous state. And if i want to get the dispatcher directly, i can write a helper function

- can't use traditional DOM events. Wtf are you doing man?
  - Can't use DOM events to create side effects. What we do is define UI interactions as state transitions. 
  - Transitions allow you to say `[nextState, myEffect]` to update the state and create a "controlled" effect (just an object representation of a side effect, very much like how VDOM uses objects to represent DOM nodes). 
  - 👉🏻 Effects in Hyperapp are the same as Elm commands.

- ## [Show HN: HyperApp – 1k JavaScript framework for building web applications | Hacker News_201805](https://news.ycombinator.com/item?id=17126670)

- Mithril is nice. One downside is it doesn't lend itself really well to compound components. Everything has to be passed down through attributes.

- It's doubtful that state changes are the bottleneck for application performance, for most applications. Rendering and managing the lifecycle of your components usually yields much more tangible perf. gains.

- If all goes according to plan, it will look even more like Elm in the next major release (2.0).

- ## [Mithril.js – A modern client-side Javascript framework | Hacker News_201808](https://news.ycombinator.com/item?id=17780897)
- I'm asking why you prefer hyperapp because Mithril has router and xhr capability built-in, and hyperapp doesn't seem to have those features. But hyperapp is really tiny though. 
- The reason to use hyperapp IMO is it is far closer to the actual Elm-style FRP model, and as such includes functional state management out of the box, in a far less awkward and boilerplate heavy way than Redux provides.

- Because HyperApp also has state management built in.
  - If I understand correctly, HyperApp enforces the so-called SAM pattern, but that's it. Calling this "state management" seems to me an exaggeration. And why would one use a view framework to do (domain/application) state management? It doesn't sound right.

- ## 🆚️ [HyperApp vs Mithril_201706](https://github.com/jorgebucaran/hyperapp/issues/225)
- Other than a custom built-in Virtual DOM, HyperApp and Mithril are very different.
- Mithril has something called auto-redrawing, that IIRC re-renders the application after calling DOM events. 
  - But other than that, there's no default state management. 
  - This trait may is desirable if you prefer to experiment with different architectures. I don't know about specific Mithril state managers libraries, but it's like in React you can use setState (default), Redux, Mobx, etc.
- HyperApp has its own built-in state management solution which is inspired and draws from the Elm Architecture. 
  - It's "kinda" like React and Redux. There's no other state management style available or possible.

- Mithril has stateful components, which are a simple and useful way to reuse code across your app and easily port to other apps.
- HyperApp components are called "custom tags", but they are stateless. That means they are pure functions that only accept props and know how to render themselves

- Mithril is bundled with `m.request`, which simplifies making HTTP requests.
- HyperApp has no built-in facilities to help you make HTTP requests. I like to use `fetch`
# discuss
- ## 

- ## 

- ## 

- ## In the "rarely useful but perhaps mildly interesting" department I (re-) discovered this little middleware-trick and thought I'd share it: 
- https://discord.com/channels/804672552348680192
  - 类似redux的middleware
  - With that middleware all actions dispatched from that app will have METADATA  as a third argument.  When you have multiple apps running on a page, this allows actions to distinguish between them
  - When would you need that? Well I have found it useful for implementing custom elements using hyperapp, where the actions need to know which element they are currently being dispatched for, so they can return effects that do stuff to that particular element.
