---
title: lib-notebook-observablehq-community
tags: [community, observablehq]
created: 2021-05-14T14:54:41.440Z
modified: 2021-05-14T14:55:00.191Z
---

# lib-notebook-observablehq-community

# discuss-stars

- ## 

- ## 

- ## [Can you run your own Observable notebook server _201805](https://talk.observablehq.com/t/noob-can-you-run-your-own-observable-server/757)
- The community could create a custom open sourced editor for observablehq, based on the runtime

- https://github.com/observablehq/runtime
  - Observable runtime lets you run Observable notebooks as true reactive programs in any JavaScript environment
- Embeddable notebooks are now available. 
  - You can download your compiled notebooks and upload them to your server, 
    - or load them directly from api.observablehq.com with your provided access key. 
  - With the first method, you’re completely independent of observablehq.com, 
  - but with the latter, you can get live updates to your (for example, dynamic programming tutorial) every time you hit “Publish” again.
- The notebook-runtime is the same codebase that observablehq.com uses to run your notebooks, and has the same browser support targets: 
  - the evergreen browsers — Chrome, Firefox, Safari, Edge and Node.js. 
  - That said, if you need wider browser support, we’d certainly be happy to look at pull requests against notebook-runtime that enable it.
- We may offer some on-premise (self-hosted) enterprise solution in the future, 
  - but our current focus is on developing cloud-hosted private collaboration for teams.

- ## [Offline Editor - Site Feedback - The Observable Forum _202104](https://talk.observablehq.com/t/offline-editor/4905)
- we’re soon going to open source the runtime for Observable, making it possible to export a notebook and include it on another website/webpage. But that won’t include the editable notebook interface or the rest of observablehq.com - unlike Jupyter, we’re really aiming to create a community and cross-pollination of concepts and code rather than individual installations.

- 202210: Any updates about it? Is there a way to work with an Observable notebook offline and to import back modifications into the Observable cloud?
  - The thread Aaron mentioned talks about number of offline editors. I assume you already looked at those. There are no plans yet to support a round-trip offline editing experience

- 
- 
- 

- ## 🚀 [Dataflow, a self-hosted Observable notebook editor | Hacker News _202105](https://news.ycombinator.com/item?id=27145515)
- I adore Observable notebooks, but the one thing that makes me hesitate in using them for everything is that the editor component itself is closed-source and only available on https://observablehq.com/
  - They're great open source ecosystem supporters - they released their runtime, their parser, their standard library and all sorts of other stuff - but the editor itself is their proprietary sauce.
  - I don't even see it as a competitor to ObservableHQ - the hosted Observable editor has collaboration features that don't even make sense for a local running version.
  - Plus, Dataflow has some great ideas of its own - in particular the live file attachments thing.

- Is that similar concept to Overleaf for LaTeX?
  - LaTeX doesn't really support interactive data visualizations or reactive re-rendering, and it's a pretty difficult environment to do things like read a CSV data file and do a linear regression in. 
  - Observablehq is closer to Jupyter, Excel, R Studio, Octave, or Tk than LaTeX.

- 
- 
- 

- ## We're excited to launch real-time collaboration on Observable!__202103
- https://twitter.com/nebrius/status/1370067809955315714
- Tell us how did you do that, what are those tech parts and libs which helped?
  - 👉🏻 We upgraded to **CodeMirror 6** and we're using their new collab module to handle local reconciliation
  - We then sync changes to/from the client through our servers using web sockets.
  - Observable already uses web sockets for syncing notebooks (you can see this when you open a notebook in two browser windows and edit one of them), so we only needed to add a few new messages to sync uncommitted changes and user presence.
- Does CodeMirror's OT model allow you to hold changes until they're syntactically correct on both sides?
  - That should be possible (the timing and implementation of sending changes is left to your integration code, so it can hold off until some condition is satisfied).
  - (Of course, the result of merging two concurrent syntactically-valid changes may still be syntactically invalid.)

# discuss-news
- ## 

- ## 

- ## 

- ## I appreciate the nod to "File over app" from @mbostock and the @observablehq team in the latest announcement.
- https://twitter.com/kepano/status/1758202572446581025
  - It's so cool that a Markdown file with code blocks can be the source for complex data visualizations and dashboards. This means the files are interoperable with @obsdmd .
- Your post strengthened my conviction in this evolution of Observable. Interoperability for the win!! Thanks for trying Framework, too.
- Probably worth mentioning @evidence_dev , a BI library integrating markdown and SQL for elegant data analytics and visualization

