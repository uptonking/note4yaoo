---
title: lib-editor-dev-block
tags: [cell, editor]
created: '2021-06-01T20:03:25.130Z'
modified: '2021-06-01T20:03:38.284Z'
---

# lib-editor-dev-block

# guide
- pros
  - 可自定义扩展的block功能太强大了
  - 设置样式十分方便
  - 引导用户操作复杂功能
  - 支持嵌套
  - 适合在输入文本较少的移动端使用，不适合在输入文字较多的桌面端
  - 容易实现virtualize，只渲染视口可见范围内的内容
  - 容易实现折叠指定block区块

- cons
  - 分散输入大段文字时的注意力，特别是光标默认的焦点位置
  - 跨block的选择

- industry
  - wordpress强推自研的开源块级编辑器Gutenberg
# blogging

## [The WordPress block editor: Why you should be using it](https://yoast.com/the-block-editor-gutenberg-why-you-should-be-using-it/)

- The future of the block editor
  - Future versions will iterate on what the block editor already does, moving to site-wide editing, instead of just the content area. 
  - The first required step for that is defining content edit areas
  - The Gutenberg project aims at making WordPress easier to use. 

- Reasons to use the block editor now
- You will be able to build layouts that you can’t make in TinyMCE. 
  - Most of the stuff we did for our recent digital story required no coding. 
  - Plugins like Grids make it even easier to make very smooth designs.
- You can make FAQs and HowTo’s that’ll look awesome in search results. 
  - Our Yoast SEO Schema blocks are already providing an SEO advantage that is unmatched. For instance, check out our free FAQ and How-to blocks.
- Simple things like images next to paragraphs and other things that could be painful in TinyMCE have become so much better in Gutenberg. Want multiple columns? 
  - You can have them, like that, without extra coding.
- Speaking of things you couldn’t do without plugins before: you can now embed tables in your content, just by adding a table block. No plugins required.
- Creating custom blocks is relatively simple, and allows people to do 90% of the custom things they would do with plugins in the past, but easier. 
  - It becomes even easier when you use a plugin like ACF Pro or Block Lab to build those custom blocks.
- Custom blocks, or blocks you’ve added with plugins, can be easily found by users just by clicking the + sign in the editor. 
  - Shortcodes, in the classic editor, didn’t have such a discovery method.
- Re-usable blocks allow you to easily create content you can re-use across posts or pages, see this nice tutorial on WP Beginner.
# discuss-stars
- ## [Choosing DB model for an app similar to Notion, Block-based ("paragraphs") or document-based?](https://stackoverflow.com/questions/71024175)
- 比较项目
  - Fetch the contents of a page
  - Render the content of a page**
  - Update the content of a paragraph in the DB
  - Alternatives for rendering very large documents *
  - Import or paste content
  - Copy content**
  - Real-Time Collaboration

- ## We've been working a new protocol at @hashintel. It's called the block protocol
- https://twitter.com/Mappletons/status/1488131234089873408
  - It allows you to build reusable blocks (aka. components) that are interchangeable across website/apps
  - To recap: 
  - We now have a standard way to create reusable blocks that can read / write semantic data and be used in any app that opts into the ecosystem. Which saves us from block fortresses.
  - And blocks create structured data by default, without devs manually doing it.
  - Disclaimer: The spec is currently a draft and has flaws.

- Do blocks compose? i.e. Can I have a block that contains other blocks inside?
  - Yes, you can - the container block would act as an embedder of the contained block, and provide it with the data and functions it needed. Maybe a straight pass through from the parent application, maybe supplementing it. This needs more testing though, with more complex blocks
  - Yeah, it seems like the types would get quite complex when you're essentially handling parametric polymorphism by allowing a container to embed arbitrary blocks

