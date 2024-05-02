---
title: lib-editor-codemirror-community-v5
tags: [codemirror, community]
created: 2024-05-02T06:02:24.353Z
modified: 2024-05-02T06:02:37.181Z
---

# lib-editor-codemirror-community-v5

# guide

# discuss-v5
- ##

- ##

- ##

- ## `inputStyle: string` config prop
- https://codemirror.net/5/doc/manual.html
- Selects the way CodeMirror handles input and focus. 
  - The core library defines the "textarea" and "contenteditable" input models. 
  - On mobile browsers, the default is "contenteditable". 
  - On desktop browsers, the default is "textarea". 
  - Support for IME and screen readers is better in the "contenteditable" model. The intention is to make it the default on modern desktop browsers in the future

- ## [CM5: inputStyle contenteditable, cursor display after goLineRight (wrapped line) - discuss. CodeMirror](https://discuss.codemirror.net/t/cm5-inputstyle-contenteditable-cursor-display-after-golineright-wrapped-line/3911)
- CodeMirror 6 works around this by drawing its own cursor while still using contentEditable _202201.

- ## 🤔🆚️ [is the `textarea` inputStyle going to be deprecated in the future? - discuss. CodeMirror](https://discuss.codemirror.net/t/is-the-textarea-inputstyle-going-to-be-deprecated-in-the-future/1278)
- If there’s ever a major rewrite of CodeMirror (the codebase is showing its age), it’s likely that it will only do contentEditable-style input. But until then, I don’t expect to completely drop textarea support.

- 👉🏻 Actually, we are now working on that rewrite and only implement contenteditable as input method for v6.
  - It’s definitely going to be much better than what CodeMirror currently does in terms of contenteditable support. You’re right that there might be things you cannot customize anymore, but that also means that we use more of what the user agent provides.

- ## [What are the pitfalls of using inputStyle 'contenteditable' in 2020? ](https://discuss.codemirror.net/t/what-are-the-pitfalls-of-using-inputstyle-contenteditable-in-2020/2389)
- The CodeMirror integration with contentEditable is more buggy and less well tested. You might run into issues. 
  - On mobile, it’s a lot better than nothing, 
  - but on desktop, to not create unnecessary regressions, we’re keeping textarea the default.
