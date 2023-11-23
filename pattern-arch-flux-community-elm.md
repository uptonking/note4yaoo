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

- ## 🤔💫 [Using Elm (or React) is a bad idea for performant graphics in the web_201601](https://github.com/elm/compiler/issues/1247)
- The reason is because using Elm's functional diffing algorithm to calculate graphics is not a good idea (it's not a good idea to do this with React, Mercury, Om, Mithril, or any library with these concepts). 
  - To have control of graphics, the pipeline to the browser renderer needs to be pure and have the smallest layer above the browser's renderer.
  - Making a game like that in Elm (or React, etc) causes the render path to go through Elm's (or React's) diffing algorithms on each and every tick of the frame that needs to be drawn. That just isn't a good idea.
- If you'd like to animate things with Elm (or React, Mithril, etc) one technique you can use for basic web sites is to use Elm only to modify CSS classes, then let the browser handle animations with CSS transitions. 
- Another technique for things like a WebGL or Canvas app would be to let Elm (or React) components care only about start and end states, then let a renderer algorithm perform the animation to/from those states.
- When using the better technique, Elm will only be put in charge of calculating state at two possible moments: at the beginning of an animation or at the end. A renderer (for example one made in Three.js) will do the hard work between the two states. 
  - Compare that to the not-so-good approach of have Elm calculate all the animation positions between the two states. Invoking the diffing algorithm (and whatever else Elm (or React) do) in each frame is overkill.

- It works by using requestAnimationFrame instead of setTimeout.

- [Rendering other things besides DOM · MithrilJS/mithril.js_201601](https://github.com/MithrilJS/mithril.js/issues/830)

- ## [Composing Programs in the Elm Architecture - Stack Overflow](https://stackoverflow.com/questions/51156702/composing-programs-in-the-elm-architecture)
- However, you should try not to emulate a component approach like React. 
  - Just use functions. Separate pages in an SPA are one example where it makes sense to have a dedicated message type and corresponding functions like you would with a program.

- ## [Resources regarding scaling Elm apps : elm_201704](https://www.reddit.com/r/elm/comments/65s0g4/resources_regarding_scaling_elm_apps/)

- ## Who did a bigger #fable app? Thinking about 50 to 70 pages. How does all the boilerplate code scale?
- https://twitter.com/MangelMaxime/status/1228718793792380928
- I suppose by boilerplate code you are speaking of the code which glues the Elmish "components" together. In my production app, we can consider having more than 80 "pages". It's not that bad, yes some of the init/update functions looks like not funny code (mostly copy/paste).
  - I only have a simple contract to respect (Model, Msg, init, view, update) but when the contract is fulfilled, I can do whatever I want.
  - The beauty, with Elmish, is that it's really low-level but easy to use.

- my understanding was that Elmish is a high-level architecture with single message loop across the whole application, and it can't be easily separated to many because components have to communicate with each other.
- Yes in general that's how Elmish is being used when you start your application from scratch (no legacy code). But when you have an already existing application you can't always make Elmish the top manager.
  - Hopefully for these case, you can embed Elmish inside a react component (react is just an example).
  - But you can write an higher abstraction on top of it. For example, if you don't like to write the explicit wiring code you can always create on abstraction for making it less verbose if you need it. My best advice is to experiment with it

- ## 🏘️ [The Elm Architecture | Hacker News_201808](https://news.ycombinator.com/item?id=17845458)
- The bit I love about the Elm Architecture that I really wish existed in other frameworks is the "Command" system, by which the "Update" step can dispatch further changes. Basically, imagine if a Redux reducer could dispatch further actions.
  - The re-frame effects in ClojureScript are a similar idea https://github.com/Day8/re-frame/blob/master/docs/Effects.md
- I think Redux middleware is the answer to this. My preferred approach is to keep all my actions as simple serializable objects, and have (potentially many) small middlewares that listen for certain action types and perform async tasks and dispatch further simple action objects.
  - There are also more fully-baked middlewares like Redux Saga, but I find that those are a bit too heavy-handed and result in too much “lock-in” for implementing your actions and action creators.

- 🤔 In what ways does the Elm architecture differ from MVC?
  - In MVC, the model-view communication is not "interactive" as defined by the article (source pushes to sink). Instead, the view pulls data from the model. There is only a general #changed notification to let the view know that the model has changed.
  - So "unidirectional" approaches fix the problems you get when you don't understand MVC
- In Flux/redux the unidirectional nature comes from all updates targeting and emanating(来自) from a single source (store), and being routed to views accordingly. An interaction from one component will never result in a disconnect where you failed to update the correct model(s) or to notify the right components of a change (hi Backbone.js).

- ## [Why Elm? [pdf] | Hacker News_201705](https://news.ycombinator.com/item?id=14293310)
- I've tried to use Elm and The Elm Architecture on a project before, but I gave up. The Elm Architecture makes it very easy to create small type safe components, but it forces parent components to manage the state + structure all children components. This makes it hard to use a component and to separate concerns.
  - The parents of each of these elements have to manually map the state changes, they have to be aware of the internal state of the components, just as I was saying.

- My top 3 complaints:
  - 1) The crazy boilerplate, the Elm architecture forces you to store all your app state in a single atom. 
  - 2) The snail(蜗牛) pace at which Elm evolves. 
  - 3) The religious(宗教的) focus on purity. Can you believe that to read the current time or generate a random number, you must be within a component's update function, ask for one or the other and you will get your result later, asynchronously?
