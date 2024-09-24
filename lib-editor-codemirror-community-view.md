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

- ## [Force a layout pass programmatically - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/force-a-layout-pass-programmatically/5914)
- Could it be that your fonts or styles are loading after the editor initializes? A `view.requestMeasure()` should cause it to re-measure its layout. Sometimes it helps to do this on a "load" event.

- ## 👾 Finished up a simple AI edit gen feature. a nice pattern is to pull a CodeMirror widget DOM element out into a React portal and then just writing the component with React. 
- https://x.com/hamiltonulmer/status/1829287750253916369
  - Way easier to integrate & mix the two types of state
  - I bet it can be made better w/ AST / position info
  - we also have schema & locally-cached data to enrich the prompt

- for this, I tried out Cursor, which did a great job of helping me scaffold in a few critical parts of the CodeMirror side. I could have done this myself but it probably ended up saving me a few hours 
  - I'm finding that Cursor is an excellent tool for people that already know how to build products – it's a real force multiplier. For me, it felt like some kind of prompt-driven autocomplete that I could verify myself.

- ## [codemirror 6 and textareas _202011](https://discuss.codemirror.net/t/codemirror-6-and-textareas/2731)
  - With codemirror 5 you can use CodeMirror.fromTextArea() to create an editor from a tag which I really like since it lets users without JS still do things and makes it easier to send data with an html form.
- This was always a dodgy hack (it involves replacing the surrounding form’s submit method, among other things) that leaks quite a bit (for example if you expect your textarea’s value to be kept in sync with the editor content), so I’m kind of happy to get away from it. It’d be easy to write something similar as a separate module, of course.

- ## experimenting with a canvas-driven CodeMirror cursor
- https://x.com/hamiltonulmer/status/1822274427142525210
  - will need to try a gradient polygon rather than a trail of thin lines

- the long-awaited feature for every rich text editor

- https://x.com/hamiltonulmer/status/1822120260910383419
  - thinking about experimenting with a canvas-driven layer for CodeMirror (for cursors and selections, not text). 
  - Goal would be to enable richer animations not achievable with css e.g. show cursor motion blur when jumping around
# discuss-blocks/notion-like
- ## 

- ## 

- ## [Editor on multiple columns - discuss. CodeMirror _202208](https://discuss.codemirror.net/t/editor-on-multiple-columns/4908)
- Just setting the editor CSS to create columns will definitely not work. The editor expects a lines to appear below each other, in order. You might be able to build something out of multiple editors by having your own code split and divide the content, but getting things like the undo history and cursor motion to work smoothly like that would probably be a lot of work.

- ## [Multiple Editable Columns with CodeMirror 6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/multiple-editable-columns-with-codemirror-6/8514)
  - My north star goal is to provide a Layout experience similar to that of Confluence/Notion
- I had a very positive experience with just replacing decoration widgets (width:100%). One can make them mutable (they can change the content on the covered ranges using basic transactions) and provide a transaction filter or something similar so that if a cursor goes into the region of the widget, it will move the focus into the nested codemirror editor.

# discuss-readonly
- ## 

- ## 

- ## 

- ## 

- ## [Switch between editor being editable or not - v6 ](https://discuss.codemirror.net/t/switch-between-editor-being-editable-or-not/2745)
- reuse the Compartment instance to alter the editable state
  - Looking more into Configuration example

