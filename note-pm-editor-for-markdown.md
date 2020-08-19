---
title: note-pm-editor-for-markdown
tags: [editor, markdown, pm, product]
created: '2019-08-22T03:45:48.886Z'
modified: '2020-07-14T13:06:18.368Z'
---

# note-pm-editor-for-markdown

## summary

- 与交互相关的操作非常容易与编辑器的功能产生联系
- 可以考虑通过提供某一类的拖拽组件代替一类应用场景的editor/builder

## features

- table editor for markdown

## markdown-editor-as-component

- editor-plugins
  - keyboard-shortcuts:preview, bold, checkbox, newLine
  - list-editing-sugar:enter, tab, delete
  - export & print    
  - import
  - auto-completion
    - math
    - link
    - @username
    - predefined-text-suggestion
  - toolbar
  - img-upload
  - word-counter
  - collapsible

- md-extension
  - gfm
      - checkbox-task-list
      - automatic-linking
      - strikethrough
      - table
      - emoji
      - syntax-highlight
      - github-only
          - issue-reference
          - username-mention
  - toc
  - footnote
  - mathTeX: formula
  - flowChart

## solution-catalog-editor-for-markdown

- https://github.com/kkfor/for-editor
- https://github.com/uiwjs/react-md-editor
- https://nhn.github.io/tui.editor/latest/ToastUIEditor
- https://github.com/RIP21/react-simplemde-editor
- https://github.com/sparksuite/simplemde-markdown-editor
- https://github.com/pandao/editor.md
- https://github.com/tuture-dev/editure
- https://github.com/andrerpena/react-mde
- https://github.com/HarryChen0506/react-markdown-editor-lite
- https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
