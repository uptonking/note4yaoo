---
title: pattern-arch-flux-blog-elm
tags: [architecture, blog, elm, flux]
created: 2023-11-21T10:18:05.594Z
modified: 2023-11-21T10:18:24.650Z
---

# pattern-arch-flux-blog-elm

# guide

# blogs-elm

## 🕹️ [The Elm Architecture · An Introduction to Elm](https://guide.elm-lang.org/architecture/)

- The Elm Architecture is a pattern for architecting interactive programs, like webapps and games.

- This architecture seems to emerge naturally in Elm. Rather than someone inventing it, early Elm programmers kept discovering the same basic patterns in their code.
  - projects like Redux have been inspired by The Elm Architecture

- Elm program always breaks into three parts: 都是fn类型
  - `Model` - the state of your application
  - `View` - a way to turn your state into HTML
  - `Update` - a way to update your state based on messages
- These three concepts are the core of The Elm Architecture.

- You can think of `Browser.sandbox` as setting up a system runtime
  - The runtime system figures out how to render `Html` efficiently. 
  - It also figures out when someone clicks a button or types into a text field. It turns that into a `Msg` and feeds it into your Elm code
- In addition to producing `Html` values, our programs will also send `Cmd` and `Sub` values to the runtime system. 
  - In this world, our programs can command the runtime system to make an HTTP request or to generate a random number.
  - They can also subscribe to the current time.

### [Side Effects](https://elmprogramming.com/side-effects.html)

- A function or expression is said to have a side effect if it modifies some state or has an observable interaction with calling functions or the outside world. 
  - For example, a particular function might modify a global variable or static variable, modify one of its arguments, raise an exception, write data to a display or file, read data, or call other side-effecting functions

- Most scenarios in which an Elm app needs to interact with the outside world tend to fall into two categories:
- Ask Elm runtime to do something. 
  - use Command
- Get notified when something happens.
  - use Subscription

- Everything is Data
  - Elm runtime handles all interactions between them and the outside world
  - The model is just some data. Msg is data too.
  - Similarly commands and subscriptions are also data.
- Program as a Data Transformation Machine
  - elm treats everything in our program as data, except the functions that operate on that data. 
  - We can treat our programs as a series of data transformation operations. 
  - This approach to building applications drastically reduces the overall complexity.

## 🕹️ [Elmish · F#](https://elmish.github.io/elmish/)

- Elmish implements core abstractions that can be used to build F# applications following the “model view update” style of architecture, as made famous by Elm.

- Model
  - This is a snapshot of your application's state, defined as an immutable data structure.
- View
  - This is a pure function that produces a new UI layout/content given the current state, defined as an F# function that uses a renderer (such as React) to declaratively build a UI.
- Update
  - This is a pure function that produces a new state of your application given the previous state and, optionally, new commands to process
- Message
  - This an event representing a 💡 change (delta) in the state of your application, defined as a discriminated union.
- Command
  - This is a carrier of instructions, that when evaluated may produce one or more messages.
- Init
  - This is a pure function that produces the initial state of your application and, optionally, commands to process
- Program
  - This is an opaque(opaque) data structure that combines all of the above plus a setState function to produce a view from the model. 

- Dispatch loop
  - Once started, Program runs a dispatch loop, producing a new Model given the current state and an input Message.

- Parent-child hierarchy is made explicit by wrapping model and message types of the child with those of the parent.

- Tasks and side-effects
  - Tasks such as reading a database or making a Web API call are performed using async and promise blocks or just plain functions. 
  - These operations may return immediately but complete (or fail) at some later time. 
  - To feed the results back into the dispatch loop, instead of executing the operations directly, we instruct Elmish to do it for us by wrapping the instruction in a command.

- Commands are carriers of instructions, which you issue from the `init` and `update` functions. 
  - Once evaluated, a command may produce one or more new messages, mapping success or failure as instructed ahead of time. 
  - As with any message dispatch, in the case of Parent-Child composition, child commands need to be mapped to the parent's type

- Most of the messages (changes in the state) will originate within your code, but some will come from the outside, for example from a timer or a websocket. These sources can be tapped into with subscriptions, defined as F# functions that can dispatch new messages as they happen.

