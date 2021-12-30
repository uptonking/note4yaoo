---
title: lib-editor-ckeditor5-issues
tags: [ckeditor, issues]
created: '2021-12-23T17:45:57.273Z'
modified: '2021-12-23T17:46:12.581Z'
---

# lib-editor-ckeditor5-issues

# plugin

## [How to pass data to a plugin?](https://github.com/ckeditor/ckeditor5/issues/5611)

- You should be able to use `editor.config`

## [Unable to update Collection after Adding it to Editor Config ](https://github.com/ckeditor/ckeditor5/issues/8172)

- 20200928
  - At this moment we do not support dynamic nor asynchronous configurations. 
- For your problem:
  - You could fetch your data asynchronously and then feed it to the editor config when using the create method.
  - Store the asynchronous data outside the editor config.
  - Update the config using `editor.config.set()`.

## [Dynamic toolbar configuration options](https://github.com/ckeditor/ckeditor5/issues/7383)

- I was always against dynamic config as it creates many problems:
  - Which properties should be dynamic? There are some which cannot be due to immense technical issues that that would cause. There are some that will never be changed by anyone. So, the ROI here would need to be checked for every case.
  - The above means that the developer will have to change which property is dynamic anyway.
  - Some properties (e.g. lists of some values) might need a smarter way to be changed than just being overridden.
  - The complexity will rise with every such property.
