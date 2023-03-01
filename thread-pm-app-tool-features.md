---
title: thread-pm-app-tool-features
tags: [products, thread, tool]
created: 2021-03-15T05:21:25.780Z
modified: 2021-10-29T15:05:07.897Z
---

# thread-pm-app-tool-features

# discuss

- ## 

- ## Perplexity AI 之前一直做的是搜索引擎，但是可能受到 ChatGPT 的启发，现在改成了 AI 对话式搜索，
- https://twitter.com/oran_ge/status/1616601591754424323
  - 通过提问来获得直接的答案，并且可以继续对答案进行追问，相比单纯的 AI 生成，这里的每个答案都有引用链接，便于用户甄别内容的真实性。

- ## 我个人体验是以推荐算法为招牌的软件最后都很容易变得娱乐化，
- https://twitter.com/zxch3n/status/1599217608355876864
  - 像头条或者微博的推荐页给我看最多的内容就是猫猫狗狗或者搞笑娱乐视频（可能也在我有时候看到很好玩的也想点进去看，但刷多了信息流就废了）。
  - 推特基于关注过滤的内容至少能保证信息的价值密度比较高
- 反了，不是「最后容易变得娱乐化」，是「最初」对每个冷启动用户（无手动订阅关系和社交关系，无行为数据）分发的内容容易娱乐化。越缺乏个人数据就越受大众整体数据的影响，而大众整体是娱乐化的。尤其在中国，分裂为一线城市的发达市场和其他地区的新兴市场，用户增长到一定规模必然被后者的数据主导
  - 如何使用数据（包括手动订阅/关注的数据）来达成特定的用户体验、社区氛围、产品定位，是「策略」上的问题。
  - 有细粒度的数据可用、能细粒度的分发，是「机制」和「架构」上的问题。

- ## 为了让我的个人网站 100 年后依然可用
- https://twitter.com/ThaddeusJiang/status/1522476166703362048
1. 使用 @TiddlyWiki 构建，真正零依赖，只有一个 HTML。
2. #OSS in GitHub，同时部署在 GitHub Pages 和 @Netlify 。
3. 使用 #互联网档案馆 备份，并且为其捐款。

- ## 推荐一个可以一键生成随机用户头像和名称的工具Random Users，
- http://xsgames.co/randomusers/
  - 网站上提供了一些参数可以选择，比如性别（男性或女性），头像风格可以是彩色、黑白或像素类型，头像形状支持圆形和方形，网站底部给出了对应的API可以直接使用。

- ## Handshake is our(Framer) new game-changing beta feature, enabling anyone to import components into production with just a URL. 
- https://twitter.com/framer/status/1454055435745611779

- ## @algolia docsearch can now index your technical blog, for free
- https://twitter.com/sebastienlorber/status/1443920402686922755
  - I believe now a Docusaurus-based tech blog would be eligible

- ## Tiny helpers
- https://tiny-helpers.dev/
  - A collection of free single-purpose online tools for web developers

- ## CODECHECK
- https://codecheck.org.uk/
- CODECHECK tackles one of the main challenges of computational research by supporting codecheckers with a workflow, guidelines and tools to evaluate computer programs underlying scientific papers. 
- The independent time-stamped runs conducted by codecheckers will award a “certificate of executable computation” and increase availability, discovery and reproducibility of crucial artefacts for computational sciences.

- ## Figma really is a much better tool for basic vector image editing than Inkscape. 
- https://twitter.com/stevage1/status/1417354508464574465
  - Upload some SVGs, easily export to PNG. And keep them organised however you want.
- also the ceo of figma write esbuild in his spare time
- And you can share workspaces

- ## natto.dev is a canvas for JavaScript.
- https://www.notion.so/Documentation-44fea11f393a4e46b5a22f5799de58ca
  - creates an eval pane which consists of an expression editor and output. 
  - This is very much like a JavaScript console. 

- ## Cloudflare Pages is now in GA! 
- https://twitter.com/Cloudflare/status/1381593197311315973
  - It's hard to believe how much the product has matured in just a few months.
  - Dogfooding through and through, on Workers, SSL for SaaS, and on top of Cloudflare's network allows us to go FAST
- Awesome! I love the addition of custom redirects with the _redirects file. Looking forward to being able to add workers to an /api directory within the same page too! 
- This is great! Any chance we might get to use the same tooling to deploy workers without a path prefix for a fully dynamic edge rendered site? 
- I get the idea from this post that Polish and Mirage are included for free as part of pages - is this correct? If so, amazing
- I get the idea from this post that Polish and Mirage are included for free as part of pages - is this correct? If so, amazing

- ## I'm excited to share a preview of natto.dev, a canvas for writing and manipulating JavaScript.
- https://twitter.com/_paulshen/status/1370402539720503298
  - It's kinda like a JS playground, script runner, API client, JSON viewer, datavis tool, .. not sure exactly but it feels like something!
- nice! dragging a column out of a table is awesome. I also like the design of the wires, ambiently visible but light enough to not feel too "in the way"
  - I could imagine a non-programmer playing with this, and gradually picking up JS by messing w the code snippets
- each pane is an expression but you could fit arbitrary long content in a single expression.
  - it's kinda like a Swift playground but you choose where the logpoints are.

- ## A new GitHub Issues is coming this Fall, with better ways to plan, track, and manage projects.
- https://twitter.com/github/status/1407731478096756739
  - https://github.com/features/issues
  - github的issues依靠用户量，要超越atlassian全家桶已经势不可挡了
- **features**
- kanban-board 与 table 无缝切换
  - 支持sort/filter/group
- issues to actionable tasks
  - 类似邮件的操作，支持多状态或进度的任务
- conversation/expression with gfm markdown
  - 支持mention、emoji reaction、attachment、references to commits/pr/releases、project milestone
- slice views
  - 从现有表格中提取数据
- keyboard shortcuts
  - Every action you can take with the mouse has a keyboard shortcut or command
- custom fields
  - like priority, dates, notes, links
- automate with code
  - codify your team's process, like auto add labels to issues
- Issues, wherever you look
  - Issues can be viewed, created, and managed in your browser/terminal/phone.
- Seems like GitHub is going to cover it all for us - from project planning to development to deployment. Excited for this release
- If you add time report and nice charts and reporting we would be glad to leave Jira
- Bookmarking this for the paper unfolding animation
  - We were inspired by "origami"(日本折纸艺术，折纸手工), because of the many ways you can setup a project table with custom fields. It felt like a canvas and folding paper to achieve different shapes.
  - https://github.com/robbykraft/Origami
- How does the animation unfold at the beginning of the video?
  - We were inspired by "origami" so the idea is that you are unfolding an issue.
- How sorting priorities are handled with labels? (Or any custom fields really) if e.g if we want to group by priority, but sorting with high priority coming first in the group and low priority coming down
  - Yep! You can group by one category, then sort by another.
- I hope it has some sync story with Jira so that our org can use it. Other parts of company deeply entrenched in Jira
- Any plans for better search, with full Boolean logic in queries? That is the one thing I would miss from Jira.