- [Implement some kind of read-only mode ](https://github.com/codemirror/dev/issues/173)
  - By default, if the editor isn't focusable, it also won't receive key events, so you can't ctrl-v on it. But I guess if you add a `tabindex` attribute to make it focusable you will have key bindings firing on the editor.
  - Since @codemirror/state 0.19.2, there's also a `readOnly` facet, on the state, which controls whether the content is supposed to be read-only (and is respected by commands and such). This is separate from the editable facet, which only controls whether the DOM for the content is focusable/editable.
# discuss-autocomplete
- ## 

- ## 🌰 [Replace default search panel with my own component - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/replace-default-search-panel-with-my-own-component/5885)
- my solution customizes search in a CodeMirror editor by removing the default panel, enabling case insensitivity, and scrolling to match occurrences
  - the code includes functions for replacing the next occurrence of the search query (replaceNext) and replacing all occurrences (replaceAll). 
  - Additionally, there are functions for undoing (undoEditor) and redoing (redoEditor) changes in the editor.

- ## [Access Decorations from tooltip (or vise versa) - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/access-decorations-from-tooltip-or-vise-versa/5462)
- The callback given to `hoverTooltip` could use the range set holding the decorations to figure out whether there’s a match at the hovered position, if hover tooltips are what you are trying to implement. If these are always-visible things, I guess you could use the decorate option to generate both mark decorations and widgets for a given match
- Supposedly you’re storing the range set produced by `MatchDecorator` in some view plugin, which you could access in the callback, so that you don’t have to look at all decorations, only the relevant ones.

- ## [Is it possible to add a Widget Decoration instead of text while selecting a variable from auto complete? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/is-it-possible-to-add-a-widget-decoration-instead-of-text-while-selecting-a-variable-from-auto-complete/6751)
- Roughly, you’d want to set up an extension that manages these widget decorations, and dispatch a transaction (probably with a custom effect attached) that creates the widget.

- ## 🤔 [Implement a code hinting style in CodeMirror 6 similar to the GitHub Copilot extension in VSCode - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/implement-a-code-hinting-style-in-codemirror-6-similar-to-the-github-copilot-extension-in-vscode/6058)
- Since that only shows a single suggestion, rather than a list of them, I think it is different enough from what the autocompletion package is doing to go with a completely separate implementation.
  - ~~Showing the completion in the document like that is a bit tricky, since inline widget decorations can’t span lines. Maybe use inline decorations for the first and last lines of the completion, and block decorations for any completely new lines.~~
  - 202308: Recent versions of @codemirror/view allow you to have line breaks in (inline-styled) widgets, so that tricks with block widgets should no longer be necessary

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

- ## [How to add animation, keyframes in the basetheme? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-animation-keyframes-in-the-basetheme/3561)

```JS
{
  '@keyframes blink': {
    from: { backgroundColor: 'aliceblue' },
    to: { backgroundColor: 'black' }
  }
}
```

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

# discuss-styling
- ## 

- ## [Dynamically changing theme in MergeView - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/dynamically-changing-theme-in-mergeview/8620)
- Define a compartment

- ## [How does CM6 decide whether dark mode is on/off? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-does-cm6-decide-whether-dark-mode-is-on-off/8397)
- This is determined by the `dark` option of the active theme. The library itself does no detection of `prefers-color-scheme` .
  - If you’re not using a theme, you get the `&light` base theme rules. If any of the themes you’re using set the editor to dark, you get &dark.

- ## [Inconsistency in EditorView.theme - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/inconsistency-in-editorview-theme/7290)
- `&light/&dark` are supported only in `baseTheme` , not in theme.

- ## 🌰💄 [Dynamic light mode / dark mode - how? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/dynamic-light-mode-dark-mode-how/4709)
  - Previously, handling this was quite straightforward; we’d simply define alternate colors for the relevant classes within a prefers-color-scheme block, in our SCSS
  - I’m struggling to understand how one handles this type of thing in v6’s themes and syntax highlighting

```JS
this.view.dispatch({
  effects: this.editorTheme.reconfigure(selectedTheme === "light" ? oneLight : oneDark)
});

// listen for the media change
window.matchMedia('(prefers-color-scheme: dark)')
  .addEventListener('change', event => {
    if (event.matches) {
      //dark mode
    } else {
      //light mode
    }
  })
```

- ## [Inline Codemirror inside Prosemirror? - discuss. CodeMirror _202311](https://discuss.codemirror.net/t/inline-codemirror-inside-prosemirror/7396)
- Is it possible to embed an inline CodeMirror view inside ProseMirror? I was thinking as an inline node, meaning instead of being a full width div, it just expands as the user types.
  - no, CodeMirror assumes it is a block element, so for this you’d have to wrap it in some kind of `inline-block` container and add a kludge that constantly resizes it to match its content size. It won’t work as a regular content-fitting inline element.

# discuss-view-render
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

# discuss-event-focus/blur
- ## 

- ## 

- ## 📱 [What is the purpose of settimeout of 10ms in updateForFocusChange? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/what-is-the-purpose-of-settimeout-of-10ms-in-updateforfocuschange/8369)
  - codemirror’s blur happens after a 10ms timeout, making it the last event, occurring after my event
- There are several types of interactions that will cause the editor to lose and then immediately regain focus (people implementing buttons that steal focus on mousedown but then immediately move it back to the editor, our own kludge for dealing with Android inappropriately closing the virtual keyboard in some situations). This timeout tries to isolate code tracking focus state from that kind of phantom(幽灵；幻觉) focus changes.
  - If you want to directly track DOM focus state, I’d recommend using a DOM event observer rather than an update listener. Those get the raw DOM events.

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

- ## [Implement draggable ranges/object through mouse curser. - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/implement-draggable-ranges-object-through-mouse-curser/4655)
- Is this dropCursor?

- ## [Drag & Drop Widget Decorator - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/drag-drop-widget-decorator/7338)
  - I have made the widget dom draggable and set the dropCursor extension in my cm configuration. My approach would to read the dropped cursor effect that the dropCursor dispatches and use that to move my widget, but two issues arise
  - In short, I want to drag a widget and when dropped read the cursorDrop anchor position, then dispatch the widget update.
  - It’s a Widget that replaces some text and I want to drag the resulting dom. So far dragging the widget is not a problem, but dropping it and making sense of it after.

- ~~You can add a `dragstart` handler on the widget, and do `event.dataTransfer.setData("text/plain", ...)` in your handler to set the content. (`dragstart` doesn’t propagate, so the editor’s drag handler doesn’t even fire in this situation)~~
  - Looking at this more closely, it seems that `dragstart` does bubble, and there’s a better solution for this. 