- You say this like generating a random number is a small deal. In a sense this is very true! From the machine's perspective generating a random number is a quick operation. However, from the perspective of maintainers who come after you losing determinism is no small thing, and IMHO deserves to be marked clearly in the type system.

- This is exactly the react/redux/flux architecture everyone is raving(极力夸赞) about.
- Given all the benefits of Elm, 6 lines of boiler plate (one line added in model, 5 lines added in update) is a small price to pay. Especially considering the small amount of components (in contrast to React, not everything is a component).
# discuss-elm-component
- ## 

- ## 🤔🤔 [Two ways to reuse views? Which do I choose?_201908](https://www.reddit.com/r/elm/comments/cqd93z/two_ways_to_reuse_views_which_do_i_choose/)
  - The first is to make it a mini elm app. I.e. `Model, Msg, init, view, update` . The caller then uses `Html.map, Cmd.map` and so on.
  - The second is like elm-sortable-table which exposes a State, init, view.

- #2 is way simpler to integrate, but your view won't be able to produce side effect via commands e.g. make an http call, get information from the DOM, etc. All the commands will need to be produced by wrapping app.
  - If you want your view to trigger side effects then you need #1.

- The rule of thumb is to use the second approach if you can and if you cannot, switch to the first approach. 
  - The first one brings in way more complexity. I can have an entire module of small reusable views implemented with the second approach BUT, the first approach would mandate one module per component.
  - this second approach for views that have to have some state in them and use the first approach only as the last resort. This usually happens if I need side-effects in the update of the component.

- ## [Does TEA mean single state at root? : elm_202112](https://www.reddit.com/r/elm/comments/ronzbo/does_tea_mean_single_state_at_root/)
- Your knowledge of React is going to be a problem for learning TEA at least that's what I found. 
  - Yes, I think you are describing it correct in that all state is at the "top root". You can define state lower at a lower view level but that state will still go through the "top root".
- You are looking for a “component architecture” which is discouraged by Elm
- It's not just discouraged, but the language ergonomics (no MonadAsk and Lenses being discouraged too) will fight you if you try to do "components". In this case the easiest thing is usually to pass in the whole state as an open record just referencing the fields your need and operate as if it's a single "global" state. The alternatives are all pretty nasty and there are no built-ins to help update nested records.
- The Elm Architecture requires that the top level model contains state for every single thing within in.
  - So that means that every key pressed means the model gets updated.
  - My understanding of the rendering is that you can use Html. Lazy to avoid updating things whose parameters don't change.

- It's like Redux (which was inspired by TEA), a single source of truth.
  - So essentially, what you have said is correct, you have to pass the updater (callback in React; action in Elm) all the way down from the top.
  - There won't be unnecessarily re-render due to diffing, but once the root state gets big enough, you'll notice lag due to diff calculations.

