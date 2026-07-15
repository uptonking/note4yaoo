---
title: dev-ing-toys-prompts
tags: [dev, prompt, toys]
created: 2026-04-11T01:31:00.503Z
modified: 2026-04-11T01:31:17.720Z
---

# dev-ing-toys-prompts

# guide

# coding-harness-xp
- ai长时间工作改代码/加测试后， build/testing/io 花费的时间可能过多， 要定期优化

- 有些常用工具AI也记不住API, 比如pdfium, 可以将代码clone到本地让ai理解

- task/goal的描述要用具体的features/bugs， 否则ai也找不到重点甚至偏移
  - ai工作时也可以直接发送instruction/goal来提醒

- ai容易工作一小段时间就停止然后提示你next, 有时候感觉是无底洞
  - /goal 可以让ai专注于目标

- ❓ 有些提示词不小心输入错误或复制粘贴错位会导致llm始终保持错误的指令/记忆

- 
- 
- 
- 
- 
- 
- 

- code-port/translation
  - 也可直接给明确的转译代码指令比模糊的rewrite更有效
  - 比如直接按模块按文件逐个转译，准确度更高，但可要求风格转换

## code-port/rewrite

- 优先 client/server architecture with sdk, 这样frontend/cli 都可以通过sdk来实现，避免重复
# prompts 🔠

## 📌 begonia(superdoc/ailovedoc)

- goals
  - pagination
  - virtualized render
  - track-change
  - multi-column layout
  - hybrid table and doc

project `superdoc` (at folder `../superdoc` ) implements renders, edits, and automates `.docx` files in the browser, headless on the server, and within AI agent workflows. but it is AGPL licensed.
- the final goal is to implement a framework-agnostic, modular, extensible, headless ai docx editing solution named `begonia` similar to `superdoc` in current folder to avoid the licensing issues.
- begonia should be implemented in a modular and extensible architecture for core features, with functional programming style.

- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible. tests are not necessary for your implementation.
- the most important feature to implement at first step is ai editing with track change support, other features can be implemented later progressively. a runnable ai editing example with track change should be provided.
- you may implement code architecture and structure similar to superdoc, but rewrite from scractch to avoid licensing issue. `EditorAdapter` is a good design, you should implement similar architecture. OOXML → ProseMirror handlers is powerful, you should implement your converter and handler by refrencing superdoc, but remember to avoid licensing issues. collaboration with yjs should be implemented. encryption/signing can be skipped now. you can reference as many superdoc code as possible, but remember to rewrite it to avoid license issue.
- please analyze related code and architecture, make a plan and implement your begonia project.

- please analyze git repo and code if you need, then explain to me what major features are in superdoc but missing in begonia.

- the most important feature is a powerful, robust, extensible, headless ai ooxml editing engine . 

please refactor code structure in begonia project to use similar architecture and code structure as superdoc, to make it easy to migrate more features in the future.

please recheck migrated features and improve the implementation in project begonia, make it runnable locally using npm without docker. Read core implementation logic details for major features, find possible bugs in code and fix them, make sure major features implementations are correct and extensible.

code at `./begonia` should use npm workspaces, typescript, prosemirror, yjs.

please continue to migrate features related to ooxml editing with ai agent progressively. this is the most important feature. 

- these are the most important features now, the goal is to achieve major feature pairity or even better.

you have worked on this problem several times but features are still lacking. They are the most important features at this moment, please migrate and improve it. make a plan and implement it to match major features of upstream without licensing issues.

- to achieve major feature parity with superdoc, help me choose the best option for long-term.

- you have migrated/reimplemented some features from superdoc to begonia.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve major feature parity(ux can differ) like superdoc for major features.

- begonia should have full feature parity matching superdoc for important/major features like document data-model, layout-engine(supports multi-column), toggling pagination, virtualized-rendering, zoom, editing engine, rich-text formatting, track-change.

- these are the most important features now, the goal is to achieve full feature pairity or even better.

- the goal now is to achieve robust and extensible ooxml editing engine with full feature parity of upstream supercode.

- the most important feature is a powerful, robust, extensible, headless ai ooxml editing engine with track change support .

- please deep research superdoc, is superdoc's solution for related feature/problem good enough? if yes, can you design a similar solution in begonia to improve it? 

- you have worked on this several times but features are still lacking. They are the most important features at this moment. DO NOT stop untill you achieve full feature parity. 

- you may deep research, and reference the upstream superdoc code(at folder `../superdoc`), you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues.
- you may even do a big code refactor for begonia to match major features of superdoc in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- you may design feature parity docs at `upstream/superdoc/reports`, when you migrate/implment features, you can recheck and update it. all checking/docs/scripts related to upstream superdoc should be put in folder `upstream`. you may even design a script to automate it.
- feature parity docs may be outdated, please read related code and recheck/update.

- research and make a full plan, then implement begonia to match major features of superdoc, or even better than superdoc, without licensing issues.

------

- yes, continue to improve.
- you may reference how superdoc implements/solves it, then do a similar or better implementation in begonia without licensing issue.

- superdoc's overall architecture is good enough to follow. Mostly begonia should use similar architecture like superdoc.
- you may analyze related architecture/code and borrow good deisgn from upstream superdoc(source code at folder `../superdoc`) and rewrite it in functional-programming style for begonia to avoid licensing issues.
- it is unnecessary to search the web for superdoc details, just analyze the source code at folder `../superdoc`.

- please recheck migrated features and improve the implementation in begonia. Analyze core data flow and implementation logic details for every major feature like editor-data-model/rich-formatting, selection range/offset/caret, document viewport/layout-engine(supports multi-column), toggling pagination, virtualized-render, zoom, track-change/diff, comment, OOXML-support, API, SDK, CLI..., compare the implementation logic/code of begonia with logic/code of superdoc to recheck and enhance the correctness of architecture and logic in begonia, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations in begonia are correct, modular, extensible for long-term maintenance. 
- core implementation for major features should be framework-agnostic without react, ui wrappers/bindings should be sub packages, react should be used very sparingly. please improve and enhance the modular, extensible, headless core editor to be framework-agnostic, correct, robust.

- prioritize and recheck/improve major features like editor-data-model/rich-formatting, selection range/offset/caret, document viewport/layout-engine(supports multi-column), toggling pagination, virtualized-render, zoom, track-change/diff, comment, OOXML-support, API, SDK, CLI... in begonia, make related features/architecture correct, modular, extensible, robust for long-term maintenance.

- if these major/important features already work without obvious bugs and have good architecture/data-flow, then you may mark current goal as achieved so that further improvements will be designed as separate goal/task.

- docs/tests/scripts might be outdated, recheck code and data flow to improve begonia.

- please recheck migrated features and improve the implementation in begonia. Analyze core data flow and implementation logic details for every major feature , compare the implementation logic/code of begonia with logic/code of superdoc to recheck and enhance the correctness of architecture and logic in begonia, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations in begonia are correct, modular, extensible for long-term maintenance. 
- recheck and improve major features/architecture in begonia, make them correct and robust without guessing, the fewer bugs, the better.

- prioritize and recheck/improve major features like editor-data-model/rich-formatting, selection range/offset/caret, document viewport/layout-engine(supports multi-column), toggling pagination, layout modes support vertical/horizontal/book like superdoc, multi-column layout supports unequal column widths like superdoc, virtualized-rendering should use scroll event listeners + spacer-based approach and have good support for horizontal-layout/external-container like superdoc, zoom in/out, Canvas-based text measurement, performant line-breaking like superdoc, track-change/diff, overlap handling in track change like superdoc, comment, OOXML-support, API, SDK, CLI.

