---
title: dev-ing-toys-prompts
tags: [dev, prompt, toys]
created: 2026-04-11T01:31:00.503Z
modified: 2026-04-11T01:31:17.720Z
---

# dev-ing-toys-prompts

# guide

# coding-harness-xp
- 有些常用工具AI也记不住API, 比如pdfium, 可以将代码clone到本地让ai理解
# prompts 🔠

## ilove-image(stirling-image)

- codebase
  - a client/server app
  - the backend handles uploads, auth, SQLite, pipelines, tool execution, AI bridge calls, and serves the built SPA

```prompt
git repo `./ilove-image`  is several commits behind `./ilove-stirling-image`. ilove-image has MIT license, while ilove-stirling-image has GPL license. 
the goal is to migrate major features from ilove-stirling-image to ilove-image. 

please analyze git commits and code if you need, then explain to me what major features are in stirling-image but missing in ilove-image.

- please make migrations to ilove-image. 
- the following 2 features can be ignored:
1. HEIC/HEIF input and output
2. CUDA Docker variant can be ignored. Lite Docker variant should be migrated.
3. any features you feel unimportant or redundant can be ignored too
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation work, but without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation clean and extensible. tests are not necessary for your implementation, but you can write some important tests if you want. do not write too many tests, if logic is simple/clear, skipping tests is ok. 

- please rename all local packages whose names start with "@stirling-image/" to "@datalking/", for example "@stirling-image/image-engine" should be renamed to "@datalking/image-engine". then update related code/tests/scripts. make sure project and tests still runs with no error using npm, without docker.

- you have migrated/reimplemented some features from ilove-stirling-image to ilove-image. 

- for important features, the goal is to achieve full feature pairity or even better.

- please refactor code structure in ilove-image project to use similar architecture and code structure as ilove-stirling-image without licensing issue, to make it easy to migrate more features in the future. 

please recheck migrated features and improve your implementation in ilove-image, make it runnable locally with npm. make sure implementation is correct and extensible.

- research and make a full plan, then implement ilove-image to match full features of ilove-stirling-image, or even better than ilove-stirling-image, without licensing issues.

```

## ilove-pdf(bentopdf)

- codebase
  - a client-side-only PDF app, not a client/server architecture
  - Core PDF work is done with browser libraries and browser runtimes like pdf-lib, pdfjs-dist, tesseract.js, and qpdf.wasm

```prompt

git repo `./ilove-pdf`  is several commits behind `../ilove-bentopdf`. ilove-pdf has MIT license, while ilove-bentopdf has GPL license. 
the goal is to migrate major features from ilove-bentopdf to ilove-pdf. 

please analyze git commits and code if you need, then explain to me what major features are in ilove-bentopdf but missing in ilove-pdf.

- please make migrations to ilove-pdf. 
- the following 8 features should be migrated:
1. dynamic WASM loading
2. bookmarks / TOC / page labels / Bates
3. attachment extract/edit
4. overlay/underlay
5. better Compare PDFs
6. better OCR
7. better Image/PDF UX
8. features: divide pages, extract images, prepare PDF for AI, PDF layers
- other features can be ignored: 
1. Forms and signing, digital signature / validation / timestamp
2. Big conversion expansion, many Office, email converters, but you can migrate some if you want 
3. Workflow/automation
4. repair PDF
5. Encryption
6. PDF to PDF/A, PDF booklet,ebook, deskew, font-to-outline, rasterize PDF, ...
7. any features you feel unimportant or redundant can be ignored
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation work, but without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation clean and extensible. tests are not necessary for your implementation, but you can write some important tests if you want. do not write too many tests, if logic is simple/clear, skipping tests is ok. 

- please recheck the migrations and improve implementation for the the following features:
1. dynamic WASM loading
2. PDF layers, overlay/underlay
3. better OCR, make ocr robust
4. better extract
- these are the most important features now, the goal is to achieve full feature pairity or even better.
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

- research and make a full plan, then implement ilove-pdf to match full features of ilove-bentopdf, or even better than ilove-bentopdf, without licensing issues.
```

## ailovedoc(superdoc)

