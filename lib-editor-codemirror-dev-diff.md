---
title: lib-editor-codemirror-dev-diff
tags: [codemirror, diff, json-patch]
created: 2024-07-29T11:49:17.052Z
modified: 2024-07-29T11:49:33.248Z
---

# lib-editor-codemirror-dev-diff

# guide

# diff-formats

## [nbdime jupyter](https://nbdime.readthedocs.io/en/latest/diffing.html)

- nbdime – diffing and merging of Jupyter Notebooks
  - Jupyter notebooks are useful, rich media documents stored in a plain text JSON format. 
  - However, primitive line-based diff and merge tools do not handle well the logical structure of notebook documents
  - nbdime provides “content-aware” diffing and merging of Jupyter notebooks.
- A diff object represents the difference B-A between two objects, A and B, as a list of operations (ops) to apply to A to obtain B
- The diff objects in nbdime are: 
  - json-compatible nested structures of dicts (with string keys) 
  - and lists of values with heterogeneous(不同种类的) datatypes (strings, ints, floats)

- nbdime vs json-patch
- operations
  - JSONPatch contains operations move, copy, test not used by nbdime.
  - nbdime contains operations addrange, removerange, and patch not in JSONPatch.
- patch 
  - JSONPatch uses a deep JSON pointer based path item in each operation instead of providing a recursive patch op
  - nbdime uses a key item in its patch op.
- diff object
  - JSONPatch can represent the diff object as a single list.
  - nbdime uses a tree of lists.

- nbdime implements a three-way merge of Jupyter notebooks and a subset of generic JSON objects.

- A merge operation with a shared origin object base and modified objects, local and remote, outputs these merge results:
  - a fully or partially merged object
  - a set of merge decision objects that describe the merge operation

- Each three-way notebook merge is based on the differences between the base version and the two changed versions – local and remote. These differences, ``base`` with local and base with remote, are then compared, and for each change a set of decisions are made. A merge decision object represents such a decision, and is represented as a dict with the following entries

- 
- 
- 
- 

# discuss-not-yet
- ## 

- ## 

- ## ✨ [Suggestion: Support true inline diff in unified merge view _202408](https://github.com/codemirror/dev/issues/1419)
  - VS Code just added this in the July 2024 update
- I don't intend to work on this.

- ## [FR: Three-way comparison for the V6 merge plugin - v6 - discuss. CodeMirror _202402](https://discuss.codemirror.net/t/fr-three-way-comparison-for-the-v6-merge-plugin/7879)
  - I am curious whether there’s a chance that the CodeMirror 6 merge plugin would support three-way diffs one day. 
  - Currently, the only alternatives I found is the CodeMirror 5 plugin 1 as well as a curious, but currently small, project called MisMerge
  - https://beartocode.github.io/mismerge/

# discuss-diff/track-changes
- ## 

- ## 

- ## 🔀🌰 [Feasability Assessment: Extension to decorate conflict markers - v6 - discuss. CodeMirror _202407](https://discuss.codemirror.net/t/feasability-assessment-extension-to-decorate-conflict-markers/8459)
  - this is not about building a three-way merge editor as many others have suggested already. This proposal is something much simpler (presumably) but related
  - When using git merge there are sometimes conflicts that Git cannot automatically resolve.
  - In a basic real-world conflict resolution scenario, the user would inspect this file and its remaining conflict markers, choose how to resolve each one
  - A full-fledged merge editor such as Beyond Compare or Kaleidoscope will typically disregard the conflict markers left by Git in the target file, and instead extract the ours, theirs and base versions from Git, and perform a three-way merge from scratch based on these three files, and then overwrite the target file with the resulting merged file.
  - In the scenario we want to target, by contrast, Git has already performed the merge of the file is question, and the file already contains the changes from both sides that did not conflict (let’s call these the non-conflicting changes ) along with conflict sections for anything Git was not able to resolve automatically.
  - We simply want to visualize those remaining conflict sections, and provide actions for a user to interact with them. There is only a single file to consider, and only a single editor is needed to resolve the remaining conflicts inside it.

- 
- 
- 

