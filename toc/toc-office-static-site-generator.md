---
title: toc-office-static-site-generator
tags: [documentation, markdown, static-site-generator, toc]
created: 2020-08-09T11:20:56.480Z
modified: 2021-07-17T03:00:02.268Z
---

# toc-office-static-site-generator

# guide

- Why use React or JS, HTML-only static sites are faster
  - try to browse it a little bit. 
  - It feels faster than a static HTML-only site thanks to preloading and only downloading what’s necessary for next pages.

- ref
  - [top static-site-generator](https://github.com/topics/static-site-generator)
# popular
- https://github.com/gohugoio/hugo /71.2kStar/apache2/202402/go
  - https://gohugo.io/
  - a static HTML and CSS website generator written in Go. 
  - Hugo takes a directory with content and templates and renders them into a full HTML website.
  - Hugo relies on Markdown files with front matter for metadata
- https://github.com/gatsbyjs/gatsby /48.2kStar/MIT/202012/ts
  - a framework based on React that helps developers build blazing fast websites and apps
- https://github.com/jekyll/jekyll /41.8kStar/MIT/202401/ruby
  - a blog-aware static site generator in Ruby
  - Jekyll is the engine behind GitHub Pages

- https://github.com/hexojs/hexo /38.1kStar/MIT/202401/ts
  - https://hexo.io/
  - simple & powerful blog framework, powered by Node.js
  - 依赖bluebird、moment、warehouse-db
  - Hundreds of themes & plugins

- https://github.com/getzola/zola /12.3kStar/MIT/202402/rust
  - https://www.getzola.org/
  - A fast static site generator in a single binary with everything built-in
  - This tool and the template engine it is using were born from an intense(强烈的，极度的) dislike of the (insane) Golang template engine and therefore of Hugo that I was using before for 6+ sites.
  - (Basic currently) multilingual site suport
  - Image processing
  - Shortcodes
  - Table of contents automatic generation
  - Breadcrumbs
  - Search with no servers or any third parties involved
  - Live reload

- https://github.com/snowpackjs/astro
  - https://astro.build/
  - Astro works a lot like a static site generator(jekyll)
  - In Astro, you compose your website using UI components from your favorite JavaScript web framework (React, Svelte, Vue, etc). 
  - Astro renders your entire site to static HTML during the build. 
  - The result is a fully static website with all JavaScript removed from the final page.

- https://github.com/vuejs/vuepress
  - /18kStar/MIT/202012/js
  - Minimalistic Vue-powered static site generator
- https://github.com/netlify/netlify-cms
  - /13.1kStar/MIT/202012/js
  - A Git-based CMS for Static Site Generators
  - Netlify CMS is a single-page app that you pull into the /admin part of your site.
    - It presents a clean UI for editing content stored in a Git repository.

- https://github.com/11ty/eleventy /8kStar/MIT/202401/js
  - https://www.11ty.dev/
  - A simpler static site generator. An alternative to Jekyll.
  - ransforms a directory of templates (of varying types) into HTML.
  - Works with HTML, Markdown, Liquid, Nunjucks, Handlebars, Mustache, EJS, Haml, Pug, and JavaScript Template Literals.

- https://github.com/getpelican/pelican
  - /10.1kStar/AGPLv3/202012/python
  - Static site generator that supports Markdown and reST syntax. Powered by Python.
- https://github.com/react-static/react-static /9.2kStar/MIT/202011/js/inactive
  - 原作者已转向next.js
  - A progressive static site is a website where every statically exported HTML page is an entry point to a fully-featured automatically-code-split React application.
  - Just like a normal static site, static progressive websites are capable of loading initial landing pages very quickly, but then extend the user experience by transforming invisibly into a single-page React application.
  - [Where is react-static 8? The state of react-static -- and its inevitable death _202203](https://github.com/react-static/react-static/discussions/1661)
    - For the projects where we normally had used react-static, we now use remix, astro, and nextjs for others.

- https://github.com/segmentio/metalsmith
  - /7.6kStar/MIT/201912/js
  - pluggable static site generator.
  - all of the logic is handled by plugins. 
- https://github.com/natemoo-re/microsite
  - https://github.com/natemoo-re/microsite/tree/main/docs
  - /524Star/MIT/202012/ts
  - a fast, opinionated static-site generator (SSG) built on top of Snowpack.
# more-ssg
- https://github.com/eleme/duang
  - https://eleme.github.io/duang/docs/intro/
  - 一种基于配置自动生成CMS的工具
- https://github.com/usebedrock/bedrock
  - https://bedrockapp.org/
  - a static site generator to create large-scale HTML prototypes and document design systems
  - 内置bootstrap4和material design主题
- https://github.com/make-my/makemy
  - makemy is a tool that parses your text-posts and creates beautiful webpages out of them 
  - Powered entirely in NodeJS 
- https://github.com/jbake-org/jbake
  - http://jbake.org/
  - /913Star/MIT/202104/java
  - a Java based static site/blog generator
# discuss
- ## why I should use eleventy over Gatsby
- https://twitter.com/CallMeWuz/status/1241171870751305728
- sure
  - Eleventy doesn't enforce conventions on you. 
    - You can choose a templating language. Gatsby forces you to use React. 
  - Eleventy doesn't serve a JS bundle by default. 
    - Gatsby can strip its added bundle with a plugin.
  - I personally love multi-page sites more than SPAs
- I'm a senior react developer and I enjoy Gatsby! 
  - The people there are doing some great work to make React projects less client-bloated, and I'm glad they reinvigorated the interest in SSG tools. 
  - I just also love that Eleventy doesn't require a complex API layer. Or React.
- @eleven_ty is _just_ #JavaScript. 
  - No React overhead ... or of any kind, really. 
  - 11ty frees you up to concentrate on your project. 
  - It drastically lowers the barrier to entry for clients and collaborators. 
  - And you will not find anything remotely as convenient, fast, and secure.

- ## Unpopular opinion: most of the sites people use gatsby for should be vanilla HTML or CSS, not even eleventy or anything.
- https://twitter.com/oleg008/status/1339311178892398593
- A lot of people use these frameworks on simpler websites to learn. Often, they might anticipate it growing and it'd just be easier to have it there. I see your point, but it's not always the case that people are over-complicating it without reason.
  - that reason is the reason for all overengineering
- I guess the problem is the lack of tooling for building things with plain css and HTML. 
  - I suspect people choose gatsby for the tooling (templating, data fetching) more than because JavaScript. 
  - There’s Hugo and it’s not bad. What other options are there?
