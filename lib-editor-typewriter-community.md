---
title: lib-editor-typewriter-community
tags: [community, typewriter]
created: 2023-02-09T12:24:36.461Z
modified: 2023-02-09T12:24:51.366Z
---

# lib-editor-typewriter-community

# guide


# not-yet

- ## [Collaboration · Issue](https://github.com/typewriter-editor/typewriter/issues/21)
- We have a cursor embed to show where the cursor of a friend is as a good start. 
- We should provide documentation or guides on creating backends for this, but I feel Typewriter shouldn't do any of that itself. It could be different packages. Typewriter's scope should be limited to exposing methods for receiving changes from elsewhere, but not connection etc.

- ## [Table support · Issue ](https://github.com/typewriter-editor/typewriter/issues/6)
- Table support requires 3 main areas of discussion and development.
  - The data model for storing tables
  - The UI for making it easy to manage tables
  - The commands needed to manage the data

- First, for the data model, my first thought was to make each row a block and separate cell content with a tab (\t) character. This maps well to CSV with tabs and newlines.
- Another idea is to make each cell a block. This gives us the ability to do a lot more such as joining cells (which I don't like much since you don't see a lot of spanning needs in most rich text editors and it makes the UI more complex).



# discuss
- ## 

- ## [Potential Change: More extensible base modules ](https://github.com/typewriter-editor/typewriter/issues/72)
  - I am working on a project that intends to create an editing experience similar to Typora. In order to achieve this, I will need to change some fundamental assumptions that the default modules take.
  - However, their current structure as raw functions makes the process of making small tweaks essentially require duplicating all logic into a new module. This means any bugfixes to the base module would need to be manually pulled over (and I'd need to be aware of them).
  - It would be awesome if these could be classes that could then be extended and their functions overridden.


- I like the closure style a lot, and really don't want to change it. But I can see how this would be beneficial for extension.



- ## [Using both MutationObserver and input event](https://github.com/typewriter-editor/typewriter/discussions/63)
- I wanted to jot down the reasons behind the decision to use `MutationObserver` as the main input recognition channel with input event as the fallback. Also note, this is implemented as a module (input) and can be replaced in the future or on a case-by-case basis if we find better solutions and as browsers progress.
  - The Android keyboard GBoard is buggy and doesn't fire the events it should for contenteditable changes. For this reason and the greatest compatibility with autocomplete and text-composition, we use MutationObserver to know when content has been edited within the editor.

- ## [Why doesn't Typewriter use Svelte to render the text content?](https://github.com/typewriter-editor/typewriter/discussions/61)
- I wanted to use Svelte. I thought it would be perfect. However, I couldn't get around certain problems in a cross-browser compatible way that didn't hurt text composition and auto-complete with mobile devices.
- An empty paragraph needs to have a `<br>` tag in it to keep it from collapsing to 0px-height. Typewriter needs to add this `<br>` in, and can do so with Svelte. However, in contenteditable, if you place the cursor in the paragraph and type a letter, the `<br>` is removed from the DOM and a text node is created. Listening to a mutation observer or input event you can read the change from the DOM and update the data model of the editor, then Svelte will update the paragraph to match the data. It tries to remove the `<br>` and throws an error because the Svelte code to do that is br.parentNode.removeChild(br) and the parentNode is null. In addition, Svelte will add a new text node to represent the letter typed, making the letter appear twice. Svelte just doesn't work well with DOM that changes out from under it. Many VDOM libraries don't either, so I had to repurpose one to do so.
- I tried several workarounds. Using the beforeinput event to stop the input so the DOM doesn't change, then updating the model and allowing Svelte to render it, works. It works until you need text composition, such as Korean or Japanese, or to type é. It also doesn't work with autocomplete and swype keyboards on the default Android keyboard and some iOS issues too. Android is also quite buggy with beforeinput with the GBoard keyboard which is Google's default.
- Using a MutationObserver to capture the changes, then reversing everything that happened in the mutation observer (putting nodes back into the DOM and removing those that were added), allowed Svelte to work, technically. It allowed the autocomplete, but it still didn't work with text composition.
- All this being said, the rendering is actually implemented as a module, so if we figure out a nice way to allow Svelte to do that, we can create a Svelte renderer module to replace the existing one and still remain backwards compatible for others.

- ## [What is the recommended way to store data in a database/create a controlled editor component?](https://github.com/typewriter-editor/typewriter/issues/66)
- `editor.getHTML() and editor.setHTML(value)` would work better for rich text. 
  - 👉🏻 If you can save JSON to your store, saving `editor.doc` and restoring it with `editor.set(doc)` is even better.
