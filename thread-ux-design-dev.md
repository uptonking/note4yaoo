---
title: thread-ux-design-dev
tags: [thread, ux]
created: '2021-03-10T11:37:30.373Z'
modified: '2021-03-10T11:38:16.053Z'
---

# thread-ux-design-dev

# guide

- https://www.screensizes.app/
  - 各种Apple设备的信息与图片

- visual ui tips
  - https://twitter.com/d__raptis

- design-tooling
  - https://colorbox.io/
    - 自动生成11阶色板、计算黑白的对比度
    - 基于hsb颜色模型探索颜色
    - [Introducing the new ColorBox](https://kvyn.medium.com/introducing-the-new-colorbox-e0109c021729)
    - [classic clolorbox](https://lyft-colorbox.herokuapp.com/)
# pieces
- ## 

- ## 

- ## 

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
