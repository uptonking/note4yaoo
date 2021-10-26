---
title: note-react-event
tags: [events, react]
created: '2021-08-13T17:53:53.973Z'
modified: '2021-08-13T17:54:06.302Z'
---

# note-react-event

# guide

# discuss

# blogging

## [React 17 removes event pooling in the modern browsers](https://blog.saeloun.com/2021/04/06/react-17-removes-event-pooling-in-modern-system.html)

- The SyntheticEvent objects before v17 are pooled.
  - This means, when an event is triggered, React takes an instance from the pool, populates its properties and, reuses it.
  - To assure consistent usage of the pooled events, React nullifies the properties of synthetic events right after executing an event handler.
  - This method saves allocations during high firing events, but adds a bit of overhead in “releasing”, “destroying” and “reusing” instances.
- Though Event Pooling was built to increase the performance, it didn’t improve the performance in modern browsers. 
- It also confused developers. 
  - For example, not being to access `event.target` in the `setState`.
  - Basically, the click event (e) is not accessible inside the asynchronous setState() due to React's Event Pooling, unless you use `event.persist()`

```JS
// not working for < v17
updateValue = e => {
  this.setState({
    value: e.target.value
  })
}

// works
updateValue = e => {
  const newValue = e.target.value
  this.setState({
    value: newValue
  })
}
```