- Isn't this what web-components are trying to solve?
  - [Isn't this basically web components?](https://github.com/blockprotocol/blockprotocol/discussions/149)
  - One additional thing that the Block Protocol provides which Web Components do not is standardising the interface between the component and the embedding application - e.g. the methods or events the WC is using.
  - The Block Protocol specifies the name and purpose for applications to provide to blocks, and blocks to use to do things. 
  - Web Components can describe their interface programmatically, but each one can be different - they are described but not standardized. 
  - This means that you often need to know the API of a specific WC in order to implement it. 
  - The aim of the Block Protocol is that all blocks have the same API, and thus new blocks can be added to an application without having to learn anything about them.
  - We are indeed aiming to build on top of the existing standards: we don't want to invent a new way of implementing encapsulated web components (there's already several of those), but instead standardize how those encapsulated components communicate with the application using them. There's a bit more in the FAQ about our relation to existing standards.
- I think this suffers from trying to be everything to everyone & yet also being fairly React centric.
  - If I had to guess you'll end up with Web Components + a Restful Entity Crud Api + MetaData.json
  - The documentation seems to be more hype than anything, I found it very hard reading

- ## Notion、WordPress 等有基于Block概念的编辑器。人们喜欢 Block。我们似乎标准化了一件事：插入新 Block 的 / 键。但是其他所有的内容都是完全专有且非标准的
- https://twitter.com/EryouHao/status/1486954447943057409
  - 如果在网络上的 Block 是可互换和可重复使用的，不是很酷吗？
  - 于是一个开放的、免费的、非专有的协议诞生了
- https://blockprotocol.org/
  - https://github.com/blockprotocol/blockprotocol
  - An open standard for building and using data-driven blocks. Make your applications both human and machine-readable.
  - Any valid HTML is already a block.

- 这个想法不错，block 最初是为了解决多人同时协作的时候的冲突问题。那以后文档就是按 block 作为基本组件了？
  - 是的。 甚至 Block 不仅应用于文档场景。例如一个纯粹的 Todo 应用也可以使用 Block 的协议来定义导入、导出、复制流转等，这样跨应用识别和适配就可能会不错。
  - WebDAV不就已经可以做到这个了吗？日历里的event和todo就是啊，结构化可协作分布式协议。有不少经验和教训在里面的。

- Gadget、Widget 换了个新名词叫 Block。

- 现在 block 们最讨厌、最影响写作体验的有两点：
  - 自动把一个段落（哪怕只有一个字）转成一个 block，不方便把一组段落设置为一个 block
  - 很难跨 block 选两句话，一跨 block 选择、就自动变成了选中两个 block
# discuss
- ## 

- ## 

- ## Anyone else sort of let down by Block Editor?_202006
- https://www.reddit.com/r/Wordpress/comments/fxatkr/anyone_else_sort_of_let_down_by_block_editor/
- I'm enjoying using the new block editor alongside ACF blocks when a section needs more customization.
- I think it's great for writing blog posts and other long-form content.
  - For page and general theme design, no, I'll stick to Elementor.
- Yeah I don't necessarily need Block Editor to show me exactly what every page will look like, but there also isn't much of anything for built-in control of how it looks.
- There are good and bad elements to Gutenberg:
  - It makes trying to build websites more difficult and time-consuming for amateurs and neighborhood hobbyists
  - It's wildly counterintuitive and clunky to say the least
  - Each new update is like using a new drag and drop builder
  - Design is clearly at the back seat to WordPress trying to build their own drag and drop builder that they believe will one day somehow compete with Wix/Weebly/Squarespace/Google Sites/Go Daddy's "Website Tonight" Generic template installer thing
- the biggest advantage of the blocks as I see it is the ability to nest them, but the 5.4 editor doesn't make that obvious or easy.
- Drag and drop kiddies still love their elementor but proper devs know better than to use 3rd party page builders. 
  - Most have adopted Gutenberg into their process or they're using ACF flexible content.
  - Me? Full on Gutenberg. Custom blocks for everything. Styling the editor is actually quite simple.
