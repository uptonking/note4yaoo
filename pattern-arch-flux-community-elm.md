---
title: pattern-arch-flux-community-elm
tags: [architecture, community, elm, flux]
created: 2023-11-20T19:03:49.266Z
modified: 2023-11-20T19:04:12.672Z
---

# pattern-arch-flux-community-elm

# guide

# discuss-stars
- ## 

- ## 

- ## 🏘️ [The Elm Architecture | Hacker News_201808](https://news.ycombinator.com/item?id=17845458)
- The bit I love about the Elm Architecture that I really wish existed in other frameworks is the "Command" system, by which the "Update" step can dispatch further changes. Basically, imagine if a Redux reducer could dispatch further actions.
  - The re-frame effects in ClojureScript are a similar idea https://github.com/Day8/re-frame/blob/master/docs/Effects.md
- I think Redux middleware is the answer to this. My preferred approach is to keep all my actions as simple serializable objects, and have (potentially many) small middlewares that listen for certain action types and perform async tasks and dispatch further simple action objects.
  - There are also more fully-baked middlewares like Redux Saga, but I find that those are a bit too heavy-handed and result in too much “lock-in” for implementing your actions and action creators.

- 🤔 In what ways does the Elm architecture differ from MVC?
  - In MVC, the model-view communication is not "interactive" as defined by the article (source pushes to sink). Instead, the view pulls data from the model. There is only a general #changed notification to let the view know that the model has changed.
  - So "unidirectional" approaches fix the problems you get when you don't understand MVC
- In Flux/redux the unidirectional nature comes from all updates targeting and emanating(来自) from a single source (store), and being routed to views accordingly. An interaction from one component will never result in a disconnect where you failed to update the correct model(s) or to notify the right components of a change (hi Backbone.js).
# discuss-effects
- ## 

- ## 

- ## 💡 [DOM side effects are difficult (focus, scrollTop...)_201511](https://github.com/evancz/elm-architecture-tutorial/issues/49)
- I understand the beauty of the ELM model but in practice it seems to me complicated to perform certain tasks, like giving the focus to an input just after insertion in the DOM.

- I have only one question with (I admit) a messy approach:
In React I can use componentDidMount to also attach e.g. a good jQuery UI dialog directly to the DOM without breaking stuff 

- ## [Producing side effects directly from view functions? - Learn - Elm_201712](https://discourse.elm-lang.org/t/producing-side-effects-directly-from-view-functions/323)
- So, as it stands, the only way to execute side-effects if with a Cmd msg. This means I can look at any piece of code and get a sense of where side-effects are happening very easily

- One concrete practical reason they shouldn’t is requestAnimationFrame batching.
  - Right now, if I subscribe to mousemove, I’ll get flooded with events when the user moves the mouse. Each time an event comes in, update runs, potentially changes Model, and potentially runs more effects.
  - However, regardless of how quickly events are coming in, the Elm Runtime still only calls view once per animation frame - with whatever the current Model happens to be at that moment. It can do this optimization safely because view only returns Html and performs no side effects.

- ## 🏘️ [RealWorld example app architected with the Effect pattern - Show and Tell - Elm_202005](https://discourse.elm-lang.org/t/realworld-example-app-architected-with-the-effect-pattern/5753)
  - The extended Effect pattern used in this application consists in defining an `Effect` custom type that can represent all the effects that `init` and `update` functions want to produce.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Does Elm compile to JS, or JS+HTML? If I only use a function to create a node, does it make a JS function, or just create the HTML? : elm_201604](https://www.reddit.com/r/elm/comments/4g3wtk/does_elm_compile_to_js_or_jshtml_if_i_only_use_a/)
- your Elm code all turns into JS. What elm-html does is create DOM nodes at runtime as required
- Most Elm programs use a Virtual Dom, which means you'll see nothing without JS.
- Elm compiles to javascript. 

- ## [Single Page Applications using Rust | Hacker News_202008](https://news.ycombinator.com/item?id=24120311)
- I am hopeful that Rust can achieve what Elm did not.
  - I really fell in love with Elm early on, back when it was an experimental language for functional reactive programming that just happened to compile to JavaScript. It was an outgrowth(发展结果; 产物) of failed experiments in FRP from the Haskell world. I thought it got so many things right -- and it totally did. But then, just as soon as it started gaining real traction, development on Elm went silent and became siloed, staggeringly slow, locked-down, and unresponsive to users. I understand why this happened and I don't even hold it against the Elm team, but it certainly stunted the language's growth and adoption.
  - Rust has a much more expressive type system than Elm. The Rust world is much more open, responsive
- Both rust and elm are geared more toward enforcing correctness through their type systems to tame complexity in large projects. In my experience, clojure, being dynamic, fits more as a comparison to vanilla JavaScript.
  - ClojureScript is compile-to-JS and can run on the backend in Node or on the frontend in browsers.

- ## [Elm 0.19 Broke Us | Hacker News_201808](https://news.ycombinator.com/item?id=17842400)
- I think Elm can learn a lot from Rust before 1.0 here. Rust made some "insane" decisions that should have pissed off the community but did not mostly because of the way the communication was handled. There were obviously some disagreements along the way which caused some valuable community members to jump ship, but overall it was really well handled and the language became better as a result.