- prioritize and recheck/improve major features like document viewport/layout-engine(supports multi-column) like superdoc, toggling pagination, layout modes support vertical/horizontal/book like superdoc, multi-column layout supports unequal column widths like superdoc, virtualized-rendering should use scroll event listeners + spacer-based approach and have good support for horizontal-layout/external-container like superdoc, zoom in/out, Canvas-based text measurement, performant line-breaking like superdoc, comment, OOXML-support, API, SDK, CLI. 
- you may deep research, and reference the upstream superdoc code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues. 
- core implementation in begonia for major features should be framework-agnostic without react, react should be used very sparingly. please improve and enhance the modular, extensible, headless core editor to be framework-agnostic, correct, robust.

### draft-begonia

- The current TASK is to refactor/improve the architecture of begonia to be more extensible/modular/headless like superdoc, so that it will be easy to implement a v2 editor without prosemirror in the future. 
  - Superdoc’s headless toolbar/UI already depend on a narrow host contract plus doc access, and the UI controller also uses a structural editor-like contract. These features of superdoc should be a good reference for how to improve begonia.
- a similar contract has been implemented in begonia, but not robust. 
  - existing begonia v1 editor with prosemirror should become one backend implementation instead of the assumed core. core type definitions in begonia should be prosemirror agnostic, a contract api like superdoc should be implemented.
  - related architecture/data-flow/logic should be migrated to use the new contract api, legacy architecture or code might be removed, related tests should be updated.
- For current TASK, you should focus more on refactoring/improving the functional extensible architecture/data-flow for begonia. after you finish the goal, major features of begonia should still work, full tests should still pass.

- 编辑器导出pdf: 内置FlowBlock的分页 如何实现 typst-pdf 的效果

- in superdoc, running `pnpm dev:super-editor` shows a mininal editor demo that supports to toggle pagination, and running `pnpm dev` shows a powerful editor demo that supports to toggle pagination, zoomable, toolbars, sidebars. please migrate the superdoc examples to begonia without licensing issues, and make it runnable locally in begonia. you should migrate all superdoc examples/features to a standalone package at `apps/playground`, the basic ux can be a list of editor example names at left sidebar, when click one example name, the demo will show on the right, so that it is easy to view and switch examples.
- please continue to improve and enhance begonia editor, and also improve the examples, you may add more modular examples to showcase the editing features.

- there are many smoke tests, it seems messy. can you refactor/redesign the tests as common units that are eaiser to maintain? 

- the tests/scripts/commands you just run took huge memory and is very slow. maybe there is some memory leak or lack of logic to stop running some commands/scripts/tests. 
- please recheck related implementation-logic/tests, improve it and make it correct and fast. 

- try to improve/refactor the full tests to make it faster so that full tests running within 1.5 minutes.
- improve the slow/complicated/heavy parts of tests, 
you might refactor/reorganize the tests architecture/logic to make it correct, fast, robust, maintainable in the long term.

### docx-editor

project `superdoc` at folder `../superdoc` is also a paginated editor like `docx-editor` in current folder. analyze related code/docs/architecture/data-flow in superdoc, explain to me how does the core superdoc editor  implement the paginated editor layout engine architecture, whether superdoc editor supports multi-column layout, whether it supports virtualized rendering for huge document. 
then compare the architecture/implementation of superdoc and docx-editor, explain the differences for core features like pagination, virtualized render, multi-column layout, track-change...

## 📌 hardoc(onlyoffice-pdf)

onlyoffice-pdf-editor(code is at several git repos in current folder) implements renders, edits, annotates `.pdf` files in the browser, but it is AGPL licensed.
- the final goal is to implement a new headless, extensible pdf solution named hardoc with in-place text editing features similar to onlyoffice-pdf-editor/adobe-acrobat at folder `./hardoc`  to avoid the licensing issues.
- hardoc pdf editor should be more of a headless client-server architecture, so that a hardoc pdf web/cli/sdk can be built on the same architecture. the hard web pdf editor ui/ux might be similar to onlyoffice-pdf-editor.
- hardoc should be implemented in a modular and extensible architecture for core pdf features like viewing and editing, with functional programming style.

- goals for pdf editing:
01. modular and extensible architecture for pdf viewing and editing: you may design sub packages like state/view/command/transform/... when you need. you may design a sdk if you want.
02. in-place text editing feature like adobe acrobat; undo/redo
03. pdf highlights, annotations with simple shapes
04. pdf file open and save
05. in-place text editing is the most important feature to implement now, the following features can be planned, but unnecessary to implement at this moment: forms, ocr, collaboration, ai-editing, complicated shapes, search. any feature you feel unimportant to in-place text editing can be delayed to implement,  but architecture should be extensible enough to support them later.

- tech stack needs to use open source libs/fwk:
you may reference architecture and implementation details of onlyoffice pdf editor. 
code at `./hardoc` should use npm workspaces, typescript.
AGPL dependencies like MuPDF should be avoided, ask for approve if you must use.

- serveral questions need to be made clear before implementation:
01. should core pdf data model be headless/dom-agnostic, so that it will be usable in nodejs?
02. should wasm like pdfium be used?
03. should canvas framework like fabric/knova be used?

please analyze onlyoffice architecture, and give tips to my question before iplementing new pdf editor hardoc.

- the core pdf editor should be modular and extensible. 

one goal is to support to view both text pdf and scanned image pdf, text pdf should also support in-place text editing like onlyoffice/adobe-acrobat. both text and scanned pdf should support annotations/highlights.

one goal is to enhance hardoc pdf editor with more important features:
01. robust undo/redo that is friendly to collaborative editing
02. ocr, you may reference how onlyoffice implements it, you may integrates Tesseract(whether to use wasm is up to you)
03. pdf search
04. view page thumbnails, pdf bookmarks, search... these ui-related features should be implemented in an extensible way like state/view so that it will be easy to adjust ux later.
05. advanced annotation shapes
07. ready for ai editing, you may reference how onlyoffice, full migration is not required
06. the core pdf editor and app should be modular and extensible. an extensible pdf sdk can be provided.

one goal is to enhance hardoc pdf editor with more features:
- collaborative editing
- ocr with llm

project onlyoffice and project at `~/Documents/repos/office/all-pdf/open-pdf-studio` can be used as implementation reference, you can reference their architecture and code, but you should rewrite code to avoid licensing issue. 
- git repo at `~/Documents/repos/office/all-pdf/open-pdf-studio` is a buggy and not-featureful pdf editor. please read related code and analyze architecture. do you think open-pdf-studio is good start point for implement a custom pdf editor?  compare the architecture of open-pdf-studio and onlyoffice.
  - 采用图片的方案

- the final goal is to implement from scratch a extensible web pdf editor named hardoc with in-place text editing features similar to onlyoffice/adobe-acrobat at folder `./hardoc`  to avoid the licensing issues. 

- 🐛
- forms, ocr, collaboration, ai-editing, complicated shapes should be planned but implementation may be delayed, so that architecture should support these features later.
- please make a plan for the extensible text editing editor first, then implement it at folder `./hardoc`.

- please refactor code structure in hardoc project to use similar architecture and code structure as onlyoffice without licensing issue, to make it easy to migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- please analyze code and docs if you need, then explain to me what major features are in onlyoffice pdf editor but missing in hardoc. 

recheck and migrate full features of True PDF text editing engine with annotation support. 

- you have migrated/reimplemented some features from onlyoffice pdf editor to hardoc.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve major feature parity(ux can differ) like onlyoffice-pdf-editor for major features.

- you have worked on this several times but features are still lacking. They are the most important features at this moment, please migrate and improve it. 

make a plan and implement it to match major features of upstream without licensing issues.

- you can reference code from onlyoffice pdf editor. feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible.  

please make a plan, then improve the core in-place text editing engine to make it correct and extensible without licensing issues.

- the goal now is to achieve full feature parity of native True PDF text editing engine like onlyoffice pdf editor.

