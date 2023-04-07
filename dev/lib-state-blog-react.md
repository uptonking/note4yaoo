---
title: lib-state-blog-react
tags: [blog, react, state]
created: 2020-11-07T13:14:54.931Z
modified: 2021-05-13T03:13:09.493Z
---

# lib-state-blog-react

# react-state-blog

## [React: Event Emitter](https://medium.com/@lolahef/react-event-emitter-9a3bb0c719)

- https://github.com/lolax/React-Insta-Clone

- You want a grandchild component to be able to trigger its grandparent component’s method in React. 
  - You could pass the method as a prop down the family tree of components to the appropriate grandchild component 
  - (this is an example of **prop drilling**).
- But there are some issues with this prop drilling pattern:
  - It can require a great deal of repetition
    - For example, intermediate components must act as messengers between the desired endpoints (grandparent & grandchild), which makes the event coordination brittle
    - if you remove or refactor any component in the middle of the chain, it can break your app
  - Furthermore, this pattern becomes more and more cumbersome the deeper your nested components go. 
    - You may have a parent component with 5 layers of nested children, and even if only the final child needs the prop drilled function, the prop still has to pass through every single intermediary.
  - Personally, this pattern feels unnatural in that it doesn’t structurally reflect my intent. 
    - My desire is to have a grandchild of arbitrary depth be able to signal for the invocation of a function that belongs to its grandparent of arbitrary depth. 
    - Ideally, I would even be able to do this across non parent/child component relationships, like sibling or cousin components, which is not easily accommodated by prop drilling.

- Instead of passing a function down as a prop in order to let the grandchild update the grandparent’s state, you could also pass down an initial state (an object, not a function). 
  - Then, have the grandchild update that state locally however it likes.
  - 父传子传状态值，然后子组件使用传入的值作为自身状态初始值
- There are a number of issues with this distributed state pattern:
  - It creates multiple (conflicting) sources of truth, undermining the integrity of state
  - It doesn’t effectively resolve the core issue with event communication between distant components, just works around it 
    - (i.e., you still can’t communicate between sibling or cousin components)
  - It is essentially a more intuitive but less effective method of prop drilling than just passing a function. 
    - It may be easier to reason about an object being passed as a prop, 
    - but this pattern has all the downsides of the regular function passing prop drilling pattern, as well as its own problems.

- I’m here to offer you an alternative to these two approaches, which instead meets the following criteria:
- Establishes a single source of truth
- Eliminates intermediate messengers & reduces prop drilling
- Better isolates responsibilities of stateful & functional components 
  - (ie. stateful components are responsible for calling their own methods to update state; 
  - functional components aren’t directly acting on state)
- Relatively simple to implement; doesn’t require external libraries

- The alternative I prefer is to use an event emitter. 
  - An event emitter establishes a direct line of communication between the two desired endpoints, removing the need to pass event information (data, callbacks) through intermediate components. 
  - The event emitter that I implemented has two types of actions — dispatch and subscribe. 
  - These aren’t special keywords; they could instead be called publish and subscribe (pub-sub), send and receive, speak and listen, egg and mango, etc. 
  - It is important to note that more actions can be defined and used, such as unsubscribe (which would be important in non-trivial applications).

``` JS
export const EventEmitter = {
  events: {},
  dispatch: function(event, data) {
    if (!this.events[event]) return
    this.events[event].forEach(callback => callback(data))
  },
  subscribe: function(event, callback) {
    if (!this.events[event]) this.events[event] = []
    this.events[event].push(callback)
  }
}
```

- First, I need to define the event emitter, which is simply an object that we can import to other components as needed.
- Next, I want to import EventEmitter to components that will be subscribing to an event and then set up the subscribe functionality. 
- Finally, I will repeat those same steps for the dispatch: import EventEmitter and set up the dispatch functionality.
- Now your components have a direct line of communication to coordinate events!

- Let’s revisit the benefits of this approach:
  - Single source of truth
  - Event coordination transcends the hierarchy of your app’s composition and eliminates the need for intermediary messenger components to be passed event-related props for components that need them farther down the tree
  - The core idea is familiar and reflected in human interaction
  - Scales effectively with project/component tree complexity

- A few drawbacks to note:
  - The setup it requires may be more work than it’s worth for simple or flat applications with minimal event-related communication between components
  - It may be confusing to other developers, although event emitters are a widespread pattern, as referenced below.
  - If you want to pass multiple parameters to this event emitter, you’ll need to contain them in a single object or array

- Node, Vue, and Angular all feature some variation of built-in event emitters or an event bus. 
  - Redux handles this exact task, as well. 
  - It takes a bit more work to use an event emitter in pure React, but I’ve found the effort to be worthwhile

- *discussion*

- For this type of IOC, i would rather use React. Context coupled with useReducer to pass down the context the “dispatch” object, rather than introduce a new paradigm(模式，范例) inside React. Is there any reason why this pattern would not be up to it ?
  - Plus, this paradigm existed long before React. Tailoring interfaces (component props) to handle implementation details (class methods) has also long been frowned upon.
  - I think that would work in a very large app with lots of React. 
    - To me the pub/sub model described above has less developer overhead and less boilerplate. 
    - I feel like this would be easier to read, especially if the Redux model is unfamiliar to the reader. 
    - If js itself offers the tools to get the job done why run into framework-specific details when you don’t have to?

