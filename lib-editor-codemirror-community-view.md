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

- ## 🌰 [Dynamic light mode / dark mode - how? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/dynamic-light-mode-dark-mode-how/4709)
- `this.view.dispatch({ effects: this.editorTheme.reconfigure( selectedTheme === "light" ? oneLight : oneDark ) })` ; 

```JS
this.view.dispatch({
  effects: this.editorTheme.reconfigure(selectedTheme === "light" ? oneLight : oneDark)
});

window.matchMedia('(prefers-color-scheme: dark)')
  .addEventListener('change', event => {
    if (event.matches) {
      //dark mode
    } else {
      //light mode
    }
  })
```

- ## experimenting with a canvas-driven CodeMirror cursor
- https://x.com/hamiltonulmer/status/1822274427142525210
  - will need to try a gradient polygon rather than a trail of thin lines

- the long-awaited feature for every rich text editor

- https://x.com/hamiltonulmer/status/1822120260910383419
  - thinking about experimenting with a canvas-driven layer for CodeMirror (for cursors and selections, not text). 
  - Goal would be to enable richer animations not achievable with css e.g. show cursor motion blur when jumping around
# discuss-autocomplete
- ## 

- ## 

- ## 

- ## [How to append to existing JavaScript autocompletions and snippets? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-append-to-existing-javascript-autocompletions-and-snippets/5587)
- Just define another completion source through language data 80, and its result will be combined with other sources.

- ## [Render autocomplete outside of editor container - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/render-autocomplete-outside-of-editor-container/7283)
- You can configure tooltips() to do this, but that will affect all tooltips.

- ## [unwanted element appear when using Decoration.replace - v6 - discuss. CodeMirror _202302](https://discuss.codemirror.net/t/unwanted-element-appear-when-using-decoration-replace/5681)
- Emitting clean HTML for use in other contexts is not something the editor will do for you.

- ## [why with codemirror6 @codemirror/autocomplete auto create hidden img? - discuss. CodeMirror _202304](https://discuss.codemirror.net/t/why-with-codemirror6-codemirror-autocomplete-auto-create-hidden-img/6173)
- This avoids a number of browser bugs caused by editing next to uneditable elements such as widgets.

