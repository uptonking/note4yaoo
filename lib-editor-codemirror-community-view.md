---
title: lib-editor-codemirror-community-view
tags: [codemirror, community, view-layer]
created: 2024-08-08T20:48:58.188Z
modified: 2024-08-08T20:49:11.571Z
---

# lib-editor-codemirror-community-view

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## experimenting with a canvas-driven CodeMirror cursor
- https://x.com/hamiltonulmer/status/1822274427142525210
  - will need to try a gradient polygon rather than a trail of thin lines

- the long-awaited feature for every rich text editor

- https://x.com/hamiltonulmer/status/1822120260910383419
  - thinking about experimenting with a canvas-driven layer for CodeMirror (for cursors and selections, not text). 
  - Goal would be to enable richer animations not achievable with css e.g. show cursor motion blur when jumping around
# discuss-coding-ai
- ## 

- ## 

- ## [Render autocomplete outside of editor container - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/render-autocomplete-outside-of-editor-container/7283)
- You can configure tooltips() to do this, but that will affect all tooltips.

- ## [unwanted element appear when using Decoration.replace - v6 - discuss. CodeMirror _202302](https://discuss.codemirror.net/t/unwanted-element-appear-when-using-decoration-replace/5681)
- Emitting clean HTML for use in other contexts is not something the editor will do for you.

- ## [why with codemirror6 @codemirror/autocomplete auto create hidden img? - discuss. CodeMirror _202304](https://discuss.codemirror.net/t/why-with-codemirror6-codemirror-autocomplete-auto-create-hidden-img/6173)
- This avoids a number of browser bugs caused by editing next to uneditable elements such as widgets.

- [Hiding widget buffers for better text wrapping - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/hiding-widget-buffers-for-better-text-wrapping/7512)
  - My understanding is that widget buffers exist to work around browser bugs with contenteditable

- ## Parallel cmd-k’s are becoming unexpectedly popular
- https://x.com/cursor_ai/status/1765512112200151391
- didn't see programmers liking parallel processing and async multitasking capabilities? or didn't realize that you built the thing that is actively building the thing... AI-Powered Devs.  of course that'd be popular, once it found some hype-men

# discuss-code-animation 💫
- ## 

- ## 

- ## 

- ## [A scalable CSS only Typewriter Effect - DEV Community _202108](https://dev.to/afif/a-scalable-css-only-typewriter-effect-2opn)
- Here is a simple typewriter effect with only a few lines of CSS where you don't need to deal with any js code.
  - Doesn't require monospace fonts
  - Can use any font
- 
- 

- ## Achieve CSS Typewriter effect under 1 minutes.
- https://x.com/Prathkum/status/1693598454092808544
  - https://codepen.io/prathkum/pen/qBqGepq
  - This method is great, the thing is that it's only good for monospace fonts, and only works on a solid color background
- Here's a different method that allows the use of any font, on any background.
  - https://codepen.io/amit_sheen/pen/YzZYoMV
- https://codepen.io/denic/pen/GRoOxbM

- ## [A Multi-line CSS only Typewriter effect - DEV Community _202204](https://dev.to/afif/a-multi-line-css-only-typewriter-effect-3op3)
- 

- ## [Typewriter Effect | CSS-Tricks _201607](https://css-tricks.com/snippets/css/typewriter-effect/)
  - Demo relies on flexbox, so that could affect the layout in testing
  - Adding more steps to the typing animation will increase the smoothness of the typing

```CSS
.typewriter h1 {
  overflow: hidden;
  /* Ensures the content is not revealed until the animation */
  border-right: .15em solid orange;
  /* The typwriter cursor */
  white-space: nowrap;
  /* Keeps the content on a single line */
  margin: 0 auto;
  /* Gives that scrolling effect as the typing happens */
  letter-spacing: .15em;
  /* Adjust as needed */
  animation:
    typing 3.5s steps(40, end),
    blink-caret .75s step-end infinite;
}

/* The typing effect */
@keyframes typing {
  from {
    width: 0
  }

  to {
    width: 100%
  }
}

/* The typewriter cursor effect */
@keyframes blink-caret {

  from,
  to {
    border-color: transparent
  }

  50% {
    border-color: orange;
  }
}
```