- The core is independent of any particular technology, instead relying on a renderer library to implement `setState` in any way seen fit. 
  - In fact, an Elmish app can run entirely without a UI!

- Every message going through the dispatch loop can be traced, along with the current state of the app. 
  - Just augment the program instance with a trace function

## [Elm Architecture in 8 lines of TypeScript for AppRun | by Yiyi Sun | Medium_201803](https://medium.com/@yiyisun/elm-architecture-in-8-lines-of-typescript-d5a33aca75c1)

- I like Elm. The main reason for me to like it is its architecture, the famous Elm Architecture.
- I have created the AppRun library to help build applications of the Elm architecture. 
- The type definition in the AppRun library is a little more complicated because AppRun uses event pub-sub, virtual DOM, async/await, and has stateful component and stateless component. 

## 📖 [Elm Patterns](https://sporto.github.io/elm-patterns/architecture/effects.html)

- https://github.com/sporto/elm-patterns
  - A collection of common patterns in Elm

### [The effects pattern - Elm Patterns](https://sporto.github.io/elm-patterns/architecture/effects.html)

- In a usual Elm application the update function returns `(Model, Cmd Msg)`. 
  - Cmd in Elm is an opaque type so update functions are not easy to test. We cannot easily inspect the commands and see if they are doing the right thing. We cannot also simulate these commands as we don't know what they are doing.
- The effects pattern allows us to deal with these issues by returning an `Effect` type instead of `Cmd msg` from `update`.
  - At the last possible moment we convert the Effect into actual commands. E.g. in the root module of the app we would have a function like: `runEffects : List Effect -> Cmd Msg`.
  - This makes a Elm application a lot more testable.

## 📖 [Beginning Elm: a gentle introduction to Elm programming language](https://elmprogramming.com/)

## 📖 [The Elmish Book 偏实战示例](https://zaid-ajaj.github.io/the-elmish-book/#/)

- https://github.com/Zaid-Ajaj/the-elmish-book
  - A practical guide to building modern and reliable web applications in F# from first principles

- The Elmish Book is a practical guide to building modern and reliable web applications in F#
- Using the Elmish library, we will build and design our applications following The Elm Architecture

## 🚧 [Make your own TEA (The Elm Architecture) - by Noah - Derw](https://derw.substack.com/p/make-your-own-tea-the-elm-architecture)

- https://github.com/eeue56/make-your-own-tea/pull/1/files /ts
  - demonstrates how to build an Elm-style event loop in TypeScript

## 🏘️⤴️ [The Elm Architecture in JavaScript | by Jas Chen | Medium_201611](https://medium.com/@JasChen/the-elm-architecture-in-javascript-eb4d5201272b)

- Compare The Elm Architecture to Redux
- 👉🏻 Something happened: Messages vs Actions
  - In Redux, an action is a plain object, it’s type is a property.
  - **messages in The Elm Architecture is a function**
- 👉🏻 Side Effects: Cmd/Sub vs Middleware
  - Middleware in Redux can be a mess. As a middleware user I have to make sure they applied in proper order, which one should I apply first? Are they going to conflict to each other? As a middleware author I have to think, Redux-Thunk intercepts functions, so I can’t make a middleware intercepts functions too. Also I have to remember to pass actions I don’t know to next middleware
  - cmd/sub: Unlike middleware of Redux, it’s not chain-able, each side effect manager only take care of it’s job.
- 👉🏻 State Management: Model/Update vs Reducers
  - Both Redux and The Elm Architecture take single central state approach. 
  - The difference is Redux slice state into several reducers, 
  - and The Elm Architecture only have one model with an update function (You can think it as a single reducer).
  - The bad part is, you have to spend time to decide how to divide your state, if you doing it wrong, you may face scaling problems. Also you will encounter questions like How do I share state between two reducers?