```prompt
`../superdoc` implemented renders, edits, and automates `.docx` files in the browser, headless on the server, and within AI agent workflows. but it is AGPL licensed.
- the final goal is to implement from scratch a new ai docx editing solution named ailovedoc similar to superdoc in current folder to avoid the licensing issues.
- ailovedoc should be implemented in a modular and extensible architecture for core features like rendering and editing, with functional programming style.

- in superdoc, running `pnpm dev:super-editor` shows a mininal editor demo that supports to toggle pagination. running `pnpm dev` shows a powerful editor demo that supports to toggle pagination, zoomable, toolbars, sidebars. please migrate the examples to ailovedoc without licensing issues, and make it runnable locally in ailovedoc. you should migrate all superdoc examples/features to a new standalone package at `apps/playground`, the basic ux can be a list of editor example names at left sidebar, when click one example name, the demo will show on the right.

- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible. tests are not necessary for your implementation.
- the most important feature to implement at first step is ai editing with track change support, other features can be implemented later progressively. a runnable ai editing example with track change should be provided.
- you may implement code architecture and structure similar to superdoc, but rewrite from scractch to avoid licensing issue. `EditorAdapter` is a good design, you should implement similar architecture. OOXML → ProseMirror handlers is powerful, you should implement your converter and handler by refrencing superdoc, but remember to avoid licensing issues. collaboration with yjs should be implemented. encryption/signing can be skipped now. you can reference as many superdoc code as possible, but remember to rewrite it to avoid license issue.
- please analyze related code and architecture, make a plan and implement your ailovedoc project.

- please analyze git repo and code if you need, then explain to me what major features are in superdoc but missing in ailovedoc.

- the most important feature is a powerful, robust, extensible, headless ai ooxml editing engine . 

please refactor code structure in ailovedoc project to use similar architecture and code structure as superdoc, to make it easy to migrate more features in the future.

please recheck migrated features and improve your implementation in project ailovedoc, make it runnable locally using npm without docker. Read core implementation logic details for major features, find possible bugs in code and fix them, make sure major features implementations are correct and extensible.

code at `./ailovedoc` should use npm workspaces, typescript, prosemirror, yjs.

please continue to migrate features related to ooxml editing with ai agent progressively. this is the most important feature. 

recheck and migrate full features of pdf compare and layers to ailovedoc. 

- the most important features to migrate and improve is:
1. full document API
2. richer OOXML editing
3. real layout/pagination fidelity
- these are the most important features now, the goal is to achieve full feature pairity or even better.

you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issue.  
you have worked on this problem several times but features are still lacking. They are the most important features at this moment, please migrate and improve it. make a plan and implement it to match full features of upstream without licensing issues.

- to achieve full feature parity with superdoc, help me choose the best option for long-term.

- you have migrated/reimplemented some features from superdoc to ailovedoc.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve full feature parity(ux can differ) like superdoc.

- ailovedoc should have full feature parity matching superdoc for important features like document data model, editing engine, rich-text formatting, layout-engine(supports toggling pagination), virtualized-rendering, document-rendering, track-change.

- these are the most important features now, the goal is to achieve full feature pairity or even better.
- make a plan, then migrate and improve full feature pairity, without licensing issues

- the goal now is to achieve robust and extensible ooxml editing engine with full feature parity of upstream supercode.

- the most important feature is a powerful, robust, extensible, headless ai ooxml editing engine with track change support .
- you may deep research, and reference the upstream superdoc code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues.

- please deep research superdoc, then can you design a similar solution in ailovedoc to improve it? is superdoc's solution good enough? if yes, solve it in a similar way for ailovedoc.

- you have worked on this several times but features are still lacking. They are the most important features at this moment. DO NOT stop untill you achieve full feature parity. 

- you may do a big code refactor to match full feature of superdoc in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- research and make a full plan, then implement ailovedoc to match full features of superdoc, or even better than superdoc, without licensing issues.

------

- you may reference how superdoc implements it, then do a similar or better implementation in ailovedoc without licensing issue.

- superdoc's overall architecture is good enough to follow. Mostly ailovedoc should use similar architecture to superdoc.

```

## hardoc(onlyoffice-pdf)