- ## 💫 Staggered Animation - CSS 逐行显示动画， 与codemirror无关
- https://x.com/alirdev/status/1817923525002530819
- I once recorded a video for a text reveal using this same approach
  - [JS Text Reveal Effect - YouTube](https://www.youtube.com/watch?v=PMiVFXZpYQo&t=140s)
- I made a video a while ago that explains this technique
  - [Css: Scoped variables - YouTube](https://www.youtube.com/watch?v=cXM0SZeWjd4)

- [Typewriter Animation in CSS - YouTube](https://www.youtube.com/watch?v=yefgBA1CecI)

- ## second attempt to generate slide deck for a paper with @Google Gemini 1.5 Pro in @revealjs .
- https://x.com/algo_diver/status/1769614261616251150
  - I tried to add colors and animations, and I also tried to guide on the structure of the presentation

# discuss-cm-view-render
- ## 

- ## 

- ## What code editor theme do you use?
- https://x.com/vladyslavmoroz/status/1821469348977918139
- Was a Solarized user for a decade. Recently switched to Nord.
- zed

- ## pleased w/ this CSS solution for a Datagrip-like contiguous border around the last-run selection in CodeMirror
- https://x.com/hamiltonulmer/status/1800939237329731718
  - 代码的不规则边框效果
  - making CodeMirror work for serious editing is largely about stacking decorations & compositing them visually in the right ways. Which is yet another thing that should be familiar to anyone who does dataviz
  - .cm-previously-run is a child of .cm-line, wraps text as selection. Use pseudoelements w/ z-index to draw bg + left/right (::before) and top/bottom (::after)
  - make sure this is below .cm-selectionLayer so you can apply mix-blend-mode: multiply and darken the selection
  - by putting the pseudoelements in explicit stacking order, you kind of "cover up" the top & bottom borders, giving the outline effect. So it's a hack, but is much nicer to do this w/ just CSS than to wrangle contiguous borders with JS or something

# discuss-view-decoration-code-folding/hide/replace
- ## 

- ## 💡 [Replacing keywords in text as they are written - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/replacing-keywords-in-text-as-they-are-written/4123)
  - my question is not so much about how to perform the text replacements but about what is the best way to trigger those replacements as the content is edited.

- You could use a `transactionFilter` that checks whether the text around any of the changed ranges (tr.changes.iterChangedRanges) the new doc matches your keyword, and adds an additional transaction that changes them when it does (`return [tr, {changes: [...], sequential: true}]`).

- ## [How to add line class to a specific line dynamically - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-line-class-to-a-specific-line-dynamically/6230)
- You set up an extension, similar to the zebra stripe example, that maintains line decorations for the lines that you want to style, and updates them as appropriate on transactions.

- ## [Widget on right side of line - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/widget-on-right-side-of-line/7235)
- It might be possible to put a block widget that is `float: right` in there, but it may also be that that causes some unexpected issues.
- I’ve finally tried this. Yes, there’s a side effect - it breaks the gutter.
  - Not sure if it’s a proper solution, but setting `height: 0;` on the widget helped me achieve this. The widget is still visible.

- ## [Highlight part of a line - discuss. CodeMirror](https://discuss.codemirror.net/t/highlight-part-of-a-line/4165)
- To style a range of text, you want Decoration.mark instead of Decoration.line.

- ## [Highlight line function - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/highlight-line-function/4627)
- I think what’s going wrong is that you’re using the line number, instead of the line offset (doc.line(lineNumber).from) when calling .range.
  - 基于Decoration.line实现

- ## [Easily track & remove content with decorations - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/easily-track-remove-content-with-decorations/4606)
- The way to do something like bookmarks would be to create a state field that tracks the positions you are interested in, and on any transaction where `!tr.changes.empty` , map all those positions to their new equivalent with `tr.changes.mapPos` . Using a range set might be an optimization for this (it is more clever about mapping large numbers of positions without looking at every single one of them).

- ## [Are these styles all right, or is this intervening too much into the editor? - discuss. CodeMirror](https://discuss.codemirror.net/t/are-these-styles-all-right-or-is-this-intervening-too-much-into-the-editor/5071)
- Mark decorations can only style content, so if there’s no content, they don’t appear, no.

- ## [How to add `Decoration.line()` for multiple lines at once? - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-decoration-line-for-multiple-lines-at-once/4156)
- You can also use RangeSet.of with a second argument of true if you can’t sort the ranges

- ## [Conditionally showing Widgets using a StateField - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/conditionally-showing-widgets-using-a-statefield/6020)
  - I’m trying to make sure those decorations only show when the cursor is NOT within the image tag. The idea is to have inline images throughout the document that are only visible when the user is not actively editing the image tag itself.
  - I started writing code the StateField’s update method to update/filter the RangeSet that’s returned based on cursor position, but it’s not working as expected. Is there a better way to accomplish this?

- No, this seems reasonable. As an optimization, you might be able to keep both the ‘full’ range set and the filtered one — have update logic that checks if the cursor is inside a range in the full set, returns the full set if not, and a filtered version if so.

- ## [Updating block-widgets // What is the order of the state update cycle, exactly? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/updating-block-widgets-what-is-the-order-of-the-state-update-cycle-exactly/8365)
- I suspect, from your message, that you’re mutating your decorations, and expecting the method to run then? That’s not how these work—they are immutable like everything else you store in your state. You replace them with a widget of the same type to have updateDOM called.

- ## 🤔 [Preferred way to create multi-line widget? - discuss. CodeMirror _202208](https://discuss.codemirror.net/t/preferred-way-to-create-multi-line-widget/4865)
- Directly via EditorView.decorations. Put the decorations in a state field, not a plugin, so that they are available before the viewport is computed.

- If you want to render widgets that are guaranteed to be only inline (i.e. Markdown links), then you should define a ViewPlugin. Those get called after the viewport has been created and are therefore much cheaper. Also, you can make use of the view.visibleRanges-property which enables you to only render those widgets for any actually visible ranges (i.e. must be within the viewport and additionally not be folded).
  - The example for inline-only-widgets is the Boolean Toggle Widgets example
- If you have widgets that may also be block-level and not just inline you have to, as Marijn said, call StateField.define(). You can – more or less – provide the same logic to compute the widgets, but since StateFields are computed prior to rendering, you can also provide block-level widgets.
  - The example for the inline and block widgets is the Underline command example. (The trick is to understand that you can also underline pieces of text that span line breaks, even if you don’t underline full lines. To me, for the past weeks, it always seemed to me inline-only just as well.)

- ## [View Plugin vs. State Field for inline replacements with line wrapping - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/view-plugin-vs-state-field-for-inline-replacements-with-line-wrapping/8129)
  - in an extension I want to (visually) replace specific strings with other strings of variable length under certain conditions using replace decorations with an inline widget. When line wrapping is enabled, this could affect vertical space by introducing line breaks.
  - The docs say clearly that if my decorations affect vertical space, I should use a state field to provide them. However, I find examples of extensions where these kind of replacement decorations are provided from a view plugin (some popular Obsidian plugins do it, where line wrapping is enabled per default).
  - I’d like to understand better why and whether I really need a state field here. 

- A plugin is fine there. What those shouldn’t do is change the block structure of the document, i.e. replacing line breaks or adding block widgets. Wrap points are not line breaks.

- ## [How to recognise if a widget is removed ? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-recognise-if-a-widget-is-removed/8180)
- You could do a check where you see if the range set’s size changed after mapping, and if so, do a scan through it to figure out which widget that you still have in your outside data was removed.

- ## [How to get widgets from DecorationSet? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-get-widgets-from-decorationset/3772)
- I’ve used DecorationSet.between to iterate the decorations in the set

- ## [Hide StateField decorations when replaced code is selected - v6 - discuss. CodeMirror _202310](https://discuss.codemirror.net/t/hide-statefield-decorations-when-replaced-code-is-selected/7219)
  - I’ve achieved the same effect using a ViewPlugin and listening to update.selectionSet to determine the decorations that should no longer be displayed and provide a filtered decoration set; however I am a) not sure that this is a good solution and b) how to achieve the same with a StateField.

- State fields should be able to react to updates in much the same way — they see every transaction that comes through, and can look at the selection of the new state.

- this introduces a new issue. Since the widget influences the vertical layout, hiding it, sometimes influences the ongoing selection (because the lines get moved around and the cursor finds itself on top of a different line). This sometimes deselects the underlying code, making the widget appear again, only to change the vertical layout once more, and so on. A simple solution would be to wait until the user is “done” selecting before hiding/showing widgets; but I think there is no such event in CodeMirror to listen to, or is there?
  - Not on the state level. You can of course listen to mouse and touch events on the view.

- ## [How to replace content with widget? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-replace-content-with-widget/4288)
- You have to provide your decorations from a state field, not a view plugin, if they are able to change the vertical structure of the editor content (because the viewport depends on that structure, and view plugins update after the viewport has been computed). 

- ## [Widget reuse between Decoration.replace and Decoration.widget - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/widget-reuse-between-decoration-replace-and-decoration-widget/6504)
- This seems unproblematic to support. See this patch. _202305

- ## [Cursor to skip Decoration.replace - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/cursor-to-skip-decoration-replace/3902)
- You may be looking for atomicRanges
- I’ve been following the boolean toggle widget example but building a replace decoration instead of a widget and I want to make them atomic.

- ## [Decoration.replace side - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/decoration-replace-side/3682/3)
- The inclusive options control the side. Replace widgets that are inclusive on a given side will cover any regular widgets at that position, whereas non-inclusive replacements won’t.
  - I’m not seeing this problem — creating two adjacent replace decorations with a widget decoration between them just works, when I try it.

- ## [Hiding pieces of code and making them non-interactive - v6 - discuss. CodeMirror _202212](https://discuss.codemirror.net/t/hiding-pieces-of-code-and-making-them-non-interactive/5433)
- Collapsed content could also be deleted in CM5 unless you set readOnly. 
  - CM6 has no equivalent to that—but you can implement behavior like that with a change filter.

- ## [How to control the line number's showing or hiding? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-control-the-line-numbers-showing-or-hiding/4439)
- Put the extensions in a compartment and enable/disable them by reconfiguring that. 

- ## [the codemirror6 how hide line number? - discuss. CodeMirror](https://discuss.codemirror.net/t/the-codemirror6-how-hide-line-number/6161/2)
- `lineNumberMarkers` with a class name that hides the gutter elements might work.

- ## [How can I customize the fold widget based on the contents of the folded text? - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/how-can-i-customize-the-fold-widget-based-on-the-contents-of-the-folded-text/6995)
- [[Folding] Show number of lines / elements folded - v6 - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/folding-show-number-of-lines-elements-folded/6950)
  - It’s not something that the library supports. If you really need this you’ll have to fork (part of) `@codemirror/language/src/fold.ts` to implement your own custom folding system.
  - `placeholderDOM/Text` are currently called from a place that knows nothing about the folded range, so this is definitely not a matter of simply adding a parameter. It’d need to overhaul the way the widgets used by this code work.

- ## [Code folding example - v6 - discuss. CodeMirror _202405](https://discuss.codemirror.net/t/code-folding-example/8226)
- You can pass in any range that you want to fold (if you’re doing your own textual scan for this), or use foldable to ask the built-in fold logic

- ## [Is ad hoc code folding possible - v6 - discuss. CodeMirror _202301](https://discuss.codemirror.net/t/is-ad-hoc-code-folding-possible/5535)
- This should work. Unless the cursor is inside the folded range, then it will automatically be unfolded again immediately.

- ## [Add folding at specific levels programmatically - v6 - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/add-folding-at-specific-levels-programmatically/7024)
- Fold points are identified by line in CodeMirror’s folding system, not by depth
  - you could write a function that runs over the entire document, finding lines that start a fold of the level you are interested in, and accumulating fold effects for their foldable ranges. You can then dispatch a transaction with those effects to fold them all at once.

- ## [Folding functions - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/folding-functions/4189)
- you can fold with foldEffect, and find foldable ranges with foldable from the language package.

- ## [Custom Code Folding - v6 - discuss. CodeMirror _202206](https://discuss.codemirror.net/t/custom-code-folding/4643)
- The general approach for that would be to iterate the parse tree scanning for nodes you want to fold (might have to read from the document to figure out property names), collect a bunch of fold effects, and dispatch those.
