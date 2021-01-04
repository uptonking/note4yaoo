---
title: lib-editorjs-docs
tags: [docs, editorjs]
created: '2020-11-16T13:20:14.528Z'
modified: '2020-12-08T13:06:30.259Z'
---

# lib-editorjs-docs

# editorjs-intro

- features
  - block-styled editor 较少了复杂度
  - clean data output in JSON
  - API designed to be extendable and pluggable

- resources
  - [awesome-editorjs](https://github.com/editor-js/awesome-editorjs)
  - [editor-config.d.ts](https://github.com/codex-team/editor.js/blob/master/types/configs/editor-config.d.ts)

- Editor.js is a block-styled editor for rich media stories. 
  - It outputs clean data in JSON instead of heavy HTML-markup. 
  - And more important thing is that Editor.js is designed to be API extendable and pluggable.

- In other classic editors, the workspace is provided by single `contenteditable` element in where you can create different HTML markup. 
  - All of us saw permanent bugs with moving text fragments or scaling images, while page parts are jumping and twitches. 
  - Or highlighting big parts of the text in the case when you just want to make few words to be a heading or bold.
  - The Editor.js workspace consists of separate Blocks: paragraphs, headings, images, lists, quotes, etc. 
  - Each of them is an independent contenteditable element (or more complex structure) provided by Plugin and united by Editor's Core.

- Classic WYSIWYG-editors produce raw HTML-markup with both content data and content appearance. 
  - On the contrary, Editor.js outputs JSON object with data of each Block.
  - You can use this data to easily render in Web, native mobile/desktop application, pass to Audio Readers, create templates for Facebook Instant Articles, AMP, RSS, create chat-bots, and many others.
  - Also, the clean data can be useful for backend processing: sanitizing(净化，删除不好内容), validation, injecting an advertising or other stuff, extracting Headings, make covers for social networks from Image Blocks, and other.

- API is the feature.
  - Each Block is provided by a plugin.
  - It's easy to create your own.
  - All main functional units of the editor — Blocks, Inline Formatting Tools, Block Tunes — are provided by external plugins that use Editor's API.
  - Any challenges and tasks you are facing can be implemented by your own plugins using the API. 

- each Block in Editor.js is provided by a Plugin. 
  - There are simple external scripts with their own logic.
  - There is the only Paragraph block already included in Editor.js. 
  - Probably you want to use several Block Tools that should be installed and connected.
  - [Link Tool for Editor.js](https://github.com/editor-js/link)

- Editor.js needs a bit time to initialize. 
  - It is an asynchronous action so it won't block execution of your main script.
  - If you need to know when editor instance is ready, you can pass `onReady` property to the configuration object
  - Similar to onReady callback, you can use the `onChange` callback to handle any modifications inside the Editor
  - Since the 2.19.0 version, Editor.js can be initialized in the read-only mode. 
    - That means that users won't have the ability to change the document content.
    - Each of the Block Tools you use MUST support the read-only mode to enable this mode in the editor.
- By default, Editor.js contains Paragraph Block included in a bundle.
  - This Blocks called `default`: it will be appended after Enter key pressing and with empty Editor. 
  - Also, it accepts paste patterns that allow rendering other Blocks by pasted URLs.
  - There is the ability to change the default Block for your own. Use the `defaultBlock` option
- You can specify the common order of Inline tools using the `inlineToolbar` property.

-To get all entry's data from Editor.js, call the `save()` method on the class instance. 
  It will return a Promise that resolves with clean data.

- A `blocks` property contains an array of objects with `type` and `data` of Editor Blocks. 
  - The values of this fields are depend on the Tools you use
  - Note that `type` field in Block data is the key of object of Editor config's `tools` property. 
    - In other words, it can be changed by you own.

# Creating a Block Tool

- In this series of articles, we will learn how to create a full-featured Block Tool step-by-step.

- We will build a Simple Image plugin that allows us to add images to our articles. 
- We need at least of two methods to create a Block Tool for Editor.js — `render` and `save`.
- The first method `render`, will create a UI of a Block that will be appended when our Tool will be selected from the Toolbox. 
- The second method `save`, will extract the Block's data from that UI.
- On saving, Editor.js will pass Block's content to the `save` method 
  - and we should implement the logic of which data we should save by our Tool. 
  - Block content is the Element returned by render with actual state of that.

``` JS
class SimpleImage {
  render() {
    return document.createElement('input');
  }

  save(blockContent) {
    return {
      //just get input's value and return our Tool's data object
      url: blockContent.value
    }
  }
}
```

- Our Block Plugin is almost done. To make that appear at the Toolbox, we should provide an icon and a title with a static getter toolbox.
- add a `tools` property to the configuration object to connect to the Editor

- When user will edit previously saved article, Editor will get saved data by the `data` property. 
  - Then the Editor will render Blocks one-by-one and pass them their data.
- We should provide a mechanism for showing saved data by our Tool. 
  - It is quite simple: data will be passed to the class's constructor, so we can save it at the property, for example this.data and access later by any method, including render

- In Editor.js each Block has a menu with actions on the right side. 
  - By default, there are such actions as moving Block up or down, Block removing etc. 
  - Block Tool have an ability to add own settings and actions to this menu.
- All you need to know for doing a Block settings is a `renderSettings` method. 
  - It will called when user clicks on the Block Actions menu.
  - We need to create our actions elements and add a handlers to them. 
  - It can be a buttons, inputs and other controls.
  - you can create any UI elements in renderSettings. 
    - So adding handlers for them is in your area of responsibility. 

- Editor passes an API object to the Tools constructor via `api` parameter. 
  - We can store it somewhere, for example in `this.api` property that can be visible from any method.

- Sometimes you need to handle pasted content with your plugin. 
  - For example, pasted headers should be handled by Header Tool and pasted images — by Image Tool.
  - Tools API allows you to substitute pasted HTML tags, Files and string patterns. 
  - To make it work you need just two things: static getter `pasteConfig` and `onPaste` method.

- Some of the Tool's fields can contain any HTML code, for example, our Caption field with Inline Toolbar enabled. 
  - It's good to be sure that saved HTML content includes only allowed tags and attributes — only created by Inline Toolbar in our case.
  - Editor.js has a build-in Sanitizer module. 

# Creating an Inline Tool

- Inline Tools allow you to make your text more informative. 
  - The simplest examples of them are bold, italic, and underline modifiers which are commonly used.
- In the next few guides you'll find step-by-step tutorial on how to create simple Marker Tool for highlighting selected text fragments.

- Every Inline Tool must provide a button — HTML element with icon or some layout — for Inline Toolbar of the Editor. 
  - When button is pressed Inline Tool receives selected text range as JavaScript `Range` object references to `TextNode` on the page. 
  - Some Tools may also provide actions for additional interactions with the user.
- To let Editor know that this Tool is inline we need to provide `isInline` static getter
- Inline Tools must provide three methods to work with Editor: render, surround, and checkState.
- `Render` method must return HTML element of the button for Inline Toolbar. 
- When user selects some text, Editor calls `checkState` method of each Inline Tool with current Selection to update the state if selected text contains some of the inline markup. 
- Finally, when button is pressed, Editor calls `surround` method of the tool with `Range` object as an argument

``` JS
class MarkerTool {

  static get isInline {
    true;
  }

  render() {

  }

  surround(range) {

  }

  checkState(selection) {

  }

}
```
- We can access the API using the `api` object passed to the Tool constructor. 
  - For Marker Tool we need styles and selection APIs.

- Editor.js sanitizes all content in several cases: on render, on paste, and on save. 
  - Each Block Tool provides sanitizer rules to let Editor know which HTML tags it should respect. 
  - However, Block Tools are not connected with Inline ones so markup added by Inline Tool will be removed on pasting or on saving. 
  - To avoid that you need to provide sanitizer rules for your Inline Tool in sanitize static getter.


