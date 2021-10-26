---
title: thread-dev-pattern
tags: [dev, pattern, thread]
created: '2021-02-19T12:22:55.958Z'
modified: '2021-02-19T12:23:12.286Z'
---

# thread-dev-pattern

# pieces

- ## 

- ## being framework-agnostic
- https://twitter.com/dai_shi/status/1434543349524877317
  - I started developing `jotai` to solve a certain issue in React. 
  - Afterward, I realized that it's more than that, a reactive coding pattern, so to say. 
  - To prove that, `jotai-jsx` is developed as a PoC (for now), which runs jotai app without React.
- So, the answer is useState and useEffect.
  - jotai-jsx's atom+useAtom+useConstant is almost equivalent to React's useState+useEffect+useRef.
- Valtio is also developed to solve an issue in React, but soon made me realize its vanilla part is useful as is.
  - valtio/utils are not tied to React, and most jotai/utils are not tied to react either.
- We use Zustand/Valtio specifically because they are agnostic to the UI rendering layer, so we can isolate our business state for testing/portability/re-usability. 
  - Additionally, it's easier to use with events beyond the UI (e.g. network events) without adding components as glue
- We use Valtio specifically because is not tied to React. One of our applications uses non React layers for specific parts. Valtio allows us to easily connect the different layers. It's such a great library
- #ReactQuery is the same. Though I don’t believe you could run React with it 😆
  - In terms of being framework agnostic, I could just use the Query Client and QueryObserver in other frameworks, correct?
  - You’d want to mimic the life cycles of useQuery as much as possible.
  - https://github.com/DamianOsipiuk/vue-query

- ## API integrations are always 1:1. So the number of required integrations required for interop scales exponentially with the number of apps.
- https://twitter.com/gordonbrander/status/1430568224106508289
  - Files act as a hub around which an open set of apps can interoperate. So the number of integrations scales linearly with number of apps.
- “You can do this with a protocol too”. Yep, any kind of interchange. The more widely supported, the larger the combinatorial space.
  - We don’t see too many federated APIs. Just a few (IMAP, etc). I wonder why?
  - I sense one reason may be that APIs are directly controlled by the SaaS product. It’s private property, rather than neutral territory. Incentives to rent out access, rather than interchange.
- You could also just have them use one protocol. In fact you still need to do this with files, these programs have to all agree to write the same file format. If you can get that level of coordination, there's nothing stopping them from all exposing the same API.
  - The Language Server Protocol is exactly this, using JSON-RPC rather than a file format.

- ## Want an early look at the tldraw renderer?
- https://twitter.com/steveruizok/status/1420836276878577665
- The project is exported as two layers, and this is the “lower” of the two: it’s job is to render shapes and run even handlers.
- In this sandbox, we’re passing the renderer a “page” with shapes, together with a state for that page; and then using the renderer’s events to make changes to that page/state.
- the renderer doesn’t actually know what shapes we have, or how to render them, so we also pass it some “shape utilities” that it can use to work with/render the shapes.
- The regular tldraw editor (the second, “higher” layer) works the same way: it’s a collection of shapes, shape utils, and lots of logic around how canvas interactions should effect the page/page’s state.
- Why export both layers? 
  - For one, it’s a great way to experiment with new shapes and interactions without having to bring along all the tldraw-specific stuff. You could build anything on top of this renderer.
  - For another, it’s a good force to keep things small, fast and separate. Improvements are easier to make (and to notice) with the separate packages.
- And as an increasingly professional canvas UI guy Zipper-mouth face it’s a good to have a clean starting point should I need to prototype other kinds of primitives or interactions for clients/work/etc.

- ## I came up with some good patterns that prevent the code from getting mixed up.
- https://twitter.com/steveruizok/status/1420502623602552833
- Events are sent from the UI to the state machine, making the UI's event handlers very simple. They just toss events back to the machine.
  - The state machine decides what (if anything) to do with the event. Sometimes that's easy to figure out.
  - Either way, if an event just changes the app state, then it's handled with a regular action. 
  - But if an event changes the document then it's run through a "command".