- the most important feature in hardoc is a powerful, robust, extensible, native True PDF in-place text editing engine with annotation support like onlyoffice pdf editor.

- you may deep research and reference good deisgn from onlyoffice pdf editor.

- please deep research the onlyoffice pdf editor, then can you design a similar solution to solve it? is onlyoffice's solution good enough? if yes, solve it in a similar way for hardoc.

- you have worked on this several times but still not solve it. 

- you may reference the upstream onlyoffice-pdf-editor code(code is at several git repos in current folder), use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues.
- you may even do a big code refactor for hardoc to match major features of onlyoffice-pdf-editor in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- you may design a feature parity doc at `upstream/parity/feature-parity.md`, when you migrate/implment features, you can recheck and update it. all checking/docs/scripts related to upstream onlyoffice-pdf-editor should be put in folder `upstream`. you may even design a script to automate it.
- research and make a plan, then implement hardoc to match major features of onlyoffice-pdf-editor, or even better than onlyoffice-pdf-editor, without licensing issues.

------

- yes, continue to improve.
- you may reference how onlyoffice-pdf-editor implements/solves it, then do a similar or better implementation in hardoc without licensing issue.

- onlyoffice-pdf-editor's overall architecture is good enough to follow. Mostly hardoc should use similar architecture to onlyoffice pdf editor. 

You should implement hardoc pdf editor in a similar architecture of onlyoffice pdf editor. If onlyoffice does not use the rust core architecure, you MUST NOT do it.

DO NOT search the web for onlyoffice pdf api, you should find and read source code of onlyoffice pdf editor directly in current folder.

- hardoc should have full feature parity matching onlyoffice-pdf-editor for important/major features like document rendering/pagination/zoom, in-place text-editing engine, undo/redo for editing, pdf annotations/highlights, plugin architecture and manager, pdf search, pdf page-thumbnails, bookmarks.

- please recheck migrated features and improve the implementation in hardoc. Analyze core data flow and implementation logic details for every major feature like document rendering/layout/pagination/zoom, in-place text-editing engine, undo/redo for editing, pdf annotations/highlights, ..., compare the implementation logic/code of hardoc with logic/code of onlyoffice-pdf-editor to recheck and enhance the correctness of architecture and logic in hardoc, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations in hardoc are correct, modular, extensible for long-term maintenance.

- docs/tests/scripts might be outdated, recheck code and data flow to improve hardoc.

- prioritize and recheck/improve major features like document rendering/layout/pagination/zoom, in-place text-editing engine, selection range/offset/caret, undo/redo for editing, pdf annotations/highlights... in hardoc, make related features/architecture correct and robust without guessing, the fewer bugs, the better.
- prioritize and recheck/improve major features like document rendering/layout/pagination/zoom, in-place text-editing engine, selection range/offset/caret, undo/redo for editing, pdf annotations/highlights, pdf search, pdf page thumbnails and navigation, bookmarks... in hardoc, make related features/architecture correct, modular, extensible for long-term maintenance.

- if major/important features already work without obvious bugs and have good architecture/data-flow, then you may mark current goal as achieved so that further improvements will be designed as separate goal/task.

- core implementation for major features should be framework-agnostic without react, ui wrappers/bindings should be sub packages, react should be used very sparingly. please improve and enhance the modular, extensible, headless core editor to be framework-agnostic, correct, robust.

### draft-hardoc

- ONLYOFFICE’s solution is good enough at the architecture level, not at the implementation level. The strong pattern in the local source is: one document-owned runtime, promotion/recognition when native editing gets unsafe, and native engine primitives for operations like scanPage, RedactPage, merge/split, form extraction, and appearance generation. 
  - For hardoc, it seems the appropriate architecture might be a service-authoritative pdf runtime, rather than trying to force every parity-critical operation through pure TS logic. 
  - hardoc should be more of headless client-server architecture. native/source first, promote only for unsafe contents/objects.

## 📌 grist-office

Project `grist` (in current folder) is a modern relational spreadsheet. It combines the flexibility of a spreadsheet with the robustness of a database. 
- The final goal is to implement an alternative modular, extensible react frontend webapp in folder `./app/client-react` at the current git branch `feat/office-react`, with almost the same features as existing backbonejs frontend webapp at `app/client`, using modern tech stacks like npm, reactjs, typescript, tailwindcss, zustand, @tanstack/react-table, @tanstack/react-router without legacy backbonejs/knockoutjs. After you finished the react webapp,  `npm run start:app` should start the new react webapp, the legacy yarn toolchain/code should still be kept for backward compatibility, the legacy backonejs should still works, so you should implement the react webapp in a way to make it easy to merge code changes from `main` branch to `feat/office-react` branch in the future, so please reuse as many code from main branch as possible.
- The core goal is to rewrite most of the existing backbonejs ui/ux with modern react ui/ux.
- react webapp should support all the routing urls of existing backbonejs webapp with @tanstack/react-router, using the same existing backend api.

- you can prioritize the core speadsheet view/create/edit/save data flow, speadsheet-unrelated features may be delayed. 

- please read and analyze git commits/code if you need, then explain to me what major features are in backbonejs webapp but missing in react webapp.

- the following features are not top priority for react webapp, might be planned but delayed if you want:
01. displayed on a static website with grist-static.
02. A self-contained desktop app for viewing and editing locally: grist-desktop.
03. Native forms. Create forms that feed directly into your spreadsheet.
04. Sandboxing options for untrusted documents
05. AI Formula Assistant 
06. integrations to airtable/...

- tech stack for react webapp needs to use open source libs/fwk:
  - use npm workspaces, typescript, reactjs(not vue), tailwindcss, zustand, no jquery/knockoutjs/backbone.
  - you can reuse upstream/existing dependencies for easier feature migration, avoid GPL-like deps.
  - for ui components, you can use base-ui, source clone is at `~/gh-mirror/mui/base-ui` for your reference.
  - use floating-ui instead of @popperjs/core, source code is here for your reference `~/gh-mirror/floating-ui/floating-ui`.
  - for data table, you should use @tanstack/react-table. the source code for @tanstack/react-table and @tanstack/react-router is cloned at folder `~/gh-mirror/tanstack` for your reference.
  - you may use zustand for state management in framework-agnostic core package, the source code is at folder `~/gh-mirror/pmndrs/zustand` for your reference.

- the most important feature in react webapp is a modular, extensible, headless spreadsheet view/editing engine with undo/redo history support like backbonejs webapp. you should implement it in a way to make it easy to merge code changes from `main` branch to `feat/office-react` branch in the future, so please reuse as many code from main branch as possible.

- you have migrated/reimplemented some features from backbonejs webapp to react webapp.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve major feature parity(ux can differ) for major features.

- you have worked on this several times but features are still lacking.

- please deep research the existing backbonejs webapp, then can you design a similar solution in react webapp to achieve full feature parity?

- you may deep research and reference the existing backbonejs webapp code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style with modern tech stacks like typescript-utils/react. 
- you may even do a big code refactor in react webapp to match major features of backbonejs webapp in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- you may design feature parity docs at `upstream/feature-parity.md`, when you migrate/implment features from backbonejs webapp to react webapp, you can recheck and update it. all checking/docs/scripts related to upstream backbonejs webapp should be put in folder `upstream`. you may even design a script to automate it.
- research and make a plan, then implement the react webapp to match major features of existing backbonejs webapp, or even better than backbonejs webapp.

- `grist-static` is a fully in-browser build of Grist for displaying spreadsheets on a website without back-end support.

-------

- please recheck migrated features and improve the implementation in react webapp. Analyze core data flow and implementation logic details for every major feature like spreadsheet data-model and rich formatting, spreadsheet editing with undo/redo and history, custom-widget, formula, drag-and-drop-dashboard, incremental-imports..., compare the implementation of react webapp with backbonejs webapp to recheck and enhance the correctness of architecture and logic in react webapp, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations in react webapp are correct, modular, extensible for long-term maintenance.

