---
title: lib-editor-app-community-contenteditable
tags: [community, contenteditable, editor]
created: 2023-06-16T02:52:41.895Z
modified: 2023-06-16T02:53:00.115Z
---

# lib-editor-app-community-contenteditable

# guide

# discuss
- ## 

- ## 

- ## 

- ## [What are the cons of using a contentEditable div rather than a textarea? - Stack Overflow](https://stackoverflow.com/questions/5284193/what-are-the-cons-of-using-a-contenteditable-div-rather-than-a-textarea)
- contenteditable="true". 
  - The major benefit is it has **auto-adjust height** as user input text/content. 
  - Also it supports rich text inside. You can mimic the Textarea by setting a max height if need.
- if you want auto height in Textarea, you might have to use js to bind some listener to the oninput hook.
  - `textarea` 不会自动调整高度，不支持文字格式


- First semantically, the purpose of a textarea is to write/edit plain text whereas with contentEditable you can edit list for instance


- In divs with contenteditable="true" the content can be html formatted, e.g. text with different colors.
- 
