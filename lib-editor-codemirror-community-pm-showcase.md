---
title: lib-editor-codemirror-community-pm-showcase
tags: [codemirror, community, showcase]
created: 2024-08-11T06:43:59.709Z
modified: 2024-08-11T07:21:18.707Z
---

# lib-editor-codemirror-community-pm-showcase

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-rich-text-cm
- ## 

- ## 

- ## 
# discuss-pm-code-docs
- ## 

- ## Google's NotebookLM is truly the best AI second brain.
- https://x.com/itsPaulAi/status/1836445715968725180
  - You can easily learn, memorize, generate new ideas, and more.
  - There's virtually no limit to the number of things you can feed it: the context window is huge (1M tokens?).

- ## 📖 [Show HN: Srcbook – A TypeScript notebook for rapid prototyping | Hacker News _202408](https://news.ycombinator.com/item?id=41291700)
  - We built this because we needed a Jupyter-like environment for TypeScript

- how do you run the code? is it securely sandboxed?
  - The code runs locally on your machine. 
  - Right now the architecture is that each Srcbook has 2 representations:
  - a markdown encoding that we use when you export. Easier to share, serialize, etc...
  - on disk, Srcbooks are actually directories under ~/.srcbook/srcbooks. The files and code is all there, and runs with your local node executable. You therefore need to be careful to not run any arbitrary srcbook you download, but there is no code ever leaving your machine

- Observable is a great notebook env for dataviz, but the bespoke js + observability patterns can feel obtuse for non-dataviz stuff.
  - Likewise, the Jupyter js kernels feel second-class and require python dependencies.
- 🆚️ How does it compare with Observable?
  - Observable is highly specialized in data visualizations (graphs, plots, etc...) and runs in the browser.
  - Srcbook is built for different use cases: we focus on a backend runtime (node) and want to solve for non-data-visualizations workflows. Use cases like prototyping with a third party npm library, running a script to test your app's behavior, or building an AI agent.
  - Compared to Observable, it's apache-2 licensed and it's self-hostable. The d3, p5 and database access you have to add yourself. With Observable user, workspace, diagramming and template management is built-in.

- I think this is more like Google Colab, where the UI renders in the browser, but offloads computation to a kernel running elsewhere.
  - As I recall, Observable uses the browser's JS runtime for computation.

- Love that this is local. I've messed around trying to get Node on Jupyter with custom kernels, but never got close to a working setup with TypeScript.
  - Two features would be huge:
  1. Web cells for intermixing UI components alongside NodeJS cells. Would be cool if there was a bridge API to call code in the Node cells as well.
  2. VSCode extension to render this all in there directly.

- This is a cool idea! I often end up just using replit to play with a library, something more like Livebook makes a lot of sense. I like that you're using markdown too, makes these files much more useful than Jupyter ones.
  - The Markdown is a really neat idea borrowed from Livebook. It allows for really good diffing if you want to version control them, and makes reviewing diffs easier. As a bonus a lot of things can read markdown and render it nicely for you.

- I wish there was also a "browser" cell, so that the execution wouldn’t be happening in the node.

- how do you plan to monetize this?
  - The plan is to have a cloud offering which runs Srcbooks as infrastructure. There are a couple of directions are considering, but essentially they boil down to helping you build an app quickly and iteratively, then serve it in production.

- why this is advantageous over just dumping a bunch of HTML files into a folder
  - Presumably this runs in node, rather than the browser, which might have implications for your dependencies (I know esm.sh shims node core dependencies and does fancy transpilation stuff, but why deal with that if you can just run direct on node).

- ## 📖 [Devbook - Show HN: Add live runnable code to your dev docs | Hacker News _202204](https://news.ycombinator.com/item?id=31004973)
- Devbook is an SDK that you add to your docs website and then every time a user visits your dev docs, we spin up a VM just for that user. 
  - The VM is ready in about 18-20 seconds. We haven't had enough time to work on optimization but from our early tests, we are fairly confident we can get this to about 1-2 seconds.
  - In the VM you can run almost anything. Install packages, edit & save files, run binaries, services, etc.
  - On the backend, the VM is a Firecracker microVM with our custom simple orchestrator/scheduler built on top that just gets the job done. 
