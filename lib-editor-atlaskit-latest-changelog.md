---
title: lib-editor-atlaskit-latest-changelog
tags: [atlaskit-editor, changelog]
created: '2021-07-14T15:37:36.676Z'
modified: '2021-07-14T15:38:06.614Z'
---

# lib-editor-atlaskit-latest-changelog

# guide

# roadmap

# changelog

- ref
  - 每个子模块都有记录自己的变更历史
  - [editor-core changelog](https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/editor-core/CHANGELOG.md)

- v146.0.0__202107
- Allows the editor mobile bridge plugin subscription listeners to optionally only update once the dom has been rendered.
- Add docStructured to ErrorBoundary
- Stop date plugin from firing a plugin state update for every selection, even if it is not date related.

- ## v145.0.0
- updated extension interface to allow dynamic toolbar buttons.
  - `ExtensionModules.contextualToolbarItems` has been removed in favor of `ExtensionModules.contextualToolbars`.
- Added a new DSL in the mobile bridge to interpret a `FloatingToolbarDatePicker`. This extends from the FloatingToolbarSelectType.
- Allow the mobile bridge to insert a date node

- v144.0.0
- Removes `allowReferentiality` & `UNSAFE_allowDataConsumer` props from editor props. These can now be toggled via the feature flags prop

- v137.0.0
- Persist scroll gutter for mobile COMPACT appearance and change mobile scroll gutter to 50px

- v127.0.0
- Remove deprecated flag `allowUnsupportedContent` and enable by default
-  avoid toolbar layout shift in comment appearance

- v126.0.0
- avoid toolbar layout shift in comment appearance

- v121.0.0
- Split annotation UI component into two pieces
  - A `createComponent` and `viewComponent`.
- `ExtensionContent` has been removed

- v115.0.0
- deprecated props have been removed from @atlaskit/editor-core:
  - mediaProvider –> Use media={{ provider }} instead
  - cardProvider -> Use UNSAFE_cards={{ provider }} instead
  - allowCodeBlocks -> Enabled by default
  - allowLists -> Enabled by default

- v113.2.0
- support nested actions in stage-0 schema; change DOM representation of actions
  - This changeset adds support for nesting actions at the schema level, currently only within the stage-0 ADF schema.
  - DOM representation of actions in renderer + editor

- ## v113.0.0_201909
- Editor Bombazine Release
- Remove applicationCard node and action mark
- Headings in the renderer now show an anchor link on hover

- v112.34.0
- Added quick insert option to open the feedback modal dialog in editor
  - In order to enable opening feedback dialog from the quick insert menu, we need to move the feedback dialog code from `ToolbarFeedback` to `Editor` itself, 
  - because initialize editor plugin from a UI component is not ideal, and it would be very difficult to get properties from an UI component.

- v112.29.0
- Media Picker Dropone component is now migrated to React.

- ## v112.18.1
- Media Picker Browser component is now migrated to React.
  - No need to explicitly teardown the component. Unmounting the component will do the work

- v112.11.0
- Put media-editor into separate editor plugin, , update @atlaskit/media-editor API
  - The new `media-editor` plugin is not dependent on the `media` plugin.

- ## v112.2.10
- MediaPicker Clipboard component is now a React Component
  - These changes provide a new React api for Clipboard component. 
  - First one to be delivered, coming next we are going to ship Browser, Dropzone and Popup.
- With the new React API we benefit from:
  - No need to programatically activate/deactivate. We will just render the Clipboard component or not.
  - Event handlers are provided by react props
  - We don't need to use a `MediaPicker` constructor and specify which flavour we want (in this case 'clipboard'). We can basically `import { Clipboard } from '@atlaskit/media-picker' `directly and use it right away.
- This is the first component we migrate fully and integrates seamlessly with the Editor

- v111.0.4
- Refactor table plugin state to use pluginFactory

- v110.0.0
- Updates react and react-dom peer dependencies to react@^16.8.0 and react-dom@^16.8.0.

- v107.16.0
- add support for custom autoformatting
  - use the `customAutoformatting` prop to provide a custom autoformatting handler that replaces on particular regex strings.

- v107.9.6
- Removed CardView and CardViewLoader from public APIs and replaced it with light-weight and stateless CardLoading and CardError components. 
  - Handling of external images is now done by Card component itself using ExternalImageIdentifier interface.

- v107.9.3
- Nodeviews now re-render without a view re-create

- v97.0.0
- Enable inline video player in Editor and Renderer

- v95.0.1
- Enables typeahead support for mobile editor

- v82.0.0
- Editor i18n: Main toolbar

- v76.0.0
- Add support for switching between different layout styles via the toolbar. 

- v73.0.0
- makes `styled-components` a peer dependency and upgrades version range from 1.4.6 - 3 to ^3.2.6
