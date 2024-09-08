---
title: thread-ux-design-dev
tags: [thread, ux]
created: 2021-03-10T11:37:30.373Z
modified: 2021-03-10T11:38:16.053Z
---

# thread-ux-design-dev

# guide

- https://www.screensizes.app/
  - 各种Apple设备的信息与图片

- visual ui tips
  - [UI Design Tips by Jim Raptis](https://www.uidesign.tips/ui-tips)
    - 作者一直在twitter上更新设计案例和示例图
  - https://twitter.com/d__raptis

- design-tooling
  - https://colorbox.io/
    - 自动生成11阶色板、计算黑白的对比度
    - 基于hsb颜色模型探索颜色
    - [Introducing the new ColorBox](https://kvyn.medium.com/introducing-the-new-colorbox-e0109c021729)
    - [classic clolorbox](https://lyft-colorbox.herokuapp.com/)

- 《52 个设计原则》每个原则都有来源推到、案例解读、边界限制，由小红书产品设计中心制作，移动端和 PC 端体验都不错
  - https://rpdc.xiaohongshu.com/52-design-principles
# discuss
- ## 

- ## 

- ## Assisted password confirmation. Made with Tailwind and Framer Motion.
- https://x.com/wickedmishra/status/1831361580396884190
  - 输入确认密码时，显示匹配字符为绿色

- ## 今天从设计师朋友那学到了排版四原则：
- https://twitter.com/moeimiku/status/1768326203197555196
  1. **对比**：利用颜色、大小、形状差异，突出重点，抓住注意力。
  2. **对齐**：通过整齐排列，创造清晰的视觉流，增强内容的可读性。
  3. **重复**：统一元素（如颜色、形状），加强品牌识别，保持设计的协调性。
  4. **亲密性**：将相关内容彼此靠近，清晰展现信息结构，引导阅读流程。

- 之前学过些绘画，感觉原理都是相通的

- ## mobbin 对创业公司和独立开发者针对太友好了，相当于你 8 美元一个月找了一批大厂高薪设计师。
- https://twitter.com/huhuhang/status/1730407554344526264
  - 例如你想给产品加一个 Checkout 页面，可以快速看到主流产品的 Checkout 页面是怎么设计的，然后可以站在巨人的肩膀上向自己想要的效果进行改动。

- ## I design and code, so I used to browse dribble, and behance to take design inspiration, but now I use them very rarely, 
- https://twitter.com/sidi_jeddou_dev/status/1720022709789237512
- Instead I use twitter and:
  - https://layers.to
  - https://recent.design
  - https://darkmodedesign.com

- ## the simplest way to work out letter spacing
- https://twitter.com/aleksliving/status/1711725832757035098
  - 一黑板的函数曲线和公式

- ## 给自己的网站添加了一个鼠标轨迹的效果
- https://twitter.com/ArvinnWang/status/1710254783486210403
  - 很早之前用这个做过一个很简单的浏览器插件，用于屏幕共享时，鼠标轨迹便于查看。

- ## 如何处理圆角嵌套关系？
- https://twitter.com/i/bookmarks
  - 内部圆角 = 外部圆角 - Padding

- ## Today's “Garden” render is a nice one after a few not-so-good editions
- https://twitter.com/georgedoescode/status/1516802985317257220

- ## I am a freelance illustrator based in the SF Bay Area. I work in editorial, publishing, and motion. 
- https://twitter.com/mcmintea/status/1513917685972701185

- ## Is it just me, or are tabs for open files in code editors completely useless? 
- https://twitter.com/devongovett/status/1509659544850415626
  - Once you have more than a few open, it's impossible to find anything without ⌘P.
- I keep them open only for undo/redo history tbh.

- ## seriously, the ability to have multiple instances of web apps open simultaneously is the platform's superpower, and a main reason i avoid native apps. embrace it. 
- https://twitter.com/Rich_Harris/status/1511003723442671616
  - if middle-clicking something changes the URL but doesn't open a new tab in your web app you are Doing Web Dev Wrong
- It’s really too bad SharedWorker is deprecated. I had a prototype working with it and it was amazing
- The browser is the super app we've always needed.
- Always add a working url in an anchor tag. Also when you catch the click event for in page functionality (SPA). The href link will be opened in a new tab/window when the user performs shift-click or middle-click!

- ## motion one支持动画的logo设计灵感
- https://twitter.com/blaindy/status/1511132868474458116

- ## 推荐一个可定制的渐变SVG波形生成器SVG Wave，它可以为UI和网站设计生成很棒的 SVG 波形，支持自定义波浪的图层、颜色、波峰和高度等等
- https://twitter.com/Larry_LiDev/status/1500069732606967816
  - 可以导出SVG和PNG格式。
  - https://svgwave.in/

- ## Preferred storage format for looping algorithmic art collectibles: gif vs mp4 vs js-dynamic-live
- https://twitter.com/golan/status/1435909958202183683
- GIF for short loops, MP4 for longer or with more colors, JS only when generative (no need to run more CPU/GPU than needed for a loop)
- Having been burned by Shockwave, Java, and Flash, I’m not sure I trust JS to still work in (say) 10 years.
  - but Shockwave, Java, and Flash were never part of shared specifications. 
- I think compared to image formats like jpeg and mp4, code in general is brittle. But I think for storing on chain long-term, code makes a lot of sense. In addition to the parameters you outlined @golan , code is (typically) far less memory to store.
- Agree, I think the fear is for browsers to stop supporting an API, like say WEBGL1 for newer or because hardwares are changing

- ## When creating form fields, do you mark the required ones, or do you mark the optional ones?
- https://twitter.com/darianrosebrook/status/1433899512049795072
- I usually go with "depends on which is more prevalent in the current form". If 90% of the fields are required it is annoying to see 'required' on them, and vice versa. Also if all fields are required then don't show anything.
- I often have marked both. Adding “optional” to the text field default state copy. Definitely helps. But minimally mark required fields because I’m not a monster.

- ## For a SPA website with a drawer menu (doc site). When using the Android physical back button should it:
- https://twitter.com/sebastienlorber/status/1433424873955610639
  ➡️ 1) Close drawer AND navigate backward
  ➡️ 2) Close drawer AND prevent backward navigation
  ➡️ 3) Just navigate backward (drawer stays open)
