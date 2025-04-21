---
title: lib-editor-codemirror-community-virtualized
tags: [codemirror, community, virtualized]
created: 2023-11-30T06:56:07.608Z
modified: 2023-11-30T06:56:24.809Z
---

# lib-editor-codemirror-community-virtualized

# guide
- pros
  - fast render for large document
  - fast render for mobile

- cons
  - in-page search 不能直接使用浏览器提供的能力
  - scroll into view如锚点滚动需要自定义实现，因为可能不在可见范围
  - 影响现有的第三方组件，如scrollbar、(syntax)highlighting
# discuss-stars
- ## 

- ## 

- ## [Content Height changes on scroll with line wrapping - discuss. CodeMirror _202403](https://discuss.codemirror.net/t/content-height-changes-on-scroll-with-line-wrapping/8008)
  - The challenge is this custom scrollbar expects to know the total height up front
- Eagerly rendering the entire document is not something the editor supports—it’d go against all the effort I’ve made to make the system fast regardless of document size. 
  - You’ll have to listen to updates with the `heightChanged` flag and adjust your scrollbar content to sync with the newly measured heights.

- ## [Horizontal scrollbar resize issue - v6 - discuss. CodeMirror _202206](https://discuss.codemirror.net/t/horizontal-scrollbar-resize-issue/4592/2)
  - Horizontal scrollbar is resizing when scrolling along document document.
  - 现象: 鼠标拖动竖直方向滚动条时，水平滚动条的宽度也在变化
  - If I get it right, the issue comes from the “viewport” as CM is rendering only a slice of the document.
  - do you think would it be possible to “enforce” the width of the “cm-scroll” element to prevent this issue ?

- The patch below should help. You won’t get the proper scroll width until the first time you scroll the widest line into view, but once you do, it should remain stable.

- ## 🤔 [How to disable virtual scroll in code mirror - discuss. CodeMirror _202406](https://discuss.codemirror.net/t/how-to-disable-virtual-scroll-in-code-mirror/8339)
- There isn’t. (And there won’t be. The performance would be terrible on larger documents.)

- ## [Improve Scroll / Performance tradeoff - v6 - discuss. CodeMirror _202411](https://discuss.codemirror.net/t/improve-scroll-performance-tradeoff/8825)
  - Is there a way to customize or disable this behaviour? For example if I scroll fast on a large file there would often be frames with no lines rendered / scrollbar behaving eradically as a result.
- No, there’s no way to change this. The system’s performance is designed about the viewport being of limited size, and making it bigger would make the editor less responsive.

- ## 💡 [Dynamic line height - discuss. CodeMirror _202106](https://discuss.codemirror.net/t/dynamic-line-height/3257)
  - I have a decorations Facet that sets the line height based on a StateField using attributes
  - This works fine while the editor contents are in view. But once I scroll the content out of view, the “artificially increased” line height is not taken into account, and so the content jumps up.
  - How can I solve it? 
  - I can’t use a block widget, because I need the line itself to have the given height. Can I hook into codemirror’s line height calculation to let the editor know that some lines are different height?

- The height of out-of-view content is modeled by the view’s internal “height map” structure, which understands widgets with estimated heights but not explicitly set heights on lines. What exactly are you implementing here? Would it be a good match for block widgets?

- Spending some more time on this problem, I think the only way to get a bulletproof solution with the current “smart” layout I have (where the two editors can take different width based on their content), is to disable the viewport optimization. I read the Codemirror code, and I can’t really see how that can be done. @marijn any ideas on how I could disable the viewport and force Codemirror to render all content? 
  - 👷 That’s not something that CodeMirror 6 currently supports, and a lot of complexity analysis in the system assumes a limited-size viewport, meaning that you’re quite likely to hit performance cliffs when working with even medium-sized (say, a few thousand lines) documents if you were to somehow disable this. So I’m not too keen on adding this option, knowing that people will turn it off and then ask for support when it messes up their user experience.
- I forked codemirror/view to hata6502/codemirror-view , and disabled viewport.
  - Disabling viewport may occur the performance issue, but it resolves the following scroll problem.
# discuss-codemirror
- ## 

- ## 

- ## 

