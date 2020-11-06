---
title: page-algs-design-pattern
tags: [design-pattern]
created: '2020-11-06T13:31:45.556Z'
modified: '2020-11-06T13:32:07.601Z'
---

# page-algs-design-pattern

## summary

## design-patterns

### [Observer vs Pub-Sub pattern](https://hackernoon.com/observer-vs-pub-sub-pattern-50d3b27f838c)

- The `observer pattern` is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.
- The Subject in the Observer Pattern is like a Publisher and the Observer can totally be related to a Subscriber 
- and Yes, the Subject notifies the Observers like how a Publisher generally notify his subscribers. 
- That’s why most of the Design Pattern books or articles use ‘Publisher-Subscriber’ notion to explain Observer Design Pattern. 
- But there is another popular Pattern called ‘Publisher-Subscriber’ and it is conceptually very similar to the Observer pattern. 
- In `Publisher-Subscriber` pattern, senders of messages, called publishers, do not program the messages to be sent directly to specific receivers, called subscribers.
- This means that the publisher and subscriber don’t know about the existence of one another. 
- There is a third component, called broker or message broker or `event bus`, 
  - which is known by both the publisher and subscriber, 
  - which filters all incoming messages and distributes them accordingly.
- In other words, pub-sub is a pattern used to communicate messages between different system components without these components knowing anything about each other’s identity. 
- how does the broker filter all the messages?  
  - Most popular methods are: Topic-based and Content-based

- Let’s list out the differences as a quick Summary:
  - In the Observer pattern, the Observers are aware of the Subject, also the Subject maintains a record of the Observers. 
    - Whereas, in Publisher/Subscriber, publishers and subscribers don’t need to know each other. 
    - They simply communicate with the help of message queues or broker.
  - In Publisher/Subscriber pattern, components are loosely coupled as opposed to Observer pattern.
  - Observer pattern is mostly implemented in a synchronous way, i.e. the Subject calls the appropriate method of all its observers when some event occurs. 
    - The Publisher/Subscriber pattern is mostly implemented in an asynchronous way (using message queue).
  - Observer pattern needs to be implemented in a single application address space. 
    - On the other hand, the Publisher/Subscriber pattern is more of a cross-application pattern.

- Despite the differences between these patterns, some might say that Publisher-Subscriber pattern is a variation of Observer pattern because of the conceptual similarity between them. And it won’t be wrong at all. Don’t need to take the differences religiously. 
