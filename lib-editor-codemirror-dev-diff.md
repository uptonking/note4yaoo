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

- ## 

- ## 

- ## [Applying a "standard" text diff patch to editor content? - v6 - discuss. CodeMirror _202509](https://discuss.codemirror.net/t/applying-a-standard-text-diff-patch-to-editor-content/9506)
  - Is there an extension (or even built in functions) for applying “standard” text diff patches to content in an editor, so that you don’t have to grab the content as string, patch that, then overwrite the content with that update?
- I’m not aware of such code. I could imagine there existing a JS library for applying patches that exposes the ranges it actually replaces (or can be modified to do so), which would make it pretty easy to generate the appropriate editor changes, but with a quick search I didn’t actually locate such a thing.

- ## 💥 [incorrect diff for large files in merge view - v6 - discuss. CodeMirror _202311](https://discuss.codemirror.net/t/incorrect-diff-for-large-files-in-merge-view/7411)
  - I’ve noticed that when using very large files with the MergeView editor, the computed diff between the files is incorrect.
  - More specifically for my case, I have 2 ~1500+ loc files that have just a couple changes between them (not more than 40-50 loc) spread out throughout the whole document (small diffs at the beginning, middle, and end of the document).
  - this is how it’s rendered in CM using the MergeView. The whole document is basically flagged as one large diff.

- Computing the diff for such large (and different) files is too expensive to do interactively, so the editor falls back to an overapproximation of the diff.
- Is there a way I can prevent the editor from falling back to the approximation?
  - If people are allowed to edit the document, it seems that having a slow (and this is super-linear, so it gets very slow quite quickly) UI update cycle would make it unusable pretty quickly.
  - If users aren’t allowed to edit, maybe just statically rendering the text is easier than having it in a CodeMirror editor.

- The longer time it takes to compute the diffs (10-20 seconds) is acceptable in principle, but I would like to inform the user with a spinner/block screen. Is there an event I can listen to to know when the computation is finished? 
  - Computing the diff is a synchronous process. So a spinner wouldn’t spin, and the UI would be entirely frozen. I don’t think that a 20 second freeze is really going to be acceptable in any circumstance, unfortunately.

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

- ## 🧮 Myers diff may generate weird deltas like the following example. It will make concurrent text updates generate weird merge results. Any suggestions? 
- https://x.com/zx_loro/status/1854568496413524165
  - My current thought is to implement an A* search on top of the edit graph that punishes noncontinuous edits
  - An update like this is also less efficient for CRDTs, even though it is a minimal edit script. Because it is harder to compress a scattered update.

- Have you tried patience/histogram diff algos? They seem to produce more “linear” diffs (not necessarily minimal, but seemingly more close to what a human would do). Although not sure how well they work with character-based granularity.
  - Yeah, they seem like designed specifically for line-based diff

- Tons of heuristics, like everybody else did?
  - working on it! Just learned a lot from diff-match-patch

- ## 🌰 [CodeMirror Merge - Calling a Function on Chunk Approval/Reject - v6 - discuss. CodeMirror _202409](https://discuss.codemirror.net/t/codemirror-merge-calling-a-function-on-chunk-approval-reject/8636)
  - I can not figure out how to trigger a function when the user has either approved or rejected a code chunk.
  - I want to run a function to know when to turn off merge view

- The extension will fire transactions tagged with a user event of "accept" or "revert". You could listen to those and, if necessary reconstruct which chunk was reverted by comparing the change’s location to the chunks that existed in the state at the start of the transaction.

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
  - I’m trying to make something like a collaborative editor that also uses @codemirror/merge (specifically, `unifiedMergeView` ). 
  - I’m currently rolling my own synchronisation logic using JSON, rather than the `@codemirror/collab` module. 
  - However, I feel like it’s not possible to get change to the original document that were made in a transaction, since the `updateOriginalDoc` StateEffect isn’t public.
  - Also, `originalDoc` not being public makes it so you have to retrieve and set the original document separately, instead of being able to use `EditorState.to/fromJSON` .
  - Also it seems like StateEffects don’t have a toJSON/fromJSON? Is there a recommended way of sending them between clients?

- There’s no build-in way to serialize effects. You’ll have to query their type and do your own thing. Because they rely on local `StateEffectType` objects, deserializing them across environments in a generic way is awkward.

- i see that `originalDocChangeEffect` allows me to make changes to the original doc in a transaction, but with only those two functions I don’t see a way to retrieve the changes made in a transaction (e.g. from accepting/rejecting a chunk).
  - You can compare the old value of getOriginalDoc to the new one to see if the document changed, but you don’t get access to the changes themselves, which makes it hard to update other clients without recomputing the full diff.

- is there a way to get the initial value of a StateField in the provide() function? I’m trying to have a set of extensions that are conditionally enabled based on the value of a state field, by having a compartment that is returned from provide() and changing using a transaction extender. But I can’t see any way of having the compartment have the right value initially if StateField.init() is used, or I’m using EditorState.fromJSON
  - No. The state configuration can’t directly depend on field/facet values. You’d have to set up some logic that reconfigures at the appropriate moment.

- If you dispatch a normal change to a unified merge view, you’re just changing the document in the editor. 
  - To update the original, which that document is compared against, dispatch a transaction with the `updateOriginalDoc` effect