- 👉🏻 Connect to view: Call view function vs Provider/Connect
  - Redux encourages users wrap components with Connect component when needed. The main concept is to decouple View and State, this goal sounds great, but the price is also very high, you write more and more code such as mapStateToProps, mapDispatchToProps, Provider and Connect to achieve it
  - In The Elm Architecture, you pass model to view function to render your view. As the result view is coupled with Model. That sounds bad. But this is the idea of The Elm Architecture — no components, only view pieces.
  - Which one is better? It depends on your needs. 
- > Scaling The Elm Architecture
  - We do not think in terms of reusable components. Instead, we focus on reusable functions…we create reusable views by breaking out helper functions to display our data.

## 📖 [Scaling The Elm Architecture · Elm 가이드](https://kyunooh.gitbooks.io/elm/content/reuse/)

- If you are coming from JavaScript, you are probably wondering “where are my reusable components?” and “how do I do parent-child communication between them?” A great deal of time and effort is spent on these questions in JavaScript, but it just works different in Elm. 
  - We do not think in terms of reusable components. Instead, we focus on reusable functions. It is a functional language after all!
  - So this chapter will go through a few examples that show how we create reusable views by 💡 breaking out helper functions to display our data.

## ⤴️ [Elmish: Functional Programming in Javascript | by Chet Corcos | Medium_201602](https://medium.com/@chetcorcos/elmish-functional-programming-in-javascript-50995f1d4b9e)

- I’d try to test my understanding of the Elm Architecture by implementing the same concepts in Javascript

- In Elm, everything is a pure function.

```typescript
type Program = {
  init   : () => state,
  update : (state, action) => state,
  view   : (dispatch, state) => html
}
```

- One benefit of building components using the init-update-view pattern is composition. 
- My favorite example that shows the abstraction power of the Elm Architecture is the undoable component. 
- Two other features that really excite me are reproducible error reporting and automated testing.

- There are sadly a couple drawbacks to this approach that I’ve noticed so far:
  - There’s an annoying amount of boilerplate needed to wrap child actions. I think Clojurescript is an interesting option to alleviate this pain because of its incredibly powerful macros
  - The entire DOM tree is re-computed after every action. I do think that this will eventually be a problem if you’re running lots of animations through the action-update cycle. It is possible to wrap these Elmish components in React components to introduce lazy evaluation. 

- The last thing we didn’t talk about yet is side-effects. Side-effects are typically the culprit of making your entire app a mess. Maybe if I have some time next week and people are interested, I’ll write another article about that.

- 👥 discussions

- Now that’s not as bad as it seems because the new state object will refer, mostly, to data in the old state object. Additionally, this allows the use of referential equality to figure out precisely the parts of the state that require re-rendering. This is what `Html.lazy` does.
- Finally, I would suggest that there are compiler optimizations that can elide the copying of immutable objects. Such optimizations are automatic, comprehensive and safe. They allow you to work in high-level immutable code that compiles down to lower-level mutable code only where the compiler detects it to be safe. I don’t think Elm implements this yet but if it ever does, all Elm code everywhere will get the optimizations for free.

- To get `bind(add, 1) === bind(add, 1)`, you should just need to memoize your bind function. Since you are using Ramda, that should just be putting `const bind = R.memoize(R.partial)` in your top-level scope.

## 🏘️ [Model-View-Update (MVU) – How Does It Work?_202002](https://thomasbandt.com/model-view-update)

## [Fable · Elmish Components with Elmish 4 and UseElmish_202210](https://fable.io/blog/2022/2022-10-13-use-elmish.html)

- Elmish, the F# implementation of the Elm Architecture, has proven to be a simple yet powerful way of managing state in UI apps. 
- However, it's been often criticized because it was designed for monolithic applications that couldn't take advantage of the component architecture of modern UI frameworks like React. 
  - Although it made your app more robust, users didn't like the boilerplate necessary to glue the full component hierarchy into a single global Elmish program.

- Feliz. UseElmish appeared as a custom React hook to solve this situation, allowing you to use Elmish at the component-level. 
- This was a great advancement but its full potential was still blocked by two problems:
  - React hooks were not designed with external stores in mind.
  - Elmish didn't check for termination of Elmish programs and didn't clean up subscriptions.
- Thankfully, these problems have been solved now thanks to React 18 (with the new useSyncExternalStore hook) and Elmish 4