- ## ⚡️ [Possible performance enhancement for very long rows - v5 _202208](https://discuss.codemirror.net/t/possible-performance-enhancement-for-very-long-rows/4897)
  - If one were to change this to use such a “windowing” solution to ultimately improve the performance, one would wrap every character into a div too. The one thing that makes this Codemirror such a perfect candidate for this solution is that it works with characters. Each character is roughly the same width (look at VS Code for instance) and height, and so calculations to achieve windowing would not be that expensive.

- Is something like this in Version 6?
  - Yes. And it’s not going to be implemented in version 5, since it would be complicated and invasive(侵袭的, 扩散的) to retrofit(更新；改型；改装).

- ## 🤔 [Overlay scrollbars in CM6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/overlay-scrollbars-in-cm6/4644)
- Content in CM6 is virtualized so I’m not sure how third party scrollbars libraries would go.

- ## [editor lines out of sync in merge view - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/editor-lines-out-of-sync-in-merge-view/7138)
- I managed to reproduce it now (it only showed up for me when I scrolled back up from the bottom). This patch overhauls how spacers are handled, and seems to help

- ## [how does codemirror stay so fast even on thousands of lines of code _20231130](https://twitter.com/RogersKonnor/status/1730043499850977383)
  - TIL it actually virtualizes the viewable nodes. Well, that makes sense, also not looking forward to virtualized scrolling in `<light-editor>` ...
  - I'll probably have to find a way to virtualize the syntax highlighting for `<light-editor>` to not tank performance

# discuss-virtualized
- ## 

- ## 

- ## [Preventing Widget deletion - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/preventing-widget-deletion/7002)
  - I have a widget which adds a Google Maps embedding. The problem is that when I scroll below and the map goes out of the viewport, the DOM node gets deleted, and recreated when back in view so the zoom level I set is gone.
  - Is there any way to prevent widgets of a certain widget type from getting deleted?

- No. Content outside of the viewport is removed from the DOM. You may, if the maps widget can handle being detached and reattached, be able to set up something like a caching layer where you reuse the same rendered DOM on a re-render, but the editor itself won’t keep out-of-view content in the DOM.

- ## 📝🏘️ [Slate – A completely customizable framework for building rich text editors | Hacker News _202107](https://news.ycombinator.com/item?id=28000086)
- The recent changes to the API in 0.50 look good. The number of iteration passes really shows. Out of the available open source editor frameworks, 🆚️ Slate is probably most similar to Notion’s internal editor system. If I had to rebuild on a framework tomorrow, it’d be Slate or ProseMirror. Still if I used Slate it would be with the expectation that I’d end up owning an aging fork of a forgotten version at some point.
- I've been using Slate heavily this year. I'm not a Slate developer, but I've read a lot of the source code, follow all the Github issues, etc., and I'm "owning an aging fork".
  - I ended up forking only the React part of Slate, which is officially a plugin, and massively rewriting it to support virtualized windowing, so we can work with very large possibly complicated to render documents. I also added fairly generic realtime collaboration support. This is currently used in https://cocalc.com for WYSIWYG editing of Markdown documents. I also have plans to extend my use of Slate with windowing to Jupyter notebooks and other document types.
  - I chose Slate over Prosemirror because the source code of Slate is Typescript written in a clear modern style, and I was able to start reading any part of it and understand it easily, whereas I find Prosemirror's core source code more difficult (this may just be a reflection of my shortcomings). I spent a lot of time initially just reading Slate PR's claiming to fix bugs, then integrating the PR's into my fork, often in a way that makes sense for my project, but likely wouldn't in general (I left helpful remarks on Github).
  - I have no plans to switch from Slate to Prosemirror. Getting virtualized windowing to work with Slate was quite difficult, but it's really table stakes for what I plan on doing longterm, and I don't even know where to begin to do virtualized windowing in Prosemirror.

- How does virtualization play with text search? Did you end up having to roll your own?
  - Yes, I very much have to implement my own text search. There are many custom elements, so I would have to roll my own anyways at some point.

- What features of Slate put it closest to Notion's editor compared to other frameworks besides the obvious one that Slate's view layer is built on top of React? Is it somehow that Slate is more suitable handling asynchronous data (e.g. server generated uuids for each block, recursively fetching content for each block and its children)?
