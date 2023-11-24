---
title: toc-lib-editor-text-examples
tags: [editor, examples, toc]
created: 2022-11-08T18:50:30.566Z
modified: 2022-11-08T19:03:33.865Z
---

# toc-lib-editor-text-examples

# popular

# textarea
- react-markdown-editor-lite /833Star/MIT/202207/ts/markdown-it/非所见即所得
  - https://github.com/HarryChen0506/react-markdown-editor-lite
  - https://harrychen0506.github.io/react-markdown-editor-lite/
  - 基于textarea和React的markdown编辑器，实现简单且清晰
  - UI可配置, 如只显示编辑区或预览区，支持编辑区和预览区同步滚动

- https://github.com/inokawa/rich-textarea
  - https://inokawa.github.io/rich-textarea/
  - A small customizable textarea for React to colorize, highlight, decorate texts, offer autocomplete and much more.
  - designed to behave as native textarea as much as possible. Supports formik and react-hook-form. 
  - IME composition handling: IME related events have some cross browser problems. This library handles them for easy to use.

- https://github.com/uiwjs/react-textarea-code-editor
  - A simple code editor with syntax highlighting.
  - 只依赖rehype、react

- https://github.com/Resetand/textarea-markdown-editor  /ts
  - UI headless simple markdown editor using only textarea
  - 依赖react
  - You can choose any markdown parser, create your own layout, and use your own textarea component that is styled and behaves however you like

- text-editor /394Star/apache2/202011/js/NoDeps
  - https://github.com/GoogleChromeLabs/text-editor
  - https://googlechromelabs.github.io/text-editor/
  - simple text editor designed to experiment with and demonstrate the new `File System Access API`s.
  - 编辑器基于textarea，撤销重做基于浏览器而不是自己实现

- https://github.com/fregante/indent-textarea
  - Add editor-like tab-to-indent functionality to `<textarea>`, in a few bytes

- https://github.com/hzpeng57/plain-text-editor /ts/vue
  - A plain text editor (based on textarea)

- https://github.com/taufik-nurrohman/text-editor /202304/js
  - https://taufik-nurrohman.github.io/text-editor
  - Text Editor is a simple JavaScript application that aims to provide accessibility improvements to the native HTML `<textarea>` elements
  - 侧重api，过于简单
  - https://github.com/taufik-nurrohman/text-editor.history
    - http://taufik-nurrohman.js.org/text-editor.history

- https://github.com/lovasoa/react-contenteditable
  - React component for a div with editable contents

- https://github.com/FormidableLabs/use-editable
  - `useEditable` is a small hook that enables elements to be `contenteditable` while still being fully renderable. 
  - This is ideal for creating small code editors or prose textareas in just 2kB!
  - there have been three options when choosing editing surfaces
    - full control with prosemirror-like
    - contenteditable
    - textarea
  - use-editable creates a `MutationObserver`, which watches over all changes that are made to the `contenteditable` element. 
    - Before it reports these changes to React it first rolls back all changes to the DOM so that React sees what it expects.
    - it also preserves the current position of the caret, the selection, and restores it once React has updated the DOM itself. 
    - This is a rather common technique for `contenteditable` editors, but the `MutationObserver` addition is what enables `use-editable` to let another view library update the element's content.
    - Since use-editable doesn't aim to be a full component that manages the render cycle, it doesn't have to keep any extra state, but will only pass the DOM's text back to the onChange callback.
# computational-editor
- https://github.com/jaredreich/calcutext
  - Calcutext is a web app where you can do calculations with your written text.
  - Write any math operations, as available in `mathjs`, as a series of written lines to make notes and do calculations
# apps
- https://github.com/Novout/betterwrite /ts/vue
  - A Open Source Word Processor
  - 依赖milkdown、vue
  - Offline First
  - Better Write works with the Entity Model, where each item in the editor is unique and independent of other content.

- https://github.com/AlexJCturbo/text_editor
  - a single-page application that runs in the browser. The app meets the PWA criteria.

- https://github.com/dannyyyspam/Text-Editor
  - (PWA) Challenge: Text Editor (J. A. T. E.)
  - Create a text/code editor that functions on a single page, follows PWA criteria, and works offline. 

- https://github.com/a6enez3r/teret
  - blogging application with a WYSIWYG editor built using Flask + SummernoteJS + SQLite (or any other relational database supported by SQLAlchemy)

- https://github.com/michael/editable-website
  - A SvelteKit template for coding completely custom website, while allowing non-technical people to make edits to the content by simply logging in with a secure admin password.password.
  - 依赖prosemirror、postgres、minio-s3-like、svelte
  - https://twitter.com/_mql/status/1655553156799922180
    - The editable infrastructure is loaded async, so that you are not shipping additional JavaScript for regular website visitors.
    - To save changes, all you have to do is sending a request to your API for persistence. In my case, I store the content in a Postgres database.
    - I kept things really simple for the first few websites I built with this approach. No caching, no permission management, no post scheduling. The admin can do anything and by hitting save, changes are live.
    - 注意git version可能丢失
# utils
- https://github.com/DenverCoder1/unicode-formatter
  - https://unicode-formatter.demolab.com/
  - Convert portions of text to fancy text using unicode fonts for use on Twitter and other sites that don't support rich text
# more
- https://github.com/leewhui/text-effect-editor
  - https://ephemeral-druid-42201c.netlify.app/
  - 一个在线 web app 去编辑字体特效，参考了 canva(可画) 的效果和实现。

- https://github.com/gfrancine/mnote
  - Mnote: a desktop app to write notes in more than just text
