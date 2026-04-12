---
title: dev-ing-toys-prompts
tags: [dev, prompt, toys]
created: 2026-04-11T01:31:00.503Z
modified: 2026-04-11T01:31:17.720Z
---

# dev-ing-toys-prompts

# guide

# prompts 🔠

## git-repo-sync-image

```prompt
git repo `./ilove-image`  is several commits behind `./ilove-stirling-image`. ilove-image has MIT license, while ilove-stirling-image has GPL license. 
I want to migrate some features from ilove-stirling-image to ilove-image. 
please analyze git commits and code when you need and explain to me what major features are in stirling-image but missing in ilove-image.

- please make migrations to ilove-image. 
- the following 2 features can be ignored:
1. HEIC/HEIF input and output
2. CUDA Docker variant can be ignored. Lite Docker variant should be migrated.
3. any features you feel unimportant or redundant can be ignored too
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation work, but without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation clean and extensible. tests are not necessary for your implementation, but you can write some important tests if you want. do not write too many tests, if logic is simple/clear, skipping tests is ok. 

you have migrated some features from ilove-stirling-image to ilove-image. 
please refactor code structure in ilove-image project to use similar architecture and code structure as ilove-stirling-image without licensing issue, to make it easy to migrate more features in the future. 

now recheck migrated features and improve your implementation in ilove-image, make it runnable locally with npm. make sure implementation is correct and extensible.

please rename all local packages whose names start with "@stirling-image/" to "@datalking/", for example "@stirling-image/image-engine" should be renamed to "@datalking/image-engine". then update related code/tests/scripts. make sure project and tests still runs with no error using npm, without docker.
```

- git-repo-sync-pdf

```prompt

git repo `./ilove-pdf`  is several commits behind `./ilove-bentopdf`. ilove-pdf has MIT license, while ilove-bentopdf has GPL license. 
I want to migrate some features from ilove-bentopdf to ilove-pdf. 
please analyze git commits and code when you need and explain to me what major features are in ilove-bentopdf but missing in ilove-pdf.

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

you have migrated some features from ilove-bentopdf to ilove-pdf. 
- please recheck the migrations and improve implementation for the the following features:
1. dynamic WASM loading
2. PDF layers, overlay/underlay
3. better OCR, make ocr robust
4. better extract images
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible. tests are not necessary for your implementation.

ocr is the most important feature in ilove-pdf project. 
please recheck your migrated ocr features and implementation logic, make sure the logic is correct without licensing issues. improve the ocr logic to make it robust and extensible.

you have migrated some features from ilove-bentopdf to ilove-pdf. 

please refactor code structure in ilove-pdf project to use similar architecture and code structure as ilove-bentopdf without licensing issue, to make it easy to migrate more features in the future. 
you may use similar file/folder names instead of the same file/folder names as the original. you may also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.

if migration/refactoring of similar code architecture as ilove-bentopdf is complicated, you can make a plan first, then migrate as the plan.

now recheck migrated features and improve your implementation in ilove-pdf, make it runnable locally with npm. make sure implementation is correct and extensible.

for the most important features pdf compare and PDF layer,  why are you always migrating and improving without full features matching the upstream? you have improved several times, why is it always lacking features behind the upstream? what is the reason? what should be done to macth the upstream? explain to me. if it it complicated, you can make a plan and discuss with me
```

- hardoc-pdf

```
onlyoffice implements renders, edits, annotates  `.pdf` files in the browser. but it is AGPL licensed.
- the final goal is to implement from scratch a new extensible web pdf editor named hardoc with in-place text editing features similar to onlyoffice/adobe-acrobat at folder `./hardoc`  to avoid the licensing issues.
- goals for pdf editing:
1. modular and extensible architecture for pdf viewing and editing: you may design sub packages like state/view/command/transform/... when you need. you may design a sdk if you want.
2. in-place text editing feature like adobe acrobat; undo/redo
3. pdf highlights, annotations with simple shapes
4. pdf file open and save
5. in-place text editing is the most important feature to implement now, the following features can be planned, but unnecessary to implement at this moment: forms, ocr, collaboration, ai-editing, complicated shapes, search. any feature you feel unimportant to in-place text editing can be delayed to implement,  but architecture should be extensible enough to support them later.

- tech stack needs to use open source libs/fwk:
you may reference architecture and implementation details of onlyoffice. 
code at `./hardoc` should use npm workspaces, typescript.
AGPL dependencies like MuPDF should be avoided, ask for approve if you must use.

- serveral questions need to be made clear before implementation:
1. should core pdf data model be headless/dom-agnostic, so that it will be usable in nodejs?
2. should wasm like pdfium  be used?
3. should canvas framework like fabric/knova be used?

please analyze onlyoffice architecture, and give tips to my question before iplementing new pdf editor hardoc.

- git repo at `~/Documents/repos/office/all-pdf/open-pdf-studio` is a buggy and not-featureful pdf editor. please read related code and analyze architecture. do you think open-pdf-studio is good start point for implement a custom pdf editor?  compare the architecture of open-pdf-studio and onlyoffice.
  - 采用图片的方案

- the final goal is to implement from scratch a new extensible web pdf editor named hardoc with in-place text editing features similar to onlyoffice/adobe-acrobat at folder `./hardoc`  to avoid the licensing issues. you can also borrow good deisgn from open-pdf-studio. forms, ocr, collaboration, ai-editing, complicated shapes, search is not required now, but architecture should support these features later.
- please make a plan for the extensible text editing editor first, then implement it at folder `./hardoc`.

- you have migrated some features from onlyoffice pdf editor to hardoc.

- I want to migrate more pdf editing features from onlyoffice pdf editor to hardoc. 
- please analyze code and docs when you need, then explain to me what major features are in onlyoffice pdf editor but missing in hardoc. 

- you can reference code from onlyoffice pdf editor. feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible. tests are not necessary for your implementation.

```

