---
title: lib-editor-atlaskit-codebase
tags: [atlaskit-editor, codebase]
created: '2021-07-12T17:18:47.506Z'
modified: '2021-07-14T15:35:53.716Z'
---

# lib-editor-atlaskit-codebase

# guide

- src-branch-commit
  - [master-snapshot-v146.0.0](https://bitbucket.org/atlassian/atlassian-frontend-mirror/commits/92512bab8602ac0bc2bc8021a488c8fa81afe4dd)
# modules

## Atlaskit Editor/EditorProps

### common editor props

- appearance/ui
  - contentComponents
  - popupsMountPoint
  - popupsBoundariesElement

- toolbar
  - primaryToolbarComponents
  - secondaryToolbarComponents
  - useStickyToolbar

- quickInsert
  - insertMenuItems

- events/cb
  - saveOnEnter
  - onEditorReady
  - onChange
  - onSave
  - onCancel

### EditorPlugins

- extensionHandlers
- extensionProviders
- dangerouslyAppendPlugins

- contextPanel

- providers
  - emojiProvider
  - taskDecisionProvider
  - searchProvider
  - annotationProviders
  - collabEditProvider
  - presenceProvider
  - mentionProvider

- media
- elementBrowser
- codeblock
- UNSAFE_predictableLists
- mentionInsertDisplayName
- placeholder

- collabEdit

- features
  - featureFlags
  - disabled
  - allowBlockType, allowTasksAndDecisions, allowBreakout
  - allowTables
  - allowHelpDialog, allowJiraIssue
  - allowExtension
  - allowTemplatePlaceholders
  - allowDate, allowLayouts
  - allowTextAlignment, allowTextColor, allowDynamicTextSizing
  - allowIndentation
  - allowFindReplace
  - allowExpand

### more settings

- tracking and analytics
  - performanceTracking
  - trackValidTransactions
  - allowAnalyticsGASV3

- extensionProviders
  - new extension API. This eventually is going to replace `quickInsert.provider, extensionHandlers, macroProvider`.

## codeblock
