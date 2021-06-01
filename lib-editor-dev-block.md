---
title: lib-editor-dev-block
tags: [editor]
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

- cons
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
- 
- 

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
