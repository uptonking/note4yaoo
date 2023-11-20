---
title: pattern-arch-flux-blog
tags: [blog, flux]
created: 2023-11-17T10:27:02.604Z
modified: 2023-11-17T10:27:12.776Z
---

# pattern-arch-flux-blog

# guide

# blogs-flux

## 🕹️ [Flux In-Depth Overview](https://facebookarchive.github.io/flux/docs/in-depth-overview/)

```
              <----- Action  <-----
             |                    ｜
Action -> Dispatcher -> Store -> View
```

- [flux-concepts](https://github.com/facebookarchive/flux/tree/main/examples/flux-concepts)

- Flux is the application architecture that Facebook uses for building client-side web applications.
  - It's more of a pattern rather than a formal framework
- Flux eschews(避开, 回避) MVC in favor of a unidirectional data flow. 
  - When a user interacts with a React view, the view propagates an action through a central dispatcher, to the various stores that hold the application's data and business logic, which updates all of the views that are affected. 
  - This works especially well with React's declarative programming style

- We originally set out to deal correctly with derived data
  - These dependencies and cascading updates often occur in a large MVC application, leading to a tangled weave of data flow and unpredictable results.
- Control is inverted with stores: the stores accept updates and reconcile them as appropriate, rather than depending on something external to update its data in a consistent way.
  - Nothing outside the store has any insight into how it manages the data for its domain, helping to keep a clear separation of concerns
  - Stores have no direct setter methods like setAsRead(), but instead have only a single way of getting new data into their self-contained world — the callback they register with the dispatcher.

- 👉🏻💡 unidirectional data flow is central to the Flux pattern
  - The dispatcher, stores and views are independent nodes with distinct inputs and outputs. 
  - The actions are simple objects containing the new data and an identifying type property.
- 👉🏻 All data flows through the dispatcher as a central hub
  - Actions are provided to the dispatcher in an action creator method, and most often originate from user interactions with the views
  - The dispatcher then invokes the callbacks that the stores have registered with it, dispatching actions to all stores. 
  - stores respond to whichever actions are relevant to the state they maintain.
  - The stores then emit a change event to alert the controller-views that a change to the data layer has occurred
  - Controller-views listen for these events and retrieve data from the stores in an event handler. 
  - The controller-views call their own setState() method, causing a re-rendering of themselves and all of their descendants in the component tree.
- This structure allows us to reason easily about our application in a way that is reminiscent(引起联想的) of functional reactive programming
  - Application state is maintained only in the stores, allowing the different parts of the application to remain highly decoupled. 
  - Where dependencies do occur between stores, they are kept in a strict hierarchy, with synchronous updates managed by the dispatcher.

- We found that two-way data bindings led to cascading updates, where changing one object led to another object changing, which could also trigger more updates. 
  - As applications grew, these cascading updates made it very difficult to predict what would change as the result of one user interaction. 
  - When updates can only change data within a single round, the system as a whole becomes more predictable.

### A Single Dispatcher

- The dispatcher is the central hub that manages all data flow in a Flux application.
- The dispatcher receives actions and dispatches them to stores that have registered with the dispatcher. 
  - Every store will receive every action. 
  - There should be only one singleton dispatcher in each application.

- It is essentially a registry of callbacks into the stores and has no real intelligence of its own — it is a simple mechanism for distributing the actions to the stores. 
  - Each store registers itself and provides a callback. 
  - When an action creator provides the dispatcher with a new action, all stores in the application receive the action via the callbacks in the registry.
- As an application grows, the dispatcher becomes more vital, as it can be used to manage dependencies between the stores by invoking the registered callbacks in a specific order. 
  - Stores can declaratively wait for other stores to finish updating, and then update themselves accordingly.

- the dispatcher is also able to manage dependencies between stores.

### Stores

- Stores contain the application state and logic.
- stores manage the application state for a particular domain within the application.
- a store registers itself with the dispatcher and provides it with a callback. This callback receives the action as a parameter. 
- This allows an action to result in an update to the state of the store, via the dispatcher. 
- After the stores are updated, they broadcast an event declaring that their state has changed, so the views may query the new state and update themselves.

- A store is what holds the data of an application. 
  - Stores will register with the application's dispatcher so that they can receive actions. 
  - The data in a store must only be mutated by responding to an action. There should not be any public setters on a store, only getters. 
  - Stores decide what actions they want to respond to. 
  - Every time a store's data changes it must emit a "change" event. 
  - There should be many stores in each application.

### Views

- Data from stores is displayed in views
- React provides the kind of composable and freely re-renderable views
- We call this a controller-view, as it provides the glue code to get the data from the stores and to pass this data down the chain of its descendants. 
- When it receives the event from the store, it first requests the new data it needs via the stores' public getter methods. It then calls its own setState() or forceUpdate() methods, causing its render() method and the render() method of all its descendants to run.
- We often pass the entire state of the store down the chain of views in a single object, allowing different descendants to use what they need

- When a view uses data from a store, it must also subscribe to change events from that store. Then when the store emits a change the view can get the new data and re-render. 
- Actions are typically dispatched from views as the user interacts with parts of the application's interface.

### Actions

- The dispatcher exposes a method that allows us to trigger a dispatch to the stores, and to include a payload of data, which we call an action.
- Actions are simple objects that have a `type` field and some data.
  - Actions should be semantic and descriptive 
  - They should not describe implementation details of that action.
- Remember that all stores will receive the action 
- The action's creation may be wrapped into a semantic helper method
- Actions may also come from other places, such as the server. This happens, for example, during data initialization

## 🕹️ [Fluxxor - What is Flux? flux vs mvc](http://fluxxor.com/what-is-flux.html)

- To best describe flux, we will compare it to one of the leading client-side architectures: MVC
- In a client-side MVC application, a user interaction triggers code in a controller. 
  - The controller knows how to coordinate changes to one or more models by calling methods on the models. 
  - When the models change, they notify one or more views, which in turn read the new data from the models and update themselves accordingly so that the user can see that new data.
- As an MVC application grows and controllers, models, and views are added, the dependencies become more complex.
  - 不知道是哪个model更新触发的view更新
- In the worst cases, a user interaction will trigger updates which in turn trigger additional updates, resulting in error-prone and difficult-to-debug cascading effects along several of these, sometimes overlapping, paths.

- Flux eschews this design in favor of a one-way data flow. 
  - All user interactions within a view call an action creator, which causes an action event to be emitted from a singleton dispatcher. 
  - The dispatcher is a single-point-of-emission for all actions in a flux application. 
  - The action is sent from the dispatcher to stores, which update themselves in response to the action.
- The flow doesn't change significantly for additional stores or views.
  - The dispatcher simply sends every action to all the stores in the application

- The flux architecture has a few key properties that make it unique and provide important guarantees, all of which are centered around making the flow of data explicit and easily understandable and increasing the locality of bugs
- Action dispatches and their handlers inside the stores are synchronous. 
  - All asynchronous operations should trigger an action dispatch that tells the system about the result of the operation
- Since stores update themselves internally in response to actions (rather than being updated from outside by a controller or a similar module), no other piece of the system needs to know how to modify the application's state. 
  - All the logic for updating the state is contained within the store itself. 
  - And, since stores only ever update in response to actions, and only synchronously, testing stores simply becomes a matter of putting them in an initial state, sending them an action, and testing to see if they're in the correct final state.
- actions tend to be semantically descriptive.
- No Cascading Actions
  - Flux disallows dispatching a second action as a result of dispatching an action. 
  - This helps prevent hard-to-debug cascading updates and helps you think about interactions in your application in terms of semantic actions.

## [How I converted my React app to VanillaJS (and whether or not it was a terrible idea) | Medium_201701](https://david-gilbertson.medium.com/how-i-converted-my-react-app-to-vanillajs-and-whether-or-not-it-was-a-terrible-idea-4b14b1b2faff)

- This little exercise started as a React replacement project, but quickly turned into a React appreciation project
  - Frameworks will often be doing a bit of extra work that you could avoid if you wrote the code yourself, this is true. But on the whole, I think this is a fair tradeoff for the improved productivity that comes with using a well-written framework that encourages some great practices.
# blogs-elm

## 🕹️ [The Elm Architecture · An Introduction to Elm](https://guide.elm-lang.org/architecture/)

- The Elm Architecture is a pattern for architecting interactive programs, like webapps and games.

- This architecture seems to emerge naturally in Elm. Rather than someone inventing it, early Elm programmers kept discovering the same basic patterns in their code.
  - projects like Redux have been inspired by The Elm Architecture

- Elm program always breaks into three parts:
  - Model — the state of your application
  - View — a way to turn your state into HTML
  - Update — a way to update your state based on messages
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

## 🤼🏻 [The Elm Architecture is the wrong abstraction for the web_202309](https://gist.github.com/chexxor/23ccf35add7dbdd33ecdd26888663140)

- There are lots of reasons to love The Elm Architecture:
  - It is easy to understand.
  - Easy time-travel debugging, due to highly restricted state. (not a feature worth designing an architecture around)
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

## [Elmish: Functional Programming in Javascript | by Chet Corcos | Medium_201602](https://medium.com/@chetcorcos/elmish-functional-programming-in-javascript-50995f1d4b9e)

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
# more
- [Managed effects and Elm. One really neat thing about Elm is that… | by Kevin Welcher | Medium](https://medium.com/@kaw2k/managed-effects-and-elm-36b7fcd246a9)
  - Normal Effects: for every step we go and do it in real time.
  - Managed Effects: we describe a task and someone else does it on their own time.

- [Learning Elm by porting a medium-sized web frontend from React_201910](https://benhoyt.com/writings/learning-elm/)
  - I don’t know the language at a deep level yet by any means, but I didn’t feel I needed to explore every nook and cranny to get the project built.
