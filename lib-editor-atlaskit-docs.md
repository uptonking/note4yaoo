---
title: lib-editor-atlaskit-docs
tags: [atlaskit-editor, docs, editor]
created: 2021-07-12T17:18:03.886Z
modified: 2021-07-14T15:36:23.541Z
---

# lib-editor-atlaskit-docs

> Atlassian editor core functionality

# guide

# overview

- @atlaskit/editor-core /Apache2/ts
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/
  - https://github.com/pioug/atlassian-frontend-mirror
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - A package contains Atlassian editor core functionality
  - 基于react class组件实现
  - 提供了针对image/file的图文混排工具
  - 还提供了多列布局工具，包括两栏、三栏、按比例、居中
  - 提供了语法树ADF显示
  - https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
    - copy the approach by Atlassian editor_v20201205

- editor-core依赖
  - 全家桶: @atlaskit/design-system-*, @atlaskit/editor-common/json/markdown/tables, prosemirror-collab/transform/utils
  - 工具: classnames, data-fns, eventemitter2, fuse.js, lodash, memoize-one, raf-schd, rusha, uuid
  - 格式: markdown-it
  - react: styled-components@3, react-intl@2, re-resizable, react-loadable, react-select, react-transition-group, react-virtualized
# examples
- [kitchen-sink-example](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - with-datasource 提供了一个经典的无限滚动表格示例

- [Lazy node example - Editor core](https://atlaskit.atlassian.com/examples/editor/editor-core/lazy-node-example)
  - Main Editor 的修改会立即同步到 Fallback Editor, 但fallback editor的修改不会主动同不到main editor

- [Full page with confluence lazy smart cards - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/full-page-with-confluence-lazy-smart-cards)

- [Node data providers - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/node-data-providers)
  - There are various cache layers outside the node view data provider. Which means that the first time you open an example will be the most accurate (as subsequent opens will have various parts cached).

- [Diffing - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/diffing)
  - 效果是，手动输入old/new doc, 点击compare显示上下布局的diff视图

- [Collaborative editing - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/collaborative-editing)

- [Collab - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/collab)

- [Annotation experiment - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/annotation-experiment)
  - 评论，可resolve

- [Table perf test - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/table-perf-test)

- [Ssr tables - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/ssr-tables)

- [Scaled editors - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/scaled-editors)

- [Resizer basic - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/resizer-basic)
  - 支持配置resize-handler大小、snapGap

- [Testing - Editor core - Atlassian Frontend Development](https://atlaskit.atlassian.com/examples/editor/editor-core/testing)
  - You're viewing an editor example page intended to be initialised and run via Playwright
# [docs](https://atlaskit.atlassian.com/packages/editor/editor-core)
- polyfills
  - promise
  - fetch
  - element.closest

- simplest editor starter

```JS
import { Editor } from '@atlaskit/editor-core';

<Editor appearance="comment" />;
```

- Editor with mentions
- Collapsed Editor

- `EditorContext` allows you, in conjunction with `WithEditorActions`, to manipulate the editor from anywhere inside the `EditorContext`. 

## props

- appearance
  - comment
    - you have a field input but require a toolbar & save/cancel buttons
  - full-page
  - chromeless
    - essentially the comment editor but without the editor chrome, like toolbar & save/cancel buttons
  - mobile
    - should be used for the mobile web view. 
    - It is a full page editor version for mobile.

## [Atlassian Document Format(ADF)](https://developer.atlassian.com/cloud/jira/platform/apis/document/structure/)

- Atlassian Document Format (ADF) represents rich text stored in Atlassian products. 
  - For example, in Jira Cloud platform, the text in issue comments and in `textarea` custom fields is stored as ADF.
- An Atlassian Document Format document is a JSON object. A JSON schema is available to validate documents.
- An ADF document is composed of a hierarchy of nodes. 
- There are two categories of nodes: block and inline. 
- Block nodes define the structural elements of the document such as headings, paragraphs, lists, and alike. 
- Inline nodes contain the document content such as text and images. 
- Some of these nodes can take marks that define text formatting or embellishment such as centered, bold, italics, and alike.
- A document is ordered, that is, there's a single sequential path through it: traversing a document in sequence and concatenating the nodes yields content in the correct order.

## [confluence macros](https://confluence.atlassian.com/doc/macros-139387.html)

- You can use macros to:
  - change the format and layout of your page
  - display media like video, audio, and social media content
  - collate and organise Confluence pages, blogs, and files
  - perform actions from a page, such as creating a page from a template. 
