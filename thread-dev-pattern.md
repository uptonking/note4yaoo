---
title: thread-dev-pattern
tags: [dev, pattern, thread]
created: '2021-02-19T12:22:55.958Z'
modified: '2021-02-19T12:23:12.286Z'
---

# thread-dev-pattern

# pieces

- ## 

- ## where does the idea that immutability is good come from?
- https://twitter.com/_binary_search/status/1362666809682444289
- Predictability. 
  - we want to easily reason about the code we write. 
  - mutations are not friendly with this, they can be wrong and get *lost* easily.
- I don’t know where the shared belief is coming from 
  - but to me it follows straight from the idea that you its good to be able to reason about code in a small context. 
  - With mutability you have to remember more.
- Having more data that you might not need is better than losing data you might need. 
  - When you mutate, you throw away the old state in the abyss(深渊，无底洞)
- If you pass it into another function you know it will not be mutated. 
  - Also you don’t have to copy the whole data structure just to be sure, 
  - and data structures can be efficiently shared if you know there are no mutations.
- An example, although a bit older, is change detection in components:
  - So if I pass down an object to the component and mutate that object by changing a value, the component doesn't know that something has changed. UNLESS it deeply watches all the object's props
  - If the component could count on the immutability of props, it would only need to watch for reference changes. That is performing much better than deeply watching all props.
- When u want to make undo function 
- People who find synchronization processes costly said that.. immutability is good !!!