```prompt

onlyoffice-pdf-editor(code is at several git repos in current folder) implements renders, edits, annotates `.pdf` files in the browser, but it is AGPL licensed.
- the final goal is to implement from scratch a new extensible web pdf editor named hardoc with in-place text editing features similar to onlyoffice-pdf-editor/adobe-acrobat at folder `./hardoc`  to avoid the licensing issues.
- hardoc pdf editor should be more of a headless client-server architecture, so that you can build a hardoc cli with a hardoc sdk. 
- hardoc should be implemented in a modular and extensible architecture for core pdf features like viewing and editing, with functional programming style.

- goals for pdf editing:
1. modular and extensible architecture for pdf viewing and editing: you may design sub packages like state/view/command/transform/... when you need. you may design a sdk if you want.
2. in-place text editing feature like adobe acrobat; undo/redo
3. pdf highlights, annotations with simple shapes
4. pdf file open and save
5. in-place text editing is the most important feature to implement now, the following features can be planned, but unnecessary to implement at this moment: forms, ocr, collaboration, ai-editing, complicated shapes, search. any feature you feel unimportant to in-place text editing can be delayed to implement,  but architecture should be extensible enough to support them later.

- tech stack needs to use open source libs/fwk:
you may reference architecture and implementation details of onlyoffice pdf editor. 
code at `./hardoc` should use npm workspaces, typescript.
AGPL dependencies like MuPDF should be avoided, ask for approve if you must use.

- serveral questions need to be made clear before implementation:
1. should core pdf data model be headless/dom-agnostic, so that it will be usable in nodejs?
2. should wasm like pdfium be used?
3. should canvas framework like fabric/knova be used?

please analyze onlyoffice architecture, and give tips to my question before iplementing new pdf editor hardoc.

- the core pdf editor should be modular and extensible. 

one goal is to support to view both text pdf and scanned image pdf, text pdf should support in-place text editing like onlyoffice/adobe-acrobat. both text and image pdf should support annotations with simple shapes and text.

one goal is to enhance hardoc pdf editor with more important features:
1. robust undo/redo that is friendly to collaborative editing
2. ocr, you may reference how onlyoffice implements it, you may integrates Tesseract(whether to use wasm is up to you)
3. pdf search
4. view page thumbnails, pdf bookmarks, search... these ui-related features should be implemented in an extensible way like state/view so that it will be easy to adjust ux later.
5. advanced annotation shapes
7. ready for ai editing, you may reference how onlyoffice, full migration is not required
6. the core pdf editor and app should be modular and extensible. an extensible pdf sdk can be provided.

one goal is to enhance hardoc pdf editor with more features:
- collaborative editing
- ocr with llm

project onlyoffice and project at `~/Documents/repos/office/all-pdf/open-pdf-studio` can be used as implementation reference, you can reference their architecture and code, but you should rewrite code to avoid licensing issue. 

- git repo at `~/Documents/repos/office/all-pdf/open-pdf-studio` is a buggy and not-featureful pdf editor. please read related code and analyze architecture. do you think open-pdf-studio is good start point for implement a custom pdf editor?  compare the architecture of open-pdf-studio and onlyoffice.
  - 采用图片的方案

- the final goal is to implement from scratch a extensible web pdf editor named hardoc with in-place text editing features similar to onlyoffice/adobe-acrobat at folder `./hardoc`  to avoid the licensing issues. 
- forms, ocr, collaboration, ai-editing, complicated shapes, search is not required now, but architecture should support these features later.
- please make a plan for the extensible text editing editor first, then implement it at folder `./hardoc`.

- please refactor code structure in hardoc project to use similar architecture and code structure as onlyoffice without licensing issue, to make it easy to migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- please analyze code and docs if you need, then explain to me what major features are in onlyoffice pdf editor but missing in hardoc. 

recheck and migrate full features of True PDF text editing engine with annotation support. 

- you have migrated/reimplemented some features from onlyoffice pdf editor to hardoc.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve full feature parity(ux can differ) like onlyoffice-pdf-editor.

- hardoc should have full feature parity matching onlyoffice-pdf-editor for important features like in-place text editing engine,undo/redo, pdf annotations/highlights, plugin architecture and manager, pdf search, pdf page-thumbnails, bookmarks.

- you have worked on this several times but features are still lacking. They are the most important features at this moment, please migrate and improve it. 

make a plan and implement it to match full features of upstream without licensing issues.

- you can reference code from onlyoffice pdf editor. feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible.  

please make a plan, then improve the core in-place text editing engine to make it correct and extensible without licensing issues.

- the goal now is to achieve full feature parity of native True PDF text editing engine like onlyoffice pdf editor.

- the most important feature in hardoc is a powerful, robust, extensible, native True PDF in-place text editing engine with annotation support like onlyoffice pdf editor.

- you can deep research and reference good deisgn from onlyoffice pdf editor.
- you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues.

- please deep research the onlyoffice pdf editor, then can you design a similar solution to solve it? is onlyoffice's solution good enough? if yes, solve it in a similar way for hardoc.

- you have worked on this several times but still not solve it. 

- you may do a big code refactor to match full feature of onlyoffice-pdf-editor in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- research and make a full plan, then implement hardoc to match full features of onlyoffice-pdf-editor, or even better than onlyoffice-pdf-editor, without licensing issues.

------

- you may reference how onlyoffice-pdf-editor implements it, then do a similar or better implementation in hardoc without licensing issue.

- onlyoffice-pdf-editor's overall architecture is good enough to follow. Mostly hardoc should use similar architecture to onlyoffice pdf editor. 

You should implement hardoc pdf editor in a similar architecture of onlyoffice pdf editor. If onlyoffice does not use the rust core architecure, you MUST NOT do it.

DO NOT search the web for onlyoffice pdf api, you should find and read source code of onlyoffice pdf editor directly in current folder ~/Documents/repos/office/all-office/onlyoffice

```