- ## 🆚️🎯 [Merge View Implementation - v6 - discuss. CodeMirror _202209](https://discuss.codemirror.net/t/merge-view-implementation/5072)
  - Not in scope are 3-way merges and spacer-less scroll synchronization, which the old implementation did support. If someone has a need for those we can talk about including them.

- A first implementation of this exists. Take a look at the code and a demo, and let me know how it looks. _202211
# discuss
- ## 

- ## 

- ## ✨🤔 How come code move detection is not a thing in all diff tools?
- https://x.com/artman/status/1951296531442573447
- Maybe because row index is not stable, better to use unique id to tracking change.
  - No row indexes or unique indexes necessary, this is comparing deletions to addition on the AST level and showing moves when they match.
- Beautiful! I've always wanted to build source control tools based on AST, never got around to doing it though
- you answered your own question, diff tools typically arent ast parsers
- sadly barely any tools work on the AST level. mergiraf does though!
- AST fr? Seems doable with plain text

- why do you have to parse the code to detect lines being moved around?
  - The moved lines might also have slight changes

- because most diff tools still don't parse out ASTs
  - Throw arbitrary AST awareness into the mix and now you have 100 different versions of diff++ that all have to understand each other somehow

- Most diff tools are using a linear-space version of the Myers diff which is fast but doesn’t work well for cases like this. 
  - Patience diff is much better https://blog.jcoglan.com/2017/09/19/the-patience-diff-algorithm/
  - You can use it in git: `git diff --patience`.

- I just thought about this. Currently, most diff algorithms and tools show moved code as deleted and added. This is because they’re likely using LCS/Myers, right? Didn’t GitClear build Commit Cruncher and add the move operator? I’ve been working on something for a while now that solves it. 

- Because they're all based on the longest common subsequence, and not on alternatives like "The String-to-String Correction Problem with Block Moves"

- They work based on edit distance and DP. It's just cheaper in terms of time complexity. I mean, edit distance only requires texts, but this thing needs constructing the whole AST first.

- How about moving a section and editing a line in it?

- Formatting detection too

- I don't think GNU diff natively supports this feature.

- I think JetBrains IDEs try to tackle code move detection, but it’s NP-hard and requires AST parsing, which can be impractical for large codebases. 

- JetBrains git tool is a top notch.
  - vscode has this feature too
- JetBrains' diff tooling works with a lot more than git.  Off the cuff, local files, clipboard, local history, probably more I've forgotten.

- It actually gets really complicated when you try to handle all the scenarios. Sometimes information is destroyed and what you try to infer ends up being deceptive/distracting instead of helpful.

- I *so* wish that diff/patch (or more specifically, whatever git uses for conflict resolution) would construct semantic changes (e.g. rename method "foo" to "bar"). Patches would be smaller, conflict less often, and I would haven't to deal with conflicts in my imports.
  - @_wilfredh says AST merging is a hard problem
- es, I can imagine why he says that. He’d never get the credit, only the blame when something goes wrong. Still, the rise of vibe-coding suggests that people are becoming more comfortable with fallible tools.  And let’s face it, merging was always somewhat fallible.

- Because the original diff implementations were written back in the 1970s (at Bell Labs) to run on a PDP-11, which means the overhead of detecting moved lines was just not possible, especially for "large" files. tl; dr historical artifact

- As someone who’s worked alot on diffing, I can answer
  - 🌴 Code often modeled as trees (think open and curly braces) — minimum edit distance with moves on tree-diff is NP-Hard
  - doing a lot of “moves” can add mental complexity (think of a tangled knot)

- http://meldmerge.org has had this for years now.
- Microsoft Word apparently even figured this out recently. Was pleasantly surprised earlier today

- when comments are attached to specific lines they are invalidated when they could just move with new code

- Simple moves are rare. Most of the time you move and change. So how will the diff tool know if you moved and changed or deleted and implemented a new version?
- Because it breaks after some nontrivial movement between files + change of some lines. The only way is to have human label every move/copy, maybe with some semi-automatic algorithm that needs slight assistance.
  - The best tool for movement detection I know is this: https://people.f4.htw-berlin.de/~weberwu/simtexter/app.html . But it's more suitable for natural text. I use it to compare my video scripts between iterations.

- computing edit distance with block moves—key to exact code move detection—is NP-complete. This hardness explains why it's not standard in diff tools; approximations are used for efficiency.

- Just make a hash table with an entry for each line in the original. Then go through the modified version and check the hash table where the line comes from.
  - it's worse than that. you want to be able to indicate minimal (sub line) edits modulo relocation, so you have to do chunked comparison ~independently of position, which you can still make more efficient with clever indexing strategy but it's not gonna be both pretty and linear.

- It's really hard to do because of all the edge cases because of all the different language's
- I guess that is because not all code move is commutative, and, what's worse, the commutativity is both language dependent and context dependent. For a diff tool to be aware of these, it will have to know each language it diffs -- i.e. be an ide. That's my understanding.

- ## [Synchronous Fold/Unfold in MergeView - v6 - discuss. CodeMirror _202405](https://discuss.codemirror.net/t/synchronous-fold-unfold-in-mergeview/8194)
  - I’m using MergeView plugin to show the difference between 2 json strings
  - The problem is when one side is folded/unfolded based on gutter click, other side remains as it was. How can I make 2 sides to fold/unfold together?

- You could observe transactions with fold effects, find the matching line on the other side (by using the chunk information), and fold that.

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
