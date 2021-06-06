---
title: lib-office-remark-issues
tags: [issues, remark]
created: '2021-06-02T16:47:53.572Z'
modified: '2021-06-02T16:48:22.804Z'
---

# lib-office-remark-issues

# issues

- ## 

- ## 

- ## 

- ## 

- ## How do I get frontmatter and content of a mark?
- https://spectrum.chat/unified/remark/how-do-i-get-frontmatter-and-content-of-a-mark~bc4fc2a9-32a7-42f1-a86a-b7de4621568b
- I need to read the .md files and get its frontmatter as well as the normal Markdown content.
- If I do this, I get the normal Markdown part converted to HTML, but the frontmatter is gone


```JS
remark()
  .use(remarkFrontmatter)
  .use(remarkHtml)
  .process(fileContent)
```
- I was trying to get the frontmatter and the normal Markdown content at the same time but as separate things. I was not trying to convert it to HTML. 
- I think I understand now that Unified is meant to be used more like an enclosed system which does everything in plugins and produces the final result. Is that correct? That makes it a little difficult to use inside other systems like website backends if you need an intermediate state like I do. But at least not impossible.
- Unified is a toolchain/ecosystem for working with ASTs.
  - AST's can take some getting used to.
  - But is a powerful and flexible way of handling content, including intermediate states.
  - Incorporating unified into a website backend is a pretty common use-case.
- Yes, the vfile `data` property is intended to store intermediate data, like frontmatter.
  - If you have a virtual file that includes some YAML frontmatter, you could also use `vfile-matter` to parse that frontmatter and include the result in `file.data`.