## grist-office

```prompt
- Grist is a modern relational spreadsheet. It combines the flexibility of a spreadsheet with the robustness of a database. 
- The final goal is to implement an alternative react frontend webapp at folder `app/client-react` at the current git branch `feat/office-react`, with the same features as existing backbonejs frontend webpp at `app/client`,  using modern tech stacks like npm, reactjs, typescript, tailwindcss, zustand, @tanstack/react-table. After you finished the react webapp, `npm run start:app` should start the new react webapp, the legacy yarn toolchain should still be kept for backward compatibility. you should implement it in a way to make it easy to merge code changes from `main` branch to `feat/office-react` branch in the future, so please keep as many code unchanged as possible.
- one goal is to rewrite all the existing backbonejs ui/ux with modern react ui/ux, but you can implement the core speadsheet view/create/edit/save data flow first, then migrate more and more features. 
- react webapp should support all the routing urls of existing backbonejs webapp, using the same existing backend api.

- please read and analyze git commits/code if you need, then explain to me what major features are in backbonejs webapp but missing in react webapp.

- the following features can be planned, but implemention may be delayed if you want:
1. Can be displayed on a static website with grist-static.
2. A self-contained desktop app for viewing and editing locally: grist-desktop.
3. Native forms. Create forms that feed directly into your spreadsheet.
4.Sandboxing options for untrusted documents
5. AI Formula Assistant 
6. integrations to airtable/...

- tech stack for react webapp needs to use open source libs/fwk:
  - use npm workspaces, typescript, reactjs(not vue), tailwindcss, zustand, no jquery/knockoutjs/backbone.
  - for ui components, you can use base-ui, source clone is at `~/gh-mirror/mui/base-ui` for your reference.
  - use floating-ui instead of @popperjs/core, source code is here for your reference `~/gh-mirror/floating-ui/floating-ui`.
  - you can reuse existing dependencies for easier feature migration.
  - for spreadshhet table, you should use @tanstack/react-table. the source code is cloned at folder `~/gh-mirror/tanstack` for your reference.
  - you may use zustand for state management in framework-agnostic core package, the source code is at folder `~/gh-mirror/pmndrs/zustand` for your reference.

- the most important feature in react webapp is a modular, extensible, headless spreadsheet view/editing engine with undo/redo history support like backbonejs webapp. you should implement it in a way to make it easy to merge code changes from `main` branch to `feat/office-react` branch in the future, so keep as many code unchanged as possible.

- you have migrated/reimplemented some features from backbonejs webapp to react webapp.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve full feature parity(ux can differ).

- you have worked on this several times but features are still lacking.

- please deep research the existing backbonejs webapp, then can you design a similar solution in react webapp to achieve full feature parity?

- you may deep research and reference the existing code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style with modern tech stacks like react/typescript-utils. 

- you may do a big code refactor to match full feature of backbonejs webapp in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- research and make a full plan, then implement the react webapp to match full features of existing backbonejs webapp, or even better than backbonejs webapp.

- `grist-static` is a fully in-browser build of Grist for displaying spreadsheets on a website without back-end support.

```

