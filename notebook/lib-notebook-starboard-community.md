---
title: lib-notebook-starboard-community
tags: [community, notebook, starboard]
created: 2021-05-11T19:25:36.057Z
modified: 2021-05-11T19:25:57.270Z
---

# lib-notebook-starboard-community

# guide

# discuss

- ## 

- ## 

- ## 

- ## [Starboard – Fully in-browser literate notebooks like Jupyter Notebook](https://news.ycombinator.com/item?id=24029002)

- Cell-by-cell notebooks like Jupyter are great for prototyping, explaining and exploration, but their dependence on a Python server (with often undocumented dependencies) limits their ability to be shared and remixed. 
  - Now that browsers support dynamic imports, it has become possible to create a similar workflow entirely in the browser.
  - That motivated me to build Starboard Notebook, a tool I wished existed

* Run entirely in the browser, there is no server or setup, it's all static files.
* Web-native, so no widget system is necessary. There is nearly no magic, it's all web tech (HTML, CSS, JS).
* Stores as a plaintext file, it will play nicely with version control systems.
* Hackable: the sandbox that your code gets run in contains the editor itself, so you can metaprogram the editor itself (e.g. adding support for other languages such as Python through WASM).
* You can import any code that targets the browser directly (e.g. puts stuff on the window object), or that has exports in ES module format.

- discussion

- I worked on a similar project
  - It's half abandoned now. 
  - one issue of js based notebook is the missing of a file system. 
  - data scientists load huge data into notebooks, this is hard to do on the web. 
  - There is the new web filesystem api, but that only helps load local files.
- [我为什么要做Epiphany](https://epiphany.pub/@shi-yan/wo-wei-shen-me-yao-zuo-epiphany)
- 我们做了Epiphany，我们心目中未来的交互式内容平台。特点:
  - 用Markdown格式书写，支持数学公式。
  - 可以嵌入交互式程序。目前支持Javascript和Python。未来会支持更多语言。
  - 一套通用的API，可以绘制图像，打印输出和创建UI与读者互动。
  - 拥有类似Github的版本管理系统，可以合作内容。
  - 支持众筹式的出版。
- 最近的两个类似平台observable和iodide都不约而同地选择了利用web技术。
  - https://github.com/iodide-project/iodide
    - /inactive
- My vision is for this to be handled by things like remoteStorage, Solid, or (if you must) Google Drive. 
  - I find having control over your data and delegating access to various apps to be a nice flow when implemented well
  - It's not a silver bullet. For larger data you can't afford to download it every time. 

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