- ## ✨🤔🌰 @cursor_ai 发布了他们的「Tab 补全」魔法背后的模型技术细节
- https://x.com/tuturetom/status/1828464855826997295
  - [Near-Instant Full-File Edits _202405](https://www.cursor.com/blog/instant-apply)
  - 微调 Llama-3-70B 模型，在 Coding 能力上匹敌 gpt-4o 和 claude 3 opus
  - 定制推理解码算法，提升速度 4～5x
  - 基于合成数据集训练

- 不是用的 Claude 吗
  - Tab 补全不是，需要速度还有兼容成本
- 一对一的场景优化，需要花很大的精力。

- https://x.com/tuturetom/status/1828604514922045874
  - 模型重写整个文件而不是写 Diff（性能更好）
  - Diff 格式参考开源项目 aider，完整 CodeBlock Diff 
  - 启发式修改：修改整个文件，9x 速度

- ## [MergeView matching regression (example) _202408](https://github.com/codemirror/dev/issues/1418)
- It's likely 6.6.2 caused this change, which reduces diffing accuracy in situations where it looks like computing the precise diff will be expensive. 
  - You can still configure this via the `diffConfig` option (adding diffConfig: `{scanLimit: 5000}` to your example seems to help). 
  - But note that you will for some documents be increasing edit latency. The default is intentionally biased towards performance over accuracy.

- ## [CodeMirror Merge Slow Diff - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-merge-slow-diff/7005)
- Seems at some document size, even the fast path is still too slow. Attached patch adds an even faster path (just treat the entire range as unchanged) for situations like this.

- ## 🐛 [incorrect diff for large files in merge view - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/incorrect-diff-for-large-files-in-merge-view/7411)
- Computing the diff for such large (and different) files is too expensive to do interactively, so the editor falls back to an overapproximation of the diff.
  - If people are allowed to edit the document, it seems that having a slow (and this is super-linear, so it gets very slow quite quickly) UI update cycle would make it unusable pretty quickly.
  - If users aren’t allowed to edit, maybe just statically rendering the text is easier than having it in a CodeMirror editor.

- ## 🆚️ [Github-styled unified text diff viewer (read-only) - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/github-styled-unified-text-diff-viewer-read-only/4913)
- The general idea would be to put a data structure describing the lines in some state field, and have separate gutters for the old and new line numbers, plus a gutter for the +/- signs, rendering markers based on the content of that data structure.
  - Or, if this is read-only, just render it without an editor, optionally using Lezer to highlight the code. That’s what the Chrome devtools do.

- @codemirror/merge also has a unified merge view feature now(202401).

- ## [I vaguely remember I saw an example of codemirror with tracking changes.  _202305](https://discuss.codemirror.net/t/track-changes/6561)
  - Any changes done in one editor was showing as a diff in the second one and one could take a snapshot of the current status. 
  - Can someone point me to the right direction to find it? Searching here and on google didnt help.
- Maybe the merge view (example) is what you mean?

- ## 💡 [Using merge w/ collab? - v6 - discuss. CodeMirror _202401](https://discuss.codemirror.net/t/using-merge-w-collab/7648)
  - I’m trying to make something like a collaborative editor that also uses @codemirror/merge (specifically, unifiedMergeView). I’m currently rolling my own synchronisation logic using JSON, rather than the @codemirror/collab module. 
  - However, I feel like it’s not possible to get change to the original document that were made in a transaction, since the updateOriginalDoc StateEffect isn’t public.

- There’s no build-in way to serialize effects. You’ll have to query their type and do your own thing. Because they rely on local `StateEffectType` objects, deserializing them across environments in a generic way is awkward.
- You can compare the old value of getOriginalDoc to the new one to see if the document changed, but you don’t get access to the changes themselves, which makes it hard to update other clients without recomputing the full diff.

- i see that originalDocChangeEffect allows me to make changes to the original doc in a transaction, but with only those two functions I don’t see a way to retrieve the changes made in a transaction (e.g. from accepting/rejecting a hunk).

- is there a way to get the initial value of a StateField in the provide() function?
  - No. The state configuration can’t directly depend on field/facet values. You’d have to set up some logic that reconfigures at the appropriate moment.

- If you dispatch a normal change to a unified merge view, you’re just changing the document in the editor. 
  - To update the original, which that document is compared against, dispatch a transaction with the `updateOriginalDoc` effect

- ## 🆚️🎯 [Merge View Implementation - v6 - discuss. CodeMirror _202209](https://discuss.codemirror.net/t/merge-view-implementation/5072)
  - Not in scope are 3-way merges and spacer-less scroll synchronization, which the old implementation did support. If someone has a need for those we can talk about including them.

- A first implementation of this exists. Take a look at the code and a demo, and let me know how it looks. _202211
# discuss
- ## 

- ## 

- ## 🌰🆚 [Adding widgets between lines instead of inside lines - v6 - discuss. CodeMirror _202207](https://discuss.codemirror.net/t/adding-widgets-between-lines-instead-of-inside-lines/4772)
  - We’re working on a CodeMirror side-by-side diff viewer similar to github’s view
- Is it possible to add dom nodes/breaks between cm-lines instead of inside using decorations
  - Yes, use block widgets, either at the end of the line above with side: 1, or at the beginning of the line below, with side: -1.

- https://replit.com/@util/CodeMirror-diff-view

- ## [Styling the outline of a merge view editor - discuss. CodeMirror](https://discuss.codemirror.net/t/styling-the-outline-of-a-merge-view-editor/7417)
- Themes passed to CodeMirror are scoped to the editor itself, so you’ll have to use raw CSS to style the `.cm-mergeView` element around them.

- ## [CodeMirror Merge Slow Diff - v6 - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/codemirror-merge-slow-diff/7005)
  - I’ve recently implemented CodeMirror Merge as an Angular component in a project and I’m finding it freezes the whole window while loading very large (182k line JSON), completely different files.
- Seems at some document size, even the fast path is still too slow. Attached patch adds an even faster path (just treat the entire range as unchanged) for situations like this.

- ## [[CM Merge] how to programmatically focus on line that has code changes - discuss. CodeMirror _202211](https://discuss.codemirror.net/t/cm-merge-how-to-programmatically-focus-on-line-that-has-code-changes/5366)
- @codemirror/merge 0.1.2 exports `MergeView.chunks` and documents the objects used in there.

- ## 🆚️ Problem: You want to compare two files.
- https://x.com/housecor/status/1817554130782568927
  - Solution: Use VS Code.
  - Right click file 1 and “Select for compare”
  - Right click file 2 and “Compare with selected”
  - A side-by-side diff displays

- I’ve also used BeyondCompare which has the ability to compare folders as well.
- Jetbrains IDEs also have a "compare selection with clipboard" option I found quite helpful
- Command + Shift + P -> Compare active file with.. also works
- code --diff file1 file2