- Your understanding is correct: Elm does not allow to abstract state, meaning that every piece of data must be contained in the Model and be manually passed around by the developer (you).
  - This approach simply removes the very possibility of most errors, as mutable (encapsulated) state is the biggest source of bugs. 
  - The downside is that Elm requires more boilerplate code than most languages and scales (in terms of software architecture) rather poorly

- ## [Approach about creating component in Elm : elm_201909](https://www.reddit.com/r/elm/comments/d2ba4q/approach_about_creating_component_in_elm/)
- Thinking in terms of components encourages you create modules based on the visual design of your application.
  - It would be way easier to just make a viewSidebar function and pass it whatever arguments it needs. It probably does not even have any state. Maybe one or two fields? Just put it in the Model you already have. 
  - If it really is worth splitting out into its own module, you will know because you will have a custom type with a bunch of relevant helper functions!
  - 👉🏻 Point is, writing a viewSidebar function does not mean you need to create a corresponding update and Model to go with it. Resist this instinct. Just write the helper functions you need.

- A component in elm terminology is the `{ init, update, view, sub }` as it encompasses a complete building block that can be reused between projects.
  - I do agree with you shouldn't try to make some generic all encompassing component just add the `init, update, view, sub` as you need them.

- At our company we follow atomic design methodology. We use elm-ui-explorer in order to be able to implement and browse al UI elements with absolute separation between views and specific use case (api calls, digesting data, etc). coming back to UI, we use the OutMsg pattern when we need sub elements to affect the parent element. This is the path we follow for each UI element.

- ## 🏘️ The component/object *cultural* distinction masks that the question "How do I use components to architect Elm code?" is equally odd._201708
- https://twitter.com/evancz/status/903266544544878592
- 1) Components are objects!
  - components = local state + methods
  - local state + methods = objects
- 2) I think this components/objects distinction serves to *culturally* distinguish JavaScript and Java. "We do not do OO like that!"
- 3) Distinguishing cultures can be very valuable! But on a technical level "local state + methods" is a decent definition of an "object"
- 4) It would be odd to ask "How do I use objects to architect Elm code?" In functional languages, you solve same problems in different ways!
- 5) The component/object *cultural* distinction masks that the question "How do I use components to architect Elm code?" is equally odd.
- 6) I try to outline ways of approaching large codebases functionally in my @elm_europe talk
  - [Evan Czaplicki - The life of a file - YouTube_201708](https://www.youtube.com/watch?v=XpDsk374LDE)
- 7) Elm wants you to write functional code! From language and libraries. It all fits together if you let it!
- [From Object Oriented Programming to Functional Programming - Inheritance and the Expression Problem](https://github.com/Dobiasd/articles/blob/master/from_oop_to_fp_-_inheritance_and_the_expression_problem.md)
- It is true that objects can be represented as recursive records and functions in an immutable language
- The same operational semantics works for "components" too. I am talking about the technical details, not the "looks". That's my whole point.

- ## 🏘️ [Components in Elm: why (not) and how?_201708](https://www.reddit.com/r/elm/comments/6x5w07/components_in_elm_why_not_and_how/)
  - I've looked at the view functions over components paradigm. This works well for small item, such as text fields and buttons. 
  - However, larger elements, such as whole pages in SPA's, often require update and subscription functions as well.
  - We can implement these functions either in their separate functions, or add all their logic in the main update and subscription functions. The later option seems like pure madness to me in terms of code quality.
  - Ideally, what I'd like to do is something like creating my view functions with Component objects instead of Html object. Component objects would contain whatever update, subscriptions and init functions are required. This would, of course, require at least a different program for the main function.

- My keynote at Elm Europe aims to be a comprehensive explanation of why it's better to do the exact opposite of this
  - [Richard Feldman - Scaling Elm Apps - YouTube](https://www.youtube.com/watch?v=DoA4Txr4GUs)
    - Have reusable components : `Html.map` and `Cmd.map`
- it's a great keynote! To me, it's definitely the most complete and understandable explanation of why you should not go the component route in Elm.

- You're thinking in terms of components. This is natural if you're coming from react or some other frondend library from an object oriented language.
  - However, elm does not have components, because components are objects. 
  - In elm, the base unit of composition is a function, not objects, nor components.
  - Instead, let your code grow naturally. Don't draw borders upfront, don't follow an arbitrary pattern.
  - Start with one file. Once it gets too large, move out parts that belong together into separate modules.
  - Try to find dependencies in your model and extract those into a datastructure.
  - Once your Msg type becomes too big, group related messages into sub messages.

- Maybe and erlang approach where each component has an state and be a separate module, and the components communicate through messages, ok no

- 💡 Because state is immutable in a functional language, attempting to encapsulate state does two things. a) try to destroy all the benefits of having immutable state to begin by bringing it back. b) wreak(造成破坏, 伤害) havoc(破坏) on the type signatures because of the weaving you have to do. 
  - The units of composition in FP are datastructures on one side and regular functions on the other. 
  - The units of composition in FP are NOT objects, for the very reason that the purpose of objects is to encapsulate a state which FP just does not even have. 
  - 👉🏻 Try to reason about your code as a series of data transformations and not a progression of state.

