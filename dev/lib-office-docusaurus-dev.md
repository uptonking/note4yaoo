---
title: lib-office-docusaurus-dev
tags: [docusaurus, office]
created: '2020-12-19T08:50:35.122Z'
modified: '2020-12-19T08:52:02.671Z'
---

# lib-office-docusaurus-dev

# guide

# pieces

# docs

# blog

- ## [Docusaurus 2019 Recap_201912](https://v2.docusaurus.io/blog/2019/12/30/docusaurus-2019-recap/)
- In 2018, we proposed to rebuild Docusaurus from the ground up.
  - a content-centric CSS framework from scratch, a plugins system, and moved from static HTML pages to be a single page-app with prerendered routes.
- Since 2.0.0-alpha40, all features in Docusaurus 1 except for translations have been ported over.
- D2's killer features are Dark Mode and its superb performance
- we implemented a plugins architecture and turned the repo into a Lerna monorepo. 
- In 2020, we want to achieve full feature parity with D1 by the first half and help the remaining Facebook projects on D1 move to D2

- ## [Towards Docusaurus 2_201809](https://docusaurus.io/blog/2018/09/11/Towards-Docusaurus-2)
- I will provide details on some of issues in Docusaurus 1 and how we are going to address them in Docusaurus 2.
- A Docusaurus 1 website is, in fact, built into a bunch of static HTML pages. 
  - Despite using React, we were not fully utilizing the features React offered, such as component state, which allows for dynamic and interactive pages. 
  - React was only used as a templating engine for static content and interactivity has to be added through `script` tags and `dangerouslySetInnerHTML`
- In addition, there is not an easy way to change how Docusaurus loads content. 
  - For example, adding CSS preprocessors such as Sass and Less was not supported natively and involved many user hacks of adding custom scripts.
- For Docusaurus 2, we will be using webpack as a module bundler and we are changing the way we serve content. 
  - Adding CSS preprocessors will be as easy as adding a webpack loader. 
  - Instead of a pure static HTML, during build time we will create a server-rendered version of the app and render the corresponding HTML. 
  - A Docusaurus site will be essentially an isomorphic/universal application. 
  - This approach is heavily inspired by Gatsby.
- For Docusaurus 2, every time we cut a new version, we will instead take a snapshot of all the docs. 
  - We will not require the content of a document to have changed. 
  - This is a space complexity trade-off for a better developer and user experience. 
  - We will use more space for better separation of concerns and guaranteed correctness.
- Docusaurus v1 is in charge of the entire layout and styling, unintentionally making it very hard for users to customize their site's appearance 
- For Docusaurus 2, layout and styling should be controlled by the user. 
  - Docusaurus will handle the content generation, routing, translation, and versioning. 
  - Inspired by create-react-app and VuePress, Docusaurus will still provide a default theme, which the user can eject from
- For Docusaurus 2, users can eject and choose their own markdown parser
  - v1 markdown parsing is currently powered by Remarkable.
  - As a rule of thumb, the user has to provide a React component, in which we will provide a children props containing the RAW string of markdown. 
  - By default, we will use Remarkable for the markdown parser and Highlight.js for the syntax highlighting
- For Docusaurus 2, we will allow users to customize the search box. 
  - However, we will still use Algolia in the default theme

- Docusaurus' mission has always been to make it really easy for you to get a website with documentation up and running out of the box. 
  - That mission does not change with Docusaurus 2.

- ## [Docusaurus 2 Design_201806](https://github.com/facebook/docusaurus/issues/789)
- v1 problems
- Current architecture is a bit tangled and makes it hard to introduce plugins.
- styling
  - All CSS is compiled into one file.
  - Does not allow adding local vendor CSS and JS
  - Docusaurus controls much of the styles and layout, Site layout is not/hard customizable 
- Routing logic is separated and resides within both server and generation code
- New features are mostly enabled via siteConfig, siteConfig will bloat(膨胀) over time
- Many components relies on process.cwd() too much (mostly for siteConfig), making it very hard to test.
- LiveReload does a full-page reload, and page reloads for changes of all files.
- Build pipeline is imperative and quite tangled(纠缠的；混乱的).

- v2 proposals
- v2 should be responsible for documentation content, routing, translation and versioning, leaving layout and styling to the end user.
  - It's not a good idea for Docusaurus to maintain the entire layout and styling as these stuff are hard to make improvements without breaking existing users' code.
- Rearchitect architecture to introduce hooks into the development and build phase so that a plugin system is possible.
- Use a module bundler like webpack

# discuss

- ## Docusaurus v1 was just simple HTML output, while v2 is a React SPA.
- https://twitter.com/sebastienlorber/status/1389128918028931074
  - v2 has lower lighthouse score, but I don't think this tool is fair for many reasons, and v2 users are happy with the v2 UX.
- We'll benefit from React innovations sooner or later, and Docusaurus can almost work if you disable the JS (ie React as non-blocking progressive enhancement)
