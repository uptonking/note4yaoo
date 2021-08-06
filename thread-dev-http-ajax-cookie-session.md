---
title: thread-dev-http-ajax-cookie-session
tags: [ajax, cookie, http, jwt, session]
created: '2021-08-06T08:30:13.653Z'
modified: '2021-08-06T08:32:26.142Z'
---

# thread-dev-http-ajax-cookie-session

# discuss
- ## 

- ## 

- ## JWT shouldn't be the default way of storing session data - because it doesn't allow logging out a user. 
- https://twitter.com/francoisz/status/1394258658641514514
  - Good old session cookies do the job fine, but yes, you'll have to keep track of sessions in a shared server-side storage. 
- You can store server side JWT and have logout
- But if you are going to have a shared server-side storage it's trivial to invalidate a JWT token on logout. And then your non-HTTP services don't need to understand cookies.
