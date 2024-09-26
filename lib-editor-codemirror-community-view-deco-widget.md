---
title: lib-editor-codemirror-community-view-deco-widget
tags: [codemirror, community, view-layer, widget]
created: 2024-09-10T11:29:19.686Z
modified: 2024-09-10T11:29:46.166Z
---

# lib-editor-codemirror-community-view-deco-widget

# guide

# discuss-stars
- ## 

- ## 

- ## 🌰 [remove decoration - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/remove-decoration/6696)
  - I am also trying to understand how this is done. I adapted the code from Decorations example
- Are you trying to clear it? In which case you can just set it to `Decoration.none` . Or are you trying to clear a specific range? If so, you’ll want to actually compare the ranges to the from and to values in the effect.
- I do want to clear a specific range ideally. Though I am not sure how to store the range of the original effect that was used to set the style in the first place. To be clear, I am not seeking to undo the last transaction, but merely capture the range of the last transaction and remove its styling. Can I store the range in the EditorState and retrieve it later?
  - You can, if you define a StateField for it. But you can also iterate over the ranges in the set, if you can somehow recognize the proper one

- ## 💡 [Modifying decorations from another plugin - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/modifying-decorations-from-another-plugin/4728)
- No, that’s not something the library makes possible, you’d have to somehow arrange for the code that creates the decorations to add a hook (facet, probably) for this.
- Is there a way to list all the facets? Unfortunately they do not provide a comprehensive API or reference.
  - No. Facets are just values, and not registered anywhere centrally.

- ## [Conflicting widget and mark decorations on empty line in CM6 - v6 - discuss. CodeMirror _202108](https://discuss.codemirror.net/t/conflicting-widget-and-mark-decorations-on-empty-line-in-cm6/3487)
- Marks will wrap around widgets (and other marks) with higher precedence. So wrapping your extension in a `Prec.fallback` to make sure it has lower precedence than the lint marks might help in this case.
- I see what’s happening now—the lint module uses EditorView.decorations to provide decorations from the state, and you use a view plugin providing them through a plugin field. 🤔 Plugin decorations currently always have a higher precedence than facet decorations. Which is problematic, I guess. I’ll spend some time thinking about how to better handle that — it seems this is a good illustration of the fact that client code needs full control over the ordering of decoration precedence.
  - I have a design for providing better control over precedence, but it’d be hard to pull off in a backwards-compatibly way, so it’ll have to wait until the next major version. 

- ## 💡 [add class to gutter of line - discuss. CodeMirror](https://discuss.codemirror.net/t/add-class-to-gutter-of-line/4602)
- Creating space between lines should definitely not be done in the gutter — the gutter element positioning is based on the heights of the block elements in the content, not the other way around. 
  - A line decoration should be able to add extra padding to a line (margins on block elements are not supported), or, possibly cleaner, use a block widget decoration to add an element between the lines.

- ## 🤔💡 [Preferred way to create multi-line widget? - discuss. CodeMirror _202208](https://discuss.codemirror.net/t/preferred-way-to-create-multi-line-widget/4865)
- Directly via EditorView.decorations. Put the decorations in a state field, not a plugin, so that they are available before the viewport is computed.

- If you want to render widgets that are guaranteed to be only inline (i.e. Markdown links), then you should define a ViewPlugin. Those get called after the viewport has been created and are therefore much cheaper. Also, you can make use of the `view.visibleRanges`-property which enables you to only render those widgets for any actually visible ranges (i.e. must be within the viewport and additionally not be folded).
  - The example for inline-only-widgets is the Boolean Toggle Widgets example
- If you have widgets that may also be block-level and not just inline you have to, as Marijn said, call StateField.define(). You can – more or less – provide the same logic to compute the widgets, but since StateFields are computed prior to rendering, you can also provide block-level widgets.
  - The example for the inline and block widgets is the Underline command example. (The trick is to understand that you can also underline pieces of text that span line breaks, even if you don’t underline full lines. To me, for the past weeks, it always seemed to me inline-only just as well.)
# discuss-widget/void/form/input
- ## 

- ## 

- ## 

- ## 

- ## 💡 [the block widget disappeared after add or remove a new line - discuss. CodeMirror](https://discuss.codemirror.net/t/the-block-widget-disappeared-after-add-or-remove-a-new-line/4855)
- I tried to simulate the onchange event here but don’t know how to do it properly. I am using a react version of CM
  - If by onChange you mean updateListener, that’s expected. If you need to track state for changes, and use that for rendering, you’re probably going to have a better time keeping it in a state field.

