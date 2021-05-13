---
title: lib-notebook-starboard-community
tags: [community, notebook, starboard]
created: '2021-05-11T19:25:36.057Z'
modified: '2021-05-11T19:25:57.270Z'
---

# lib-notebook-starboard-community

# guide

- ## Google docs is apparently moving to a canvas based editor. 
- https://twitter.com/devongovett/status/1392597989768585218
  - This is horrible for accessibility and a great example of what *not* to do. 
  - I’m surprised no one flagged this
- They could have worked with the Chrome team to help improve standards where they are lacking and make the web better for all of us, 
  - but instead decided to reimplement the browser themselves. Very disappointing.
  - Well, to be fair, the old one was also very broken. But at least it had the potential for improvement. Switching to canvas kinda prevents that.
- Would you say that implementing web apps with the canvas API no-go?Are there other downfalls to be aware of? (aside of a11y problems)
  - Text selection, copy/paste, find in page, spell checking, dictionary, system wide text replacement/auto correct, etc would all need to be rewritten and would not integrate as expected with the system.

- ## [Google Docs will now use canvas based rendering: this may impact some Chrome extensions](https://workspaceupdates.googleblog.com/2021/05/Google-Docs-Canvas-Based-Rendering-Update.html)
- We’re updating the way Google Docs renders documents. 
  - we’ll be migrating the underlying technical implementation of Docs from the current `HTML-based` rendering approach to a `canvas-based` approach 
  - to improve performance and improve consistency in how content appears across different platforms. 

# discuss

- ## 

- ## 

- ## 

- ## I created an open source literate notebook system similar to Jupyter Notebook but for Javascript that runs entirely in the browser
- https://www.reddit.com/r/javascript/comments/i2gtnl/i_created_an_open_source_literate_notebook_system/
- I think Observable is a really cool tool, it's a bit different:
  - Observable has quite some magic, it's not just Javascript you can type there (there is a compile step to make it possible). 
  - With Starboard the plan is to make it trivial to export as a static website, with vanilla javascript that's a lot more easy.
  - The reactive system they have there is powerful, but also a bit confusing sometimes. 
- Starboard is just plain javascript (for better or for worse ^^). 
  - You can run cells out of order, which is a feature I actually enjoy in Jupyter when I'm still in the exploratory stage.
  - Observable is a walled garden, you can't export the notebooks into say a text file and use it independently, they own the ecosystem 
  - (and that's fair, they have to make back the millions in investment they received). 
  - Starboard is open source and it is built with the idea of customization and portability in mind
  - I think both the tools have different usecases and can definitely co-exist
- Are you sure you don't want to borrow the reactive system? Not only does it let you create more readable notebooks (all helpers/imports at the end), but it significantly reduces the amount of bugs you have to deal with while writing your notebook.
  - I think it has pros and cons, but you are right that you can definitely easily introduce bugs. At least in Javascript your variables will be scoped to the cell unless you explicitly use var or share it otherwise (e.g. putting it on window), that helps a little bit.
  - I see reactivity as a potential plugin, the way I tried to design Starboard is such that it's all just vanilla javascript and plugins can change which cell types are available or the way cells are interpreted or run. In the short term I want to support Python through project Pyodide, that will also just be a plugin.
- How do you compare to Stencila?
  - From what I can tell it's a layer on top of Jupyter and Rmarkdown, so it probably relies on a server your notebook needs to talk to, whereas Starboard is fully client side