- [Hiding widget buffers for better text wrapping - v6 - discuss. CodeMirror _202312](https://discuss.codemirror.net/t/hiding-widget-buffers-for-better-text-wrapping/7512)
  - My understanding is that widget buffers exist to work around browser bugs with contenteditable
# discuss-code-animation 💫
- ## 

- ## 

- ## 

- ## 💡 [A scalable CSS only Typewriter Effect - DEV Community _202108](https://dev.to/afif/a-scalable-css-only-typewriter-effect-2opn)
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

- ## 💫 [A Multi-line CSS only Typewriter effect - DEV Community _202204](https://dev.to/afif/a-multi-line-css-only-typewriter-effect-3op3)
  - The effect relies on using a Monospace font and knowing the number of characters. 
  - Yes, I am starting with the drawbacks but that was the price for a generic and easy-to-use code.
- 
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

- ## ☄️ My another challenge this year: a sponsorware project "Code Animate" _202202
- https://x.com/dai_shi/status/1493213723150131205
  - I have been thinking about building this tool since last year to help my creating coding tutorials. 
  - https://code-animate.axlight.com/
  - One of the tools inspired me is asciinema, so it definitely seems interesting. 
  - On the otherhand, my goal is not to play back. I want something like what I did with Excalidraw-Animate
- Not to be a pessimist but I don't think this would be an enjoyable experience for tutorials. I personally would prefer the text never move. Diff style tutorials are good for this IMO. It's also not great for accessibility.
  - Maybe, maybe not. It's more for making it like a live session. I agree the final code should be some sort of texts.
- I love the idea. I experimented with something similar last year, a different diff animation for 
@codehike_
: https://x.com/pomber/status//pomber/status/1383524087331393550. But I haven't used it yet.

# discuss-emoji
- ## 

- ## [Backspace on some multi-codepoint glyphs deletes characters separately - v6 - discuss. CodeMirror _202311](https://discuss.codemirror.net/t/backspace-on-some-multi-codepoint-glyphs-deletes-characters-separately/7403)
  - Left and right arrow keys move around multi-codepoint glyphs, such as :arrow_left: and :running_woman:t2:, atomically. Forward delete similarly works on the glyphs atomically.
  - However, pressing backspace after these multi-codepoint glyphs seems to delete the characters separately. Is the latter behavior controlled by CM itself, and if so, is it intended?

- This is intentional behavior and matches how many editors (for example Firefox’s native edit controls and VS Code) behave.

- 
- 
- 

- ## [For some emojis, it takes 2 keystrokes to delete - Bug graveyard - Obsidian Forum _202206](https://forum.obsidian.md/t/for-some-emojis-it-takes-2-keystrokes-to-delete/39500)
- Obsidian does not seem to handle combining codepoints like these well. Instead, it treats these as two individual grapheme clusters, meaning that text editing gives them separate boundaries. But really they should have a single combined boundary

- [backspace on Emoji does not remove whole grapheme cluster _202106](https://github.com/codemirror/dev/issues/516)
  - This was intentional behavior, but on closer look it indeed seems that other editors don't work like that, so attached patch drops it.

- ## [Some emoji don't show up as emoji, but instead unicode alternates _202206](https://github.com/codemirror/dev/issues/883)
- That seems to be your browser's native rendering of those—at least, in Firefox and Chrome on Linux, I'm seeing the same — putting "\u26a0 \u{1f631}" in HTML causes the browser to render the first as a monochrome glyph, and the second as a colored emoji (unless I add a \ufe0f after the warning character). So this is expected behavior, as far as I'm concerned.
  - It'd be possible to write a plugin similar to highlightSpecialChars that replaces anything that looks like an Emoji without a variant selector with an Emoji that has a color variant selector, if that's what you want to do.

- ## [Markdown emoji previewing - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/markdown-emoji-previewing/5186)
- Yes that can be implemented via “replacing decorations”, see Example: Decorations 

- ## [Challenges on implementing operational transformation server in Golang due to javascript unicode string length - v6 - discuss. CodeMirror _202210](https://discuss.codemirror.net/t/challenges-on-implementing-operational-transformation-server-in-golang-due-to-javascript-unicode-string-length/5124)
  - Everything works pretty well when Golang server implements codemirror/state text.ts in Go language and uses utf8. RuneCountInString, which counts how many characters there are in a string.
  - ‘:+1:’.length is 2 and that doesn’t any longer match with rune length in Go that is 1 and applying ChangeSet fails.
- CodeMirror intentionally uses UTF16 code point counts throughout, in order to be able to use String.length. If you are using another convention in the OT system, you’ll have to make sure you convert to and from that when going between CodeMirror and that system. Forking @codemirror/state is not going to be needed.

# discuss-cm-view-render
- ## 

- ## 

- ## 

- ## [Getting the DOM Rect(s) of a text range that may be split across lines? - discuss. CodeMirror](https://discuss.codemirror.net/t/getting-the-dom-rect-s-of-a-text-range-that-may-be-split-across-lines/6777)
- The equivalent to charCoords is coordsAtPos, and you can use moveToLineBoundary to find the visual start/end of a line. Or use the built-in tooltip feature and let that manage tooltip positioning.

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

# discuss-event-scroll
- ## 

- ## 

- ## 

- ## [Smooth scroll to selection position? - discuss. CodeMirror _202208](https://discuss.codemirror.net/t/smooth-scroll-to-selection-position/4875)
- You can get the current scroll position with `view.scrollDOM.scrollTop` . The desired scroll position you’d have to compute based on the position you want to see ( `view.coordsAtPos` ) and the editor rectangle ( `view.scrollDOM.getBoundingClientRect` ).

- `view.lineBlockAt` should work for out-of-viewport positions, though it may be an estimate, rather than a precise value if they (or other content between them and the current scroll position) haven’t been drawn before.

```JS
const f = view.state.doc.line(lineNumber);
const { qq } = view.coordsAtPos(f.from); // can return null

view.scrollDOM.scrollTo({ qq, behavior: 'smooth' });
```

- ## 💡 [CM6 Scroll To Middle? - discuss. CodeMirror _202102](https://discuss.codemirror.net/t/cm6-scroll-to-middle/2924)
  - Is there a way to configure the “scrollIntoView” option in a transaction update to scroll the selection to the middle of the screen rather than the bottom?

- Not currently. 
  - I think the best way forward would be to write your own view plugin that does this. Something like…

- Got this working. The math here was a bit off because `coordsAtPos` gets the scrolled position, not the absolute one, so you have to add the scroller’s `scrollTop` to it. Also I had to add a timeout of 1ms so that it doesn’t interfere with CM’s native scrolling.

- 💡 Using a transaction extender that adds a scroll effect to transactions that scroll the cursor into view will cause less DOM reflows (and allow you to use the existing centering code).
# discuss-event-drag
- ## 

- ## 

- ## 

- ## 
# discuss-view-decoration-code-folding/hide/replace
- ## 

- ## 

- ## 

- ## 

- ## [Creating a Decoration that updates on an interval - v6 - discuss. CodeMirror _202210](https://discuss.codemirror.net/t/creating-a-decoration-that-updates-on-an-interval/5121)
  - I realized that view.dispatch() will refresh the gutters. I put that on an interval in my ViewPlugin and now my gutters update on an interval as I had hoped.

- Decorations aren’t stateful and don’t do imperative things. You’ll want the interval to be managed by a view plugin, which just replaces the decoration with a new one. 
  - If you really need to keep the existing DOM of your widget and just update it, you can give your widget type an `updateDOM` method that takes a different widget instance and updates the DOM representation.
- Can I use this technique with gutters? That is, can a view plugin provide gutters and/or update/replace gutters?
  - Yes, you can do something similar with gutter markers.
  - your plugin’s `provide` option can create a gutter that has access to the plugin, in order to read marks from it.

- ## [Decoration.mark() has lower precedense over styleTags()? - discuss. CodeMirror](https://discuss.codemirror.net/t/decoration-mark-has-lower-precedense-over-styletags/7397)
- Wrapping your decoration extension in Prec.highest should probably fix this.

- ## 💡 [Composing multiple DecorationSets - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/composing-multiple-decorationsets/2922)
- State-level decorations can be provided in bulk with `computeN` , something like…
  - `EditorView.decorations.computeN(s => s.field(f))`

- You could also create a view plugin providing multiple decoration sets by providing an array of plugin field providers for `PluginField.decorations` via the `provide` option in the plugin spec, but that only works if the number of sets is known in advance.

- ## [a display bug - discuss. CodeMirror](https://discuss.codemirror.net/t/a-display-bug/4074)
  - i find that when i set parent node’s style display to none of CodeMirror, then use the replaceSelection() API to replace some contents, and then i set parent node’s style display to block, the contents of CodeMirror didn’t change until after i click the editor area. is this a bug?
- No, refresh() is the way to solve this. The editor has no way to notice that it became visible.

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

- ## 🤔 [Easily track & remove content with decorations - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/easily-track-remove-content-with-decorations/4606)
- The way to do something like bookmarks would be to create a state field that tracks the positions you are interested in, and on any transaction where `!tr.changes.empty` , map all those positions to their new equivalent with `tr.changes.mapPos` . Using a range set might be an optimization for this (it is more clever about mapping large numbers of positions without looking at every single one of them).

- ## [Are these styles all right, or is this intervening too much into the editor? - discuss. CodeMirror](https://discuss.codemirror.net/t/are-these-styles-all-right-or-is-this-intervening-too-much-into-the-editor/5071)
- Mark decorations can only style content, so if there’s no content, they don’t appear, no.

- ## [How to add `Decoration.line()` for multiple lines at once? - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-decoration-line-for-multiple-lines-at-once/4156)
- You can also use `RangeSet.of` with a second argument of true if you can’t sort the ranges
  - Or keep using a builder and add some extra logic to make sure you insert them in order.

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
  - I’ve achieved the same effect using a `ViewPlugin` and listening to `update.selectionSet` to determine the decorations that should no longer be displayed and provide a filtered decoration set; however I am a) not sure that this is a good solution and b) how to achieve the same with a StateField.

- State fields should be able to react to updates in much the same way — they see every transaction that comes through, and can look at the selection of the new state.

- this introduces a new issue. Since the widget influences the vertical layout, hiding it, sometimes influences the ongoing selection (because the lines get moved around and the cursor finds itself on top of a different line). This sometimes deselects the underlying code, making the widget appear again, only to change the vertical layout once more, and so on. A simple solution would be to wait until the user is “done” selecting before hiding/showing widgets; but I think there is no such event in CodeMirror to listen to, or is there?
  - Not on the state level. 💡 You can of course listen to mouse and touch events on the view.

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
