---
title: lib-edit-typst-latest-changelog
tags: [changelog, latex, typst]
created: 2026-06-19T12:33:59.398Z
modified: 2026-06-19T12:34:13.992Z
---

# lib-edit-typst-latest-changelog

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-news-typst 🆕
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Typst 0.15 Released : r/typst _202606](https://www.reddit.com/r/typst/comments/1u6n3qx/typst_015_released/)
  - 0.15 released with MathML support, variable fonts, bundle export (experimental), multiple bibliographies, among many other additions.
- [Typst: Typst 0.15 contains multitudes – Typst Blog _202606](https://typst.app/blog/2026/typst-0.15/)
  - When we first released Typst, PDF was the only supported export format. In Typst 0.5, we added PNG export and in Typst 0.8 SVG export. Those two were still very close to PDF export in that they all hook in after Typst has fully laid out the document. Then, in Typst 0.13, we added experimental support for HTML export. This is a structurally very different output format, as it needs to hook in earlier, with layout being fully delegated to the browser.
  - In our effort to port the documentation on https://typst.app/docs to Typst itself, we needed a way to export multiple HTML pages from a single Typst project.
  - while designing the feature, we've discovered a beautiful generalization: Why add this new element and restrict the feature to HTML? We already have an element that can represent an entire HTML document: The document element.
  - With the new bundle export, the document element takes on this new role and is complemented by a new asset element. I'm sure some of you will abuse the asset element as an output channel to do raw computation with Typst. 
  - One other new feature in Typst 0.15 that's very useful in combination with bundle export is the within selector that scopes an introspection down to the descendants of a specific element. Introspections are by default global to a full bundle. With this selector, you can scope them down to a specific document.

- Still lacking functional wrapped figures unfortunately
- All good but the major journals still don't accept it. I wanted to use it but because of this single fact, had to install several gigabytes of LaTeX engine only to write a paper.

- ## [The day has come: variable fonts work in Typst : r/typst _202606](https://www.reddit.com/r/typst/comments/1ty908f/the_day_has_come_variable_fonts_work_in_typst/?sort=top)
  - the well-known axes (wght, slnt, wdth, opsz...) get set automatically from weight / style / stretch / size like you'd expect — but you can still override them
  - custom axes go through a new variations dict, keyed by the case-sensitive 4-letter tag

# discuss-changelog
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## 