- The new Elmish version includes termination capabilities and subscription cleanup, so instead of assuming there is one single global Elmish program, now you have full control of its lifecycle, which makes integration with React components a breeze.

- Elmish 4 Subscriptions
- Subscriptions must include now an IDisposable that will be invoked by Elmish when cleaning up.
- The Program.withSubscription function is now evaluated after every update. This makes it really easy to activate or deactivate subscriptions on demand.

- Fable. React. UseElmish is the spiritual successor of Feliz. UseElmish and takes advantage of React 18 and Elmish 4

## [Understanding UI Components in Elm_202212](https://www.crowdstrike.com/blog/tech-center/understanding-ui-components-in-elm/)

- This post explored the benefits of stateless components, and how Elm pressures us towards using them over stateful components.
  - When we lean into this, it leads us to write components which are easy to compose and apply in new ways
  - The main downside is that we can more easily introduce inconsistent behaviors across different uses of the same components.
- here are a few rules of thumb:
  - Prefer stateless components
  - Let the page itself own as much of the state as possible
  - Stateful components work best when used as close as possible to the component tree root

- Our two camps are very similar to “presentational” and “container” components or “dumb” and “smart” components, which you may know from React and Angular.

- [Robot Buttons from Mars @ Elm in the Spring - YouTube_201906](https://www.youtube.com/watch?v=PDyWP-0H4Zo)

## [Child-Parent Communication in Elm: OutMsg vs Translator vs NoMap Patterns_201707](https://rchaves.app/elm-child-parent-communication-patterns/)

- When your app Elm start growing, you will want to break it apart in smaller pieces to be able to scale
- I believe Child-Parent Communication is often more importante when scaling and doing SPAs, that’s why lots of stuff I found was reading this reddit thread about Scaling Elm App

## ⏰ [Elm 2022, a year in review - DEV Community_202302](https://dev.to/lucamug/elm-2022-a-year-in-review-33pp)

- 按月份和日期整理

## 🆚️🏘️ [Elm and Event Sourcing_201607](http://marcosh.github.io/post/2016/07/09/elm-event-sourcing.html)

- Event sourcing is somehow already present in the Elm Architecture, but not at a userland level. 
  - Anyway, as we saw, it is quite straightforward to bring it at the user level. This allows us not to lose any data in the interaction between our application and the user

## 🆚️🟦⤴️ [Differences between TypeScript and Elm - DEV Community](https://dev.to/lucamug/typescript-and-elm-3g38)

- TypeScript's type system is not sound, by design. 
- Elm's type system is sound and it infers all types. It uses the Hindley-Milner type system that is complete and able to infer the most general type of a given program without programmer-supplied type annotations or other hints.

- TypeScript mitigates the problem but runtime exceptions can still happen. “Mutation by reference” is one of the cases that can generate runtime exceptions.
- Elm's sound type system together with other design choices guarantees no runtime exceptions.

- TypeScript mitigates the issue with the strictNullChecks flag. When it is set to true, null and undefined have their distinct types and you’ll get a type error
- Elm does not have either null or undefined. Elm leverages the type system in case of missing values, with the types Maybe (called Option in other languages) and Result.

- TypeScript does not support pattern matching. It can support "exhaustiveness" with switch statements under certain conditions
- Elm's support pattern matching (with the `case...of` syntax). Elm's pattern matching always applies exhaustiveness.

- TypeScript doesn't support real immutable data structures. In JavaScript, mutability is the default
- Elm's data is fully immutable, by design. Including also in all the dependencies.

- ### [TypeScript feels worth it until you use something like Elm | Hacker News](https://news.ycombinator.com/item?id=22057260)
- TypeScript feels worth it until you use something like Elm, then you realize just how lacking and TypeScript's type system truly is.
  - TypeScript's major weakness is that it doesn't want to break away from Javascript. That strict dedication to being a superset means the type system explodes into ten thousand builtin types the come, seemingly at times, from nowhere, simply to control for the wildness of Javascript. 
  - This leads to nearly impenetrable error messages regarding types, especially if you have a stack trace involving more than one object/record type (whatever you want to call it), it will expand all of them and just, no. It's unreadable. It can be read, but it cannot simply be grokked.
  - TypeScript just doesn't impress me. I get far better results from other languages for a whole lot less work. TypeScript claims to want a balance between correctness and productivity but the language gives me neither of those things. My typical experience is that I wrote almost the same amount of actual code, but now also with types. Elm lets me write far less total code. Less code means less bugs and more productivity, and better types and better correctness is what gives you those things.
- typescripts goal is to be a superset of javascript, which has resulted in many many libraries now shipping with typescript type definitions as officially supported things within libraries. Elm ( or any other client side language) simply hasn't had that kind of impact.
# blogs-cons

## 🤼🏻 [The Elm Architecture is the wrong abstraction for the web_202309](https://gist.github.com/chexxor/23ccf35add7dbdd33ecdd26888663140)

- There are lots of reasons to love The Elm Architecture:
  - It is easy to understand.
  - Easy time-travel debugging, due to highly restricted state. (not a feature worth designing an architecture around).
  - Designed around update commands and pure functions, which is great for testing.

- And there are reasons to dislike The Elm Architecture:
  - Can't easily create components which encapsulate their own state.
  - Semi-encapsulated components require "wiring" through every semi-encapsulated component up to the app root.
  - Leads you to think it scales to big websites, but its docs don't even mention how to handle links and URLs.

- Incorrect abstractions for the web
- Duplicated DOM state
  - A web page element is not a pure function -- it is state. A pure function can return a description of the desired state of an element, but it requires an interpreter to realize the desired state, a thing currently referred to as the "virtual DOM". This may seem like a fine abstraction, but it effectively completely duplicates the real state of the DOM, which can lead to problems. It also has an impact on run-time memory useage.
  - To be fair, using virtual DOM isn't exactly described as an intentional part of The Elm Architecture, but the architecture relies on it! The "View" should be a pure function of the "Model", and the interpreter should flawlessly realize the desired "View" into the DOM. There are situations in which the desired can't be flawlessly realized, such as text field inputs with cursor position and selected text, as I experienced.
- Unique "Update" for every state update
- URLs and support for different paradigms
- Code-splitting and lazy-loading routes
- Components & re-using 3rd-party components

## 🛑 [The Biggest Problem with Elm_201911](https://cscalfani.medium.com/the-biggest-problem-with-elm-4faecaa58b77)

- The biggest problem with Elm isn’t that the language lacks higher level abstractions like many Haskellers complain. Or that the language keeps removing advanced features in favor of the beginner experience.
- The FFI (Foreign Function Interface) mechanism, which allows developers to call Javascript from Elm, leaves a lot to be desired especially compared to other functional languages. 
  - And while this mechanism would benefit from returning a Task instead of a Cmd, it too is not the biggest problem.
- The fact that Elm is the only language I’ve worked with in almost 4 decades that has NO official support for private libraries is still not its biggest problem.

- 🛑 These problems pale in comparison to the biggest reason we’re leaving Elm for PureScript: the Elm Architecture.

- The Elm Architecture works well for lots of cases, but one size never fits all.

- As your program grows in complexity, you find yourself creating modules or actually sets of modules that contain the following files: model/view/update/sub/msg
  - Except for the top-level `update`, we have to manage calling `update` in each of these lower-level Update modules. This is complicated further with the need to call Cmd.map.
  - Same goes for calling `view` in the View module. And like `update`, Subscriptions are complicated by having to call Sub.map.
- All of this Plumbing boilerplate is necessary because TEA doesn’t have a mechanism for handling anything but a single Update, Model, View, and Subscription at the top-most level. The rest is up to you.
- This is only part of the problem.

- State Management Nightmare
- Imagine when your user navigates to a page, you need to make multiple calls to the backend to retrieve data. 
  - There are two choices: make the requests in parallel or serial.
  - Those new to Elm may think that this code could be helped by an `async` library. That was my first reaction. I thought I could just build a function to do this, but you can’t because update functions must return to the Elm Runtime before all of the async calls have completed.
  - If you try to do this in a library, you’ll quickly realize that you’re burdening the caller with managing yet another update function and Model. The limitations of TEA really become apparent here.

- Spaghetti Execution
- We use Websockets in our app, but since we’re no longer allowed to write our own Effects Managers and since the Websocket support was recently removed from Elm, we are forced to do Websocket communication over Ports and write our Websocket code in Javascript.
- This means that we have to listen for messages coming back from the Websocket using Subscriptions in every single place Websockets are used.

- The real problem isn’t that the hammer is too small. It’s that the job is too big
- Learning the limitations of a tool is really important. 
  - You can work around them, but the cost is complexity and lines of code.

- My team has a ~half-million LOC Elm app in production and is having a similar experience with the Elm architecture. The signal-to-noise ratio of the code-base is just too low. The majority of the code is state plumbing rather than actual business logic.

## 🛑 [Elmish side-effect model probably ok for Elm - NOT for Redux](https://blog.javascripting.com/2018/09/26/why-elmish-side-effect-model-is-inferior/)

- Why I think Elmish side-effect model is inferior(低的，次要的)
- https://twitter.com/tomkisw/status/1044893049090961409
- Are you familiar with Rx and Cycle.js? That is the logical conclusion of events as the source of truth.
  - yup there’s technically no logical difference between generators with async semantics (redux-saga) and streams.
- 👉🏻 the difference with cycle is there is no state other than the event streams and everything is then derived from that. 🧐 Interestingly this was elms original approach but they have moved to the elm architecture as its simpler.
- I need to read it again. We've come to a similar realisation that declarative side-effects are not enough: you also need to be able to control and orchestrate their timing. Like in a typeahead where you want to debounce an input and cancel an inflight request.
  - You talking about event log being the source of truth rather than state is really helpful, I didn't think about it this way before and it gives me a lot of food for thoughts: so thank you

## 🌰 [On Endings: Why & How We Retired Elm at Culture Amp_202304](https://kevinyank.com/posts/on-endings-why-how-we-retired-elm-at-culture-amp/)

- Elm comes “batteries included” for building web apps, with virtual DOM rendering, managed state, effects, and subscriptions, and almost everything else you might need built in.

- Elm is easy to try inside React: an Elm app can run as a React component embedded in an React app
  - You can try Elm as an experiment by writing (or re-writing) a small rectangle of your app’s UI as an Elm app. 
  - You can try Elm as an experiment by writing (or re-writing) a small rectangle of your app’s UI as an Elm app. 
- Because some teams were building with React while others were building with Elm, Culture Amp’s design system, Kaizen, needed to support both 
  - It became more and more difficult to keep both versions of a component in sync. 
- The pain this caused our Design System team was enough to push us to start experimenting with Web Components
- In the end, our experiment revealed Web Components (even with a nice framework around them) to be different enough from both React and Elm that using them meant effectively adding a third view framework to our tech stack, with its own foibles, limitations, learning curve and maintenance burden
- we acquired another company whose entire codebase was written in React
- Around this same time the momentum around Elm’s own development and that of its tooling was losing steam. 
# more
- [Managed effects and Elm_201610](https://medium.com/@kaw2k/managed-effects-and-elm-36b7fcd246a9)
  - Normal Effects: for every step we go and (we) do it in real time.
  - Managed Effects: we describe a task and someone else does it on their own time.

- [Learning Elm by porting a medium-sized web frontend from React_201910](https://benhoyt.com/writings/learning-elm/)
  - I don’t know the language at a deep level yet by any means, but I didn’t feel I needed to explore every nook and cranny to get the project built.

- [Comparing Elm With Reflex_202103](https://typeable.io/blog/2021-03-22-reflex-vs-elm.html)
  - Reflex is a framework that allows creating reactive web applications in Haskell.

- [Using the Builder Pattern for Elm Components – Software, Fitness, and Gaming – Jesse Warden_202203](https://jessewarden.com/2022/03/using-the-builder-pattern-for-elm-components.html)
  - I had the opportunity to build some components and quickly found many needed a lot of parameters.
  - Builder Pattern is powerful in helping your API be easier to use, not having order problems, and preventing existing code from having to be changed if you add a feature.
  - this creates a ton of setter functions in your component code to support this style 