# code-review

```prompt

please recheck migrated features and improve your implementation in project ailovedoc, make it runnable locally using npm without docker. Read some implementation logic details for major features, find possible bugs in code and fix them, make sure major features implementations are correct and extensible.

for project ailovedoc, please refactor code structure when you need, to make sure all source code and tests files should have less than **800** lines of code(other code-unrelated or unimportant files are not required. ). because if too many code exists in a single file, it will be hard to maintain. small files and modular architecture are always preferred.

please recheck migrated features and implementations for possible licensing issues. if the code is too similar to upstream, you can adjust the risking code to avoid licensing issues. if features are already migrated under different names, it is unnecessary to design it as a standalone/separate tool as the upstream did, this also helps to avoid licensing issues.

document what you have migrated from which commit id for future migration reference at file `doc/devlog-migrations.md`. you can also add some concise(less than 120 lines) migration guide/steps/tips in it to make it easy to do migrations later.
```

# tests

```
you have migrated/impelmented some features in project ilove-image, but when you implement features, tests are not taken good care of. please fix and update existing tests. 
make sure all tests run and pass locally with npm. you can update/fix tests file by file progressively. outdated or over-complicated or hard-to-maintain tests can be removed. 
```

# rafactor

```prompt
please refactor code to migrate from pnpm to npm.
please keep as many code as possible unchanged, so most bun scripts and code should be kept for backward compatibility, but bun wont be used any more. bun code should not be removed. you should create new script for nodejs or add new entrypoint for nodejs. now update your plan.

you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it without licensing issue.  
```

# toys

# play

- ailovedoc

```prompt
`./superdoc` implemented renders, edits, and automates `.docx` files in the browser, headless on the server, and within AI agent workflows. but it is AGPL licensed.
the goal is to implement from scratch a new docx editing solution similar to superdoc at folder `./ailovedoc`  to avoid the licensing issues.
code at `./ailovedoc` should use npm workspaces, typescript, prosemirror, yjs.
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation correct and extensible. tests are not necessary for your implementation.
- the most important feature to implement at first step is ai editing with track change support, other features can be implemented later progressively. a runnable ai editing example with track change should be provided.
- you should implement code architecture and structure similar to superdoc, but rewrite from scractch to avoid licensing issue. `EditorAdapter` is a good design, you should implement similar architecture. OOXML → ProseMirror handlers is powerful, you should implement your converter and handler by refrencing superdoc, but remember to avoid licensing issues. collaboration with yjs should be implemented. encryption/signing can be skipped now. you can reference as many superdoc code as possible, but remember to rewrite it to avoid license issue.
- please analyze related code and architecture, make a plan and implement your ailovedoc project.

you have migrated some features from superdoc to ailovedoc.
please analyze git repo and code when you need, then explain to me what major features are in superdoc but missing in ailovedoc.

please refactor code structure in ailovedoc project to use similar architecture and code structure as superdoc, to make it easy to migrate more features in the future.

please recheck migrated features and improve your implementation in project ailovedoc, make it runnable locally using npm without docker. Read some implementation logic details for major features, find possible bugs in code and fix them, make sure major features implementations are correct and extensible.

please continue to migrate features related to ooxml editing with ai agent progressively. this is the most important feature. 

recheck and migrate full features of pdf compare and layers to ailovedoc. 

the current most important features to migrate and improve is:
1. full document API
2. richer OOXML editing
3. real layout/pagination fidelity

you may reference the upstream code, use similar dependencies, and implement similar logic, but you should rewrite it without licensing issue.  you have done it several times but features are still lacking. They are the most important features at this moment, please migrate and improve it. make a plan and implement it to match full features of upstream without licensing issues.

```

# llm-toolchain

```prompt
i start this llm api gateway by `dist/one-api --config config.yaml`. when i use codex-cli with it, codex always shows "exceeded retry limit, last status: 429 Too Many Requests". please analyze logs and related code , and explain to me which channels/providers triggerred the rate limit ?
```

# more

```prompt

```
