---
title: lib-office-gitbook-mdbook-community
tags: [community, gitbook, mdbook]
created: 2024-01-18T05:11:49.479Z
modified: 2024-01-18T05:12:04.708Z
---

# lib-office-gitbook-mdbook-community

# guide

# discuss-not-yet
- ## 

- ## 

- ## 🌐️ [Add multilingual support](https://github.com/rust-lang/mdBook/issues/5)
- Multiple designs possible:
  - One SUMMARY.md to rule them all
  - One SUMMARY.md for every language

- My suggestion is to have "one SUMMARY.md per language", but support page-to-page cross-linking between the different languages. 
  - The easiest way to do this is to consider that the files with the same name are the same chapters. In 99% this should work. 
  - A more complex way to do this is to add some kind of identifier to each file (something like UUID). If the identifiers of the files are identical, we can cross-link them.

- I've released a version 0.2 of mdbook-i18n-helpers._202308
# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Is there a self hosted GitBook alternative? : r/selfhosted _202101](https://www.reddit.com/r/selfhosted/comments/kphfbl/is_there_a_self_hosted_gitbook_alternative/)
- There are a lot of git powered static site generators 
- There is Notaku which uses Notion to edit the content and publishes it as a website with search, dark mode, .etc
