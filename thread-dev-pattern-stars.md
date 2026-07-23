---
title: thread-dev-pattern-stars
tags: [dev, pattern, refactor, thread]
created: 2021-04-07T10:20:26.431Z
modified: 2023-11-29T15:23:06.805Z
---

# thread-dev-pattern-stars

# guide

# discuss
- ## 

- ## 

- ## 

- ## 之前看的一篇文章 在 AI 时代真的不需要 SDK 了，我把几个 SMS 的服务从 SDK 直接改写成了基于 HTTP 请求的 thin wrapper。
- https://x.com/CatChen/status/2079949032395596134
- 问题是将来维护的成本全转移到你身上了，HTTP API 更新了你可能就要对应更新。更关键的是你不知道 API 什么时候会更新，你可能为此又要多部署一个监控 API 有没有发生重大变化的服务。
  - 同意啊，本来可以外包给别人的时间和别人的token的事情，反而hand writtenSDK，没有必要。 在AI的时代，重复造轮子的事情依旧存在。

- 生产用这种代码，后续对方的接口和协议变更，你没有及时跟进调整，怎么解？正常引入官方 sdk还可以快速升级一下 sdk（稳定性和维护性由厂商兜底）。这种让 AI 快速读源码然后提取精装版的行为不可控，sdk 有些极端场景会考虑和兜底，精简代码遇到直接扑街。

- ## I wrote up a bit about the different types of cancellation/unregistration that exist, and why AbortSignal is a solid choice for DOM Observables in JavaScript.
- https://twitter.com/BenLesh/status/1729970596715376698
  - I think it's worth sharing, because it's a general API design choice some folks need to make. "What's the best way to add and remove some resource like a callback from some other thing?"
