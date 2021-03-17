---
title: thread-dev-pattern
tags: [dev, pattern, thread]
created: '2021-02-19T12:22:55.958Z'
modified: '2021-02-19T12:23:12.286Z'
---

# thread-dev-pattern

# pieces

- ## 


- ## 


- ## Which approach would you prefer for defining CORS?
- https://twitter.com/lukeed05/status/1369145056460906499
  - Option 1 - an `options` argument. The negative is that this requires addl runtime code *even if* you never enable CORS.
  - Option 2 – a "prepare" hook that lets you do anything.
  - Please note that these would *very likely* be mutually exclusive. AKA, `prepare()` supersedes `options.cors` and vice versa.
- So I think most votes for `Option 1` are so that you don't have to deal with the CORS header names. I get it.
- I like the option 2 because it teach you the headers + you don't have the overhead of thinking how your API maps into actual CORS headers.

- ## How do you prefer to name hooks that provide booleans and their results?
- https://twitter.com/erikras/status/1367029738880061441
  - let foo = useFoo()
  - let isFoo = useFoo()
  - let isFoo = useIsFoo()
- “Asymmetric非对称的 naming” (second) case it the most beneficial, and the most hard to constantly follow
- I never have a single value returned from a hook, I always use an object. 
  - Everytime I ever tried that, I ended up wanting to add more elements to be returned and having to refactor all the consumers of the hook.

- ## Folks who have are familiar with both Protobufs/gRPC and GraphQL (incl Relay/Apollo/Amplify etc) 
- https://twitter.com/swyx/status/1364852210144747522
  - how would you compare/contrast their priorities and ideal usecases?
- I've used both extensively for years (and Avro) I'd rank them GraphQL > Avro > Protobufs which hurts, because I'm a Gopher first. 
  - GraphQL's schema IDL expressiveness and tooling is first-rate. 
  - Avro has amazing back/forward compat tooling, and protobufs is ...protobufs.
  - Clearly my preference is explicit types, good tooling, clear docs, and performance behind that. Avro and protob are within a negligible % of each-other. But Avro works best (along side Apache Parquet) for the long-tail of BI/reporting needs in my org.
  - gRPC on the other hand, multi-plexing stuff screaming fast over HTTP2 between [micro] services feels so fast, you can hardly believe there's a network in the middle, but the cost in debuggability and being stuck with protob is kinda high.
  - I would favor GraphQL for anything "user facing" (incl internal) with a well written schema (in the original schema definition language, not in some "compiles from my language to SDL). For speed, archival, "downstream" reporting, etc I'd take Avro
- Go with REST/GraphQL when you start.
  - Introduce gRPC only when REST/GraphQL does not fit the scope.
- Protobuf suits fast-evolving systems i.e back-end services through “non-breaking” flexibility: versioning, reserved fields, non-breaking name changes (preserves index)
  - GraphQL suits more change-sensitive systems (client-side apps)
- Every technology has an inciting use case, and then we try to extend it and turn it into the uber-tool, sometimes to the detriment of the original tech. The extensibility of both I think is still being determined.

- ## Where is the course to learn how to manipulate ASTs so I can do cool things 
- https://twitter.com/ryanflorence/status/1362840515725590528
- [A talk](https://speakerdeck.com/xjamundx/hiking-through-the-javascript-forest) about Abstract Syntax Trees (ASTs) in JavaScript and how to use them to create codemods and eslint rules

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
