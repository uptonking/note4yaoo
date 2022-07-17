---
title: lib-editor-ckeditor5-react
tags: [ckeditor, lib, react]
created: 2021-11-07T11:01:44.444Z
modified: 2021-11-07T11:02:15.399Z
---

# lib-editor-ckeditor5-react

# guide

# faq-repeat

## 如何在ckeditor插件中更新react组件的状态

- model变化后，会自动触发downcast，rerender整个react组件

## 如何在react组件中更新ckeditor的数据

- 在react组件中更新ckeditor的model
  - 通过预定义command，editor.execute('cmd', args)

- 在react组件中更新ckeditor的editing view

## [Update CKEditor config on the basis of React state](https://stackoverflow.com/questions/59907888)

- 如何动态修改配置的问题
  - 思路是将可配置的部分做成state，初始化时就设置state，之后更新state即可，
  - 可考虑添加新的配置项到配置对象，而不是重新创建配置或插件对象

- getEditorConfig which would give me the changed config 
- Next a helper function which creates a new editor instance and adds it to the DOM.
- In one of the issues, it is suggested to destroy the old editor and create a new one when you want to update the config.
- destroy old editor instance and use the addEditor function to create a new one. 
  - The getEditorConfig should give you the updated config you wish to apply for the new editor.

- [Changing configuration options of a CKEditor instance](https://stackoverflow.com/questions/7636277)
  - Usually the configuration options will work only upon creation. 
  - You might be able to perform some tricks and so get some of the options to work at a later time, but that's usually more difficult.

- How to change CKEditor 5 plugin configuration programmically
  - simply destroy existing editor instance and create new one with updated configuration

## 如何更新ckeditor的config

- [How to change the editor configuration dynamically?](https://github.com/ckeditor/ckeditor5-react/issues/193)
  - Currently, there's a way to restart the editor when the component's `id` property changes 
  - When `id` property changes, the component restarts the editor with new data instead of setting it on an initialized editor.
  - There's no other way to change the editor configuration dynamically for now

- [Dynamic toolbar configuration options](https://github.com/ckeditor/ckeditor5/issues/7383)
  - I was always against dynamic config as it creates many problems
  - In my opinion, it should be opt-in by the plugin authors

- [How can i change config dynamically?](https://github.com/ckeditor/ckeditor5-react/issues/122)
  - You can't change the config dynamically on a ready editor's instance. 
  - If you'd like to update the editor with a new config, **you should destroy it and initialize once again with the new config**.
# faq
