---
title: thread-dev-engineering
tags: [dev, engineering, thread]
created: '2021-01-21T17:51:54.496Z'
modified: '2021-01-21T17:52:13.333Z'
---

# thread-dev-engineering

# guide

# pieces

- ## 

- ## I don't use TDD This is what I do instead: code -> test -> docs (CTD)
- https://twitter.com/sseraphini/status/1376636172080922629
- CPT - code > production > test
- Tdd is great but it usually it is not so practical while you are still exploring the implementation space
- I do the opposite: docs code test, DCT
- TDD is interesting for pure functions that you know the expected result and use the test as a tool to automatically check if you are doing it right. Test functions manually are boring if it's not trivial.

- ## it never ceases to amaze me how much some people will resist showing their code after asking a question and saying "this doesn't work".
- https://twitter.com/acemarke/status/1376656948926496768
  - Sometimes I can provide an answer after just hearing a description.
  - but most of the time, I need to see the _real code_ to debug the issue.

- ## Is there any kind of a utility lib that will scan a JS file and identify code that doesn't match a given set of features supported by a target browser?
- https://twitter.com/acemarke/status/1376703719669182471
  - I'm basically looking for something like (notional): `is-browser-safe ie11 my-file.js` .
- eslint-plugin-compat
- eslint-ie11-compat

- ## What's the right process for a library to drop support for IE11/ES5-only environments in its published artifacts? 
- https://twitter.com/acemarke/status/1376381894279987209
  - Should that be a new major, or a minor?
  - Right now our CJS/ESM files are back-compiled to ES5 syntax for IE11 support.
- So "major" seems to be the consensus answer so far, which is reasonable.
- We're planning for RTK Query to be released in RTK 1.6. It's additive only, so that doesn't require a new major.
  - I really want to keep RTK and the new RTK Query features accessible to as many devs as possible. On the other hand... IE11. Ew.
  - Maybe put these out in 1.6, and then begin planning RTK 2.0 that drops ES5-only support?

- ## Where do you put tests and why? same folder vs separate tests/ folder
- https://twitter.com/claviska/status/1375071253753647118
- Separate “tests” folder because clutter etc. 
  - Also if you are concerned that things aren’t getting test, you can also setup code coverage and know for sure.
- Framework's default
  - It's configurable, but I'm looking at one with a tests folder. My concern is, if tests are independent of the things they're testing, it's easy to forget to add/update them (particularly for contributors and large codebase)

- ## If you deploy your app to serverless platforms (Vercel and friends) but you use services (Postgres, Redis, etc) that don’t have auto scaling, then your app is not serverless at all. It’s only an illusion.
- https://twitter.com/flybayer/status/1373824547506511873
- We just shift the bottleneck. Classic manufacturing efficiency optimization problem

- ## I always wondered about Google, how do you push through the internal competition? Android, PWA, Flutter. 
- https://twitter.com/sebmarkbage/status/1373775862219292674
  - I sit here with an amazing community, team, org and management support. 
  - Yet all I can think of before every Monday is the people that don’t believe in me or what we’re doing.
- You have to lead and stand by your decision: Think of Steve Jobs coming back to Apple and bring all that Objective-C guys from Next.
  - It was the better technology - but heck it was unpopular at that time. And despite all the lows he denied all alternatives (Java, Flash).
- I worked at companies where such competition is a norm. 
  - In my experience, that's what helped to avoid such feeling. 
  - Helpful competition promotes stuff that works, kills stuff that does not; 
  - it allows people to focus on the objectivism of the tech not the subjectivism of feelings.

- ## Wondering sometimes if, instead of more libs, we shouldn't offer more first-class copy-and-paste solutions.
- https://twitter.com/mpocock1/status/1372986732354883588
  - Copy and paste an entire component lib and then tweak to your heart's content
- I'm absolutely against this: the good thing about libs is that they are documented and tested configurable blocks. All code should be libs, even our own. Coding for open source enforces code quality (at least at the boundaries).
  - Libs are wonderful, invaluable. But choosing libs for _all_ solutions is perhaps too dogmatic. There should also be space for when you want to grab something pre-built and modify it.