- I really like number 2 but it seems like a workaround implementation.
  - It’s about  browser behavior. It’s ok if is a Android app, but it is’nt expected in web browser back button.
- Open or Close the drawer is the internal component’s action IMO, that’s why I choose the 1st answer 
  - 2 would also close it, so why 1 and not 2?
  - Ok, I mean whether it will close or not doesn’t matter to me Smiling face with open mouth and smiling eyes I’m focusing on whether it will navigate back or not

- ## I think Skeleton Screens are often not the best UX. 
- https://twitter.com/samselikoff/status/1407125948567334913?s=21
  - Most React frameworks optimize for them but (a) they require a ton of extra engineering effort and (b) I'd prefer nice loading spinners here. 
  - Fewer UI states to mentally distinguish.
- The bit you said about it being an extra cognitive load is so true - hadn’t thought of it that way before but it makes sense!

- ## Do you wish the entire extended color palette was enabled by default or is that too much selection, making it hard to actually benefit from the constraints?
- https://twitter.com/adamwathan/status/1430203942173126660
- The ideal solution, IMHO, would be leaving the choice to the developer who'll use it. Separate packages? Installation flags?
  - It already is up to the developer, you can set up whatever color palette you want in your config. This is just about the defaults.
- With JIT, enabling all colors is the first thing I always do.
- With JIT having the extended colors doesn't bug me much. 
  - But having all the different grays does. It'll be "annoying" for auto-completion alone because they'd all have "gray" in the name. 
  - Also typing "text-" is gonna suggest a bazillion new classes
- with JIT I feel like restricting the color palette arbitrarily makes no sense
- Sounds like enabling all colors will increase CDN build size, but will also reduce your customer support load.
  - I vote enable all. The time it takes for site visitors to download and cache the new CDN build is very small, but the time it saves for your team is meaningful.
- It feels like enabling all would actually harm some of Tailwinds benefits.
- Honestly, I rarely enable all for every projects. There always a fews that are used more regularly than others. In my case is gray and its variants.

- ## UX tip: ever you need to truncate text, add the full text to the title tag so user will be able to read full text
- https://twitter.com/renatorib_/status/1418275875779485701
  - But you will need to find another solution for mobile.
  - 利用title属性添加鼠标悬停提示

