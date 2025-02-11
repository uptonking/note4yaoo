---
title: lib-editor-lexical-examples
tags: [examples, lexical-editor]
created: 2022-05-15T18:37:13.995Z
modified: 2022-05-15T18:37:27.994Z
---

# lib-editor-lexical-examples

# guide

- who is using #lexical
  - mdxeditor

- lexical-starter
  - [VanillaJS Codesandbox](https://github.com/facebook/lexical/issues/1845)
# popular
- verbum /529Star/MIT/202211/ts
  - https://github.com/ozanyurtsever/verbum
  - Verbum is a fully flexible rich text editor based on react, lexical-playground and lexical framework.

- ghost-koenig-editor /46Star/MIT/202301/js/非块级拖拽
  - https://github.com/TryGhost/Koenig
  - https://koenig.ghost.org/
  - Components of Ghost's Editor
  - 基于lexical实现
  - Any content other than text are what we call cards.

- webstudio-designer /172Star/MIT>AGPLv3/202212/ts
  - https://github.com/webstudio-is/webstudio-designer
  - https://webstudio.is/
  - Webstudio Designer is a NoCode Visual Tool inspired by Webflow
  - block块级元素不支持拖拽
  - 依赖lexical-editor、radix-ui、stitches、remix-auth、downshift
  - [Change license from MIT to AGPL V3_202307](https://github.com/webstudio-is/webstudio/pull/1980)

- https://github.com/mdx-editor/editor /ts/lexical
  - https://mdxeditor.dev/
  - https://mdxeditor.dev/editor/demo
  - open-source React component that allows users to author markdown documents naturally
  - MDXEditor is a rich, client-side component that does not benefit from server-side rendering. To use it in your server components, you should use next/dynamic
  - 依赖lexical、codemirror6、radix-ui、hast、mdast、react-diff-view、react-hook-form

- https://github.com/mdmahendri/lexical-review /MIT/202501/ts
  - https://mdmahendri.github.io/lexical-review/
  - an implementation of review mode based on the ability of Lexical text-editor
  - Support review-mode only for textual change; does not support yet format change
  - Is there a way to delete one character at a time?
    - at first, i set it to character, but change that after realizing that deleting word is more efficient (at least in my language).
    - for now, you need to copy paste the package and modify it here where the backspace is work at `character` level for insertion
- https://github.com/Ramnath-Karthikesan/lexical-track-changes /NALic/202405/ts
  - I've implemented a basic version of track changes in the Lexical Editor. 
  - The concept involves creating two nodes, one for insertion and one for deletion, inspired by the structure of the link node in Lexical. 
    - A custom plugin is then developed to listen for specific operations such as KEY_DOWN_COMMAND and KEY_BACKSPACE_COMMAND. 
    - Based on the current user selection, the plugin executes the node insertion or deletion operation.

- https://github.com/juliankrispel/lexical-workshop-playground
  - Getting started with lexical by jumping in the deep end

- https://github.com/juliankrispel/lexical-react-boilerplate
  - Boilerplate for lexical editor projects

- https://github.com/lyove/lexical-vanilla-editor /MIT/202301/js/inactive
  - An extensible web text-editor based on Lexical Vanilla Js
# lexical-based-editors
- https://github.com/palerdot/react-slite /202305/ts/代码过于简单
  - This react component provides a slack like rich text editing experience powered by slate.js
  - Starting v0.2.0, react-slite is powered by lexical.
# examples
- https://github.com/konstantinmuenster/lexical-rich-text-react-demo  
  - [How To Build A Text Editor With Lexical and React](https://konstantin.digital/blog/how-to-build-a-text-editor-with-lexical-and-react)

- https://github.com/mahmedyoutube/lexical-editor-tutorial /202304/js
  - [Complete lexical editor tutorial in React and MUI (Material Ui library) from scratch - Part 5 - YouTube](https://www.youtube.com/watch?v=qTKDn_CflH8)

- https://github.com/vnugent/lexical-examples /202309/ts
  - https://lexical-examples.vercel.app/
  - While I find the framework a bit easier to work with than Slate.js, it still requires a lot of bolierplate to implement a basic plain text editor. 
  - This repo contains a few "recipes" that I may need in future projects.

- https://github.com/wingedrasengan927/medium-ai /MIT/202305/ts
  - https://medium-ai.vercel.app/
  - open-source, AI-powered text editor inspired by medium.com

- https://github.com/calcom/cal.com /AGPLv3/202403/ts
  - https://github.com/calcom/cal.com
  - open-source Calendly alternative
  - 黑色圆角线框风格
  - https://github.com/calcom/ui
# extensions
- https://github.com/konstantinmuenster/lexical-floating-menu
  - https://lexical-floating-menu.vercel.app/
  - Improve your text editing experience with an intuitive floating menu / bubble menu
  - Designed for @lexical/react. 
  - Headless & fully customizable.
# mobile
- https://github.com/facebook/lexical-ios /MIT/202402/swift
  - An extensible text editor/renderer written in Swift, built on top of TextKit, and sharing a philosophy and API with Lexical JavaScript.
  - written in Swift, and targets iOS 13 and above. (Note that the Playground app requires at least iOS 14, due to use of UIKit features such as UIMenu.)
  - Lexical iOS is used in multiple apps at Meta, including rendering feed posts that contain inline images in Workplace iOS.
# utils
- https://github.com/RegiByte/lexi-kit /19Star/MIT/202305/ts
  - a set of tools that can be used to build rich text editors with Lexical without having to reinvent the wheel every time.
  - We try to follow the coding standards found in the Lexical framework, so if you are familiar with it, you should feel right at home.

- https://github.com/fedemartinm/lexical-minifier
  - Exporting the state of the lexical editor can result in a large and unoptimized JSON structure. 
  - This package offers a solution by minifying and unminifying the code produced by the lexical editor, reducing the time it takes to obtain or send the serialized state in a request and freeing up valuable storage space.
# more-lexical