- What you described is the basic idea behind the architecture of Crown. You “install” packages within the framework by cloning with git subrepo. You own the code but can still pull changes from upstream

- ## For tools that don't have multi-versioned docs sites: what are good techniques for how they indicate a particular API or option was added/modified in a specific lib version?
- https://twitter.com/acemarke/status/1373102543371390979
- just a line at the top of the page/section mentioning the version works fine. I think I've seen that pattern in a bunch of pages on Next.js and some other docs.
- api.jquery.com/blur/ Of course that's how things were done back in the day I guess 
  - The version added for a method is always specified, also there are always notes about the differences between versions.
- Kotlin docs show you which version APIs were added in and if they are supported in JavaScript, JVM and/or native

- ## Developers that can't or don't write good comments aren't great developers yet.
- https://twitter.com/BenLesh/status/1372562839475470336
  - Add comments about WHY code exists, not what it does.
- Comments cannot be tested and should therefore be assumed to be wrong.

- ## What's the coolest open source project in the JS or Wasm ecosystems you've seen that's *new* within the last year?
- https://twitter.com/_jayphelps/status/1372249383291457540
- esbuild
- We just finished a show on Remotion and @JNYBGR - how to programmatically make videos with React. It's really excellent and empowering technology.
- css-in-js: SnackUI - the final React style library
  - The smart SwiftUI-inspired UI kit for React Native & Web.

- ## I don't actually show much of my coding work in public, largely because I do most of my coding at my day job.
- https://twitter.com/acemarke/status/1372374988762779649
  - Even then, teammates normally only see "final" code in my PRs, and don't often see how many mistakes I made along the way to get to that final result.
- A couple nights ago I decided I'd see if I could try writing a faster implementation of the RTK mutation detection logic. I did get it passing all our tests.
  - It appears to be like 15x _slower_ than the original.
  - I guess the point here is, consider this your semi-inspirational reminder that everyone screws up - you just don't always see that happening visibly.
  - I am now trying to figure out _why_ my implementation is slow.
  - today I deployed a new build of our app to prod. small app, single server, half-automated deploy process.

- ## What are some times you've needed to keep data synced between two SaaS products? (eg: keep a Trello board synced w/ a Notion table)
- https://twitter.com/geoffreylitt/status/1371509957779148802
  - Looking for example use cases for a sync tool I'm working on
  - Could also be things like "needed to keep this Salesforce data updated in a Google Sheet"
- In design-engineering teams:
  - Figma Comments <> Trello Cards <> GitLab Issues
  - Trello being the middle ground for managers who‘re afraid of Figma/ GitLab
- Personally: Airtable <> Google Sheets

- ## The #1 tech skill to have is comfort in coding, on the fly, in front of other people.
- https://twitter.com/AdamRackis/status/1370875384812740610
  - Expect to be given some silly use case, ie, "write a class that take two strings, and tracks which is longer"
  - Be comfortable talking through the requirements, asking questions, etc.
- Expect to iterate on it, over and over, with requirements being added. Ie, "now optionally take an array of strings, and, if an array was passed, track the shortest string. If just two strings were passed, like before, then ..."
- Most important tip I can give: **think out loud**. Always. Turn the voice in your head you normally think with, off, and think out loud.
  - If you get stuck, talk it through, out loud. Explain why you're stuck. Ask questions. Your interviewer is there to help you. Seriously.
- The worst thing you can do is stop coding, and freeze up, panicking in your mind. Talk it through.
- Expect to be asked questions in your domain to test how deeply you know it. I was asked about everything from arrow functions, to Promises, to web sockets.
  - The deeper you know your stuff, and can demonstrate it, the better.
- If you're asked about arrow functions, don't just say they're shorter syntax sugar.
  - Mention lexical this.
  - Mention lexical arguments.
  - Mention lack of a Prototype and [[Construct]] slot.
  - Show them you're someone who knows their shit.
