---
title: lib-fwk-nodejs-trpc-community
tags: [backend, community, nodejs, trpc]
created: 2022-11-03T09:43:51.167Z
modified: 2022-12-19T01:50:43.427Z
---

# lib-fwk-nodejs-trpc-community

# guide

# discuss
- ## 

- ## [Let's Learn tRPC!](https://www.learnwithjason.dev/let-s-learn-trpc)
- So traditionally speaking when you do an API nowadays, you probably want to document your API somehow with a schema or something like that. 
  - So there are two main ways of doing APIs today. 
  - One is swagger/open API schemas or GraphQL. 
- But when you're working with either Open API or GraphQL, you sort of bring in a new language into the stack. 
  - Either it's YAML or GraphQL, even though your both front and back end might be written in the same language. 
- So what tRPC tries to do is instead of you having a clunky API definition, you just write functions on your back end. 
  - Then you can infer the type signature of those functions on your client. 
  - So it completely removes the need for an API schema because it's guaranteed by TypeScript itself. 
- 👉🏻 So RPC stands for remote procedure call. So tRPC is TypeScript remote procedure call. It helps you to call remote functions on your client.

- is this related to gRPC?
  - No, it's not related at all. It's a common misconception because of the similarity of the names. But both are sort of RPC-inspired things, right.

- ## [Naming / other transports / JSON-RPC · Issue #6 · trpc/trpc](https://github.com/trpc/trpc/issues/6)
- the name trpc sort of implies it being a generic RPC and not a specific type of transport
- still, there's a lot of http concepts (status codes) etc

- ## [Why isn't JSON-RPC more widely adopted? | Hacker News](https://news.ycombinator.com/item?id=34211796)
- I was told by the author of tRPC, that they use JSON-RPC behind the scene.
- Whoa, that's news to me. Is this called out anywhere online? I've been following tRPC a bit and it looks really great. I only wish it wasn't locked into using TypeScript on the server.
  - It's the dream dev experience I've been chasing. I'm trying to get as close as I can using auto-generated gRPC-Web.

- I have experience working on some JSON RPC Load Balancer, and I can tell that it's one of the worst choices for an API:
  - Method Name is a part of the body itself. So you have to parse it to make a decision on how to dispatch it. That's an extra cost.
  - Error Code is a part of the response. So you have to parse it each time to figure out if it's a success. Also, some clients just give an HTTP Error Code instead. So you have to handle both.
  - It can also be batched. Which introduces a lot of unspecified use cases.
  - Like how are you supposed to dispatch those batched? Should they go to the same upstream? Or can it be parallelized? Should the order be preserved?
  - With batches, the slowest request always blocks the in-flight response. You have to wait for all calls to be finished before producing a final response. That's a huge performance bottleneck. Also, what you do if some of them never finished?
  - A lot of uncertainties about the ID. Especially because it can be a different type (int or string), which sometimes introduces two different handlers in the code. And there are no guarantees IDs are not repeating in the same batch. To make it worse, some clients rely only on the request/response order ignoring the IDs.
  - Another problem is that it has no idea of Metadata, which is important for many real systems. For example, to do an Auth. Or do Caching and other optimizations.
- So as an outcome, everyone just makes two layers. On the HTTP level, you have auth, routing, error handling, multiplexing, etc. And then you realize that JSON RPC only introduces extra complexity.
- Graphql shares many of the same issues. 

- JSON-RPC/OpenRPC seems like a great option for APIs. Why isn't it adopted more widely?
  - [OpenRPC](https://open-rpc.org/) Specification defines a standard, programming language-agnostic interface description for JSON-RPC 2.0 APIs.
- Parsing makes it hard.
  - Consider writing an HTTP based RPC server. I parse the first line. It tells me the location and the method. Followed by a bunch of key value pair headers where both the key and the value are strings.
  - So far so good, I could write all of the above in C or Go pretty easily. Finally comes the body. I can unmarshall this in Go or parse this in C easily because I can I know what to expect in the body by the time I get there. This is because I already know the method and location.

- Contrast this with JSON RPC. I have to partially parse the entire object before I know what function is being called. Only then can I fully parse the arguments because I don't know what type they are (or in other words, which struct the arguments correspond to) until I know what function is being called, what version of RPC is being used, etc.
  - Super annoying. And HTTP is just sitting there waiting to be used.
  - HTTP allows for incremental parsing. I can parse the first few lines separately from the body. It makes handling input really nice.
  - Having everything in a single JSON object doesn't allow for incremental parsing because the standard says I can't guarantee order of key value pairs when an object is concerned.

- JSON RPC tends to embed credentials into the body, where REST puts them in the URL string or headers. This gives you the advantage of load balancers being able to fast drop misbehaving clients for load shedding. You also have the security advantage of authenticating a legitimate client before handing off the payload to a parser (both as a DoS vector, or the risk of parsing untrusted data).

- When I’ve considered JSON-RPC in the past, the lack of easily identifiable URLs was the main drawback in my mind due to the difficulty of testing and debugging—the same reason I would never use gRPC or similar on my own projects. That said, I think a well-made browser extension would fix this issue for most people, similar to GraphQL, but it still introduces friction that isn’t immediately beneficial. I’d still give it a try in the future!

- gRPC actually does have easily identifiable URLs. Protobufs can be heavyweight, but it's trivial to use a different encoding like JSON.

- The problems with JSON-RPC are mostly in its design, it's not ergonomic and its type system is a joke. There are many better alternatives ranging from gRPC (still not ergonomic and not modular) to Protoforce (extremely powerful and ergonomic but only marginally adopted).

- It's not that parsing JSON to a JSON-like data structure is hard. That's easy.
  - It's the overhead of having to parse it to a generic JSON-like data structure at all, before knowing what the keys and values mean, so you can then transform the JSON-like data structure to the program's API structs.
- If you knew the shape of the RPC method before parsing the JSON body, the body would be parsed directly to target language structs and variables, without using any generic key-value objects (dicts/hashes/maps), any generic arrays, or even any strings in some cases (when JSON strings represent enums). 
  - For many RPCs there would be no memory allocations during JSON body parsing. 
  - But you don't know the shape, so you either have to allocate memory and store the input in key-value objects, arrays and strings temporarily, or parse the JSON body in two passes, the first pass to get the shape for the second pass.

- Methods can be expressed in http method, and resource can be expressed in url. Response status can be expressed in http statuses.
  - Some people prefer that for lower payload size. Others prefer byte encoded payloads like msgpack instead of json. In trading platform api's i've noticed that.
  - Also, using url based resources lets you route these requests at the network proxy level (caddy haproxy nginx envoy traefik etc).

- JSON-RPC isn’t that much better than passing your own JSON formatted messages over HTTP. So I don’t think it gets you too much incremental value these days.
  - REST is a form of an RPC. 

- ## [Is a monorepo mandatory?](https://github.com/trpc/trpc/discussions/1860)
- No, a monorepo is not mandatory but you will lose some of the benefits of using tRPC if you don't use it since you will lose guarantees that your client and server works together.
  - One way you can leverage tRPC is to publish a private npm package with the types of your backend repo and consume them in your frontend repo.

- I tried generating a TS declaration file to share TS types with other projects, and it seems to be working properly.
  - On backend, generate a server.d.ts file.
  - On frontend, copy and paste server.d.ts and import it 
  - I also think it'd be great if trpc implements a functionality for generating a type file, instead of having to do the above.