- We chose Firecracker for 4 reasons:
  * (1) the security with a combination of their jailer
  * (2) its snapshotting capabilities
  * (3) quick booting times
  * (4) option to oversubscribe the underlying server resources
- The way Devbook works is that you use our frontend SDK on our website. The SDK pings our backend and we boot up a VM.

- https://github.com/firecracker-microvm/firecracker /apache2/202405/rust/python
  - http://firecracker-microvm.io/
  - Firecracker is an open source virtualization technology that is purpose-built for creating and managing secure, multi-tenant container and function-based services that provide serverless operational models. 
  - Firecracker runs workloads in lightweight virtual machines, called microVMs, which combine the security and isolation properties provided by hardware virtualization technology with the speed and flexibility of containers.
  - The main component of Firecracker is a virtual machine monitor (VMM) that uses the Linux Kernel Virtual Machine (KVM) to create and run microVMs. 
  - Firecracker was developed at Amazon Web Services to accelerate the speed and efficiency of services like AWS Lambda and AWS Fargate. 

- Very good idea, and you're not alone. The upcoming documentation for React will have a similar feature built on Sandpack
- We've used https://docusaurus.io/docs/markdown-features/code-blocks do this ourselves. No need to use codesandbox.
  - Docusaurus maintainer here. Yes we like MDX and live code blocks to embed natively runnable code in your page. I don't like the idea of loading a remote iframe much (at least for most cases using JS).
  - The StackBlitz / WebContainer approach also seems better than a remote VM + iframe
  - We'll likely use a project called React-Runner in the future, quite similar to our current setup (real native embed) but lighter.

- Since you're using Firecracker, it's hard to understand how it takes 20 seconds to boot a VM. AWS Lambda worst performer (JVM) I think takes much less than that, like 5 seconds in cold start. Why don't you offer warmed VMs? Like reserved concurrency in AWS Lambda. Preemptively increase the number of VMs (like an auto-scaler) as traffic increases.
  - We have a few unoptimized things happening on our infra in the moment. We are working on it to make it better and it will be better soon. Most likely around 1-2 seconds.

- This seems like a great alternative to passing around postman collections separate from documentation

- 🤔 Isn't this something similar to Jupiter Books, where you can have executable code?
  - Devbook allows you to integrate the "interactive code experience" natively into your docs. It's not just embedding an iframe. We can also handle use-cases like CLIs better since you can add a full emulated terminal (like RunOps did on their landing page) to your website and control it with JavaScript.

- Is there a way to declare the code in the backend, instead of the frontend? Declaring the code in the frontend and having the VM execute whatever comes from it is asking for serious abuse.
  - Yes! You can predefine the whole VM with our CLI via a simple Dockerfile

- how about going the opposite way, while staying in your code editor you can interact with some documentation that guides you to integrate with their code
  - Stay tuned to what we are building
# discuss
- ## 

- ## 

- ## 

- ## It can Record then and then Replay text editing actions you take on a `<textarea>` . "Live coding without the stress"
- https://x.com/LeaVerou/status/1584250066029928449
- It would be so cool if @codePen supported recording scripts and replaying them — I've checked and Rety *could* support CodeMirror with some tweaking, as it does produce the necessary events.

- ## joplin: The new Markdown editor is based on CodeMirror 6 _202312
- https://x.com/joplinapp/status/1732067094903050470
  - Joplin 2.13 is now available
  - New beta Markdown editor 
  - The new Markdown editor is based on CodeMirror 6! This means a consistent editor experience across desktop and mobile apps, paving the way for future mobile plugin support. 

- ## At @Replit , we're placing a big bet on CodeMirror 6, a new code editor that's fast, minimal, and extensible. _202201
- https://x.com/SergeiChestakov/status/1486025274240090114
  - Unlike CM6, Monaco is bloated, difficult to customize, and doesn't support mobile (which is becoming increasingly important).

- 
- 
- 
