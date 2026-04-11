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
please analyze git commits and code as you need and explain to me what major features are in stirling-image but missing in ilove-image.

- please make migrations to ilove-image. 
- the following 2 features can be ignored:
1. HEIC/HEIF input and output
2. CUDA Docker variant can be ignored. Lite Docker variant should be migrated.
3. any features you feel unimportant or redundant can be ignored too
- feature-by-feature file map may have licensing risk. you can do it, but please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation work, but without licensing issues.
- in your implementation, you can also improve the code logic for features and make your implementation clean and extensible. tests are not necessary for your implementation, but you can write some important tests if you want. do not write too many tests, if logic is simple/clear, skipping tests is ok. 

you have migrated some features from ilove-stirling-image to ilove-image. 
please refactor code structure in ilove-image project to use similar architecture and code structure as ilove-stirling-image, to make it easy to migrate more features in the future. 

now recheck migrated features and improve your implementation in ilove-image, make it runnable locally with npm. make sure implementation is correct and extensible.
```

- git-repo-sync-pdf

```prompt

git repo `./ilove-pdf`  is several commits behind `./ilove-bentopdf`. ilove-pdf has MIT license, while ilove-bentopdf has GPL license. 
I want to migrate some features from ilove-bentopdf to ilove-pdf. 
please analyze git commits and code as you need and explain to me what major features are in ilove-bentopdf but missing in ilove-pdf.

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
please refactor code structure in ilove-pdf project to use similar architecture and code structure as ilove-bentopdf, to make it easy to migrate more features in the future. 
please use similar file/folder names instead of the same file/folder names as the original. you can also use similar implementation logic for features, but MUST not use the same function/variable names as the original. please make sure your feature implementation correct and extensible, without licensing issues.

if migration/refactoring of similar code architecture as ilove-bentopdf is complicated, you can make a plan first, then migrate as the plan.

now recheck migrated features and improve your implementation in ilove-pdf, make it runnable locally with npm. make sure implementation is correct and extensible.

please rename all local packages whose names start with "@stirling-image/" to "@datalking/", for example "@stirling-image/image-engine" should be renamed to "@datalking/image-engine". then update related code/tests/scripts. make sure project and tests still runs with no error using npm, without docker.
```

# code-review

```prompt

please recheck migrated features and improve your implementation in project ilove-image, make it runnable locally using npm without docker. Read some implementation logic details for major features, find possible bugs in code and fix them, make sure major features implementations are correct and extensible.

for project ilove-image, please refactor code structure when you need, to make sure all source code and tests files should have less than **800** lines of code(other code-unrelated or unimportant files are not required. ). because if too many code exists in a single file, it will be hard to maintain. small files and modular architecture are always preferred.

please recheck migrated features and implementations for possible licensing issues. if the code is too similar to upstream, you can adjust the risking code to avoid licensing issues. if features are already migrated under different names, it is unnecessary to design it as a standalone/separate tool as the upstream did, this also helps to avoid licensing issues.

document what you have migrated from which commit id for future migration reference at file `doc/devlog-migrations.md`. you can also add some concise migration guide/steps/tips in it to make it easy to do migrations later.
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

```

# toys

# play

```prompt

```

# more