- ## 🌰 [Cursor to skip Decoration.replace - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/cursor-to-skip-decoration-replace/3902)
- You may be looking for atomicRanges
- I’ve been following the boolean toggle widget example but building a replace decoration instead of a widget and I want to make them atomic.

- ## [How to get folded source code inside foldWidget.toDOM() from @codemirror/fold - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-get-folded-source-code-inside-foldwidget-todom-from-codemirror-fold/3527)
- toDOM should just render the data that’s already in the widget object, not access anything external.

- ## [How to wrap a range in an element - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-wrap-a-range-in-an-element/8341)
  - When I traverse the snytax tree and come across Frontmatter, I would like to wrap the entire Frontmatter range in a div. is this possible?
- No, it’s not possible to wrap a bunch of lines in a DOM element. You can style the lines with line decorations, but you cannot create any structure bigger than a line, except if you replace the entire set of lines with an (uneditable) block widget decoration.

- ## [Recomputing gutter heights for line widgets - discuss. CodeMirror](https://discuss.codemirror.net/t/recomputing-gutter-heights-for-line-widgets/4351)
- You can call `EditorView.requestMeasure` to ask the view to measure its content again when something changes dynamically.

- ## [Best way to update widgets live while typing? - discuss. CodeMirror](https://discuss.codemirror.net/t/best-way-to-update-widgets-live-while-typing/3691)
  - What’s the best way to update those widgets as the user is typing in the document
- You could use `transaction.changes` to determine which range is changed, and only re-scan lines around that, using `RangeSet.update` to update the set of widget decorations.

- ## [How to recognise if a widget is removed ? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-recognise-if-a-widget-is-removed/8180)
- You could do a check where you see if the range set’s size changed after mapping, and if so, do a scan through it to figure out which widget that you still have in your outside data was removed.
  - i was able to do it how you suggested, the Decoration as RangeSet got everything I needed

- ## [How to use decoration widget as a function arguments - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-use-decoration-widget-as-a-function-arguments/7793)
- You could add a `mousedown` handler to the widget that causes its extent to be selected, and set up the plugin that displays these to render those that are precisely selected as highlighted.

- ## 🌰 [Link widget is clicked only if editor is out of focus - v6 - discuss. CodeMirror _202311](https://discuss.codemirror.net/t/link-widget-is-clicked-only-if-editor-is-out-of-focus/7433)
- The issue is that your widget doesn’t define an eq method (and generally isn’t set up to be easily comparable), causing the editor to re-render it every time you recreate your decorations. This causes the link you’re clicking to disappear as the editor loses focus, breaking the browser’s native behavior.

- ## [Atomic widget example - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/atomic-widget-example/4986)
- You’re not including any key bindings, so you’re getting the browser’s native cursor motion and deletion behavior, which doesn’t know about the atomic ranges. Include the default keymap.

- ## [Gutter marker next to decoration-replaced lines with a widget - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/gutter-marker-next-to-decoration-replaced-lines-with-a-widget/7075)
  - I want to show my own gutter marker next to block widget that’s created through Decoration.replace

- ## [Is view.requestMeasure required when a block widget changes height? - v6 - discuss. CodeMirror _202301](https://discuss.codemirror.net/t/is-view-requestmeasure-required-when-a-block-widget-changes-height/5604)
  - I have a block widget which renders its contents asynchronously. 
  - The documentation says that the widget should call view.requestMeasure if the height of the widget changes
  - However, it seems in my experience so far that the editor’s height map is correct even if the block widget doesn’t call view.requestMeasure.
  - Is it always a requirement to call view.requestMeasure() after updating the contents of a widget, if the height changes?

- recent versions of @codemirror/view will also automatically remeasure themselves when the content height changes.

- ## [block widgets display on mouse event - discuss. CodeMirror](https://discuss.codemirror.net/t/block-widgets-display-on-mouse-event/4790)
  - change block widget content when the mouse hover over a code block.
- There’s no automated way to do that – you’ll have to listen to mouse events to detect the hover, and replace the widget.
- how can i update the widget content inside the event handler. I wonder what triggers the widget update?
  - You should be able to use a plugin that exposes decorations, change the decoration set on the appropriate DOM effects, and call `view.update([])` to have the view redraw the decorations.

