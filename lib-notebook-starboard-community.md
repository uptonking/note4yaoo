---
title: lib-notebook-starboard-community
tags: [community, notebook, starboard]
created: '2021-05-11T19:25:36.057Z'
modified: '2021-05-11T19:25:57.270Z'
---

# lib-notebook-starboard-community

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