- prioritize and recheck/improve major features like spreadsheet data-model and rich formatting, spreadsheet editing with undo/redo and history, custom-widget, formula, drag-and-drop-dashboard, incremental-imports... in react webapp, make related features/architecture correct and robust without guessing, the fewer bugs, the better.

- if these major/important features already work without obvious bugs and have good architecture/data-flow, then you may mark current goal as achieved so that further improvements will be designed as separate goal/task.

- RBAC or ui/ux is not important at the moment, related feature may be delayed, you can update the parity docs.

-------

- the browser/nbrowser related features/tests like `npm run test:nbrowser:react-smoke` can be very slow.
- please recheck related implementation-logic/tests, improve it by making the downloaded binary/resources cached locally, so that later testing/running can reuse it directly if already existed. improve the cache logic, and update related data-flow/tests, make sure the implementation is correct, robust, extensible without unnecessary redownloading.

- the tests/scripts/commands you just run took huge memory and is very slow. maybe there is some memory leak or lack of logic to stop running some commands/scripts/tests. please recheck related implementation-logic/tests, improve it and make it correct and fast. 

- recheck and improve it, make related features/data-flow/architecture correct and robust without guessing, the fewer bugs, the better.

- every time you update some code, running tests is very slow, can you improve it?

### draft-grist-react

## slaides(PPTist)

project `PPTist` at `../PPTist` is an online presentation webapp that replicates most of the commonly used features of MS PowerPoint, allowing for the editing and presentation of PPT online, also supports AIPPT. But it has AGPL license.
- project `slaides` at current folder is an old version of `PPTist` with apache2 license, but many commits behind PPTist.

- please read and analyze git commits/code if you need, then explain to me what major features are in PPTist but missing in slaides.

- the final goal is to implement a framework-agnostic, modular, extensible, headless ai ppt editing solution named `slaides` with features similar to `PPTist` to avoid the licensing issues. legacy vue code should be kept for reference only.
- goals:
01.  re-architect slaides project to have a framework-agnostic headless core package, with react/vue ui binding package and appropriate utils package.
- migrate PPTist's robust feature-rich ppt view/editing features to slaides, this is the most important feature, the goal is full feature parity for ppt view/editing, for example page zoom, Page Editing, Element/Images/Shapes Editing, Rich text editing, Slide Show...
01.  undo/redo support, friendly to collaboration.
02.  Import/export .pptx files, Export local files (PPTX, JSON, images, PDF).
03.  Mobile friendly: Basic editing, Basic preview, Play preview.
04.  migrate PPTist's ai editing solution to slaides, better to implement as a separate package: ai workflow, outline editing, use template, streaming-generation...
05.  a runnable demo/example should be provided.

- the following features can be planned, but implemention may be delayed if you want:
- the following features should be implemented if the core architecture is stable:
01. table
02. chart
03. Formulas
04. Audio, Video
05. vue ui binding

- tech stack for project slaides needs to use open source libs/fwk:
  - projects/packages at `slaides` should use npm workspaces, typescript, reactjs(not vue), tailwindcss.
  - you can reuse dependencies from PPTist for easier feature migration.
  - for rich text editing in ppt, you should still use prosemirror. the source code for prosemirror is cloned at folder `~/Documents/repos/yaoo/nostalgia-studio/editor-prosemirror/src-pkgs` for your reference.
  - you may use `zustand/vanilla` for state management in framework-agnostic core package, the source code is at folder `~/gh-mirror/pmndrs/zustand` for your reference.
  - for drag-drop, you may use  `~/gh-mirror/atlassian/pragmatic-drag-and-drop` to implement robust dnd.
  - all local packages names should start with `@datalking/`, for example @datalking/slaides-core, @datalking/slaides-react ...

- project PPTist can be used as implementation reference, you can reference its architecture and code.
- you may deep research and reference the upstream code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issue. 
you may use similar file/folder names instead of the same file/folder names as the original. you may also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.

- the most important feature in slaides is a framework-agnostic, modular, extensible, headless ai ppt view/editing engine with undo/redo history support like PPTist.

- you have migrated/reimplemented some features from PPTist to slaides.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve major feature parity(ux can differ) for major features.

- you have worked on this several times but features are still lacking.

- please deep research the PPTist, then can you design a similar solution in slaides to achieve full feature parity?

- you can deep research, referencing good deisgn from PPTist editing engine.

- you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues.

- you may even do a big code refactor to match major feature of PPTist in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- research and make a full plan, then implement slaides to match major features of PPTist, or even better than PPTist, without licensing issues.

## 📌 aichorage(janai/tranfromerlab-app)

- goals
  - 重后端、弱前端

project jan(at folder `../jan` ) is a apache2-licensed, local, powerful chatgpt-like tauri app that supports to download and run LLMs, Connect to cloud llm api, install custom llm backend like custom llama.cpp.
- project transformerlab-app(at folder `../all-runtime-llamacpp/transformerlab-app-electron`) is a AGPL-licensed electron app that supports to train, fine-tune, chat with your own model locally. it can be used to train/tune local model, but it also supports to import local models, install custom llm backend plugin, run and chat with local model.
- project unsloth-studio(at folder `../unsloth`) is a AGPL-licensed webapp that supports to run and train text, audio, embedding, vision models on Windows, Linux and macOS. It supports to run local gguf/mlx models, but it cannot install custom llm backend. It also supports auto detect locally downloaded models in local huggingface-cache/ollama/lmstudio.

- The final goal for aichorage is to implement an jan-like webapp/electron-app/cli with headless, extensible, client-server architecture in current folder with the same features as existing jan webapp/tauri-app/cli, but built using modern tech stacks like python, uv, npm workspaces, reactjs, @tanstack/react-router, @base-ui/react, typescript, tailwindcss, oxlint, oxfmt. After you finished the work, so `npm run dev` should start the webapp. you should implement the goal in a way to make it easy to migrate code changes/features from jan to aichorage in the future.
- The core goal is to support most of the existing jan features/ux, like Download and run LLMs, Connect to cloud llm api, install custom llm backend like custom llama.cpp, chat with local llm or cloud llm api. since jan is apache2 licensed, you can reuse/rewrite whatever code you need from jan repo. you may reuse jan web-app(at `../jan/web-app`) or just reuse/rewrite any code you want, but you should rewrite the jan rust backend with a good custom python implementation which you can borrow design and rewrite code from jan-rust-code/transformerlab-app/unsloth-studio to avoid license issue. you may implement the core llm download/run/chat/tool-call data flow first, then migrate more features later. 
- you may reuse most webapp code from jan, ux may differ. Since you can reuse many frontend code, the python backend should be the hard work. Strictly following jan-rust-backend architecture/logic/code is unnecessary. 
  - transformerlab-app-electron repo gives a good reference for how to support to install multiple backend plugin like llama.cpp/mlx-vlm/mlx-audio from ui, you may reference useful architecture/features/code from it and migrate this custom llm backend feature to aichorage(llama.cpp first, others may be delayed), you should ignore llm training/tuning code from it. tranfromerlab-app electron app also supports windows/linux/mac, you may reference the bundling logic if you want. 
  - unsloth-studio webapp also supports windows/linux/mac, you may reference the bundling logic if you want. unsloth-studio supports auto detect local models from local huggingface-cache/lmstudio, please migrate it to aichorage. unsloth-studio also supports llama-server/mlx-lm/mlx-vlm backend on windows/linux/mac, also a good reference. you should ignore llm training/tuning code from it. Unsloth studio can provide 2 llm apis that both support streaming, tool calling, and vision inputs: Anthropic-compatible api /v1/messages , OpenAI-compatible api /v1/chat/completions and /v1/responses. unsoloth-studio llm api has very very good fixes for tool-calls. It also support web search.
  OpenAI-compatible api should be implemented in aichorage, anthropic api may be delayed. 