- ## [Inline widgets that come directly after a block widget do not work well _202305](https://github.com/codemirror/dev/issues/1165)
- This is by design — block and inline widgets cannot be freely mixed like this, and their side values are not in the same space. 
  - Block widgets not on line boundaries are tricky to define in general, and in fact only allowed because forbidding them would be even more complicated than supporting them
- Attached patch adds an option ( `inlineOrder` ) to widget decorations that should make this possible. This behavior would be somewhat error-prone by default when multiple independent extensions are placing widgets at a position, so I've made it opt-in.

- ## 🌰 [How to get focusin events on a custom widget decoration - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-get-focusin-events-on-a-custom-widget-decoration/6792)
  - I’m adding a custom widget decoration (a contenteditable div) and would like to receive focusin events for this widget. 
  - While I can get a mousedown event with event.target set to this contenteditable div, the focusin event which follows it has event.target set to the div containing the entire CodeMirror editor. 
- Look at `WidgetType.ignoreEvent` – I suspect the editor is handling events in your widget that it shouldn’t, and thus claiming back focus when it is clicked.

- ## 🌰 [Positioning block-level widgets - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/positioning-block-level-widgets/3060)
- The problem is that you are using a view plugin to insert height-influencing decorations.
  - Block widgets should definitely be kept in a state field.
- It turns out the weird behavior I was experiencing was caused by adding a vertical margin to my block widget
  - Oh, indeed, margins between block elements will confuse the editor. Any whitespace should be kept inside of your element. I’ve updated a doc comment to mention this.

- ## [Editable Decoration Widget for inline editing encrypted/decrypted text - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/editable-decoration-widget-for-inline-editing-encrypted-decrypted-text/4276)
  - The goal is, that the user will never see the encrypted text and can edit the decrypted text like a normal text value, but in the background the encrypted text will be updated
  - i don’t find any way making an inline edit possible. Even when using a html-input, the textbox cannot get focus and the cursor will be placed before or after the input field.
- I suspect the problem is in your ignoreEvent method. By letting the editor handle all evens in your widget, you are preventing direct interaction with it. return true might help a lot (though possibly you’ll want to return false for some events, such as drag events that target the outer widget element).

- ## 🌰 [Inability to use ::selector with an `<input />` widget when using the `drawSelection` plugin - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/inability-to-use-selector-with-an-input-widget-when-using-the-drawselection-plugin/8182)
  - I’m trying to add an inline input (as a widget) to my editor
  - One of the main things I haven’t managed to sort out yet is getting the selection styling back so that you can actually see text you’ve selected.
  - After a little digging, I have found that it is the presence of the `drawSelection` plugin which is breaking `::selection` (which makes sense). 
  - another issue I’m having is how to make the `<input />` autofocus when it is rendered. I can technically make it work by adding a setTimeout or requestAnimationFrame right before I return the DOM element in toDOM, but obviously I don’t want to actually do that.

- ## [CodeMirror 6 Input Widgets - Implementations - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-6-input-widgets-implementations/7690)
- Chrome devtools has a slider type thing when you hover over numbers in the CSS inspector, which may be similar to what you’re looking for (but isn’t a widget).

- ## 💡 [Focusing inputs within widgets - v6 _202210](https://discuss.codemirror.net/t/focusing-inputs-within-widgets/5178)
  - I have noticed that it’s very difficult to “steal” the focus from the editor DOM and apply it to my own widget. Basically, if a user clicks on an element, that element has focus for a fraction of a second and then the editor element itself regains focus.
  - EDIT: If I move the contenteditable field into a child element, it works as expected

- Widgets intentionally always get set to `contenteditable=false` , or they would become part of CodeMirror’s editable content element. 
  - You should be able to introduce new `contenteditable=true` child elements inside of them.
# discuss-markdown
- ## 

- ## 🌰 [Conditionally-rendered block replace decoration breaks selection rendering and gutter · Issue · codemirror/dev _202407](https://github.com/codemirror/dev/issues/1406)
- I can see it behaving weirdly that way. This was an update issue where some parts of the view state didn't get recomputed though they should, for decoration changes like that, even if the resulting block heights didn't change. Attached patch should help with that.