- ## When dealing with dates in a dashboard, would you like to see that in a human-readable language like "Created 5 hours ago" or just as a regular date format like "19/07/2021 04:09:03, 791"?
- https://twitter.com/bruno__quaresma/status/1417127583632740355
- In this scenario, I’d prefer “Created 5 hours ago”, just like Twitter, it shows the hours only.
- Think Excel dates formatted as a number
- Personally I prefer to see the date rather than the relative time.
  - It especially drives me crazy on GitHub when trying to debug an issue where I know the precise day and time when the issue was introduced but the commit time is listed as "last month".
- I'd say human readable only within "current day" and then more precise format after.
- I love the human readable, and always use this format!
  - It makes sorting a little weird though.  Just make sure if you're using a datatable or something that you don't end up sorting it alphabetically (as you'll need to sort with the unformatted date)
- Depends on the context. Human readable dates with full date-time on the tooltip is a better approach, IMO.
- Human readable with full datetime on hover 

- ## How To Design Better Shadows 
- https://twitter.com/d__raptis/status/1410268576775344135
1. Add more blur to make your shadow look smoother
2. Offset the shadow on the Y-axis
3. Reduce the opacity
4. Reduce spread to make the shadow look like it's created by a smaller element
- Bonus:
  - Add a subtle light gray border when both the background & card are white

- ## I wonder if any user research has been done about trash cans vs ⛔️ icons vs `X` to signify "delete this item". 
- https://twitter.com/LeaVerou/status/1410207899633209351
- [Removing an item from a list: Trashcan Icon vs X](https://ux.stackexchange.com/questions/98238/)
- The "+" and "-" can be confused with "expanding" and "collapsing". 
  - That's why I prefer the trash can to signal a deletion. And a floppy disk for saving! 
- I don't have any documentation, but in my head the bin/trash stores deleted items, it's not usually an actionable item. 
  - The minus and X are more direct actions. X is also more commonly used for Close, rather than Delete.

- ## Here's how I'll determine whether you read a blog post. 
- https://twitter.com/kentcdodds/status/1401011415666675713
  - The backend will only actually record it if it's been over a week since the last time you read it (yes, you'll get credit for reading it multiple times).
- Will the visibility events on tab/window changes?

- ## Then it's a good practice to place your CTA at the end of this flow to lead users to take action.
- https://twitter.com/d__raptis/status/1397209106218463237
  - It states that the user's eyes travel according to a `Z-shaped` path from the top-left area to the bottom-right area. 
  - Gutenberg Principle (aka Z-Pattern Layout)

- ## Landing Page Teardown
- https://twitter.com/d__raptis/status/1395378798661615619
- Choose visuals that demonstrate your product's value over pure screenshots.
- Promote use cases over features!
- Use clear pricing tables
- Boost your SEO game by showcasing your best pages

- ## Better Image Overlays
- https://twitter.com/d__raptis/status/1392511897589669891
  - Avoid plain text over images. Use fading gradient overlays to strengthen the contrast instead. 
  - Use black gradient & white text (or other high contrast combos) to make sure that the text is visible regardless of the background colors.

- ## UX pattern question: I've got 5-ish categories. Each can be "true", "false", or "off". Is there a good input type
- https://twitter.com/acemarke/status/1389679142405279752
- What is the difference between false and off?
  - "Off": no filter applied for this category
  - "True/False": filter applied, matching that value
- Radio inputs with labels can be styled to look like a button group. Bootstrap utilizes this and it nicely works with keyboard navigation.

- ## Trying to write the most terse theme preference check to insert at the top of the document head. Order or precedence being:
- https://twitter.com/michaeltaranto/status/1389062386691104775
  - Site preference
  - OS preference
  - Fallback to light mode with neither
  - Fallback to light mode with no JS.
  - Tell me where I'm wrong 
- how would you handle preference set by a backend API?
- Reading this Tweet though I'm thinking maybe I should split the script in two, one for reading inline, and the other for modification.
  - Yeah I'd definitely suggest decoupling the two. One is on the hot path for rendering, the other is a bit more of an edge case right?
  - Yeah, if any of the modification code can be extracted it would be better to load it the same way as the rest of the JS on the page. Only reading code has to be inlined. Hopefully it doesn’t complicate setup and usage too much to split them.

- ## The most requested feature of the year is here—announcing Auto Size 
- https://twitter.com/framer/status/1387783277390573572
  - 主要是卡片大小会随文字变多而变长变宽
  - 折叠展开的动画会显示背景变短变长的过程
  - And it works dynamically on everything from text to interactions. Design expanding accordions, dropdowns, buttons, and more.
- [Auto Size](https://www.framer.com/updates/2021-04-29/)

- ## 687 plugins! Really? We might need some form of categorizing system to group them all in order to simplify "browsing".
- https://twitter.com/klaskarlsson/status/1386279983023284228
- A plugin’s plugins plugin.
- Not so sure that is a good idea if tags are more than plugins.
- I've been pretty happy just using the search, which is super fast and will match any words in the plugin description as well as the title.

- ## Skeleton loaders (supposedly) make your app feel faster, but am I the only one that feels like *animated* skeleton loaders make it feel even slower?
- https://twitter.com/markdalgleish/status/1386618622181724161
  - 很多观点认为，骨架屏让用户感觉速度变慢了，不值得做
- If you have large animated areas they will require your attention. When you pay attention to something while you wait, it will feel slower.
  - The whole idea of skeleton loaders is to reduce motion on the page.
- Most of my friends refresh as soon as they see them because they think something broke on the page 

- ## I wrote a few words about why design files are disposable artefacts and code is the source of truth.
- https://twitter.com/petermcreaper/status/1384280996548255747
- The people who use our apps and websites will never see our beloved design files. 
  - The only thing that actually matters is the code that gets shipped to production — because that is what our users will see and experience.
- A better way to think about our design files is as artefacts that we use to communicate our design intent. 

- ## Should pure selection changes be part of an app's undo/redo stack?
- https://twitter.com/steveruizok/status/1382660618361143296
- I think Photoshop does it because a selection is a complex shape that can be modified. 
  - But on programs where it‘s just a collection of items 
  - I think the majority avoids it being a part of the history.
- No. They are an edge case for me. For that time I'm SHIFT - selecting a bunch of layers and make a mistake. All else, selection is annoying in the undo-stack.
  - It's also confusing to me. My brain assumes layer states in the undo-stack. Having selection states as well, makes intuitive undo-ing impossible.
- Personally don’t like it, I never want to redo/undo a selection, always an actual change. Which means that if I selected things in between changes it then « pollutes » the changes thread

- ## When it comes to Dark Mode, my strategy has always been to manually create a second set of colors. 
- https://twitter.com/JoshWComeau/status/1380549061204439042
  - This wonderful blog post by @LeaVerou shows how we can derive the palette automatically using CSS variables and LCH colors
- [Dark mode in 5 minutes, with inverted lightness variables](https://lea.verou.me/2021/03/inverted-lightness-variables/)
- The problem with HSL
  - The root cause is that HSL lightness does not actually correspond to what humans perceive as lightness, and the same lightness difference can produce vastly different perceptual differences.
- LCH is a much better color space for this technique, because its lightness actually means something, not just across different lightnesses of the same color, but across different hues and chromas.

- ## What are all of your favourite features of design system docs sites?
- https://twitter.com/colmtuite/status/1379570553674170368
- props configurator with copy code button
  - all variants shown
  - guidelines (with examples in context) for both devs and designers
  - search
- Interactive demo
  - Props configurator 
  - Related components section that highlights the distinction and when to use one vs the other.
- checklist that reflects component status
  - release notes 
  - an easy way to edit/add docs
  - design data mapping
- Code examples & copy buttons
- Let’s be serious we all only care about the pretty grid of color swatches.
- Show me variants and states and let me toggle stuff on and off. 
  - Showing all the stuff is probably better, but sometimes not feasible if there’s too much. 
- Drag n drop builder mode
- the material design guidelines for where and how to use (and also how to extend/customize) components still beats all of the design systems docs out there.  the ultimate benchmark I believe. the case studies are all just gems.

- ## Design system tip: if you have opaque backgrounds/borders on UI components, use mix-blend-mode: multiply, so they work on different coloured backgrounds.
- https://twitter.com/colmtuite/status/1377968794434428929
- I have always struggled with this concept. How do you ensure contrast ratios for accessibility? My color system is contrast based. So I can recommend a lighter color within the same hue to put on top of it rather than allow opacity which could drastically shift based on context
- Our color system is designed for specific, but extremely common, use cases.
  - So 300–500 are designed for interactive backgrounds, like hover, active, selected, and highlighted states.
  - 200 is designed for static backgrounds, and 300–500 are guaranteed to work well on top.
- What do you do for dark mode?
  - You could try mix-blend-mode: difference, or use alpha transparency instead, or a few different things.
- This is what I've been looking for to use instead of postcss color functions. Gotta give a try!
- I think rgba works too
  - Yep, but then they wouldn't be opaque.
  - I mean... technically yes? but functionally they're not opaque if you're using a blend mode

- ## Destructive actions should be cancellable (even better, they should be undoable).
- https://twitter.com/fortysevenfx/status/1376253883417251843
- I think I’d prefer a “are you sure” modal to instantly click instead of the wait here
- Do you know how it's implemented? Only in front and if you close window you don't delete or in back and the timer is synchronized with front? I'm never sure how make it and generally choose to 2 times validations (delete → are you sure ?) for deleting
  - So far I implemented only the timer on the front-end (React hook), which delays the destructive action, leaving time for the user to change their mind, but without interrupting their workflow with a modal if they actually intended to perform this action.

- ## indiebrands.io now features mockups auto-generated for each brand.
- https://twitter.com/lauridskern/status/1370787677021347843
  - https://indiebrands.io/

- ## Development foreshadows the future of product design. Trend: How devs work now is how designers will work in 3-5 years. 
- https://twitter.com/domyen/status/1370515481979985924
  - Here's a thread about how dev can change design
  - Variables » Design tokens 
  - Components » Components 
  - UI states » Variants
  - Design primitives are established. 
  - Design is more creative yet more homogenous(同质的). 

- ## Pro-tip for UI developers: always assume that your users will rage-click any of your buttons multiple times out of frustration. Program accordingly.
- https://twitter.com/DavidKPiano/status/1370083861472935942
  - Instead of disabling buttons, you can explicitly model your state and transitions so that rage-clicks and other edge-cases are handled correctly. Let your users rage against the state machine.
- and not only for UI developers, a rage-clicker caused a massive outage in one of my previous jobs.
- Specially gamers
- I like the confidence a state machine gives you here: you can click all you want, but you’ve already transitioned to a different state and there’s way less chance something unexpected will happen.
- Always give feedback

- ## Avoid round checkboxes. 
- https://twitter.com/argyleink/status/1329230409784291328
  - They make a radio list confusing by allowing multiple selection! 
  - Round the corners of your checkboxes all day, but be weary of the misleading effect a round checkbox can have
- Who does not know that checkboxes are used for multiselection and radio buttons are used for unique selection. I had a pretty long discussion with our designer a while a ago.
- I recently did some small research on this topic and LOTS of Android and IOs apps uses the round checkboxes for no reason: Gmail, Outlook, Drive, One Drive... To name a few.

- ## Floating field labels are bad for accessibility! Don’t use them just because Google does.
- https://twitter.com/devongovett/status/1364577800116711424

- ## Quick tip: don't use a datepicker on date of birth fields. That's dumb.
- https://twitter.com/brad_frost/status/1362771518137249794
- Working with localization, I would say that it’s not dumb at all. 
  - Lots of people fill out in wrong order since they have different format for the date.
- Why do date pickers for birth dates always start on the most granular level (days)?  
  - Why not show a grid of years (easy to scroll) > select month > select day? 🤔 
  - Date pickers are a super powerful UI component, but are rarely implemented correctly

- ## How we built a profile card generator for Storybook
- https://storybook.js.org/blog/generative-image-service/
- No dev blog is complete without custom auto-generated social images

- ## If you are wanting to reference a tweet on a page, don't embed, just use a simple image + alt text + link.
- https://twitter.com/TheRealNooshu/status/1350578919389470721
- Just a note that https://tweetcyborg.com converts a tweet to a simple image for you. 
  - No idea if this is the best service to do it, but it works
- What about inlining a copy of the tweet, with minimum styles, like I did here for example?
  - I’m using this plugin for @eleven_ty , if it can be an inspiration
- I've found exactly the same thing. 
  - Twitter's embedding is very inefficient. 
  - I'm still trying to find something which will turn it into an image + alt text + link automagically. 