- ## [Interesting ideas in Observable Framework _202403](https://simonwillison.net/2024/Mar/3/interesting-ideas-in-observable-framework/)
- There are a lot of really interesting ideas in Observable Framework.
  - A static site generator for data projects and dashboards
  - JavaScript in Markdown
  - Everything is still reactive
  - Only include the code that you use
  - Cache your data at build time
  - Comparison to Observable Notebooks

    - The notebook editor itself isn’t open source—it’s a hosted product provided on observablehq.com. You can export the notebooks as static files and run them anywhere you like, but the editor itself is a proprietary product.
    - Editable notebooks are a pretty complex proprietary file format. They don’t play well with tools like Git, to the point that Observable ended up implementing their own custom version control and collaboration systems.
    - Notebooks (really documents) are now single text files—Markdown files with embedded JavaScript blocks. It’s all still reactive, but the file format is much simpler and can be edited using any text editor, and checked into Git.
    - It’s all just standard JavaScript now—no custom syntax.

  - A change in strategy
- 
- 

- ## @observablehq 2.0 defines a file format, local support, and open source framework
- https://twitter.com/tmcw/status/1758142768877023451
- If I understand this correctly, the (evolving) business model here is analogous to making the compiler for a language free, but offering an IDE as a subscription service. http://Observablehq.com is still the way we're expected to develop, in our browsers. I hope this works out.
- looks excellent. notebooks have never really clicked for me as a non-data-scientist

- ## 🎯 open-source static site generator — Observable Framework — for creating fast, beautiful data apps _202402
- https://twitter.com/observablehq/status/1758167290942525738
- Did you give up on the "custom js" idea? 
- my dream is you making jupyter notebooks that don’t suck. My dream is seeing a python interpreter that works just like your current JS custom interpreter.
  - You should try writing Python data loaders in Framework! As soon as you save changes to your Python file, the page updates instantly with fresh data without you needing to reload.

- Maybe it worth a try to make a plugin for obsidian that can render the Observable notebook in the local environment. It would be a game changer for the note taking experience.

- ## 🎯 [Announcing Observable 2.0! - Announcements - The Observable Forum _20240215](https://talk.observablehq.com/t/announcing-observable-2-0/8744)
- doesn’t this obsolete your paywall model?
  - Yes. Observable is now free again for individuals, including private notebooks and databases connectors. And you can pay for larger (>5) teams and more hosted projects.
  - we think notebooks are a nice complement to Framework projects

# discuss
- ## 

- ## 

- ## 

- ## it's too easy to get stuck in an infinite loop with autorun enabled. 
- https://twitter.com/zxch3n/status/1600659901080297472
  - if natto guesses you're writing a loop, it'll now automatically disable autorun.
- CodePen solved this by injecting custom code into loops if I remember correctly. The code will abort the loop if it takes too long to run
- yep! that's the most robust approach but i'd like to avoid injecting code if possible (1. needs to load parser before code can run. 2. changes runtime behavior)

- ## One great thing about using @observablehq is that I am not "locked in". 
- https://twitter.com/steren/status/1525226330039521280
  - notebooks can be exported in idiomatic JavaScript, and later loaded on my own website:

- ## To help investigate userspace bugs in long running @observablehq notebooks, I used @mootari 's access-runtime notebook to create a notebook state snapshot function. 
- https://twitter.com/tomlarkworthy/status/1508384106937303043
  - Now you get a readout of all the cells and their current state, and value is availible.

- ## Anyone seen any good patterns for running automated tests in an @observablehq notebook?
- https://twitter.com/simonw/status/1495094294851428352
- If ya looking for more end-to-end or integration tests: https://github.com/asg017/observable-prerender
  - Otherwise, abstracting your JS code into a separate package is always cool, or moving your data processing into a node script is also helpful

- ## Observable’s Not JavaScript_201906
- https://news.ycombinator.com/item?id=20184181
- I kinda want Observable to be it's own language that can compile to JS
  - And it kinda is. We provide a parser¹ and a runtime², and you can download a copy of any notebook compiled to a JavaScript module
  - That said, we’re explicitly designing for the reactivity of the notebook environment. 
- What's the rationale for results above code?
  - On Observable, each cell is a unit that can be evaluated independently, with two sides to it — you have the source code editor, and you have the rendered display (either a chunk of DOM or canvas that you’ve drawn, or an interactive inspector for JS values).
  - Now, the important thing is that the code half of the cell is often collapsed. 
  - If the code is on top, the entire cell jumps when it opens and closes, pushing the rendered display up and down. 
  - If the code is on the bottom, it emerges from the half of the cell that is always there, and the display is stable.
  - the rendered value as primary and the source code as secondary.
- Non-linear is a plus. Why force an order. Spreadsheet is non-linear and it works pretty well
- Clicking to reveal can be simply addressed with a global Expand-All toggle.
- What I'm talking about is editing code with Vim-like keys INSIDE the cells. An implementation of the Ace Editor or something similar would be amazing.
  - We use CodeMirror and are considering the vim bindings, but it’d probably be something we launch at the same time as user-configurable key bindings.