- ## 🤔 [Conditionally showing Widgets using a StateField - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/conditionally-showing-widgets-using-a-statefield/6020)
  - I’m trying to make sure those decorations only show when the cursor is NOT within the image tag. The idea is to have inline images throughout the document that are only visible when the user is not actively editing the image tag itself.
  - I started writing code the StateField’s update method to update/filter the RangeSet that’s returned based on cursor position, but it’s not working as expected. Is there a better way to accomplish this?

- No, this seems reasonable. As an optimization, you might be able to keep both the ‘full’ range set and the filtered one — have update logic that checks if the cursor is inside a range in the full set, returns the full set if not, and a filtered version if so.

- ## [Using a Decoration instead of a markdown code block postprocessor - Developers: Plugin & API - Obsidian Forum _202404](https://forum.obsidian.md/t/using-a-decoration-instead-of-a-markdown-code-block-postprocessor/79718)
  - I’ve developed a plugin that postprocesses Markdown code blocks that have an iframe language tagged on them, and then runs any JavaScript in that code block inside of an iframe.
  - It looks like Obsidian has its own Markdown flavor, hypermarkdown, and the syntaxTree that you get if you write a ViewPlugin or StateField is that, and there doesn’t seem to be an actual element type for code blocks.
  - Are there any plugins that do this, or documentation for it? Meaning, a plugin that exposes a ViewPlugin or StateField and uses the syntax tree generated in order to get the code within a code block?

- are you using: registerMarkdownCodeBlockProcessor ? That works in both reading mode and live preview.

- ## [Hide markdown syntax - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/hide-markdown-syntax/7602)
- that’s what atomicRanges does—causes the whole range to be treated as a single thing for the purpose of cursor motion and backspacing. Some systems like this show the marks as text again when the cursor is on/near them.

# discuss-folding/hide/replace
- ## 

- ## 

- ## 

- ## [Code folding for PostgreSQL doesn't work as expected. - v6 - discuss. CodeMirror _202403](https://discuss.codemirror.net/t/code-folding-for-postgresql-doesnt-work-as-expected/7993)
- You can use `foldService` to provide custom, non-syntax-tree-based fold ranges if you want.

- ## [a display bug - discuss. CodeMirror](https://discuss.codemirror.net/t/a-display-bug/4074)
  - i find that when i set parent node’s style display to none of CodeMirror, then use the replaceSelection() API to replace some contents, and then i set parent node’s style display to block, the contents of CodeMirror didn’t change until after i click the editor area. is this a bug?
- No, refresh() is the way to solve this. The editor has no way to notice that it became visible.

- ## 💡 [Replacing keywords in text as they are written - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/replacing-keywords-in-text-as-they-are-written/4123)
  - my question is not so much about how to perform the text replacements but about what is the best way to trigger those replacements as the content is edited.

- You could use a `transactionFilter` that checks whether the text around any of the changed ranges (tr.changes.iterChangedRanges) the new doc matches your keyword, and adds an additional transaction that changes them when it does (`return [tr, {changes: [...], sequential: true}]`).

- ## [How to add line class to a specific line dynamically - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-line-class-to-a-specific-line-dynamically/6230)
- You set up an extension, similar to the zebra stripe example, that maintains line decorations for the lines that you want to style, and updates them as appropriate on transactions.

- ## [Widget on right side of line - v6 - discuss. CodeMirror _202310](https://discuss.codemirror.net/t/widget-on-right-side-of-line/7235)
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

- ## [Updating block-widgets // What is the order of the state update cycle, exactly? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/updating-block-widgets-what-is-the-order-of-the-state-update-cycle-exactly/8365)
- I suspect, from your message, that you’re mutating your decorations, and expecting the method to run then? That’s not how these work—they are immutable like everything else you store in your state. You replace them with a widget of the same type to have updateDOM called.

- ## [Block decoration and gutter line numbers - discuss. CodeMirror](https://discuss.codemirror.net/t/block-decoration-and-gutter-line-numbers/3710)
- You should always use state decorations for block decorations or other height-influencing things. I haven’t found a way to cheaply check this at run-time, but the docs mention it.

- ## 🆚 [View Plugin vs. State Field for inline replacements with line wrapping - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/view-plugin-vs-state-field-for-inline-replacements-with-line-wrapping/8129)
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

# discuss-decoration
- ## 

- ## 

- ## 

