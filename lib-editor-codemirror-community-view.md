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

- ## 💡 [Using css transform results in incorrect behavior · codemirror/dev _202010](https://github.com/codemirror/dev/issues/324)
- 202309: the view supports translation and scaling. Other types of transformation are probably never going to be supported, but translation is easy, and I believe I've added the necessarily logic to make scaling work properly.
  - 202311: Closing this. Support for more complicated transforms is not planned.

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

- ## [Multiple Editable Columns with CodeMirror 6 - v6 - discuss. CodeMirror _202408](https://discuss.codemirror.net/t/multiple-editable-columns-with-codemirror-6/8514)
  - My north star goal is to provide a Layout experience similar to that of Confluence/Notion
  - CM expects lines to follow each other, and to provide a clean experience with cursor and undo
- I had a very positive experience with just replacing decoration widgets (width:100%). One can make them mutable (they can change the content on the covered ranges using basic transactions) and provide a transaction filter or something similar so that if a cursor goes into the region of the widget, it will move the focus into the **nested codemirror editor**.
  - There is no need to rerender the nested editor, if you provide updateDom method to a widget

# discuss-autocomplete/tooltip
- ## 

- ## 

- ## [Highlight some text while hoverTooltip is activated - discuss. CodeMirror _202408](https://discuss.codemirror.net/t/highlight-some-text-while-hovertooltip-is-activated/8506)
  - I want to support LSP hover in CM, so I used the hoverTooltip plugin, it sends the LSP textDocument/hover request and show a tooltip for it, that’s good.
  - However, LSP server will also return a range object, which represents user-focused semantic object, I want to highlight the text in range during the hover tooltip. Is there a good way to do it? Thanks!

- This is currently difficult to do, since you cannot really recognize the transactions that open or close a hover tooltip. Would a feature that gives you access to the state field storing the active tooltips produced by the hover tooltip, which you could wire up to `EditorView.decorations.compute`, solve this problem for you?

- ## [need help about highly customized codemirror/autocomplete - discuss. CodeMirror _202210](https://discuss.codemirror.net/t/need-help-about-highly-customized-codemirror-autocomplete/5170)
  - I want to highly customize the style of autocomplete and bind some events to achieve the effect of cascading components
- @codemirror/autocomplete is rather specialized for classical code editor completion style. It looks like you’re trying to do something hierarchical there, which it definitely doesn’t support.
  - The tooltip feature in @codemirror/view can be useful when implementing something like this. There’s no other completion functionality available.

- ## [How to add custom completions before language completions? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-custom-completions-before-language-completions/7790)
- These are sorted first by how well they match the typed input, and then by `boost` , and finally by `localeCompare` . 
  - In this case, because you typed a lower-case b, the word break is considered a better match than Banana, because its case matches. There’s no real way to override match-quality ordering.

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

- ## 

- ## AI SDK 4.0.26 With the new smoothStream 'line' option, you can stream out full lines with a configurable delay _202501
- https://x.com/aisdk/status/1876657568929759566
- I think doing it client side is even better because you get the full stream, so you can only delay certain UI-rendered tokens but not tokens related to a custom built parser
- I like Gemini's fade-in effect. I spent a while trying to get that to work a few months ago but never got it quite right.

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
- 
- 

