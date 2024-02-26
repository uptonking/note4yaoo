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

- ## 

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
- If I could go back and rebuild all mutation requests, I **would design them to return confirmation data only - no entity data**.
- To understand what I mean, imagine that we have a web application that has a Contact entity. 
  - And, I have an API end-point that allows me to rename the Contact with a POST request
  - `POST /api/contact/4/rename?name=Hanna+Banana` .
  - Historically, in my web application, this POST request would execute the use-case - renaming the Contact - and would then return the Contact data with the new name field in tow(紧随着，陪伴着)
- If I were to build this POST request today, however, I would code this to return a 204 No Content response. 
  - A 204 is a success code, confirming that the POST request was handled by the application; however, it wouldn't contain any other data.
  - **If the client-side application needed the modified data**, it could either optimistically update its own view model locally as part of the request processing; or, it could make a subsequent request back to the server to get the modified data for its view.
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

- ## 

- ## design patterns like Gang of Four and Clean Code are a scam made up by consultants that didn’t have the time to understand your codebase and wanted to parachute in and out of clients for loads of money.
- https://twitter.com/leostera/status/1762018884444463355
  - they were not designed to make software better.
