---
title: note-dev-state-blog-event-pubsub
tags: [blog, pattern, state]
created: '2020-11-07T16:22:08.166Z'
modified: '2020-11-07T16:22:57.121Z'
---

# note-dev-state-blog-event-pubsub

## guide

## event-emitter

### [From Pub-Sub pattern to Observer pattern](https://medium.com/@huytrongnguyen1985/from-pub-sub-pattern-to-observer-pattern-f4ae1e425cc9)

- There are two major differences between Observer pattern and Pub-Sub pattern:
  - Observer pattern is mostly implemented in a synchronous way, 
    - i.e. the observable calls the appropriate method of all its observers when some event occurs. 
    - The Pub-Sub pattern is mostly implemented in an asynchronous way (using message queue).
  - In the Observer pattern, the observers are aware of the observable(Subject). 
    - But, in Pub-Sub pattern, publishers and subscribers don’t need to know each other. 
    - They simply communicate with the help of message queues.
- in Pub-Sub pattern we focus on publish/subscribe action 
  - while in Observer pattern we should focus on publisher and subscriber.

``` JS
class PubSub {
  constructor() {
    this.handlers = [];
  }

  subscribe(event, handler, context) {
    if (typeof context === 'undefined') { context = handler; }
    this.handlers.push({ event: event, handler: handler.bind(context) });
  }

  publish(event, args) {
    this.handlers.forEach(topic => {
      if (topic.event === event) {
        topic.handler(args)
      }
    })
  }
}

export default new PubSub();
```

- There are two main strategies for observer pattern:
  - Push behaviour — when an event happens Observable object will notify all Observers by sending all the new data to them
  - Pull behaviour — when an event happens Observable object will notify all Observers and each Observer will pull the information it needs from the Observable
- The most popular library for Observer pattern is RxJS with those concepts

### [Understanding Event Emitters](https://css-tricks.com/understanding-event-emitters/)

- https://github.com/charliewilco/cyclops

``` typescript
interface Events {
  [key: string]: Function[];
}

// class is just a preference. Storing events in an object is also a preference. 
// We could just as easily have worked with a Map() instead. 
export class EventEmitter {
  public events: Events;
  constructor(events?: Events) {
    this.events = events || {};
  }

  public subscribe(name: string, cb: Function) {
    (this.events[name] || (this.events[name] = [])).push(cb);

    return {
      unsubscribe: () =>
        this.events[name] && this.events[name].splice(this.events[name].indexOf(cb) >>> 0, 1)
    };
  }

  public emit(name: string, ...args: any[]): void {
    (this.events[name] || []).forEach(fn => fn(...args));
  }
}

//  we could do all of this with a function
function emitter(e?: Events) {
  let events: Events = e || {};

  return {
    events,
    subscribe: (name: string, cb: Function) => {
      (events[name] || (events[name] = [])).push(cb);

      return {
        unsubscribe: () => {
          events[name] && events[name].splice(events[name].indexOf(cb) >>> 0, 1);
        }
      };
    },
    emit: (name: string, ...args: any[]) => {
      (events[name] || []).forEach(fn => fn(...args));
    }
  };
}
```

## ref
