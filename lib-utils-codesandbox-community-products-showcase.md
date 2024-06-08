---
title: lib-utils-codesandbox-community-products-showcase
tags: [codesandbox, community, showcase, web-ide]
created: 2024-05-12T15:38:57.844Z
modified: 2024-05-12T15:39:22.456Z
---

# lib-utils-codesandbox-community-products-showcase

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Bitbucket Embraces the Cloud IDE | Hacker News _201502](https://news.ycombinator.com/item?id=9033670)
- I've been doing this with Cloud9 for quite some time now. Just link your Bitbucket account (or Github, for that matter), and you can work with it directly in the Cloud9 IDE. Haven't checked out CodeAnywhere in a while, though, so I'm going to see how it compares.

- It's not IDE. It's just a code editor. Where're refactoring, navigation, find usages?

- 
- 
- 
- 

- ## [Show HN: Strada – Cloud IDE for Connecting SaaS APIs | Hacker News _202402](https://news.ycombinator.com/item?id=39469657)
- Look very similar to the script builder portion of https://github.com/windmill-labs/windmill, but not open-source, not self-hostable, without open-source integrations (https://hub.windmill.dev/) and without a workflow engine

- ## [Launch HN: Nimbus (YC W22) – Cloud dev environments for teams | Hacker News _202208](https://news.ycombinator.com/item?id=32496462)
- Nimbus is more like local development, we're building for teams that use a wide set of IDEs. Think of us as a "machine first" cloud environment instead of "repo first". So its like having a laptop in the cloud for every project.
  - Our differences means we've prioritized local editor integrations, use a full EC2 machine dedicated to each user, aim to be more flexible (e.g. you can schedule when your machines are active), and provide more power (right now up to 8vcpu 32gb ram, but customizable by us).
  - Codespaces, Gitpod and the like are repo first and provide containers instead of VMs. Codespaces doesnt support non-VS Code Users. Gitpod tops off at 8gb or 12gb of ram. We also decided not to go the browser based IDE path that Stackblitz took because the engineers we talked to really didnt want a new IDE.

- Cloud9 IDE Appvia Coder CodeSandbox CodeZero.io DevSpace Desktop Tilt Env0 Floxdev Gitpod Itopia Spaces LocalStack MetalBear Azure DevTest Labs Visual Studio Codespaces Nimbus Okteto SourcePro Porter Codeready Workspaces Repl.it Stackblitz Strong.network Subpoint Solutions Tangram.dev

- 
- 
- 

- ## [Show HN: Eleven – open-source alternative to Codespaces | Hacker News _202212](https://news.ycombinator.com/item?id=34142602)
- Running it in a VM is a huge maintenance overhead. This at first glance looks like a great PoC. You might have to eventually support kubernetes or ecs equivalent thing on each cloud provider from production readiness point of view as well as from admin perspective, the way gitpod works.

- ## [Show HN: ClassroomIO – an in-browser programming environment for education | Hacker News _202404](https://news.ycombinator.com/item?id=40000022)
- I’m excited to introduce ClassroomIO 
  - It’s an educational platform that provides an in-browser code editor and execution environment. 
  - The idea is to make teaching programming easier by eliminating the technical barriers that educators and students often face.
  - It's more like CodeSandbox, but tailored specifically for educational purposes.

- What does this do that http://REPL.IT or Jupyter Notebooks do not do?
  - Replit is similar, this product is like it but tailored specifically for educational purposes.
  - As for Jupyter Notebooks – ClassroomIO allows you to create an assignment and have a group of students work on it simultaneously without interfering with one another. (Maybe you can do this somehow in Jupyter, but I don't know how.) Also, it supports more languages and the flow is more like a regular console app.

- the code is sent to the server for execution.
# discuss-alternatives
- ## 

- ## 

- ## 

- ## [Show HN: Codebox - Cloud IDE as a Service | Hacker News _201312](https://news.ycombinator.com/item?id=6864052)
- This looks nice but it's missing one feature that's stopped me from adopting services like this after having tried a couple of them - let me download the VM!
  - There are I think two fundamental problems with remote IDEs. One is of course offline mode, and I don't think "sync your code later" is a solution unless it also lets you "test your code now". The other is remote resource restrictions that mean you can only use a remote IDE for some of your projects and still have to maintain a complete local environment for everything else.
  - Being able to download the VM means local hardware for projects that need more hardware, and real offline mode for people that need it. Going open source allows for this but it still leaves all the work of setting up each box which can be a real PITA (cloud9 is very hit-or-miss) and that can probably be monetized especially with the added benefits of remote access for when that is better or necessary.

- [Show HN: Codebox - Open-source cloud and desktop IDE | Hacker News _201401](https://news.ycombinator.com/item?id=7023393)
- I'd love to see someone build an IDE that lives locally but syncs up to a cloud service so I can pull everything back down to a different machine and work there. I think you could actually do this with Docker, where your "IDE" would not be an editor, but a virtual system with the code, the database, a web server, the right version of Python/Ruby/foo, dependencies, etc., and you could use whatever editor you wanted. As you worked, the app would use Docker to save the state of the world and push it up to the server. It seems like this would get the benefits of cloud IDEs but still provide the low latency and flexibility of working locally. I don't have the time or expertise to build it, but I hope someone will!
- Codebox.io actually users Docker behind the scenes by the way. So those VMs could be moved to the desktop as well.

- How does this compare with Cloud9?
  - Codebox & Cloud9 share some similarities (IDE's built with web technologies). 
  - However we have a big emphasis on modularity, ease of use. We have a Desktop app (linux/mac) coming in the pipes. Our cloud version has offline support (so you can code even when the network cuts). And a handful of other things. For example our hosting platform supports stacks (swappable VM images), that allow us to provide our clients with tailored environments to suit their needs (languages & frameworks they use).
- It might be worth noting that some of the key components used by Codebox are actually developped by Ajax.org (the Cloud9 team) like the ACE code editor component and the vfs system.

- The idea of encapsulated VM boxes is intriguing.
  - The IDE itself isn't tied to specific VMs, it can run on your own server, your own desktop/laptop or our cloud.
  - We provide stacks and VMs for all common languages and frameworks (PHP, Java, Dart, Node.js, Python, Ruby, Go, C/C++, Lua) as of right now.
  - The community can also contribute new stacks providing support for other languages.

- On our cloud service (https://www.codebox.io) we do run each app in a seperate container/VM of course.
# discuss-alternatives-stackblitz
- ## 

- ## 🚀 We are introducing TutorialKit by @stackblitz _202406
- https://x.com/elmd_/status/1798765386118373487
  - [TutorialKit | Create interactive coding tutorials](https://tutorialkit.dev/)
  - that allows you create highly interactive tutorials in no time powered by the WebContainer API 
- I think it may have pretty big potential for internal education. You often have tooling not publicly available where your "go to dev setup" for new projects involves many plugins and configs that can be hard to explain.
  - Yes! This can for sure be used internally for onboarding und internal education. TutorialKit allows you to authenticate so you can install private packages as well. You can also get it entirely on-prem and have WC run in your own infra and then deploy it all internally.

- ## [Our architecture is based entirely on SystemJS & Unpkg and uses no code from CodeSandbox _201708](https://medium.com/@ericsimons/our-goal-was-to-port-vs-code-npm-and-webpack-loaders-to-run-entirely-in-your-browser-and-still-8751f39e5b0f)
- Our architecture is based entirely on SystemJS & Unpkg and uses no code from CodeSandbox or the Webpack bundling service ya’ll made.
- From the start, our goal was to port VS Code, NPM, and Webpack loaders to run entirely in your browser and still work offline. With StackBlitz, the browser is installing, bundling, and serving everything — our servers don’t do any of that.
- We’re attempting to build the first fully in-browser IDE.

- ## [Stackblitz – Online VS Code Editor for Angular and React | Hacker News _201708](https://news.ycombinator.com/item?id=14925957)
- 🆚️Could you please explain what is the difference between your project and csb
  - From the start, our goal was to port VS Code, NPM, and Webpack loaders to run entirely in your browser and still work offline. With StackBlitz, the browser is installing, bundling, and serving everything — our servers don’t do any of that.
  - While CodeSandbox is a nice playground for React apps specifically, we have never intended (nor have any aspiration) to compete in the online playground space. We’re attempting to build the first fully in-browser IDE.

- CodeSandbox does almost everything in the browser however. The only thing it doesn't do in the browser is dependency bundling, which StackBlitz does in this case.

- Essentially CodeSandbox can work offline if you already had the website open while you're online, then you can still continue offline. 
  - StackBlitz has the advantage that the tab where your application is can also be opened initially offline, which is handy for showing your application when you have no connection, but if I'm not wrong you cannot continue developing offline

- Is there Source Control integration?
  - Not yet, but that's absolutely on the near-term roadmap
# discuss-alternatives-replit
- ## 

- ## 

- ## 

- ## 📱 [Replit Mobile App | Hacker News _202210](https://news.ycombinator.com/item?id=33263432)
- This is one of those examples for me where the idea is far superior than the implementation. 
  - The idea of anyone being able to quickly write code from anywhere, as the main promo video suggests, is fantastic and greatly motivating. 
  - In practice, coding on an iPhone (even with an innovative new joystick), is gimmicky(花招; 噱头) at best, given how deeply ingrained good ergonomics are in the coding process.
- This is mostly aimed at people who don't have the luxury of coding from a computer.

- Microsoft's "Touch Develop" research project from a decade ago was actually amazingly productive and usable. It made each separate part of a line of code into a selectable element, and used predictive analysis to guess what your next entry would be with surprising accuracy. So, for example, if you've already created a variable within a specific scope like a function, when you've come to a point in a line where a variable would be useful like "a += [variable could go here]", you could just tap-select it from a list. Since the named elements were kept track of, you could select and rename a variable or function and it would automatically be changed everywhere. You could grab whole functions like this and move them around as needed.
  - Conceptually, imagine that instead of writing out a line of code as a text sentence, you were assembling the program's syntax tree by choosing from a pile of premade items you've created, and then being able to grab whole branches at a time and manipulate them. It was an interesting experiment.

- ## ✨ [Replit now supports every programming language in Nix | Hacker News _202105](https://news.ycombinator.com/item?id=27269292)
- 
- 

- ## [Repl from Repo | Hacker News _201912](https://news.ycombinator.com/item?id=21765872)
- Gitpod is awesome and a really bright team behind it. 
  - However, Repl.it is different in that we're focused on speed and minimal configuration. You don't even need to login to clone a repo and start it.

- Will this change the pricing model at all? Or add a new tier? 
  - No, not at all. Our infra costs are a lot less than most people expect.