- Commands create entries in the undo / redo stack. They have two methods: "do" that produces a change and "undo" that produces the opposite change.
  - Other actions lead to "sessions". A session has a lifecycle: it begins, updates many times, and then ends or is cancelled. Sessions produce state changes but they don't add to the undo/redo stack.
  - Sessions themselves can be complex, usually caching "snapshots" of data that are used throughout the session. This helps make behaviors like drawing much more smooth.
  - If a session completes, then it returns a command. This way, an interaction like dragging shapes (or "translating") will "undo" back to where the shapes were before the drag, ignoring all of the changes in between.
  - Since the commands and sessions all just operate on an object, they're really easy to test. I've been good on this rebuild to give everything at least cursory tests as I bring things over.
- My hope with this kind of architecture is that it's easy for a contributor to quickly focus in the part of the app they want to improve. Still bugs with transforming rotated shapes btw—any takers?
- Thanks Steve for your detailed post on state designer and command pattern.
  - I envy the way most of the code you put into the state. It makes individual components light weight.
  - But state is getting scary.

- ## full stack developer Tips, 对于可以为空的的属性
- https://twitter.com/ThaddeusJiang/status/1404252068064337922
- API: 
  - 为空则不返回，不要返回 null (这里我想说的是返回结果)
- Client: 
  - 声明：使用 optional properties，形如 name?: string
  - 调用：使用 使用 optional chaining operator，形如 name?.length

- ## Let's say you submit a form, via POST, to /form. 
- https://twitter.com/jaffathecake/status/1385485629392293890
  - Then, that page uses `pushState({}, '', '/foo')` to change the URL to /foo, without reloading the page.
  - If the user presses refresh, what do _you_ think should happen?
- First rule of form posts: return a 303 redirect (possibly to the same URL) to specifically avoid those kind of cases.
  - So I leave it to browser vendors to define what's best UX for those cases that everyone should avoid

- ## ReactQuery's `staleTime` default is 0ms and this gets a few people scratching their heads every now and then. 
- https://twitter.com/tannerlinsley/status/1385258144549330952
  - The explanation is pretty simple:
  - "How is the data on the screen always up to date?"
  - is a much better question to be asking than
  - "Why is my data not updating?!"
- I also recently discovered this behaviour when I was setting up react-query in a project. 
  - It went against my initial expectation but it does make sense to have 0 as the default to ensure up-to-date data always. 
  - If the concern is too many API request, it is easy to override.

- ## Two hard engineering problems that show up in all systems eventually:
- https://twitter.com/undef_obj/status/1382350128380485642
  - Dealing with distributed state
  - Handling concurrent updates
  - The more you learn about how to address these with different algorithms and systems, the better off you'll be in the long run.
- For enterprise systems I'd add a third:
  - Authorization and governance
  - It's an often overlooked(忽视的) part of enterprise development, but insanely difficult to manage at scale unless it's baked in.
  - Try to break the problem down to a more primitive state. What is authorization? It's taking the triple (user, operation, object) and applying it at runtime. This is state that must be consistent (see original tweet) or authorization is faulty.
  - I like to think of Authorization Metadata in terms of a Lampson Access Control Matrix

- ## It(vuejs) still blows my mind that I can make a living by giving away all the code I write for free.
- https://twitter.com/youyuxi/status/1382100303206625282
- You can do that because you CHANGE lifes.
- You are living a dream while helping people build the best they can.
- The fact about knowledge is the more you share, more you will get. You are legend mate.
- If you create something amazing, people will want to pay for even free stuff
- Vue is such a beautiful tool. So easy to do and maintain a semi-complex application. Vue Just changed my life. Thank you
- explain this business model
  - Adding value to the lives of others.
  - BUSINESS MODEL - COMPANIES AND GOOD PEOPLE SPONSOR HIS WORK WHICH BENEFITS EVERYONE, NOT JUST THEM.
- Does it blow your mind that companies then take that free code and charge extortionate rates for people to use it
- By the way, you make my job easier. 
- I’m very glad you’re making a living off of it, because me too.

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