- most features/ux from jan should be migrated/reimplemented in aichorage. rag should be planned, but rag implementation may be delayed.
- multi-user/team/workspace concepts in tranfromerlab-app should be implemented in aichorage, you may borrow the good design/architecture of transformerlab-app, but strictly following is unnecessary. all custom backend plugins may be installed in global scope, but each team can only use plugin enabled in their team. a default workspace and username/password should be created so that user can use it easily by just click login.
- aichorage backend/runtime/web should be extensible, configurable, flexible. Apart from good defaults value, a `.env.example` should be provided in related sub packages if you want. you may borrow some good design/config from upstream jan/transformerlab-app/unsloth-studio.
- all llm backend/runtime should be optional that supports to install/uninstall/enable/disable, so that the architecture is extensible and flexible. but llama.cpp should be installed by default to make it easy to use out of the box. you may design a standalone llm-runtime package to make the architecture modular, resuable, extensible.

- tasks that may be planned but delayed(not in current goal): RAG, full parity of Jan-style UI/UX, complicated multi-user/team/workspace/RBAC, anthropic-compatible api, embedding models.

- some local models if you need: ~/.lmstudio/models/unsloth/LFM2.5-1.2B-Thinking-GGUF/LFM2.5-1.2B-Thinking-UD-Q5_K_XL.gguf, ~/.lmstudio/models/unsloth/gemma-4-E4B-it-UD-MLX-4bit, ~/.lmstudio/models.

- tech stack for project aichorage needs to use open source libs/fwk:
  - you can use similar dependencies from jan/transoformerlab-app/unsloth-studio for easier feature migration. AGPL deps should be avoided.
  - you may use `zustand` for state management, the source code is at folder `~/gh-mirror/pmndrs/zustand` for your reference.
  - Apart from reusing existing jan ui/ux, you may use `@base-ui/react` for new ui/ux, the source code is at folder `~/gh-mirror/mui/base-ui` for your reference.
  - for python backend/cli, unsloth-studio/transformerlab-app has good codebase and architecture, you may reference them.

- you have migrated/reimplemented some features from upstream jan/transformerlab-app/unsloth-studio to aichorage.

- you may deep research and reference the code of upstream projects(jan, unsloth-studio, transformerlab-app), you may use similar dependencies, and implement similar logic, but you should rewrite it without licensing issues.
- you may even do a big code refactor for airchorage to match major feature of jan in a extensible architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- you may design a feature parity doc at `upstream/feature-parity.md`, when you migrate/implment features, you can recheck and update it. all checking/docs/scripts related to upstream jan/transformerlab-app/unsloth-studio should be put in folder `upstream`. you may even design a script to automate it.
- research and make a good design, then implement aichorage to match major features of jan, or even better than jan, without licensing issues.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve major feature parity(ux can differ) like jan for major features.

- you have worked on this several times but features are still lacking.

- aichorage should have full feature parity matching jan for important/major features like llm search/download, running local gguf/mlx models, chat with local models or cloud llm api.

- these are the most important features now, the goal is to achieve major feature pairity or even better.
- make a plan, then migrate and improve major feature pairity, without licensing issues

- please deep research jan(at folder `../jan` ), then can you design a similar solution in aichorage to improve it? is jan's solution good enough? if yes, solve it in a similar way for aichorage.

- research and make a full plan, then implement aichorage to match major features of jan, or even better than jan, without licensing issues.

------

- yes, continue to improve.
- you may reference how jan implements/solves it, then do a similar or better implementation in aichorage without licensing issue.

- you may borrow good deisgn from to upstream jan/transformerlab-app/unsloth-studio and rewrite it to avoid licensing issues.

- jan's overall architecture is good enough to follow. Mostly aichorage should use similar architecture to jan.

- please recheck migrated features and improve the implementation in aichorage. Analyze core data flow and implementation logic details for every major feature like pluggable-llm-runtime(llama.cpp, mlx-lm, mlx-vlm), model-search/download/auto-discovery/caching, openai-compatible api, chat with local-model/cloud-llm-api-provider..., compare the implementation logic/code of aichorage with related jan/transformerlab-app/unsloth-studio logic/code to recheck and enhance the correctness of architecture and logic in aichorage, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations in aichorage are correct, modular, extensible for long-term maintenance. 

- prioritize and recheck/improve major features like pluggable-llm-runtime(llama.cpp, mlx-lm, mlx-vlm), model-search/download/auto-discovery/caching, openai-compatible-api, chat with local-model/cloud-llm-api-provider... in aichorage, make related features/architecture correct, modular, extensible for long-term maintenance. 
- tasks that may be planned but delayed(not in current goal): RAG, full parity of Jan-style UI/UX, complicated multi-user/team/workspace/RBAC, anthropic-compatible api.
- if these major/important features already work without obvious bugs and have good architecture/data-flow, then you may mark current goal as achieved so that further improvements will be designed as separate goal/task.

- recheck and improve it, make related features/data-flow/architecture correct and robust without guessing, the fewer bugs, the better.

- docs/tests/scripts might be outdated, recheck code and data flow to improve aichorage.

- 
- 
- 
- 

-------

- unsloth-studio has very good support for openai-compatible api and anthropic-compatible api and gguf/mlx/vlm, text, vision, TTS audio, embedding models, you may reference it if you need. it also support auto inference settings, chat templates editing, self-healing tool-calling, advanced web search, code execution, you may reference the architecture/code and rewrite/improve it for aichorage.

- local model testing/running can be very slow and take huge disk space.
local model testing/running can be very slow.
- please recheck implementation logic related to model/llm-runtime-backend downloading and related tests, improve it by making the downloaded models/binary/resources cached locally, so that later testing/running can reuse it directly if already existed. improve the cache logic, and update related data-flow/tests, make sure the implementation is correct, robust, extensible without unnecessary redownloading. 

- try to improve/refactor the full tests to make it faster so that full tests running within 3 minutes.
- improve the slow/complicated/heavy parts of tests, 
you might refactor/reorganize the tests architecture/logic to make it correct, fast, robust, maintainable in the long term.

- lm studio can load multiple models at the same time, and it also supports Parallel Requests, Multiple requests to the same model or different models can be processed simultaneously, this feature is powerful and increases productivity. core engine source code of lm studio is at folder `~/Documents/repos/ai-ml-llm/all-runtime-mlx/mlx-engine` and `~/Documents/repos/ai-ml-llm/all-runtime-mlx/lms` for your reference. you may analyze code in lm studio core engine, unsloth-studio and transformerlab-app , then you may get some ideas from their code and implement/improve something like Parallel Requests in aichorage.
- lm studio also supports to show model working log that can display the prompt processing or token generation progress(lm studio has this feature in ui as developer logs). if there is something like this in the lmstudio code or unsloth-studio code or transformerlab-app code, you may get some ideas from their code and implement something like model logs in aichorage. it is better to design a option to configure the log level like off/debug/verbose/user/ai/..., you might design an extensible/robust architecture for the logging.
- please continue to improve and enhance aichorage, and improve the features.
- for every ai message in jan chat, ai model metadata like token generation speed, token count, and other metadata can be shown under the ai message, please refer to related code and migrate/improve this feature to aichorage.

- in jan app, there is a download manager that supports to show download progress and provides downloading related features. please refer to the code of jan(at folder `../jan` ) and migrate this feature to aichorage. you might reuse ui of jan, but the downloading related backend like pause/resume/cancel/... should be rewritten in python, you might improve this feature in aichorage.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

### draft-aichorage

- cloud-only version: mineru-api, openai-like api