- ## [How to insert text with decorations? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-insert-text-with-decorations/7704)
- If you use `view.state.changes` to create a `ChangeSet` object for your changes (which you can also `dispatch` ), you can use that to map positions from the document space before the change to after. 
  - Also probably makes sense to dispatch both the changes and the decorations in a single transaction.

- ## [How to add decoration without focusing the editor on dispatch? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-decoration-without-focusing-the-editor-on-dispatch/6283)
- What was going on was that the DOM changes needed to apply that update messed up the DOM selection, which was still in the editor despite it no longer having focus. And restoring a proper DOM selection apparently randomly moves focus back into the editor. This patch tries to detect and undo this phenomenon.

- ## [Make decoration editable within non-editable instance - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/make-decoration-editable-within-non-editable-instance/5190)
- I guess you could simply use a transaction filter. See the single-line editor example

- ## [How to retain higher-order highlight style with Decoration.replace() - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-retain-higher-order-highlight-style-with-decoration-replace/3279)
- Decorations with lower precedence now produce parent nodes wrapping the nodes created by decorations with higher precedence.
  - I think the best way to find the bold text would be to iterate through the syntax tree—and that should also give you information about the text’s parent nodes, making it relatively straightforward to add classes for those.

- ## 🗑️ [how to delete widget decoration when I press delete key? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-delete-widget-decoration-when-i-press-delete-key/3753)
- The editor itself won’t do that (the command bound to delete by default just deletes text in the document, and isn’t aware of any non-document elements you may be showing), so you’d have to bind a custom command that notices the cursor is before such a decoration and somehow instructs the extension managing the decoration to remove it to delete (at a higher precedence than the default binding).

- ## 🗑️ [Prevent user to delete decoration - discuss. CodeMirror](https://discuss.codemirror.net/t/prevent-user-to-delete-decoration/5793)
- A change filter can be used to block certain kinds of changes. I’m not sure about preventing copying. Possibly a transaction filter that prevents the first character from ever being selected is what you want.

- ## 🗑️ [Backspace on decoration with atomic ranges not working correctly - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/backspace-on-decoration-with-atomic-ranges-not-working-correctly/6641)
- atomicRanges affects keyboard cursor motion and deletion, but does not prevent selections that point into the ranges in general. You could use a transaction filter if you want to guarantee that no functionality ever puts a selection end at some position.

- ## [Prevent cursor position before a widget at the start of a line - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/prevent-cursor-position-before-a-widget-at-the-start-of-a-line/5745)
- is it possible to place a widget decoration at the start of a line in such a way that the cursor can only be positioned on the line after the widget, not before it?
  - A transaction filter is probably the best way to do this.

- ## [Conflicting widget and mark decorations on empty line in CM6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/conflicting-widget-and-mark-decorations-on-empty-line-in-cm6/3487)
- 

- ## 🆚 [Detect cursor motion into atomicRanges widget - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/detect-cursor-motion-into-atomicranges-widget/6399)
  - I tried transactionFilter it works by its own flawlessly. However, I don’t know how to prioritize it over atomicRange features.

- If you don’t want the atomic range treatment, it seems you could just avoid marking your ranges as atomic, no?
  - After two days, I have realized, I probably need to implement a custom version of atomicRanges where one could control this behavior, then there is no need in making more complicated version of atomic ranges.

- ## [How to add classes to lines? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-add-classes-to-lines/3039)
- after digging in a bit more, the piece I’m struggling with now is figuring out how to dig into the markdown parser to determine whether a given line is part of a code block
  - Iterating over the syntax tree is probably the easiest approach.

- ## 💡 [unable to decorate codeblocks/fenced code - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/unable-to-decorate-codeblocks-fenced-code/7585)
  - I want to decorate the whole code block or fencedCode
- You’d have to iterate over the lines touched by a given code block and add a decoration at the start of each.

- ## 🌐️ [Translate block of text between view and state - v6 - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/translate-block-of-text-between-view-and-state/6913)
- You can replace pieces of the document with other content (using `Decoration.replace` ), but that content won’t be editable, so this doesn’t sound like it would do what you want. 
  - I think you’ll need to do something like this at another level than the editor-view level—i.e. put the translated content in the editor state, possibly along with information about the position and origin of translated blocks, and do the translation outside of it.

- ## ⏱️ [Creating a Decoration that updates on an interval - v6 - discuss. CodeMirror _202210](https://discuss.codemirror.net/t/creating-a-decoration-that-updates-on-an-interval/5121)
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
