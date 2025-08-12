---
title: lib-editor-prosemirror-dev-diff
tags: [diff, prosemirror, track-change]
created: 2025-08-07T17:21:52.673Z
modified: 2025-08-07T17:22:10.051Z
---

# lib-editor-prosemirror-dev-diff

# guide

# discuss-stars
- ## 

- ## TinyMCE 8.0’s Suggested Edits changes the way teams work , for good _202508
- https://x.com/joinTiny/status/1955255652319633475
  - 产品动画很好

- ## [The Third Bit: Diff and Merge for ProseMirror _201711](https://third-bit.com/2017/11/22/prosemirror-diff-merge/)
- I think it would be really exciting to implement a general JSON-based diff-and-merge for ProseMirror that leveraged the structural information in the schemas in the way that Compare++ and SemanticMerge do syntax-aware merging for code. 

# discuss-diff
- ## 

- ## [Diff plugin - discuss. ProseMirror _202309](https://discuss.prosemirror.net/t/diff-plugin/5837)
- No ready-made solution exists for this. It is possible to distill some steps down to a set of changed ranges with `prosemirror-changeset` , and display those in a document as decorations (widgets for deleted text, inline styling for inserted text), but a bunch of custom code is needed for that.

- ## 🌰 [How to compare the differences between different texts(No Steps)？ - discuss. ProseMirror _202404](https://discuss.prosemirror.net/t/how-to-compare-the-differences-between-different-texts-no-steps/6337)
- I have solved it, I use this open source libraryhttps://github.com/hamflx/prosemirror-diff/blob/master/src/diff.js, I use [diff-match-patch]

# discuss-track-change
- ## 

- ## 

- ## 🚀🌰 [Releasing prosemirror-suggestion-mode - Show - discuss. ProseMirror _202502](https://discuss.prosemirror.net/t/releasing-prosemirror-suggestion-mode/8239)
  - I’d found a few old threads on this but they all seemed to have not resulted in a solution
  - so I wrote my own and thought I’d do so as a plugin and release it.
  - In that last thread @marjin suggests doing this with prosemirror-changeset. As mention in my Implementation Choices I went down that path and have a branch linked there but ran into issues (may have been understanding things wrong) when individual changes were approved/rejected.
  - After talking with @SMores I realized several issues and limitations and largely did a full re-write. It now supports all step types, markup and utilizes prosemirror commands

- 👷 @handlewithcare/prosemirror-suggest-changes: It looks like we took a very similar approach! We opted for a “decorator” around dispatchTransaction, rather than appendTransactions, and made step handlers for the other step types as well.
# discuss
- ## 

- ## 

- ## [Visualize changes between 2 tiptap jsons - discuss. ProseMirror _202504](https://discuss.prosemirror.net/t/visualize-changes-between-2-tiptap-jsons/8328)
  - I want to diff 2 rendered versions of tiptap jsons
- Sharing my ideas to approach this:
  - Traverse both documents - The obvious way is to use some diffing library like diff-match-patch , json-diff or something to obtain text differences, but handling structural differences like complete node deletions/insertions are very tricky and difficult especially for documents with custom nodes and to make highlights
  - Comparing rendered HTML - This is kinda unreliable way , but it works for some cases.
  - Wrap insertions/deletions with Marks - This approach is to intercept transactions and wrap them with marks, we can capture deletions by `invertStep()` but the tricky part is with cursor misalignment and ghost nodes.
  - another idea is get mappings and content through prosemirror-changeset and map them at end, but the offsets may differ as the document content is changed.

- We create a custom text representation from the prosemirror document, use git to find the differences and then visualize this as another prosemirror document. Works quite well.

- i’ve tried normalizing my document into markdown, create html of 2 versions and diff them using a npm package, it went well. But the goal is to maintain the structure as it is, for simple documents, these approaches will be fine, but i have custom nodes and re-structuring plain text back to custom nodes seems not practical