- [Upgrading the CSS only Multi-line Typewriter effect - DEV Community _202109](https://dev.to/afif/upgrading-the-css-only-multi-line-typewriter-effect-2269)
  - create a more fancy variation of the "writer effect" using only CSS.
  - Filling, Sliding, Shot, Random, Fragmentation

- ## 💫 [Multiline CSS-only typewriter effect - DEV Community _202109](https://dev.to/alvaromontoro/multiline-css-only-typewriter-effect-18p4)
  - it could be "close" to the one https://dev.to/afif/a-multi-line-css-only-typewriter-effect-3op3, but using different elements and properties
- The idea of this effect is having two different moving elements: the text container in itself and a pseudo-element used to hide the content.
  - The container animation is simple: it grows a given height (the specified line height) until all the text has been displayed or the container reaches a limit of lines (500 by default). It happens in steps, so each line is revealed at a time.
- 🧐 Required styles: the animation requires all lines to have the same height, so a `line-height` value is needed. It's "vertically monospaced."
  - Limited backgrounds: the background must be a solid color. Otherwise, the animation of the pseudo-element will be revealed.

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

# discuss-styling/theming
- ## 

- ## 

- ## 

- ## 💡 [How do I get selected text to highlight? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-do-i-get-selected-text-to-highlight/7115)
- Don’t set non-transparent line backgrounds. The selection is drawn as a layer behind the text, so you’re hiding it.
- You’ll want to use transparent colors for text background styles. The selection (and other layers) are rendered behind the text, so if you give that an opaque background, you hide anything behind it.

- ## [How can I change the color of selected text? - Stack Overflow](https://stackoverflow.com/questions/12339667/how-can-i-change-the-color-of-selected-text)

```CSS
/* drawSelection */
.cm-selectionBackground,
/* browser-native selection */
.cm-editor ::selection {
  background-color: #ccc !important;
}

/* To reset to the browser's default, rather than drawSelection's custom color*/
.cm-selectionBackground {
  background-color: highlight !important;
}
```

- ## [CSS style for border of editor - discuss. CodeMirror](https://discuss.codemirror.net/t/css-style-for-border-of-editor/3097)
- If you are using v6, you can do something like:

```js
const myTheme = EditorView.theme({
  "&": {
    fontSize: "12pt",
    border: "1px solid #c0c0c0"
  },
  "&.cm-editor.cm-focused": {
    outline: "none"
  }
});
```

- ## [Change where/when Theme `<style>` Element is Injected - discuss. CodeMirror _202402](https://discuss.codemirror.net/t/change-where-when-theme-style-element-is-injected/7821)
- Due to Next’s restrictions, we ended up needing to go the ShadowDOM route, like @dimanik94 describes, so that the styles get contained inside of the shadow root and Next can’t obliterate them. Our implementation gets rather involved, but the example they provide should work

- ## [EditorView.theme from facet value - v6 - discuss. CodeMirror _202407](https://discuss.codemirror.net/t/editorview-theme-from-facet-value/8477)
  - What is a good way to provide a Theme derived from the value of a Facet? Say there’s a facet full of custom colors that a theme wants to use.
  - I’ve attempted Facet.compute, StateField, ViewPlugin and more but I can’t seem to get anything that will allow me to get the current facet’s value to then use to build a separate theme extension.

- A theme is a composite extension, not just a single facet value, so you can’t use something like `Facet.compute` for it. You’d have to use a compartment and apply an actual reconfiguration effect (possibly in a transaction extender) to do something like this.

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

- ## 💄 [Styling and theming design discussion - v6 - discuss. CodeMirror _202102](https://discuss.codemirror.net/t/styling-and-theming-design-discussion/2958)
- We’re not going to “just use” plain CSS files
- please keep any knee-jerk hostility to CSS-in-JS out of the thread
  - Styles will be distributed over various packages. Users can not be expected to manually include the styles for all the packages they (transitively) load, and bundlers don’t (yet) provide a standardized way to bundle styles.
  - I’d really like to have proper isolation/scoping on CSS class names. Something like that is necessary for themes in any case. Being able to load multiple versions of the library without those interfering with each other is a plus.

# discuss-lineWrapping
- ## 

- ## 

- ## [Editor driven line wrapping - v6 - discuss. CodeMirror _202210](https://discuss.codemirror.net/t/editor-driven-line-wrapping/5125)
  - I’m from Replit and I’ve been working on an extension for adding indentation preserving line wrapping to our editor. 
  - Basically, me and other people at Replit have come up with… maybe 5 or more methods to add this feature and all of them have serious problems. They depend on CSS hacks, widget/mark decorations which require particular DOM layouts, etc.
  - where line breaks are in control of the browser. And with that you only get two choices (basically), which is breaking on every character, or breaking on what the browser considers a “word”.
  - I think most users would rather lines not break in the middle of words, but often the browser makes terrible choices with word based line breaks.
  - Decorations in general mess with line wrapping, as the browser will treat the edge of an inline-block (and others) as a word break point, which causes some problems. An example scenario would be placing a checkmark widget before a word, with the word being a label. Unless you wrapped both the checkmark and the label word in another decoration, the browser might choose to line wrap directly after the checkmark, which would be confusing.

- Doing line wrapping properly, taking into account the actual width of the glyphs, bidirectional text, and character types, is far from trivial, and as you probably expected, I’m not very attracted to the idea of increasing the scope of the library to include this.
  - I really don’t want to implement hanging indent (and/or line wrapping) in the core library, sorry.

- there are a lot of approaches we tried, and the current one uses `padding-left` on the line element, and then wraps the beginning whitespace in a decoration and uses negative margin on that element to shift the first row of a line. This is basically a modification of the technique where you use `padding-left` and `text-indent` together.
  - The issue with the padding-left and text-indent technique is that it has inconsistent behavior with tabs and between browsers. I have no idea why, but if you use tabs instead of spaces, negative margins/indents start to act in a stepwise… pattern? It feels inexplicable to me. It’s not consistent between browsers either.
  - You can get around this somewhat by doing what my current technique does, which is wrapping the beginning whitespace in an element so that you kind of “isolate” the problematic tab characters, and then you shift that element to offset the first line. 
  - However, because this is kind of an abuse of the whole decoration system, it breaks when other extensions (such as a linter) wrap lines or at least a part of the beginning whitespace in a mark decoration.

- ## 🌰 [Making Codemirror 6 respect indent for wrapped lines - v6 - discuss. CodeMirror _202102](https://discuss.codemirror.net/t/making-codemirror-6-respect-indent-for-wrapped-lines/2881)
- Plugin that makes line wrapping in the editor respect the identation of the line. 
  - It does this by adding a line decoration that adds padding-left (as much as there is indentation), and adds the same amount as negative "text-indent". 
  - The nice thing about text-indent is that it applies to the initial line of a wrapped line.
- Thanks for that! I adapted your version to not use any dependencies other than Codemirror itself. I removed the React bit and replaced the Lodash for loops

- I discovered that the text-indent trick used by all solutions in this thread interferes with the library’s rectangular selection. 
  - The left side will grow outside the text when the first line in the rendered viewport is indented.
  - I think I have made it. First, use ::before to create pseudo-elements with negative margin-left that mimic the effect of text-indent. Second, set border-left on lines instead of margin-left so that active line background still covers the indentation.
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

- ## 

- ## [Handling focus changes in StateField - v6 - discuss. CodeMirror _202303](https://discuss.codemirror.net/t/handling-focus-changes-in-statefield/6138)
  - How to handle focus changes in StateField update function? Should I use UpdateListener which dispatches some effect like FocusChangeEffect when focusChanged?
- By default, focus changes do not cause transactions and thus cannot be observed by the editor state. You can use `focusChangeEffect` to tell the editor to dispatch a given effect when focus changes, and react to those in your state field update method.

- ## [View.hasFocus is false when adding focus programmatically - v6 - discuss. CodeMirror _202111](https://discuss.codemirror.net/t/view-hasfocus-is-false-when-adding-focus-programmatically/3734)
- I think this is because `view.hasFocus` check for `document.hasFocus()` which is only true if the window/tab has focus from the OS. 
  - That means programmatically setting the active element (with .focus()) won’t affect view.hasFocus when the OS user isn’t focused on the web page.

- ## [How to set cursor position in Codemirror editor - Stack Overflow](https://stackoverflow.com/questions/33394855/how-to-set-cursor-position-in-codemirror-editor)
- Before you set the cursor position you have to focus on the editor.

- ## 🤔 [set cursor position in v6 - discuss. CodeMirror _202206](https://discuss.codemirror.net/t/set-cursor-position-in-v6/4476)
  - `editor.dispatch({selection: {anchor: N, head: N}})`

- Could it be that the editor is simply not focused? The cursor won’t be visible then.

- ## [How to programmatically remove focus from the editor? - v6 - discuss. CodeMirror _202108](https://discuss.codemirror.net/t/how-to-programmatically-remove-focus-from-the-editor/3429)
- `cm.contentDOM.blur()` should work.

- ## 📱 [What is the purpose of settimeout of 10ms in updateForFocusChange? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/what-is-the-purpose-of-settimeout-of-10ms-in-updateforfocuschange/8369)
  - codemirror’s blur happens after a 10ms timeout, making it the last event, occurring after my event
- There are several types of interactions that will cause the editor to lose and then immediately regain focus (people implementing buttons that steal focus on mousedown but then immediately move it back to the editor, our own kludge for dealing with Android inappropriately closing the virtual keyboard in some situations). This timeout tries to isolate code tracking focus state from that kind of phantom(幽灵；幻觉) focus changes.
  - If you want to directly track DOM focus state, I’d recommend using a DOM event observer rather than an update listener. Those get the raw DOM events.

- ## [Trigger a StateEffect when focus changes - discuss. CodeMirror _202302](https://discuss.codemirror.net/t/trigger-a-stateeffect-when-focus-changes/5701)
  - I need to dispatch a state effect when the editor’s focus changes (on focus and on blur), and I am struggling to figure out the right way to go about this
- Would it be possible for focusChangeEffect to pass the source of the focus change (pointer vs keyboard) as an argument?
  - The editor knows just as little about that as you do. It’s just responding to a focus or blur event.

- ## [CodeMirror react component losing focus on input - v6 - discuss. CodeMirror _202103](https://discuss.codemirror.net/t/codemirror-react-component-losing-focus-on-input/3053)
- I assume you’re recreating the editor on every update. You don’t want to do that for efficiency reasons, and also because removing and recreating the focused DOM will indeed remove its focus.

# discuss-event-scroll
- ## 

- ## 

- ## 🌰 [cursorScrollMargin for v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/cursorscrollmargin-for-v6/7448)
  - In CodeMirror 5 it was cursorScrollMargin, am I right in thinking that in V6 I should be using EditorView.scrollMargins ?

- No, EditorView.scrollMargins is not what you need here. There is no way to configure this at the moment, except is you are scrolling something into view explicitly with EditorView.scrollIntoView.

- I’ve iterated on this and fixed heaps of bugs with my previous implementation, and I’m leaving it here in case anyone wants to implement this

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

- ## 🤔 [Resizing Codemirror 6 - v6 - discuss. CodeMirror _202106](https://discuss.codemirror.net/t/resizing-codemirror-6/3265)
- You should be able to style the outer (.cm-editor) element with a resize CSS property and then arrange for view.scheduleMeasure() to be called when it is actually resized so that it can update its internal layout.
  - The idea would be to use the CSS of the parent element to change the editor’s size in response to user actions (or using browsers’ `resize` CSS support), and then call `requestMeasure` to make sure the editor picks up on any layout changes it needs to make. Nothing complicated is required. You didn’t really explain what is going wrong, so I can’t really help here.

- [How to resize codemirror6 | PageHelper Docs](https://pagehelper.lets-script.com/blog/codemirror6-resize/)

- ## [Implement draggable ranges/object through mouse curser. - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/implement-draggable-ranges-object-through-mouse-curser/4655)
- Is this dropCursor?

- ## [Drag & Drop Widget Decorator - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/drag-drop-widget-decorator/7338)
  - I have made the widget dom draggable and set the dropCursor extension in my cm configuration. My approach would to read the dropped cursor effect that the dropCursor dispatches and use that to move my widget, but two issues arise
  - In short, I want to drag a widget and when dropped read the cursorDrop anchor position, then dispatch the widget update.
  - It’s a Widget that replaces some text and I want to drag the resulting dom. So far dragging the widget is not a problem, but dropping it and making sense of it after.

- ~~You can add a `dragstart` handler on the widget, and do `event.dataTransfer.setData("text/plain", ...)` in your handler to set the content. (`dragstart` doesn’t propagate, so the editor’s drag handler doesn’t even fire in this situation)~~
  - Looking at this more closely, it seems that `dragstart` does bubble, and there’s a better solution for this. 