- Invisible state that mutates can create hard to understand bugs

- ## 🤔 [Help! Am I using components? : elm_201609](https://www.reddit.com/r/elm/comments/54en9u/help_am_i_using_components/)
- What you're doing is using Elm like you'd use React, which is a perfectly natural thing to want to do. And it will work. But it's clunky and not the nice way to do things. 
  - Imagine that instead of writing 10 React components and combining them under one master component representing the entire page, you just write one React component, and use a lot of helper methods within that component to get snippets of the JSX that would normally be in its own component's render method.
  - That's how you normally use Elm. There's one model, for the entire application. There's one update function. There's one view function. All the things you'd making separate components now will just be simple functions that take in the model and return some HTML. You can put those functions in separate files, to keep things organised.
  - think about it. Why do we split things up into lots of React components? So we can think about a piece of the whole in isolation? We can already do that with any function in Elm, because they're pure. So we can compartmentalise the state, make sure elements don't mess with each other's stuff? Elm values are immutable.
  - There isn't really a problem in Elm with having the entire application be one component. 
  - You can always break things out into separate Elm projects/components if things are getting really overloaded for you

- Just completed a 'flattening rewrite'. 1300 lines down to 1000 lines and pleasant to strip away the communication code which was mostly parent updates calling child updates and wrangling the results.
  - Main issue is naming as I now have much more in one file and there are a few places where previous reasonable names now conflict.
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

- ## [[Question] Is Elm a smart decision for a long term project in 2023? : elm_202308](https://www.reddit.com/r/elm/comments/164ipl0/question_is_elm_a_smart_decision_for_a_long_term/)
- It’s bear market for Elm XD. Builders are still building:
  - Evan preparing work related to backend
  - Mario continuing to improve Lamdera
  - Simon continuing to improve tooling (elm-watch)
  - Matthew continuing to improve ui (elm-ui v2 in preparation)
  - Ryan continuing to improve SPAs (elm-land)
  - Dillon continuing to improve SPAs (elm-pages)
  - Jeroen continuing to improve linting (elm-review)

- ## [Why does TEA use separate `msg` type and `update` function? Why not just pass `model -> (model, Cmd)` functions to `Html` ](https://discourse.elm-lang.org/t/messages-purpose/6778)
- Msgs are the way an Elm program communicates with the world outside Elm. 
  - Msgs come from user interactions events, such as clicks on html elements, but they also come from IO events like http requests and ports.
- `update` is a central place to interpret all incoming msgs in to changes to the model.
- Elm could have picked an architecture with lots of call back functions being passed to the runtime for it to call but having a central place to deal with things that can change the model makes it easier to see how and why the model can change.
- A model -> (model, Cmd) passed to an onClick makes it tricky to figure out exactly what kind of things can change the model, that Cmd would need to include it’s own callback to update the model in someway too, which might also return other Cmd that would have it’s own call backs. While this can work (clearly, it’s how most JS apps work), it does make it harder to find which code interacts with the model.
- Having a single callback function for all events mean that you have a single tree of functions to look at when evaluating how and why the model can change.

- Having a single Msg type is great for listing what interactions are possible in the project, which has a number of benefits. Spreading all of that into view and subscriptions makes it very hard to know what can happen and can’t. 

- Cutting msg out, is similar to how the folks of Hyperapp 27 have decided to do it. One plus you get from that, is a “free” splitting of your update into smaller functions, since you pretty much don’t have one anymore.

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
