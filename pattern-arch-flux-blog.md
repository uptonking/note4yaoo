---
title: pattern-arch-flux-blog
tags: [blog, flux]
created: 2023-11-17T10:27:02.604Z
modified: 2023-11-17T10:27:12.776Z
---

# pattern-arch-flux-blog

# guide

# blogs-flux

## 🧩 [Flux In-Depth Overview](https://facebookarchive.github.io/flux/docs/in-depth-overview/)

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

## 🧩 [Fluxxor - What is Flux? flux vs mvc](http://fluxxor.com/what-is-flux.html)

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

## 🆚️ [Unidirectional User Interface Architectures_201508](https://staltz.com/unidirectional-user-interface-architectures.html)

- 👥 [Unidirectional user interface architectures | Hacker News_201508](https://news.ycombinator.com/item?id=10115314)
  - The overview is really great, but I think you only scratched the the surface. With ambitious task to cover such a broad topic, it's hard to go into all details in one post
# more
