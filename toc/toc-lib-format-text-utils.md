---
title: toc-lib-format-text-utils
tags: [format, text, toc, utils]
created: 2023-09-01T03:54:37.254Z
modified: 2023-09-01T03:56:10.056Z
---

# toc-lib-format-text-utils

# guide

# popular

# examples

# utils

# diff-match-patch
- https://github.com/google/diff-match-patch
  - https://github.com/JackuB/diff-match-patch
  - The Diff Match and Patch libraries offer robust algorithms to perform the operations required for synchronizing plain text.
- https://github.com/karak/diff-match-patch-line-and-word /ts
  - An extension module that adds line-mode and word-mode on google-diff-match-patch, hosted as diff-patch-merge at NPM
- https://github.com/gamedevsam/diff-match-patch-emoji-issue
  - isolates and demonstrates the emoji diff problem in the diff-match-patch

- ts-port
  - https://github.com/rars/diff-match-patch-ts
  - https://github.com/nonoroazoro/diff-match-patch-typescript

- https://github.com/jhchen/fast-diff /apache2/202305/js
  - a simplified import of the excellent diff-match-patch library into the Node.js environment
  - The match and patch parts are removed, as well as all the extra diff options. What remains is incredibly fast diffing between two strings.
  - The diff function is an implementation of "An O(ND) Difference Algorithm and its Variations" (Myers, 1986) with the suggested divide and conquer strategy along with several optimizations Neil added.

- https://github.com/NPCDW/HtmlDiff
  - Html文本比对实现，基于google的diff_match_patch

- https://github.com/ace-diff/ace-diff
  - A diff/merging wrapper for Ace Editor built on google-diff-match-patch
# diff
- https://github.com/icflorescu/textdiff-patch /ISC/js
  - simple module for applying lean text diff delta patches created by textdiff-create.
  - https://github.com/icflorescu/textdiff-create /ISC/js
    - simple module for creating lean text diff deltas, based on the excellent fast-diff by Jason Chen.
    - Instead of sending the entire block of text to the server on each save, you'd ideally want to submit a "minimal patch" for each operation

- https://github.com/danielduarte/diffparse /MIT/202211/js/inactive
  - Simple parser for Diff files (unified diff format)
  - Parse a diff file from its filepath or string
  - https://github.com/danielduarte/diffsplit /MIT/202006/js/inactive
    - Easy split of .diff & .patch into its files
    - This CLI utility splits .diff or .patch files in unified format into parts by file without deleting or overwriting anything.
    - [Unified Format (Comparing and Merging Files)](https://www.gnu.org/software/diffutils/manual/html_node/Unified-Format.html)

- https://github.com/davidar/pandiff
  - Prose diffs for any document format supported by Pandoc
  - Supported output formats:
    - HTML
    - PDF, via LaTeX
    - Word docx with Track Changes
    - CriticMarkup

- https://github.com/wickedest/Mergely /js/LGPL
  - http://www.mergely.com/
  - [Mergely Visualized Diff demo](https://codepen.io/wickedest/pen/yLowrde)
  - a JavaScript component for differencing and merging files interactively in a browser (diff/merge).
  - It is suitable for comparing text files online, such as .txt, .html, .xml, .c, .cpp, .java, .js, etc.
  - Mergely has a JavaScript implementation of the Longest Common Subsequence (LCS) diff algorithm, and a customizable markup engine. It computes the diff within the browser.

- https://github.com/GumTreeDiff/gumtree /java
  - GumTree is a syntax-aware diff tool. 
  - It improves text-based diff tools in two important ways
  - We already deal with a wide range of languages: C, Java, JavaScript, Python, R, Ruby

- https://github.com/MrWangJustToDo/git-diff-view /MIT/202404/ts
  - https://mrwangjusttodo.github.io/git-diff-view/
  - A Diff View component for React / Vue, just like Github
  - core只依赖lowlight
  - https://github.com/wooorm/lowlight /MIT/202310/js
    - Virtual syntax highlighting for virtual DOMs and non-HTML things
    - This package uses `highlight.js` for syntax highlighting and outputs objects (ASTs) instead of a string of HTML.
    - This package is useful when you want to perform syntax highlighting in a place where serialized HTML wouldn’t work or wouldn’t work well. 
    - You can use the similar `refractor` if you want to use `Prism` grammars instead. 
    - If you’re looking for a really good (but rather heavy) alternative, use `starry-night`.

- https://github.com/praneshr/react-diff-viewer /MIT/202007/ts/inactive
  - https://praneshravi.in/react-diff-viewer/
  - simple and beautiful text diff viewer component made with jsdiff and React.
  - Inspired from Github diff viewer, it includes features like split view, inline view, word diff, line highlight and more. It is highly customizable and it supports almost all languages.

- https://github.com/rtfpessoa/diff2html /MIT/202412/ts
  - https://diff2html.xyz/
  - https://diff2html.xyz/demo
  - Pretty diff to html javascript library (diff2html)
  - diff2html generates pretty HTML diffs from git diff or unified diff output.
  - diff2html makes it easy to share static html representations of diffs with anyone, independent of the provider 
  - Any GitHub, Bitbucket or GitLab commit, pull/merge request urls.
  - https://github.com/pbu88/diffy /202206/ts/inactive
    - https://diffy.org/
    - Share diff output in the browser with an nodejs server
    - diffy.org is an amazing tool created by pbu88 to share your diffs and uses diff2html under the hood.
    - The mongodb data will be stored on the data/ folder.

- https://github.com/kpdecker/jsdiff /7.4kStar/BSD/202403/js
  - http://incaseofstairs.com/jsdiff/
  - A JavaScript text differencing implementation
  - Based on the algorithm proposed in "An O(ND) Difference Algorithm and its Variations" (Myers, 1986).
  - 支持按chars/words/lines比对，还支持patch
  - If you need behavior a little different to what any of the text diffing functions above offer, you can roll your own by customizing both the tokenization behavior used and the notion of equality used to determine if two tokens are equal.
  - jsdiff deviates from the published algorithm in a couple of ways that don't affect results but do affect performance:
    - jsdiff keeps track of the diff for each diagonal using a linked list of change objects for each diagonal, rather than the historical array of furthest-reaching D-paths on each diagonal contemplated on page 8 of Myers's paper.
    - jsdiff skips considering diagonals where the furthest-reaching D-path would go off the edge of the edit graph. This dramatically reduces the time cost (from quadratic to linear) in cases where the new text just appends or truncates content at the end of the old text.

- https://github.com/inkling/htmldiff.js /MIT/201803/js/inactive
  - Diff algorithm that understands HTML, in the browser.
  - htmldiff.js is a JavaScript port of https://github.com/myobie/htmldiff by Keanu Lee at Inkling.
  - This is diffing that understands HTML. Best suited for cases when you want to show a diff of user-generated HTML (like from a wysiwyg editor).
# command-line
- https://github.com/Textualize/rich /python3.7+
  - https://rich.readthedocs.io/en/latest/
  - a Python library for rich text and beautiful formatting in the terminal.
  - The Rich API makes it easy to add color and style to terminal output. 
  - Rich can also render pretty tables, progress bars, markdown, syntax highlighted source code, tracebacks, and more.
  - All Rich renderables make use of the [Console Protocol](https://rich.readthedocs.io/en/latest/protocol.html), which you can also use to implement your own Rich content.
  - Rich works with Linux, OSX, and Windows. True color / emoji works with new Windows Terminal
  - Rich works with Jupyter notebooks with no additional configuration required.
# more