## slaides(PPTist)

```prompt
- project `PPTist` at `../PPTist` is an online presentation webapp that replicates most of the commonly used features of MS PowerPoint, allowing for the editing and presentation of PPT online, also supports AIPPT. But it has AGPL license.
- project `slaides` at current folder is an old version of `PPTist` with apache2 license, but many commits behind PPTist.

- please read and analyze git commits/code if you need, then explain to me what major features are in PPTist but missing in slaides.

- the final goal is to implement a framework-agnostic, modular, extensible, headless ai ppt editing solution named `slaides` with features similar to `PPTist` to avoid the licensing issues. legacy vue code should be kept for reference only.
- goals:
1. re-architect slaides project to have a framework-agnostic headless core package, with react/vue ui binding package and appropriate utils package.
- migrate PPTist's robust feature-rich ppt view/editing features to slaides, this is the most important feature, the goal is full feature parity for ppt view/editing, for example page zoom, Page Editing, Element/Images/Shapes Editing, Rich text editing, Slide Show...
2. undo/redo support, friendly to collaboration.
3. Import/export .pptx files, Export local files (PPTX, JSON, images, PDF).
4. Mobile friendly: Basic editing, Basic preview, Play preview.
5. migrate PPTist's ai editing solution to slaides, better to implement as a separate package: ai workflow, outline editing, use template, streaming-generation...
6. a runnable demo/example should be provided.

- the following features can be planned, but implemention may be delayed if you want:
- the following features should be implemented if the core architecture is stable:
1. table
2. chart
3. Formulas
4. Audio, Video
5. vue ui binding

- tech stack for project slaides needs to use open source libs/fwk:
  - projects/packages at `slaides` should use npm workspaces, typescript, reactjs(not vue), tailwindcss.
  - you can reuse dependencies from PPTist for easier feature migration.
  - for rich text editing in ppt, you should still use prosemirror. the source code for prosemirror is cloned at folder `~/Documents/repos/yaoo/nostalgia-studio/editor-prosemirror/src-pkgs` for your reference.
  - you may use `zustand/vanilla` for state management in framework-agnostic core package, the source code is at folder `~/gh-mirror/pmndrs/zustand` for your reference.
  - for drag-drop, you may use  `~/gh-mirror/atlassian/pragmatic-drag-and-drop` to implement robust dnd.
  - all local packages names should start with `@datalking/`, for example `@datalking/slaides-core`,`@datalking/slaides-react`...

- project PPTist can be used as implementation reference, you can reference its architecture and code.
- you may deep research and reference the upstream code, you may use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issue. 
you may use similar file/folder names instead of the same file/folder names as the original. you may also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.

- the most important feature in slaides is a framework-agnostic, modular, extensible, headless ai ppt view/editing engine with undo/redo history support like PPTist.

- you have migrated/reimplemented some features from PPTist to slaides.

- please recheck logic parity detail by detail for every major feature, the goal is to achieve full feature parity(ux can differ).

- you have worked on this several times but features are still lacking.

- please deep research the PPTist, then can you design a similar solution in slaides to achieve full feature parity?

- you can deep research, referencing good deisgn from PPTist editing engine.

- you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issues.

- you may do a big code refactor to match full feature of PPTist in a similar architecture, to make it easier to maintain and migrate more features in the long term. legacy code may be migrated or removed by rewriting.

- research and make a full plan, then implement slaides to match full features of PPTist, or even better than PPTist, without licensing issues.

```