- You know what I was never, ever asked about, even once? JS Frameworks
  - Oh, you've written apps in React, Svelte, Vue and also Angular? Nobody gives a shit.
  - Companies care a lot more that you have deep language mastery, vs having played with a bunch of different frameworks.
- You know what else I was never asked about? CSS Frameworks.
  - Tailwind seems really, really cool. But maybe learn the fundamentals of CSS before you dive in, there.

- ## friendly reminder that http-only cookies don't protect you from XSS
- https://twitter.com/benawad/status/1370532233698770947
  - if someone can inject code they don't need your token, they can just make fetch calls on that users behalf
- The solution to this is using CSP, right?
  - The solution is "don't trust user input"
  - Yep but not all browsers respect the policy. And if you parse malicious code comming for user inputs it doesn't matter if the browser respect the CSP especially if that code can be rendered by other users too
- Very true. If you've an XSS you're actually flawed and a local jwt should be the least of your worries

- ## Webpack have achieved production server Hot Module Reloading between apps using module federation
- https://twitter.com/ScriptedAlchemy/status/1370555543136301060
  - No cold start, no downtime, no new process. I've seen the future, and its got zero-downtime

- ## Preemptive Pluralization is (Probably) Not Evil
- https://www.swyx.io/preemptive-pluralization/
- What if we just assumed we might have two of everything?
- Before you write any code — ask if you could ever possibly want multiple kinds of the thing you are coding. If yes, just do it. Now, not later.
- But I think Preemptive Pluralization(先发制人多元化) — projecting forward into hypothetical situations when you need N types of a thing — is exempt, even though you are literally optimizing for a future you don't currently live in.
- It is a LOT easier to scale code from a cardinality of 2 to 3 than it is to refactor from a cardinality of 1 to 2. 
- Robust code is optimized for change (more in a future blogpost).
- Let's address two obvious criticisms of Preemptive Pluralization:
  - Increased code complexity: Functional languages and other abstractions can help make array or matrix operations almost as easy to work with as regular operations.
  - Slow performance from doing extra loops: Loops only cost significantly when you have lots of N. By definition, if you are pluralizing prematurely, N = 1.
- Listen up, this is sound advice that I can attest to after years of experience. 
  - You will almost always need two or more. 
  - If you end up not needing 2 or more, the risk/reward is worth it in almost every situation.
  - Just Pluralize It.
- I've made this type of refactor more times than I care to count, and it's always a pain. Absolutely good advice.

- ## 3rd party integrations today are like:
- https://twitter.com/ryanflorence/status/1370405429189046278
  - First, add our 100kb browser SDK
  - Now fetch to your "api route"
  - Now use our server side sdk
  - Now back in the browser use our browser SDK
  - A little config on the third-party dashboard + `<form> ` would have been way simpler.
- But you know that A in JAM is for API and you can make a `<form method=post>` , right?
  - Yes indeed, but so many services require browser javascript and you can't actually process that post on the server.
- `<form method=post>` .
  - automatically serializes data
  - automatically fetches an "api route"
  - automatically changes the page state when complete
  - automatically adds pending indication to the user interface
  - works cross origin if needed
  - This is how you communicate a mutation.
- use `<form>` , Then use `<Form>` , when you've got the time/energy/skill to implement a nice pending/optimistic UI. 
  - Remix doesn't care which one you use, it's all the same!

- ## For a long time, I was always unhappy with my code. I never trusted it, never liked it.
- https://twitter.com/eveporcello/status/1369678978827493376
  - Then I discovered: Testing, Refactoring
  - With both, I worry much less about getting code right initially—I can always improve it later. 
  - Testing also lets me trust my code.

- ## My problem with types added to every function and object is that they occupy my brain when I scan the code when I don't need them. 
- https://twitter.com/oleg008/status/1369956575964782594
  - They are just cluttering the code most of the time. 
  - I want to go back to clean JS code but still have the types hints when I want them.