- [How to removeEventListener? · WICG/observable](https://github.com/WICG/observable/issues/75#issuecomment-1832698540)
  - Return a means of removing the resource, (RxJS does this with `subscribe(): Subscription` , other APIs might return a removal function like `subscribe(cb: Callback): UnsubscribeFunction` , etc.
  - Provide a separate unregistration function. This is what `addEventListener` and `removeEventListener` are. Or think of like the Observer pattern's Subject: `addObserver/removeObserver` , etc.
  - Allow the consumer to pass in a token-based cancellation mechanism. This is `AbortSignal` , or in something like . NET, `CancellationToken` , etc.
- Every single one of the above is just a different way to do the same thing. They all have advantages and disadvantages.
- `AbortSignal` has the most advantages for `Observable` because it allows the cancellation mechanism to be created before the subscription starts, when the subscription could emit values synchronously (as is required of anything that is going to model `EventTarget` ). It's also nice because there's no need to keep the `EventTarget` instance itself on-hand to unregister the listener, like you would if you had to use `removeEventListener` .
  - Sort of: You not only have to have a handle to your function, but you must also have a handle to the actual target as well, AND you have to know the "magic string" it was registered under. So you need 3 components: `target.removeEventListener('type', func)` . With an `AbortSignal` , you only need to have a reference to the `AbortController` to unregister the listener.

- removeEventListener has to be the most annoying thing in JS. Thankfully in modern JS there's usually a nice framework wrapping it.
  - Terribly, in some cases (DOM events), you need 4 pieces of information to remove a listener! In addition to the three you mentioned, you also need to know whether the listener was added for the capture or bubble phase of the event.

- ## 📝 [Things I Regret: Returning Modified Data In API Response Payloads](https://www.bennadel.com/blog/4019-things-i-regret-returning-modified-data-in-api-response-payloads.htm)
- https://twitter.com/BenNadel/status/1377583041263058949
  - After working on the same application for close to a decade, one software architectural decision that I've come to really regret is returning modified data in an API response payload. 
  - I really wish I had been better about apply CQRS in my code.
  - CQRS强调的是 command与query访问的数据模型不同，分别根据command与query需求的不同特性设计数据模型
- one software architectural choice that has bitten me is the decision to return modified data in an API response payload. 
- If I could go back and rebuild all mutation requests, I **would design them to return confirmation data only - no entity data** .
- To understand what I mean, imagine that we have a web application that has a Contact entity. 
  - And, I have an API end-point that allows me to rename the Contact with a POST request
  - `POST /api/contact/4/rename?name=Hanna+Banana` .
  - Historically, in my web application, this POST request would execute the use-case - renaming the Contact - and would then return the Contact data with the new name field in tow(紧随着，陪伴着)
- If I were to build this POST request today, however, I would code this to return a 204 No Content response. 
  - A 204 is a success code, confirming that the POST request was handled by the application; however, it wouldn't contain any other data.
  - **If the client-side application needed the modified data** , it could either optimistically update its own view model locally as part of the request processing; or, it could make a subsequent request back to the server to get the modified data for its view.
- In the case of a create request, such as to create a new Contact record within the application, I would return a 200 OK with a response payload; 
  - but, it would only contain the unique identifier of the newly-created Contact (assuming synchronous processing).
  - And, again, if the client-side application needed the fleshed-out data for the newly-created Contact record it could either optimistically update its own view-model locally; or, it could make a subsequent request - using the returned id value - to get the fleshed-out Contact record. 
  - The client-side application could even do both (an optimistic update locally plus a subsequent request to the server as the source of truth).
  - in the long-run, I think it would have forced us to keep our code much, much cleaner and easier to maintain and evolve over time.
- This is Really Just Command-Query Responsibility Segregation(隔离) (CQRS)
  - Inherently, there's nothing really wrong with returning state in a "command" request. The problem is, People are sloppy; and lazy; and have an irrational fear of code duplication. 
  - And this causes them to make code worse over time by coupling command-request responses to application views.
  - Now imagine how this sloppiness can build-up over time. First it's an avatarUrl, then it's a isLoggedIn flag, then it's a lastContactedAt timestamp. 
  - Slowly, and eventually, the data requirements for different application views leak out into the rest of the application.
  - Not only does this mean more data over the network, it also means more processing time on the server and a markedly increased chance that any change to the API response payload will accidentally break some unexpected view within the application.

- discussion
- Single responsibility can cause what appears to be unnecessary thrashing, 
  - but the code is so much more maintainable
- no need to regret this. 
  - I think it comes down to consistency once the decision is made.
  - For example, the graphql apollo world now is embracing the pattern you are regretting, returning changed data as a call result
  - A GraphQL context is interesting. And, I think different enough to have different rules. Since GraphQL allows the client to tell the server what it needs, 
# discuss-design-pattern
- ## 

- ## 🤼 [为什么java中不流行使用链式调用? - 知乎](https://www.zhihu.com/question/40095316)
- 我日常主要工作是业务发开发，很少使用链式调用。主要的原因是 链式调用让类的方法产生了依赖，从而导致你很难判断现在实例处于什么样的状态。
  - A->a()->b()->c() ，请问此时c状态是什么？你很难确定，因为c此时的状态依赖a, b函数
  - 你就需要一步一步的追踪，增加了阅读代码成本。

- 链式调用的核心就在于调用完的方法将自身实例返回

- https://x.com/ibuildthecloud/status/1919602049169215569
  - Have I ever mentioned I hate the builder pattern.
  - I program go and I prefer a struct. Builders in practice typically just populate a data structure and then have a "build()" method with all the logic. So basically it's just a lot of sugar for a struct and a factory method.
  - Trying to guess what the spring webclient builder wants in any given situation is... "fun."
  - Java doesn’t have default parameters and the builder pattern is a way around it. You readed my mind. It is an old language related pattern
  - those chain of functions can be just params instead
  - it’s a sign of bad language design

- https://x.com/htmx_org/status/1919571679577084033
  - Just good ol’ explicit deterministic code with just the right amount of ceremony. Few of us will die on this hill (alone).
  - I love functional Java

- ## design patterns like Gang of Four and Clean Code are a scam made up by consultants that didn’t have the time to understand your codebase and wanted to parachute in and out of clients for loads of money.
- https://twitter.com/leostera/status/1762018884444463355
  - they were not designed to make software better.
