---
title: thread-dev-optimization-refactor
tags: [dev, optimization, refactor, thread]
created: '2021-04-07T10:20:26.431Z'
modified: '2021-04-07T10:21:02.611Z'
---

# thread-dev-optimization-refactor

# guide

# pieces

- ## 

- ## [Things I Regret: Returning Modified Data In API Response Payloads](https://www.bennadel.com/blog/4019-things-i-regret-returning-modified-data-in-api-response-payloads.htm)
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
