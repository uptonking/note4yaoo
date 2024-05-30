---
title: page-dev-xp-devtools-build-package
tags: [dev-xp, devtools]
created: 2021-09-14T19:35:42.893Z
modified: 2021-09-14T19:36:26.597Z
---

# page-dev-xp-devtools-build-package
# guide

# packaging

- npm打包分发的方式，不如docker/ollama-run方便，但jspm在线源的设计就很方便了
# [5 Things I Learned Building Snowpack to 20, 000 Stars](https://dev.to/fredkschott/5-things-i-learned-while-building-snowpack-to-20-000-stars-b9d)

## Background

- I created Snowpack. 
  - If you're not familiar, Snowpack is a web build tool that fundamentally unlocked the "unbundled web development" movement that Snowpack, Vite, SvelteKit and other modern dev tools leverage today.
- In this post, I want to share 5 things that I learned growing Snowpack from the initial commit to almost 20, 000 GitHub stars and over 1, 000, 000+ downloads.

- I started an experimental JavaScript project. Codename: Pika.
  - Its unifying mission could be best summarized as, "ESM is this cool new technology, lets do more stuff with it."
- I created @pika/pack (a publishing tool for npm package authors), Pika CI (a Github action that let you npm install or even import() any GitHub PR), a failed in-browser code editor, and a next-gen JavaScript CDN that went on become Skypack.
- The biggest standout of the bunch was @pika/web, which let you install any npm package to run directly in the browser without a bundler (ex: react -> /react.js). 
  - You probably know this project better under its newer name: Snowpack.

## Lesson 1: Start with a personal frustration

- Snowpack began as a tool to convert any npm package to a single JavaScript file that you could run in the browser. 
- This small, straightforward tool would unlock an entirely new mode of web development that is now referred to as "Unbundled Web Development".

### Lesson for open source maintainers:

- Build for yourself, first. 
  - If you're frustrated by something, chances are other developers are too. 
  - Question everything.

## Lesson 2: move fast, stay small

- When you're working on a new project, you rarely know what code will be important long-term and what code is about to be deleted. 
  - I've thrown away enough code in my career to have learned that there's sometimes value in fast, messy coding. 
  - When you're starting a new project, it's okay to be a bit messy.
- To keep the project on track, I focused on a single feature: "give me a package name, and I'll convert it to ESM." 

- My overall recommendation is to test your idea and get together a working demo as quickly as possible. 
- In practice, this means four things:
  - Use existing tools! 
    - Fork a similar open source project or use an existing tool internally if it can save you time.
  - Write messy code! 
    - At the earliest stage, you probably don't know exactly know what you're building. 
    - Premature refactoring can sometimes be worse than never refactoring at all, so keep your code flexible for as long as possible.
  - Keep scope small! 
    - Don't build half-baked, half-working features. 
    - Instead, focus on doing one thing very well.
  - Skip tests! 
    - Confirm that you're building something useful before spending your free time writing tests for it. 
    - Nothing is worse than writing tests for something that you end up never using.
- The obvious downside to this "move fast" advise is that it is not sustainable long-term.
  - Moving fast means taking on tech debt, which you will absolutely need to repay at some point if your project becomes successful. 
  - As soon as you have some users who like what you're doing, you should begin to re-prioritize stability, refactoring and testing. 
- Paying down tech debt can be a slog. 
  - But, silver lining: If your project never takes off, then congratulations! 
  - You didn't waste any time testing something that no one wanted

### Lesson for open source maintainers:

- Write messy code, keep scope small, and skip any unnecessary work until you know that you're building something useful.

## Lesson 3: Fix fast

- One of the reasons Babel was successful is how quickly I was able to quickly fix bugs and release new versions. 
  - I would regularly have releases out within minutes of a bug report. 
  - This was critical during the early days when adoption was low. 
  - Being able to unblock users quickly would often make them more excited to use Babel even though they ran into a bug.

### Lesson for open source maintainers:

- Your first users are essential. Prioritize fixing their issues over everything else.

## Lesson 4: Practice good storytelling

- if you want people to use your project, you eventually need to tell them about it. 
- To start, just share your project with a friend or colleague and ask them for their thoughts. 
- When you're ready to share your project with a larger audience, you have a few options for how to do it. 
  - One popular choice is to tell your story in small, visual pieces over time. 
  - This is how Sebastian built excitement for Rome for almost 2 years before its launch. 
  - Mark Dalgleish has also done a great job of promoting vanilla-extract on Twitter this way.

### Lesson for open source maintainers:

- Promote your work. 
  - Find a style of storytelling that fits you and your project.

## Lesson 5: Ignore your haters, listen to your users

- If you're lucky, you can tell the difference between ignorant criticism and constructive criticism. 
  - Ignore the ignorant stuff (aka haters) but listen to the constructive feedback if you can. 
  - If someone shows that they took the time to at least attempt to understand your project in good faith, their feedback will usually have some value if you can spot.
- A common constructive criticism is when someone clearly tried understand your work, but still misunderstood some key part of it.
  - remember that clear communication is your responsibility. 
  - When someone misunderstands your work, it usually means that you could improve your README or documentation or general storytelling in some way.

### Lesson for open source maintainers:

- Haters gonna hate, ignore them. 
  - Learn how to spot the good-faith, constructive criticism.

## Main Takeaway: Support your early users

- If you're starting a new open source project, the best thing that you can do is make sure that your first 10 users are happy. 
- And if this all sounds like too much work, remember that open source software has no rules. It's supposed to be fun. 
  - Building for yourself or a smaller audience is totally fine, in which case you can go ahead and ignore most of this advice.

## Discussion

- one thing that gets into my mind is: how have you dealt with technical debt in Snowpack? I can see it's covered with tests now, but testing legacy code is always challenging.
