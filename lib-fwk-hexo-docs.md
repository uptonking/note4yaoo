---
title: lib-fwk-hexo-docs
tags: [docs, hexo]
created: 2024-02-09T10:54:05.814Z
modified: 2024-02-09T10:54:16.176Z
---

# lib-fwk-hexo-docs

# guide

# docs
- You can modify site settings in `_config.yml` or in an alternate config file.

- Front-matter is terminated by three dashes when written in YAML or three semicolons when written in JSON.
  - title
  - date: created date
  - updated
  - tags/categories: Not available for pages
  - permalink: Overrides the default permalink of the post.
  - published: For posts under _posts, it is true, and for posts under _draft, it is false
- Only posts support the use of categories and tags. 
  - Categories apply to posts in order, resulting in a hierarchy of classifications and sub-classifications. 
  - Tags are all defined on the same hierarchical level so the order in which they appear is not important.

- Tag plugins are different from post tags. They are ported from Octopress and provide a useful way for you to quickly add specific content to your posts.
# more
