---
title: lib-editor-codemirror-community-compatibility
tags: [codemirror, community, compatibility]
created: 2024-08-11T06:40:25.390Z
modified: 2024-08-11T06:40:41.476Z
---

# lib-editor-codemirror-community-compatibility

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-input-ime
- ## 

- ## 

- ## 

- ## 💡 [Replace chinese character with other input, someting strange - v6 - discuss. CodeMirror _202405](https://discuss.codemirror.net/t/replace-chinese-character-with-other-input-someting-strange/8265)
- I suspect the Chinese input method uses composition in this case. Unfortunately, browsers do odd buggy things if you interfere with the text around the cursor during composition, including duplicating text.
  - Your options are to not respond to composition-based input (for example by checking `tr.isUserEvent("input.type.compose")` ), or to set things so that the replacement happens after composition finishes (in a view plugin listening to `compositionend` events).

- ## ❓ [EditorView compositionend state  _202302](https://github.com/codemirror/dev/issues/1069)
  - I use codemirror in a react component, and want to trigger props.onChange when code changes
  - when use IME, I want to trigger onChange only when composition end, how can I konw this state.

- Indeed,  `view.compositing` is still true when the last change the the composition is applied. You could set a timeout when composing changes come in, to flush them when view.composing is false, maybe?

- ## [Replace chinese character with other input, someting strange _202405](https://discuss.codemirror.net/t/replace-chinese-character-with-other-input-someting-strange/8265)
- I suspect the Chinese input method uses composition in this case. Unfortunately, browsers do odd buggy things if you interfere with the text around the cursor during composition, including duplicating text.
  - Your options are to not respond to composition-based input (for example by checking `tr.isUserEvent("input.type.compose")` ) , or to set things so that the replacement happens after composition finishes (in a view plugin listening to compositionend events).

- ## 🐛 [codemirror/view 6.28.2 version will cause abnormal input of Chinese input method _202406](https://github.com/codemirror/dev/issues/1396)
- 
- 

- ## [Mac OS native chinese IME, prompt pos not right _202407](https://github.com/codemirror/dev/issues/1409)
  - 只有中文输入法的S键会触发，其他按键不会触发
- This is a Chrome issue, which I've already reported here, but so far no competent person seems to have picked it up. Sometimes multiple pressing the +1 button on that issue page (might require logging in) helps getting attention to it.

- [EditContext displays the IME interface in the wrong place for IME at the start of a line [351029417] - Chromium](https://issues.chromium.org/issues/351029417)
# discuss
- ## 

- ## 

- ## [Experimental support for EditContext - discuss. CodeMirror _202404](https://discuss.codemirror.net/t/experimental-support-for-editcontext/8144)
  - Chrome has started shipping edit context, a feature that allows JavaScript to intercept editing actions, including composition-based ones, in a way that isn’t as problematic as the old ‘just see how the DOM changes and hope for the best’ approach. 
  - Mozilla is considering the proposal but hasn’t put out a position yet. 
  - Apple is responding with deafening silence as usual.
  - I’m generally a bit wary of Blink-only APIs, but since this may help tame the endless mess of virtual keyboard behavior on Andoid, I built a proof-of-concept implementation that uses this feature, when available, to capture text input. The interface was surprisingly pleasant to use, and fits into CodeMirror rather well. 
  - @codemirror/view 6.28.0 ships with EditContext support. I’ve disabled EditContext use by default in 6.28.1 again until I work those out.

- ## 才知道 pointermove 事件会按照屏幕刷新率，合并手写笔/鼠标的输入事件。
- https://x.com/zQwQs/status/1822331239740666306
  - 需要通过 `event.getCoalescedEvents()` 捞出来那些被隐藏的事件。

- ## 💡 [Focus behavior issue - Editor doesn't lose focus when you click above it - discuss. CodeMirror _202407](https://discuss.codemirror.net/t/focus-behavior-issue-editor-doesnt-lose-focus-when-you-click-above-it/8468)
- Is this in Chrome? That browser has some weird behavior around what focus does when clicking near editable content. You’ll see the same with a plain `contentEditable` div. There’s not a lot CodeMirror can do about this, without aggressively interfering with the browser’s focus behavior.
- Yes it is in Chrome, I checked in Firefox and it works fine, but I could not reproduce it with a plain `contenteditable` div that I tested in Chrome
  - Likely some of the styles or wrapper elements we use influence the behavior. I’m not invested enough in this to try and isolate which, but you could try if you have the time.
- 💡 I found out that to ensure proper flex child behavior for the editor content, such as flex-grow and flex-shrink, you need to encapsulate the contenteditable element within an additional div. This approach appears to resolve the focusing and blurring issues of contenteditable elements when they are direct children of a flex container in Chrome browsers.

- ## 🤔 [Backwards compatibility of codemirror6 - JupyterLab - Jupyter Community Forum _202402](https://discourse.jupyter.org/t/backwards-compatibility-of-codemirror6/23851)
- I was just wondering if anyone could tell me if codemirror6 is backwards compatible with JupyterLab3 or will it only work with JupyterLab4?
  - In core, it will only work with JupyterLab 4. It’s possible someone could write an extension that would replace some renderers with codemirror 6 (e.g. notebook cell inputs), but likely not all of them (e.g. settings editor).
  - 💡 There was an attempt to generalize the `ICodeEditor` to allow alternate implementations (e.g. to support monaco integration), but this never really worked out, and supporting two versions of the same library is particularly challenging when the breaking changes are almost total.