- ## TIL: passing multiple `-m` options to `git commit` creates paragraphs in the message.

- ## How to identify mistakes in a code structure to learn from:
- https://twitter.com/cse_as/status/1369281929162285063
  - When you go back to a part in the project your team worked on earlier & it takes you more than 10 seconds to pinpoint where the needed code is, it probably wasn't structured in a way that made sense.

- ## A list of basic Linux commands every developer should know:
- https://twitter.com/iamdevloper/status/1368866110951596032
1. Open your browser
2. Head to your favourite search engine
3. Type "how to copy a file to another directory"
4. Click the first Stack Overflow link
5. Copy the top voted answer
6. Blindly paste it into your terminal

- ## When should I (not) use mocks in testing?
- https://dev.to/kettanaito/when-should-i-not-use-mocks-in-testing-544e
- Depending on the software that is being tested, there are multiple things that can be mocked:
  - Environment and context.
  - API communication
  - External dependencies.

- ## Writing software is basically a 2 step process: 
- https://twitter.com/housecor/status/1368569429202792448
  - Ask the computer to do something
  - Verify its response
  - That’s why I believe in creating fast feedback loops. The faster I get a response, the more productive I can be.
- Feedback loops also involve CI, designer-developer collaboration, automated tests, among others. Any improvement that you do in any of those increases your productivity!
- You missed the 3rd step. Swear at the computer when the response is wrong and you can't see the problem.
- What are your favorite techniques for this?
  - Mock APIs
  - Small tickets so I get teammate and user feedback faster
  - Automated unit tests and TDD
  - Build and test small components in isolation
  - Create custom dev tools
  - Use Cypress to avoid interacting with the app manually while coding
- In all seriousness though, this is why I love to write my code using TDD.

- ## is there a "modern" UI for OpenAPI? built with @reactjs that could be very customizable?
- https://twitter.com/sseraphini/status/1367851096421568512
  - I'm like to embed my API inside @docusaurus
  - but redoc takes the full page and swagger UI has some dark mode issues

- ## You can't mock cloud semantics locally but you can mock the API surface. AWS is very stable. 
- https://twitter.com/brianleroux/status/1367851230785990663
  - Folks say you shouldn't use local emulation because of this but I respectfully disagree. It's slower. 
  - Tighten those feedback loops. Test locally AND in an identical staging stack.
- Fwiw, same discussion happened in mobile a decade ago. You can't use an emulator they said. Mostly ppl said that because the emulators sucked. 
  - Ppl don't say that about mobile dev anymore. Cloud will have the same cycle.
- I was firmly in the “don’t emulate AWS” camp until I actually tried using localstack. 
  - If the bits you need to emulate are supported, it works quite well.
  - It's additive too. Work local and then test in a staging stack. Makes step 2 shorter which has higher latency anyhow. 
  - I'm fairly certain this meme happens every new platform because vendors and frameworks add emulation later. It's an excuse while they get their shit together.

- ## 99% of what I do in a large codebase is find pre-existing examples, copy-paste structure, fill in the holes and clean up. That's it.
- https://twitter.com/deech/status/1366859264732635148
  - Relevant skills: find pre-existing examples, copy-paste structure, fill in holes, clean up
  - Irrelevant skills: category theory, able to whiteboard delete for a red-black tree
- This is definitely how big company code works! Sometimes to a surprising effect. 
  - You might check in some random pattern you haven’t given much thought to while filling in some hole. 
  - Then a year later you find your code in a 1, 000 places with tiny changes. Hope it was good code.

- ## Is Webpack's code-splitting just garbage or are there more tricks to implement?
- https://twitter.com/mattgperry/status/1366344701964648450
- Why do you think it is garbage?
  - Because moving a single enum into its own file yielded a 11kb/89% saving.
  - This is incredibly delicate and has implications about how a project should be structured (no more than one export per file). As far as I can tell, for no good reason. It isn't the case with Rollup.
