---
title: lib-collab-community-showcase
tags: [community, crdt, showcase]
created: 2023-05-21T14:54:56.318Z
modified: 2023-05-21T15:46:35.896Z
---

# lib-collab-community-showcase

# guide

# discuss
- ## 

- ## 

- ## [Show HN: RemoteStorage – sync localStorage across devices and browsers | Hacker News_202401](https://news.ycombinator.com/item?id=38972358)
- the native localStorage API is super useful for keeping track of state between sessions in the same browser, but it's not as good a solution when your data needs to be shared across multiple devices or browsers.
  - I built remoteStorage to help fix that. Using the same API as localStorage, remoteStorage allows you to easily read and write data on the fly while maintaining state across browsers and devices in order to provide a better user experience.
  - The server is built with Nest.js with a disk-persisted Redis Database. It can be deployed in a few minutes using Docker.
  - One of the biggest challenges when building this was coming up with a secure scheme for handling authentication while still keeping the API dead simple for frontend devs to use. While the project is intended to store non-sensitive data like impression events/preferences, I still wanted to make sure data couldn’t easily leak or be tampered with.
  - One solution has been to generate a unique secret UUID per user on your own backend to identify the user. Alternatively, you could create a simple wrapper/proxy API around remoteStorage that uses your own authentication method to verify the user's identity before allowing them to access the data (this is super simple to build with React Server Components).
  - my main idea with the library is to make it super simple for front end engineers to store preferences/flags server side without needing backend engineering work. Basically as simple as using localStorage itself

- The bit about finding a unique ID for the user is the whole pain point though. The only way to do that really is for the user to create an account on some service that I host. And if I have that, I probably have my own hosted data storage anyway.
  - You totally _should_ have your own backend / auth when using this. It is not a database.

- Very cool overall but the sync->async change means you can't always use it as a drop-in replacement. 
  - the server is blazingly fast as it leverages Redis and Fastify under the hood.

- The use case is limited, a project has it's own backend, why need to add a new sub-system for tiny data storage?
  - A common difficulty is the simplest scenario, where do I store this frontend user preference? How do I store this that prevents nagging multiple times across devices?
- This sounds like something that should just be an extra JSON column in the users table of any SQL database. Backend team shouldn't be withholding backend support if remembering this data is actually important.

- How are the conflicts resolved?
  - This is handled by Redis, as such, the last write will win. As the primary key is tied to the user id, there will not really be a concept of Machine A vs Machine B as the end user can only be in one place at a time.

- What is special with the server? I was surprised you offered a community-hosted server.
  - The server is nothing special by design, just essentially Docker/Node/Redis with persistence enabled.

- So, just a UUID to authenticate? How do you recover/reset in case it gets lost?
  - You'd need to keep track of that somewhere for now, but as someone else suggested here, we could soon extend the library to support JWTs for authentication.

- Has anyone felt the same pain points with localStorage before?
  - For Sandstorm, we've always want to make sure app data is stored on a server, but an increasing number of web apps love to use localStorage as a cheap hack to avoid writing a backend. I recall a bunch of attempts back in the day, but we were always looking for a simple way to include something with an app written to use localStorage which could store the data on a server backend instead.