- I'm not sure WYSIWYG is a good idea, and I think the block editor is a pretty great illustration of where the concept falls short.
  - WYSIWYG is limiting, requires a massive amount of extra tooling and styles, and it never actually works because the presentation layer is not flat or static.
  - The better solution is to tell your stakeholders to fill out form fields with no styling, and to take care of that elsewhere.
- The book editor should have been something like elementor free.

- ## Has Your Opinion of the Block Editor Changed?_202009
- https://www.reddit.com/r/Wordpress/comments/im77i3/has_your_opinion_of_the_block_editor_changed/
- I love it. Hated it at first, but once I gave it a shot I'm sold. It's my go-to and I haven't touched the Classic Editor in quite some time. 
  - For starters, I'm a full stack developer, and I develop using plain text editors and no GUI-based IDE. 
  - I'm the exact demographic that should hate Gutenberg because it's not consistent with my normal workflow.
  - Gutenberg is the now, and the future. 
  - It absolutely should not be used like a page builder, but it is an incredibly effective way to manage basic content in an intuitive way and with the least amount of code bloat possible.
  - I hated Gutenberg at first, I'm sold. 
  - It's faster and more effective than formatting content from scratch
  - and it's easier and more intuitive for my clients to use and understand.
- I hated it at first but it’s pretty powerful stuff. 
  - Yeah I think the embed blocks are what have really sold me on it, especially the Twitter and Flickr ones.
- GenerateBlocks does wonders to make responsive layouts.
- It would be much better if they could add in character and paragraph editing: line-height, font size, etc.
- I like it. I forced myself to use it because it became standard.
- The block editor was first released to the public in June 2017.for nearly 5 years now
  - Yes, the early versions were very rough, but the ones that were released in both the plugin and in the release of WordPress 5.0 have always been extremely usable.

- ## 5M+ Wordpress sites use “Classic Editor” plugin_202102
- https://news.ycombinator.com/item?id=25647164
- We're now seeing over 235k posts a day made using the Gutenberg editor. 
  - The iOS and Android versions support the majority of the blocks now, and are being re-licensed using the MPL so they can be easily embedded and used by other apps.
- Gutenberg is a really robust and active project in its own right, separate from WordPress, and I hope that it becomes a cross-CMS standard.
  - If you've worked on any sort of editor, block system, page builder, etc Automattic are hiring very aggressively for senior JS positions. 
- Most WP visual editors / page builders are terrible. They produce bloated code, huge page sizes, poor SEO. Gutenberg does all this stuff right. But it doesn't try to be a full-fledged design environment either.

- https://news.ycombinator.com/item?id=15509383
- The block-based content is an idea that has been around for a long time and is embodied in several CMS's.
  - Concrete5, Craft, Wagtail, Kirby Builder, Lektor Flow Blocks, ACF/FCF, Wordpress Gutenberg
  - Concrete5 has them baked into its core, ExpressionEngine and Craft CMS have the "Matrix" fields, Wagtail has "Streamfields"
- there are **2 advantages** I've found to the block-based approach:
  - The editing interface can be custom-tailored to the content and the non-technical users who are editing the site via a GUI interface can be more "guided" through the data. 
    - E.g. a photo gallery can have repeating list of slides and each slide has separate image + caption fields. 
    - This is hard to do with a single WYSIWYG editor (Wordpress uses "shortcodes", for example, but those are a terrible UI for most non-technical users... the whole point of a GUI is to not have to use code)
- The front-end HTML+CSS markup can more easily be customized around the content fields. 
  - since each photo + caption of a slide is a discreet content field, I can insert that into any photo gallery markup I want. 
  - If the input data is itself HTML (as it would be from a WYSIWYG editor), I don't have that ability (unless I parse the HTML I guess, but that is terribly brittle and making a ton of assumptions about the generated HTML that will probably change depending on WYSIWYG widget version, where the content was pasted in from, etc).