- nope, webpack just offloads more to Terser whereas Rollup do a lot more work on its own, this can make a big diff for some projects, 
  - also - Rollup makes some pragmatic choices sometimes whereas webpack tries to be super strict and safe, which also can make a big diff
  - So do you personally tend towards single-export files?
  - This is a good advice if u want to keep things as treeshakeable as possible - ive thought about creating a rollup plugin that would chunk a project this way automatically. I dont want to split files manually. Never got to it though

- ## As a CS prof, I use binary search practically every day to figure out which part of the paper is crashing LaTeX.
- https://twitter.com/bradreaves/status/1365061879744315398
- I take quadratic computer time to avoid the logarithmic human time for the binary search (a.k.a. re-compile every few keystrokes).
- This is how I used to teach kids to debug. 
  - When a problem is really hard to find, try and reduce code in half, recursively, until the program works
- Divide and comment 😋

- ## Want to find a perf problem? Throw something big at it.
- https://twitter.com/kuvos/status/1364929672652464132
  - 88mb of js will probably do

- ## Integration testing tip: Avoid creating many small tests. Instead, create a few big tests. 
- https://twitter.com/housecor/status/1364584436755480578
  - Here’s why: There’s a lot of overhead in starting each integration test. 
  - So to build a fast integration test suite, favor “big” tests over “small” tests.
  - Example: Imagine I have a todo app. I don’t write separate tests for create, update, and delete. Instead, I create a single test that checks all three. I name the test “should support adding, editing, and deleting todos”.
- And when the test fails, you don't know why.
  - In Cypress that’s clear. It shows what line. And even records and screenshots.

- ## Best CSS debugger: `border: 1px red solid;` .
- https://twitter.com/kyleshevlin/status/1363901000948408320
- I have to say this every time: This is close, but it's NOT the best.
  - It's better to use `outline` than to use `border` . Why?
  - Because `border` affects layout, changing the width and height of its element. `outline` has no affect on layout, whatsoever.
- It's especially important to use `outline` instead of `border` when testing the cumulative layout shifts
- Good call. Its also useful to keep in mind when trying optimize for a better Cumulative Layout Score, if there are larger shifts in elements that could alter the CLS.  Though something as small as a border may not be enough for the algorithm to catch, I am not sure.
- Sometimes, I do prefer using backgrounds, like: `background-color: rgba(0,0,0,0.1)` , I can see how much an element takes, and how they stack
  - But most of the time, outline is the way to go

- ## Imagine if tools like Sketch and Figma let you write expressions the way Excel does.
- https://twitter.com/markdalgleish/status/1363703556109312007
  - e.g. calculating a background based on another element: `=darken(getBackground($ELEMENT_NAME, 10%))` .
- Transpile to CSS vars and ship as code
- Figma could expose the API in editor in addition to using it for plugins. That’d be sweet!
  - It's already done. You can use it in the console.
  - Good point. I think a part of writing “expressions”, not code is making it more approachable. For example, a small thing excel does when writing expression’s is letting you click to select fields and inserting them into the expression.
- It's really clever that Excel doesn't refer to writing expressions as "writing code." More tools should let you "write expressions" rather than underestimating their users' intelligence.