- 
- 
- 
- 
- 
- 

- 优化数据库的结构

- 对并行执行的支持度如何? 同时运行多个backend/runtime? 同一个runtime运行多个模型? 多个请求的queue?

- 是否是都采用binary的方案? 同时运行多个backend/runtime时，是否存在端口冲突?

- tasks that are out of scope for near-term parity and may be delayed:
  - team/workspace/rbac: basic owner/member safeguards are sufficient for now; broader workspace ACL parity may be delayed.
  - running embedding models: embedding-model import and runtime execution may be delayed.
  - full parity for Jan-style UI/UX is unnecessary; aichorage UI/UX may differ.

- 🤔 是否要实现管理本地已有的ollama/lmstudio, 如start/stop
  - pros: 对使用本地已有工具的场景更友好
  - cons: 内置runtime需要支持多种格式如 /v1/chat/completions, /v1/responses， 还要考虑本地ollama的版本、模型版本， 带来的问题比收益多
  - 参考很多主流开放性ai的产品如cursor/cherry-studio, 都支持用户配置api，所以通过平台/系统来管理本地的工具是非必要的

## 📌 dreamansion/redmansion(vscode-obsidian/zotero)

- tips
  - 可用域名 dreamansions

- goals
  - ~~replace monaco with codemirror6~~ , 可替换的文本编辑器似乎价值不大
  - 📈 obsidian bases: with agentfs
  - pdf editing
  - pdf backlink/citation/preview
  - obsidian rich-editor and plugin: 内置了很多核心插件(实现方式不一定是插件，只提供了开关)如filetree/search/backlinks/bases, canvas, slides, graph-view
    - 如何兼容obsidian的plugin: 下载后 批量替换api? 自动转换?
    - 第三方插件: obsidian-homepage, obsidian-outliner, obsidian-iconize, obsidian-admonition
  - knowledge-base

project `directus` (at folder `../directus` ) is a source-available licensed, powerful, flexible, headless backend platform that helps users to build projects better/faster. It provides rest api, working with new or existing databases, content versioning, draft/publish content, support to change data model without restarting server, optional Realtime Data, file management, modules/hooks, extensions and marketplace, user account/auth, Policy-based Access Control, admin management studio webapp, horizontal scaling, workflow automations, SDK, AI Assistant.

- The final goal for this project `dreamansion` is to implement an directus-like backend platform with headless, extensible, flexible architecture in current folder with similar features like directus core features, but built using modern tech stacks like npm workspaces, expressjs, knex(for db crud), reactjs, @tanstack/react-router, @base-ui/react, typescript, tailwindcss, oxlint, oxfmt. you should implement the goal in a way to make it easy to migrate code changes/features from directus to dreamansion in the future.
- The core goal is to reimplment most of the existing directus features, like rest api, working with new or existing databases, content versioning, draft/publish content, i18n, data model relationships like one2many/many2one/many2many/many2any/translations/..., support to change data model without restarting server, optional Realtime Data, file management, modules/hooks, extensions, sdk, simple user account/auth, Policy-based Access Control, admin studio ui, horizontal scaling. since directus is source-available, you might refer to its architecture/data-flow/logic/code, but you should rewrite it in dreamansion to avoid license issue. backend architecture of directus is really extensible, you may borrow the good design and data flow, admin frontend of directus should be rewritten in react, @tanstack/react-router, @base-ui/react. 
- project directus-schema-sync(at folder `../directus-schema-sync`, apache 2 license) implements a way to sync Directus schema, configuration and selected data between environments. similar feature should be implemented as a sub package in dreamansion. you may reuse the apache code if you want.

- features that may be planned but delayed(not in current goal): full parity of directus-style admin UI/UX, complicated multi-user/team/workspace/access-control, sso auth, workflow automations, extension marketplace, AI Assistant, MCP server, GraphQL API.
- features that may be ignored in dreamansion: GraphQL API.

- you have migrated/reimplemented some features from upstream directus to dreamansion.

- you may deep research and refer to the architecture/data-flow/code of upstream directus, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional-programming style for dreamansion without licensing issues.
- you may even do a big code refactor for dreamansion to match major feature of directus in a extensible architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- you may design a feature parity doc at `upstream/feature-parity.md`, when you migrate/implment features, you can recheck and update it. all checking/docs/scripts related to upstream directus should be put in folder `upstream`. you may even design a script to automate it.

- these are the most important features now, the goal is to achieve major feature pairity or even better.
- research and make a plan, then migrate and improve major feature pairity, without licensing issues

- please deep research directus(at folder `../directus` ), then can you design a similar solution in dreamansion to improve it? is directus's solution good enough? if yes, solve it in a similar way for dreamansion.

- research and make a full plan, then implement dreamansion to match major features of directus, or even better than directus, without licensing issues.

- research and make a good design, then implement dreamansion to match major features of directus, or even better than directus, without licensing issues.

------

- you may refer to how directus(source code at folder `../directus`) implements/solves it, then do a similar or better implementation in dreamansion without licensing issue.

- directus's overall architecture is good enough to follow. Mostly dreamansion should use similar architecture like directus.
- you may analyze related architecture/code and borrow good deisgn from upstream directus(source code at folder `../directus`) and rewrite it in functional-programming style for dreamansion to avoid licensing issues.
- it is unnecessary to search the web for directus details, just analyze the source code at folder `../directus`.

- please recheck migrated features and improve the implementation in dreamansion. Analyze core data flow and implementation logic details for every major feature like rest api, working with new or existing databases, content versioning, draft/publish content, i18n/translation, data model relationships like one2many/many2one/many2many/many2any/translation/..., support to change data model without restarting server, optional Realtime Data, file management, modules/hooks, extensions, sdk, ..., compare the implementation logic/code of dreamansion with related logic/code of directus to recheck and enhance the correctness of architecture/data-flow and logic in dreamansion, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations in dreamansion are correct, modular, extensible for long-term maintenance. 

- prioritize and recheck/improve major features like rest api, working with new or existing databases, content versioning, draft/publish content, i18n/translation, data model relationships like one2many/many2one/many2many/many2any/translation/..., support to change data model without restarting server, optional Realtime Data, file management, modules/hooks, extensions, sdk, ... in dreamansion, make related features/architecture correct, modular, extensible, robust for long-term maintenance.

admin management studio webapp

- if these major/important features already work without obvious bugs and have good architecture/data-flow, then you may mark current goal as achieved so that further improvements will be designed as separate goal/task.

- recheck and improve major features, make related features/data-flow/architecture correct and robust without guessing, the fewer bugs, the better.

- docs/tests/scripts might be outdated, recheck code and data flow to improve dreamansion.

------

- the tests/scripts/commands you just run took huge memory and is very slow. maybe there is some memory leak or lack of logic to stop running some commands/scripts/tests. 
- please recheck related implementation-logic/tests, improve it and make it correct and fast. 

- try to improve/refactor the full tests to make it faster so that full tests running within 2.0 minutes.
- improve the slow/complicated/heavy parts of tests, 
you might refactor/reorganize the tests architecture/logic to make it correct, fast, robust, maintainable in the long term.

### draft-vscode

- 对vscode-editor的修改是否会导致不兼容 coder-server

- for the core editor, is it possible to use codemirror v6 to replace monaco editor by rewriting related logic with codemirror v6 state/view/plugin? 
- https://code.visualstudio.com/api/extension-guides/custom-editors this doc shows vscode support custom editor, it seems a promising idea.

- the final goal is to keep all exisitng vscode features working, just add a new `./scripts/dreamansion.sh` like existing `./scripts/code.sh` to start the app with codemirror v6 editor.
  - also add new `./scripts/dreamansion-web.sh`
- you should implement it in a way to make it easy to merge code changes from `main` branch to new `feat/codemirror` branch in the future, so please keep as many code from main branch unchanged as possible, most of codemirror related code/scripts should be designed as separate package or file without touching exising files.

