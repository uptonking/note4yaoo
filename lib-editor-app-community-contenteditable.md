---
title: lib-editor-app-community-contenteditable
tags: [community, contenteditable, editor]
created: 2023-06-16T02:52:41.895Z
modified: 2023-06-16T02:53:00.115Z
---

# lib-editor-app-community-contenteditable

# guide

- textarea的缺点
  - textarea中回车换行后元素高度不会自动增加，可能会出现滚动条，但contenteditable会自动增加高度
  - 不支持格式化文本如bold/italic
  - 不支持插入图片等非文本元素
  - getSelection() doesn't work on the content of `<textarea>` and `<input>` elements in Firefox, Edge (Legacy) and Internet Explorer
# discuss-selection-caret
- ## 

- ## 

- ## 🌰 How I built this cursor
- https://twitter.com/moonriseTK/status/1714542054498603090
  - The green one is the selection, the black is hover haha. Probably unclear in the video, mb. 
  - The first bit is just being able to figure out the closest caret position based on the mouse position. You can do this using a semi-obscure DOM api called `caretPositionFromPoint` .
  - Then you can set up a mouse-move listener and render where your caret would land based on the mouse coords. You'll probably want to use a signals based library; going through React's runtime can be too slow for this.
  - We don't want to show the mouse caret *and* the preview caret at the same time, so we toggle showing the mouse cursor within a certain distance (exaggerated the threshold here, you want it to be about the length of a char)
  - Another thing we can do is preview the marks of the preview caret position e.g. make it wider for bold or slanted for italic. With prosemirror, you can do this using the `posAtCoords` api, resolving the pos, and getting the marks.
  - The last part is just adding a linear interpolation (lerp) between the caret preview and mouse cursor so it doesn't feel quite as rigid, and you end up with the demo.
  - One other detail: updating the cursor using divs and mousemove is about 2-3 ms behind than if you use the css cursor attribute. So use the browser cursor when the mouse is far away, then set cursor: none when nearby
- Why do I think this is a good user experience? 
  - Default text cursors don't provide any feedback about where your caret is going to land or what styles the text has. It's also just ugly; the cursor obscures the text right where your eyes are.
  - Apple realized this too and they have a fantastic WWDC video talking about how they redesigned the iPadOS pointer interactions from scratch.
- Are there any edge cases to this, apart from browser support for the DOM API methods? Does it work on mobile? 
  - 本示例适合在桌面端通过键盘移动光标的效果，不适合移动端
  - This thread is about the hover caret preview so it’s not applicable really. One thing i’ve noticed is that it doesn’t really work for empty paragraphs (probably bc of how PM shows them). Another annoying thing I will have to deal with at some point is that paragraphs have spacing between them and clicking on that empty margin goes to the front of the paragraph rather than the actual nearest caret position. This is super annoying and every editor is like this but idk if theres anyway to extend the editable region except lineheight
- this fancy design remind me of another great job from bike editor
  - Yeah! This was another approach I saw, altho its for the selection caret. I just show the formatting of the stored marks for the anchor caret (so wider if bold, slanted if italic, etc)

# discuss-textarea
- ## 

- ## 

- ## Anyone have any good resources on making your own contenteditable plaintext editor?
- https://x.com/RogersKonnor/status/1841179945848225884
- If it’s plaintext why does it need to be contenteditable at all? IMO a great way to do plaintext editors is to use a simple textarea. If you need syntax highlighting with colors, consider overlaying a copy of the text on top of the text area where you control the colors.
  - It falls apart at like 2k+ lines. I need to profile it and figure out whats causing the slowdown. Its not `<textarea>` itself. Cant tell if its layout thrashing or all the calls to Prism and if i need to throttle it
- re:
  1. I think Prism is too heavy for this use case.
  2. Doing virtual rendering to only render the “visual” code should help with the perf a lot.
  3. Probably will need a new kind of parser that can parse partial code well.
- I was hoping to avoid that... I guess trying to make contenteditable work with virtualization is probably asking for even more trouble than just using what I have already.

- Did you try content-visibility to see if that helps performance?
  - I believe I did, but I didnt know notice a difference.

- Yeah I would guess the bottleneck is the prism back and forth. Have you tried tree-sitter?
  - treesitter goes against the whole ethos of being a small library on top of `<textarea>`. I may look at "lezer" which powers codemirror to get incremental parsing.
  - and needing to compile individual grammars and use WASM is not my idea of fun

- A client of mine did this and regrets it. They moved to Monaco editor.

- The legitimate answer I've seen is don't. Perhaps https://developer.mozilla.org/en-US/docs/Web/API/EditContext_API is a better place to look but alas it's chromium only ATM. I'm not sure if Mozilla and WebKit are opposed or just haven't prioritised yet.

- ## ✨ TIL about `field-sizing: content` in css， chrome默认启用
- https://x.com/destroytoday/status/1835405977316655563
  - 支持自动增加高度为内容高度
  - it’s on by default on Chrome vs behind a flag. I read a post that said Safari committed to implement it
  - firefox probably never will lol... i hate firefox so much

# discuss
- ## 

- ## 

- ## [Ask HN: Why is working with contenteditable is so hard? | Hacker News _202409](https://news.ycombinator.com/item?id=41462298)
- Because different browsers insert the content in a different fashions. The reliable way to use contenteditable is to intercept keypresses and modify the inner HTML yourself, i.e. use contenteditable only to use the cursor affordance.

- ## [Rich text editors and rendering engines | Hacker News_202307](https://news.ycombinator.com/item?id=36600434)

- ## [What are the cons of using a contentEditable div rather than a textarea? - Stack Overflow](https://stackoverflow.com/questions/5284193/what-are-the-cons-of-using-a-contenteditable-div-rather-than-a-textarea)
- contenteditable="true". 
  - The major benefit is it has **auto-adjust height** as user input text/content. 
  - Also it supports rich text inside. You can mimic the Textarea by setting a max height if need.
- if you want auto height in Textarea, you might have to use js to bind some listener to the oninput hook.
  - `textarea` 不会自动调整高度，不支持文字格式

- First semantically, the purpose of a textarea is to write/edit plain text whereas with contentEditable you can edit list for instance

- In divs with contenteditable="true" the content can be html formatted, e.g. text with different colors.
- 