- [Excel is visual programming because you're placing data, labels, variables and calculations in physical space.](https://twitter.com/markdalgleish/status/1363727357169704963) 
- This makes VBA is the javascript of the spreadsheet world
- arent all programming languages like this as well? only difference is that it’s not bound by y and x axis

- ## Sometimes it’s overwhelming to change some complex feature in the existing code.
- https://twitter.com/BenLesh/status/1362762796501401601
- I used to do this. But it's often dangerous. I try to take a more measured approach now.
  1. Make a couple of PoCs off to the side to see what I learn.
  2. Carefully improve the code and add tests in the parts of the code I'll be touching, and see what I learn.
  3. Add the feature.
- I find that after part 2 above, often the approach I take is different and better than what I did in some of my PoC work.
- The main difference between the new code and deleted code: The deleted code has been tested and hardened, if only by users. 
  - It already has behaviors that are expected. 
  - Depending on complexity, a "big bang" rewrite has little hope of recapturing all of that.
- Even when I've had insane test coverage, there were missing corners. 
  - I've found big bang rewrites have a higher probability of regression. 
  - Better to push existing code around until it looks like a rewrite. But this is my experience.

- ## The reason Vite requires .jsx extension for JSX processing is because in most cases plain .js files shouldn't need full AST transforms to work in the browser.
- https://twitter.com/RyanCarniato/status/1362178225493839874
  -  Allowing JSX in .js files means every served file must be full-AST-processed just in case it contains JSX.
- We have been struggling about enforcing this because it makes so much sense, but figured there wouldn't be enough community backing. 
  - But if major tools like Vite go this way that is amazing. It never should have been just .js when you consider compilation

- ## Introducing Blazepack - a super fast dev server powered by @codesandbox sandpack bundler.
- https://twitter.com/ameerthehacker/status/1361615692294852613
  - Supports @reactjs, @vuejs, @angular
-  It is a thin wrapper around the sandpack bundler, so it support React fast refresh, HMR and all the cool stuffs that sandbox supports

- ## How are some of you actually working on _side tech projects_? I'm struggling to even maintain energy for day-job projects lately.
- https://twitter.com/brian_d_vaughn/status/1361520253604421634
- I get anxious without side project. It’s how I relax.
  - When the brain is full of errant(错误的、行为不当的) thoughts and ideas, only way to get anything done at work is to regularly clean the brain.
- don't believe everyone on twitter. Specially in the Dev community.
  -  I have experienced it a lot that people try to talk them selfs better than they actually are. Per se it is not a problem. 
  -  But it promotes a bad reputation for devs. We don't code 24/7

- ## Offline support has been part of the PWA installability criteria since the beginning. 
- https://twitter.com/ChromiumDev/status/1358817467661967365
  - In Chrome 89, we'll warn you if your PWA doesn't have an offline experience. 
  - In Chrome 93, we'll start enforcing the updated install criteria for new PWAs.
- If all you need is a baseline offline fallback page without actually delivering a true offline experience (which, acknowledgedly, many apps don’t need or can’t), then give my article a read
  - [Create an offline fallback page](https://web.dev/offline-fallback-page/)

- ## When learning something new, it’s easy to fall in to the trap of comparing your work to seasoned professionals and think everything you’re doing is wrong. 
- https://twitter.com/steveschoger/status/1358588140328538115
  - Lately I’ve been trying to embrace this learning period because it’s a small window of great discoveries.
- Constant learning from seasoned profs, using my previous dev knowledge mixed with theirs, change code as I find better or more efficient solutions, seasoned profs's solutions are not always right or appropriate for the current app.  Having a blast and always learning.

- ## which companies are using @GraphQL in production nowadays?
- https://twitter.com/mxstbr/status/1358351658078634014
- Frontend teams at Danske Bank use GraphQL, mostly driven through Apollo. 
  - Microservices are still on REST so there's redundancy maintaining a mid-tier just for conversion.
  - GraphQL has most significant advantages when adopted by backend teams which isn't the case at most places.
- Using it in production at @skillshare . 
  - Running Apollo Gateway as API composition layer to allow frontend decoupled monolith -> microservices migration.
- @OrbitalChat uses it for admin-based stuff. 
  - The more interactive part is done with Firebase Real-time database and Firestore direct from the client. 
  - Also @SketchADay is 98% GraphQL and a couple of little plain JSON-over-HTTP bits
- GitHub and Contentful
- @AirbnbEng uses it quite a lot

- ## If you don't know which code is calling your function, use console.trance()
- https://twitter.com/sseraphini/status/1356654950198239233
- I used `console.log(new Error)`

- I usually also do “console.log = console.trace” to locate and remove some console.log

- ## Hyphens are pretty. Underscores are ugly and don’t belong in URLs
- https://twitter.com/mscccc/status/1355525419152384002
- What about emojis in URLs? 
- [URL as UI](https://www.nngroup.com/articles/url-as-ui/)

- ## "The DOM is bad for apps" makes me laugh pretty hard. 
- https://twitter.com/_developit/status/1355670204366393347
  - It's effectively the same type of abstraction as a scene graph, but because we use it poorly it must be bad!
- I think the dom is very much bad for apps, who in their right mind would say otherwise. 
  - Why else do we have frameworks abstracting it. 
  - Most people don't know or see a dom when they make apps and that is a good thing.
  - That is the same reason why we have rejected a component model built on that pile of perpetual backward compat which is the dom.
- The browsers dom is virtual, bc it's faster. 
  - Every GUI system is split into a logical/virtual & a visual tree, otherwise you wouldn't be able to schedule, or, well, virtualize. 
  - Ever used a virtual list, I suppose you did. 
  - FBs "vdom" has better scheduling than the "dom", facts. 
- aren't some of the most popular apps just app shells with a web-view?
  - that, or react-native which uses a tree abstraction very similar to the DOM anyway
- Well, if we just used fixed height for everything and there was never a need to refresh layout I think most html apps would be as fast as 'native' - as if running apps in a JVM/runtime is native anyway - if it's not assembly writing directly to a framebuffer it's trash

- ## Software tradeoffs
- https://twitter.com/housecor/status/1355144710185230336
  - Build vs Buy
  - Reuse vs Copy
  - Sync vs Async
  - Serial vs Parallel
  - Dynamic vs Static
  - Concise vs Explicit
  - Unified vs Separate
  - Secure vs Convenient
  - Simple vs Configurable
  - Centralized vs Distributed
  - Convention vs Configuration
  - **Avoid picking sides. Think tradeoffs.**
- I am not sure you want to trade off security for convenient
  - Perhaps, but companies do so everyday. 
  - Using other people’s software is convenient, but adds security risk by trusting other people’s code.

- ## Will Vite replace vue-cli? 
- https://twitter.com/youyuxi/status/1354584410482499585
  - Initially I wasn't sure, but at this stage I believe it will eventually be the case.
  - The main disparity(不同；差异，悬殊) now is just test runner integrations.
- Check out uvu by @lukeed05 . 
  - Native ESM support, very much in the spirit of Vite. 
  - No test compilation step by default, no special integration needed.
  -  When I need to test in the browser, I just start my Vite dev server and use puppeteer in uvu tests. It's refreshingly simple
- We could make a plugin for web test runner
  - It should be relatively straightforward if we can proxy browser requests to some transform API or middleware. 
  - We already have a plugin for snowpack
- There was discussion in vue-cli about letting plugins replace webpack as the builder
- after a few years of running large enterprise apps on vue-cli, I've had to break out of the test runner integrations to avoid the lag time between test runner updates, and vue-cli updates. 
  - vue-cli is still a great tool... 
  - But would love to see a more decoupled approach in vite

- ##  what are your team’s package.json script naming conventions for development mode, your build stage, and potentially running the built thing?
- https://twitter.com/jaredpalmer/status/1353083840424763392
  - I used to be in the ‘start, build, start:prod’ team 
  - but now I’m actually leaning toward ‘dev, build, start’

- ## A little technique we use all the time to audit the layout shifts and avoid performance issues.
- https://twitter.com/smashingmag/status/1352185650091581441
1. Add * { outline: 3px solid red } to your CSS.
2. Record the loading of your site/app.
3. Review it by exploring what happens in slow motion.
4. Adjust and minimize shifts.

- Great tip, thanks! This one's less visual and more programmatic from the 'Performance' tab in Chrome.
  - You can hover over the 'Moved from' keys and this will visualise the movement in the browser window.
  - And using this method you can even see down to the shift caused by web fonts loading.
- We can also use a `PerformanceObserver` to log elements causing layout shift to the console
- Remember this trick from when i started to learn css.
  - Always use to troubleshoot when some problem arises while postioning elements..