- analyze vscode source code and architecture/data-flow, deep-research the monaco-editor related features, then explain to me whether it is possible to replace/rewrite monaco editor with codemirror v6(replace the core editing feature first, other features can be planned but delayed.)

- 
- 
- 
- 
- 
- 

### directus

### vscode-research

- goals
  - ~~replace monaco with codemirror6~~ , 可替换的文本编辑器似乎价值不大
  - 📈 obsidian bases: with agentfs
  - obsidian rich-editor and plugin: 内置了很多核心插件(实现方式不一定是插件，只提供了开关)如filetree/search/backlinks/bases, canvas, slides, graph-view
    - 如何兼容obsidian的plugin: 下载后 批量替换api? 自动转换?
    - 第三方插件: obsidian-homepage, obsidian-outliner, obsidian-iconize, obsidian-admonition
  - knowledge-base
  - Replace Monaco's core editing feature (text buffer, cursor, selection, basic operations) with CodeMirror v6, while keeping most existing VS Code code unchanged for easier future merges from main branch to feat/codemirror branch.

project `vscode` in current folder is a popular, open-source, powerful coding ide that provides editor, workbench, fileTree, global/in-file search, extension, cmd-palette, copilot-agent. 

- codemirror v6 source code is at folder `~/gh-mirror/codemirror` for your reference.
- text editor can be implemented with codemirrror v6, diff editor can be implemented with `@codemirror/merge` package at `~/gh-mirror/codemirror/merge`.

- The custom editor API path is NOT viable. Custom editors use webviews (iframe isolation) which prevents synchronous model updates, direct access to decorations/diagnostics, native find/replace, undo/redo integration, and language service features. The only viable path is to replace the internal editor widget implementation.
  - The custom-editor is an alternative editor association built on webviews and separate resolver inputs, not a drop-in replacement layer for the built-in text editor stack.

- Can Stay Unchanged (Strong Abstractions)
  - ITextModel (src/vs/editor/common/model.ts)
  - Editor Input Layer (src/vs/workbench/common/editor/)
  - Editor Groups (src/vs/workbench/services/editor/)
  - Model Service (src/vs/editor/common/services/model.ts)
  - BaseTextEditorModel (src/vs/workbench/common/editor/textEditorModel.ts)
- Tight Coupling Points (Monaco Leaks Into Workbench)
  - ICodeEditor / IDiffEditor interfaces (src/vs/editor/browser/editorBrowser.ts:606)
  - CodeEditorWidget instantiation (src/vs/workbench/browser/parts/editor/textCodeEditor.ts:41)
  - ICodeEditorService workbench wrapper (src/vs/workbench/services/editor/browser/codeEditorService.ts)
  - Editor Options (src/vs/editor/common/config/editorOptions.ts)
  - Type guards scattered throughout
- Would Need Rewrite (Monaco-Specific Features, live in src/vs/editor/contrib/ and are Monaco-specific "contributions")
  - bracketMatching, clipboard, codeAction, codeLens, colorPicker
  - contextmenu, cursorUndo, dnd, find, folding, format
  - gotoLine, hover, inPlaceReplace, indentLines, inlineHint
  - inspectTokens, linesOperations, linkedEditing, message
  - multicursor, parameterHints, placeholder, quickCommand
  - quickOutline, referencesSearch, rename, selectionHighlight
  - snippet, suggest, wordHighlighter, wordOperations, etc.
- Strategy for Phase 1: Implement core editing only. Defer these features. They map to CodeMirror extensions, but reimplementing them all is Phase 2+ work.

- Implementation Strategy: Minimal Existing-File Changes
  - Create a parallel implementation alongside Monaco, then add minimal abstraction points in existing files to wire in CodeMirror
  - Approach: Implement ICodeEditor Interface with CodeMirror Backend

- Verification: Phase 1 Success Criteria
  01.  Open text file — File loads, text displays correctly in CodeMirror widget
  02.  Edit text — Typing, insertion, deletion work, content syncs to ITextModel
  03.  Undo/redo — CodeMirror's history extension integrated with VS Code's undo stack
  04.  Save file — ITextModel content saves correctly (model independent of editor)
  05.  Cursor/selection — Cursor moves, selections work, events emit correctly
  06.  View state — Close and reopen file restores cursor position, scroll position
  07.  Split editor — Multiple views of same model work (ITextModel shared)
  08.  Editor options — Font size, line numbers, readOnly config apply to CodeMirror
  09.  Editor groups — Tabs, layout, groups work unchanged (Monaco-free layer)
  10. Search in file — Basic find works (find contrib feature deferred to Phase 2)

- Phase 2+: Monaco Contribution Features (Deferred)
  - Each Monaco contribution in src/vs/editor/contrib/ maps to a CodeMirror extension

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

## ilove-image(stirling-image)

- codebase
  - a client/server app
  - the backend handles uploads, auth, SQLite, pipelines, tool execution, AI bridge calls, and serves the built SPA

git repo `./ilove-image` is several commits behind `./ilove-stirling-image` . ilove-image has MIT license, while ilove-stirling-image has GPL license. 
the goal is to migrate major features from ilove-stirling-image to ilove-image. 

please analyze git commits and code if you need, then explain to me what major features are in stirling-image but missing in ilove-image.

- please make migrations to ilove-image. 
- the following 2 features can be ignored:
01. HEIC/HEIF input and output
02. CUDA Docker variant can be ignored. Lite Docker variant should be migrated.
03. any features you feel unimportant or redundant can be ignored too
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation work, but without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation clean and extensible. tests are not necessary for your implementation, but you can write some important tests if you want. do not write too many tests, if logic is simple/clear, skipping tests is ok. 

- please rename all local packages whose names start with "@stirling-image/" to "@datalking/", for example "@stirling-image/image-engine" should be renamed to "@datalking/image-engine". then update related code/tests/scripts. make sure project and tests still runs with no error using npm, without docker.

- you have migrated/reimplemented some features from ilove-stirling-image to ilove-image. 

- for important features, the goal is to achieve major feature pairity or even better.

- please refactor code structure in ilove-image project to use similar architecture and code structure as ilove-stirling-image without licensing issue, to make it easy to migrate more features in the future. 

please recheck migrated features and improve the implementation in ilove-image, make it runnable locally with npm. make sure implementation is correct and extensible.

- research and make a full plan, then implement ilove-image to match major features of ilove-stirling-image, or even better than ilove-stirling-image, without licensing issues.

## ilove-pdf(bentopdf)

- codebase
  - a client-side-only PDF app, not a client/server architecture
  - Core PDF work is done with browser libraries and browser runtimes like pdf-lib, pdfjs-dist, tesseract.js, and qpdf.wasm

git repo `./ilove-pdf` is several commits behind `../ilove-bentopdf` . ilove-pdf has MIT license, while ilove-bentopdf has GPL license. 
the goal is to migrate major features from ilove-bentopdf to ilove-pdf. 

please analyze git commits and code if you need, then explain to me what major features are in ilove-bentopdf but missing in ilove-pdf.

- please make migrations to ilove-pdf. 
- the following 8 features should be migrated:
01. dynamic WASM loading
02. bookmarks / TOC / page labels / Bates
03. attachment extract/edit
04. overlay/underlay
05. better Compare PDFs
06. better OCR
07. better Image/PDF UX
08. features: divide pages, extract images, prepare PDF for AI, PDF layers
- other features can be ignored: 
01. Forms and signing, digital signature / validation / timestamp
02. Big conversion expansion, many Office, email converters, but you can migrate some if you want 
03. Workflow/automation
04. repair PDF
05. Encryption
06. PDF to PDF/A, PDF booklet,ebook, deskew, font-to-outline, rasterize PDF, ...
07. any features you feel unimportant or redundant can be ignored
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation work, but without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation clean and extensible. tests are not necessary for your implementation, but you can write some important tests if you want. do not write too many tests, if logic is simple/clear, skipping tests is ok. 