- I like having the Event Emitter (event bus, etc) be a separate simple object rather than a framework piece. And yes, you definitely want unsubscribe.
  - One other point for consideration is that this implementation may have been a singleton?
  - I’ve found that I often want two types of emitters, one that is scoped only to a component, so it can’t leak and other components can’t eavesdrop(窃听). 
  - And then I want a “global” emitter to facilitate component to component integration — and this one should be a singleton to make things easier to integrate.

- A nice and clean approach, but it reduce the reusability of components.

- This is a nice approach and gives lot of functionality with least headache and will also be very fast to implement and change.
  - But this definitely needs an unsubscribe function.
  - A probable solution is to just store each subscribe with a subscribe key(as a dict of key->function) and loop thru key for that event on fire
  - Without unsubscribe, we would left with multiple subscriptions on component re-creations(if that happens for some reason)
  - I have been using vanilla js callbacks and functions inside of our react application 
    - and the memory footprint of the app is really low as compared to pure redux state based model(event after being careful of multiple state changes and after using very light weight selectors)

- How would you approach a situation where the grandparent component needs to subscribe to events from the grandchild component, but you want to uniquely identify the events so that only that one particular instance of the grandparent component subscribes.
  - The eventName is just a string. 
  - In the form, you can create a unique id and use that in the subscribe event string.
  - You would then need to pass this id down to all of the children/grandchildren, but it would be just a single string and not an actual callback. 
  - Every child even could use that same string when publishing to an event. 
  - So if there are 10 possible events that could be called, you don’t have to pass all 10 callbacks down, just this one string that they all use in the event name when publishing.

- This is pretty clean. 
  - But the problem is there is no way to subscribe to a local event. 
  - Any component can subscribe to any event and so in a large scale application it will become tuff and confusing to where is the event being fired from? 
  - (For ex: If a developer is debugging some part of the app, they might not find where the event is firing from so it would consume time and confusion in terms of developer experience)
  - If we can find a way to localize these parent events, then it will become trivial during the debug where the or how the data is manipulated and flowing. And we can prevent unexpected bugs.

## [Event Emitter instead of lifting state up in React](https://medium.com/@krzakmarek88/eventemitter-instead-of-lifting-state-up-f5f105054a5)

- https://github.com/krzaku281/react-event-emitter

- Everybody knows lifting state up hell in our small applications. 
  - Where Redux or different state manager that is too much. 
  - But without that when we want to sharing state for distant component. 
  - We have to find the closest common ancestor and next passing through all descendant components till state will be pass to proper.
- Unfortunately, when that situations will be frequent, application will become unmanaged, components huge and code dirty
- Event emitter has some useful functions:
  - on, adds listener and start listening on specific events
  - off, removes listener for specific event type
  - once, like above but after first event occurrence
  - emit, invokes event and can add payload when is needed
- In React applications without any state library (e.g. Redux), we should find the closest common ancestor where we will keep state and keep handling function for click. 
  - Next pass handling function and state from ancestor to main, sidebar and header and connect them in that components. 
  - Then in header component add some logic to handling only first state change.

``` JS
import EventEmitter from 'eventemitter3';

const eventEmitter = new EventEmitter();

const Emitter = {
  on: (event, fn) => eventEmitter.on(event, fn),
  once: (event, fn) => eventEmitter.once(event, fn),
  off: (event, fn) => eventEmitter.off(event, fn),
  emit: (event, payload) => eventEmitter.emit(event, payload)
}

Object.freeze(Emitter);

export default Emitter;
```

``` jsx
import React from 'react'
import Emitter from '../services/emitter';
import '../styles/Main.css';

class Main extends React.Component {
    state = { inputValue: '' };
    
    handleOnClick = e => {
        // 触发事件，发送数据
        Emitter.emit('INPUT_FROM_MAIN', this.state.inputValue);
    }
    
    render() {
        return (
            <div className="main">
                <h3>Main content</h3>
                <input type="text" value={this.state.inputValue} onChange={(e) => this.setState({inputValue: e.target.value})} />
                <input type="button" value="Send to other components" onClick={this.handleOnClick} />
            </div>
        )
    } 
}

export default Main

import React from 'react'
import Emitter from '../services/emitter';
import '../styles/Sidebar.css';

class Sidebar extends React.Component {
    state = { sidebar: 'Default sidebar' };

    componentDidMount() {
        // 执行监听，接收收据
        Emitter.on('INPUT_FROM_MAIN', (newValue) => this.setState({ sidebar: newValue }));
    }

    componentWillUnmount() {
        Emitter.off('INPUT_FROM_MAIN');
    }

    render() {
        return (
            <div className="sidebar">
                <h3>{this.state.sidebar}</h3>
                <div>Sidebar listens on new input all the time. Don't forget clean up when destoy component.</div>
            </div>
        )
    }
}

export default Sidebar
```

# ref

- [One way to manage React global state with EventEmitters](https://gist.github.com/mhart/6ca15a54541caae04a075db76b68c06c)