# code-review 👀

```prompt

for project hardoc, please recheck migrated features and improve your implementation, make it runnable locally using npm without docker. Analyze core data flow and implementation logic details for major features, find possible bugs in code and fix them, make sure major features implementations are correct and extensible.

please recheck migrated features and implementations for possible licensing issues. if the code is too similar to upstream, you can adjust the risking code to avoid licensing issues. if features are already migrated under different names, it is unnecessary to design it as a standalone/separate tool as the upstream did, this also helps to avoid licensing issues.

document what you have migrated from which commit id for future migration reference at file `doc/devlog-migrations.md`. you can also add some concise(less than 120 lines) migration guide/steps/tips in it to make it easy to do migrations later.
```

# tests

```
you have migrated/implemented major features in project react web, but when you migrated/implemented features, tests are not taken good care of. please fix and update existing tests. 
when you improve the tests, you can also improve the source code logic by fixing or refactoring code. DO NOT get locked to the risk code that has weak or wrong logic, you should fix them.
finally make sure all tests run and pass locally with npm. you can update/fix tests file by file progressively. outdated or over-complicated or hard-to-maintain tests can be removed or rewritten. 
```

# rafactor

```prompt
The goal is to refactor existing code and architecture to be more clear, extensible, functional-programming style, while improving logic correctness at the same time.
One task is to remove `class extends` inheritance and js prototype. `class extends` inheritance and prototype MUST be avoided by refactoring and rewriting.
es6 class may be used very very sparingly. No confusing `this`, no prototype. 
Prefer to avoid relying on dynamic binding, `.bind()`, `.call()`, `.apply()`, or method context unless truly necessary. 

Prefer composition over Inheritance: Replace class hierarchies with small, composable functions.
Prefer pure functions, immutable data, explicit inputs/outputs, and small composable functions.
Extract repeated logic into small, composable, named functions. The core logic becomes a pure function that can be unit tested.
Use function composition instead of nested calls.
If a function is too large, decompose it into smaller pure functions composed together.

Prefer explicit parameters, local variables, closures, or plain objects.
Prefer to reduce hidden state, side effects, mutation, and tightly coupled modules.
Prefer to avoid mutating inputs. prefer immutable-style functions: `(state, action) => newState`.
Prefer to replace mutation with immutable transformations.
Prefer to replace nested imperative logic with composition, mapping, filtering, or small helpers.
Prefer `map/filter` if it is better than LOOP. `reduce` should be avoid, you may use LOOP to replace `reduce`.

No Side Effects in Core Logic: Separate core business logic from I/O (database calls, network requests, DOM access, console.log). Core business functions must be pure; side effects should be pushed to the edges of the application.
Prefer to extract all side effects (logging, API calls, DOM updates) to the function's edges.

Identify shared mutable state across modules (globals, singletons, module-level variables), and improve the architecture to make it resuable and clear.

you may do some big code refactor to improve the architecture and data flow logic, to make it easier to maintain in the long term.

make a plan, refactor and improve the codebase progressively.

Keep the existing code/architecture working. Do not rewrite the whole codebase at once. you may refactor and improve code progressively.

yes, continue to refactor and improve towards more functional-programming style
```



```prompt
for project ailovedoc, please refactor code structure if you need, to make sure all source code and tests files should have less than **700** lines of code(other code-unrelated or unimportant files are not required). because if too many code exists in a single file, it will be hard to maintain. small files and modular architecture are always preferred.

please refactor code to migrate from pnpm to npm.
please keep as many code as possible unchanged, so most bun scripts and code should be kept for backward compatibility, but bun wont be used any more. bun code should not be removed. you should create new script for nodejs or add new entrypoint for nodejs. now update your plan.

Make minimal, mechanical changes first, then deeper improvements only when safe.

you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it in functional programming style without licensing issue. 
```

# toys

# play

# llm-toolchain

```prompt
i start this llm api gateway by `dist/one-api --config config.yaml`. when i use codex-cli with it, codex always shows "exceeded retry limit, last status: 429 Too Many Requests". please analyze logs and related code , and explain to me which channels/providers is the cause of the rate limit ?
```

# more

```prompt

```