- please recheck the migrations and improve implementation for the the following features:
01. dynamic WASM loading
02. PDF layers, overlay/underlay
03. better OCR, make ocr robust
04. better extract
- these are the most important features now, the goal is to achieve major feature pairity or even better.
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible. tests are not necessary for your implementation.

ocr is the most important feature in ilove-pdf project. 

please recheck your migrated ocr features and implementation logic, make sure the logic is correct without licensing issues. improve the ocr logic to make it robust and extensible.

- you have migrated/reimplemented some features from ilove-bentopdf to ilove-pdf. 

please refactor code structure in ilove-pdf project to use similar architecture and code structure as ilove-bentopdf without licensing issue, to make it easy to migrate more features in the future. 

you may deep research and reference the upstream code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issue. 
you may use similar file/folder names instead of the same file/folder names as the original. you may also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.

if migration/refactoring of similar code architecture as ilove-bentopdf is complicated, you can make a plan first, then migrate by the plan.

now recheck migrated features and improve your implementation in ilove-pdf, make it runnable locally with npm. make sure implementation is correct and extensible.

for the most important features like pdf compare and PDF layer, why are you always migrating and improving without full features matching the upstream? 
you have improved several times, why is it always lacking features behind the upstream? what is the reason? 
what should be done to macth the upstream? explain to me. if it it complicated, you can make a plan and discuss with me.

- please deep research related code of ilove-bentopdf, then can you design a similar solution in ilove-pdf to achieve full feature parity?

- research and make a full plan, then implement ilove-pdf to match major features of ilove-bentopdf, or even better than ilove-bentopdf, without licensing issues.
# code-review 👀

for project hardoc, 
please recheck migrated features and improve the implementation, make it runnable locally using npm without docker. Analyze core data flow and implementation logic details for major features, find possible bugs in code and fix them, refactor code if you need, make sure major features implementations are correct, modular, extensible for long-term maintenance.
- docs/tests/scripts might be outdated, recheck code and data flow to improve begonia.

please recheck migrated features and implementations for possible licensing issues. if the code is too similar to upstream, you can adjust the risking code to avoid licensing issues. if features are already migrated under different names, it is unnecessary to design it as a standalone/separate tool as the upstream did, this also helps to avoid licensing issues.

document what you have migrated from which commit id for future migration reference at file `doc/devlog-migrations.md` . you can also add some concise(less than 120 lines) migration guide/steps/tips in it to make it easy to do migrations later.

# tests
- run the full tests and fix the bugs

- running full tests/scripts is a little slow. maybe there is some memory leak or lack of logic to stop running some commands/scripts/tests.

- improve the slowest part of tests first, 
review the whole tests architecture/logic, then improve it, you might refactor/reorganize the tests to make it correct, fast, robust, maintainable in the long term.

- tests files in each package should existing as sibling folder of `src`. for example, all tests for `packages/core/src` should be put at ``packages/core/__tests__` , tests files like `parse.test.ts` should not be put inside `src` folder.

- you have migrated/implemented major features in project react web, but when you migrated/implemented features, tests are not taken good care of. please fix and update existing tests. 
when you improve the tests, you can also improve the source code logic by fixing or refactoring code. DO NOT get locked to the risk code that has weak or wrong logic, you should fix them.
finally make sure all tests run and pass locally with npm. you can update/fix tests file by file progressively. outdated or over-complicated or hard-to-maintain tests can be removed or rewritten. 

- you have improved the codebase several times, but running the tests/parity/scripts took a lot of time for your every improvement.  please refactor and improve the tests/parity/scripts/devops/ci to make it faster and more maintainable.  you may combine/deduplicate/reduce/clean/redesign some tests/parity/scripts/devops/ci/outdated/legacy if you need. update the readme/docs after your cleanup.
# rafactor
- analyze the core data-flow/code-logic of major features, find possible bugs and memory leak, improve it for the long term maintenance.

The goal is to refactor existing code and architecture to be more clear, extensible, functional-programming style, while improving logic correctness at the same time.
One task is to remove `class extends` inheritance and js prototype. `class extends` inheritance and prototype MUST be avoided by refactoring and rewriting.
es6 class may be used very very sparingly. No confusing `this` , no prototype. 
Prefer to avoid relying on dynamic binding, `.bind()` , `.call()` , `.apply()` , or method context unless truly necessary. 

Prefer composition over Inheritance: Replace class hierarchies with small, composable functions.
Prefer pure functions, immutable data, explicit inputs/outputs, and small composable functions.
Extract repeated logic into small, composable, named functions. The core logic becomes a pure function that can be unit tested.
Use function composition instead of nested calls.
If a function is too large, decompose it into smaller pure functions composed together.

Prefer explicit parameters, local variables, closures, or plain objects.
Prefer to reduce hidden state, side effects, mutation, and tightly coupled modules.
Prefer to avoid mutating inputs. prefer immutable-style functions: `(state, action) => newState` .
Prefer to replace mutation with immutable transformations.
Prefer to replace nested imperative logic with composition, mapping, filtering, or small helpers.
Prefer `map/filter` if it is better than LOOP. `reduce` should be avoid, you may use LOOP to replace `reduce` .

No Side Effects in Core Logic: Separate core business logic from I/O (database calls, network requests, DOM access, console.log). Core business functions must be pure; side effects should be pushed to the edges of the application.
Prefer to extract all side effects (logging, API calls, DOM updates) to the function's edges.

Identify shared mutable state across modules (globals, singletons, module-level variables), and improve the architecture to make it resuable and clear.

you may do some big code refactor to improve the architecture and data flow logic, to make it easier to maintain in the long term.

make a plan, refactor and improve the codebase progressively.

Keep the existing code/architecture working. Do not rewrite the whole codebase at once. you may refactor and improve code progressively.

yes, continue to refactor and improve towards more functional-programming style

for project begonia, please refactor code structure if you need, to make sure all source code and tests files should have less than **700** lines of code(other code-unrelated or unimportant files are not required). because if too many code exists in a single file, it will be hard to maintain. small files and modular architecture are always preferred.

please refactor code to migrate from pnpm to npm.
please keep as many code as possible unchanged, so most bun scripts and code should be kept for backward compatibility, but bun wont be used any more. bun code should not be removed. you should create new script for nodejs or add new entrypoint for nodejs. now update your plan.

Make minimal, mechanical changes first, then deeper improvements only when safe.

you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issue. 

there are many onlyoffice-pdf-editor audit/report code/scripts in this project, please reduce them and make them tidy. you can reorganize related code/scripts and track feature parity under a specific folder at `./upstream` to make it easy to maintain and migrate more features in the long term.
it would be better if you could make a scripts like `npm run check:upstream-parity` to check feature parity with upstream superdoc. and you may update related markdown/json/reports by running the scripts.

in project hardoc, 
current code is under active development. please review and refactor code if you need to make code more clean, correct, and extensible. please refactor outdated/legacy code that contains something like `superdoc/v0/v1/v2/v3/Compat/legacy...` by keeping only the right architecture or good implementation in the long term and removing legacy/deprecated code, so that the latest code does not contain legacy code and the logic is more clean and easier to maintain in the long term.

- try to avoid circular dependencies

- try to avoid hard-coded config/option
# toys

# play

# llm-toolchain

```prompt
i start this llm api gateway by `dist/one-api --config config.yaml`. when i use codex-cli with it, codex always shows "exceeded retry limit, last status: 429 Too Many Requests". please analyze logs and related code , and explain to me which channels/providers is the cause of the rate limit ?
```

# more

```prompt

```
