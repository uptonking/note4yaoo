---
title: thread-tool-scripts
tags: [scripts, thread, tool]
created: 2023-12-11T10:11:55.588Z
modified: 2023-12-11T10:12:09.159Z
---

# thread-tool-scripts

# guide

# discuss-stars
- ## 

- ## 

- ## [shell - Make `rm` move to trash - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/42757/make-rm-move-to-trash)
- The previous answers mention commands `trash-cli` and `rmtrash` . Neither of those are found by default on Ubuntu 18.04, but the command `gio` is. 

# discuss
- ## 

- ## 

- ## Polyfill CDN 服务 http://polyfill.io 被中国菠菜 CDN 收购
- https://twitter.com/isukkaw/status/1763650534198972721
  - 先开几十个 PR、把 http://polyfill.io 赶出 GitHub、统统换成 http://cdnjs.cloudflare.com/polyfill

- ## Emitting all the output of an app to stdout, while writing a filtered subset to a file? Not a problem with `tee` and process substitution
- https://twitter.com/gunnarmorling/status/1756715764168417372
  - [Filtering Process Output With tee - Gunnar Morling _202402](https://www.morling.dev/blog/filtering-process-output-with-tee/)
  - Recently I ran into a situation where it was necessary to capture the output of a Java process on the stdout stream, and at the same time a filtered subset of the output in a log file. 
  - The former, so that the output gets picked up by the Kubernetes logging infrastructure. 
  - The latter for further processing on our end: we were looking to detect when the JVM stops due to an OutOfMemoryError, passing on that information to some error classifier.
  - Simply redirecting the standard output stream of the process to a file wouldn’t satisfy the first requirement. 
  - Instead, the `tee` command offers a solution: it reads from stdin and writes everything to stdout as well as a file

- ## Why stdout is faster than stderr in rust?
- https://twitter.com/orhunp_/status/1745025263350464650
- [Why stdout is faster than stderr? - Orhun's Blog](https://blog.orhun.dev/stdout-vs-stderr/)
  - I recently realized stdout is much faster than stderr for Rust
  - According to UNIX, every process has three streams opened for it when it starts up: stdin/stdout/stderr
  - These I/O (input/output) streams are typically attached to the user's terminal via tty (TeleTYpe) which can be described as an interface that enables access to the terminal.
  - The conclusion is that stdout making less write calls thus able to render more frames in the same amount of time. 
  - In other words, `stderr` blocks until the write function for each frame is rendered to the terminal whereas `stdout` returns faster.
  - There must be some buffering happening for stdout.
  - we now know that the reason why `stderr` is slower than `stdout` is that it is not buffered. So can we somehow achieve a faster (more performant) I/O with stdout by doing something like "better buffering"?
  - `std::io::stdout()` is faster than `std::io::stderr()` because the use of line-buffered vs no buffering.

- unbuffered
  - in go, os. Stdout is unbuffered as default
  - in zig
- buffered
  - in python, sys.stdout is line buffered
  - in c/cpp

- ## 又学到了，当你 format 了整个仓库之后， git blame 就会废掉，全是 format 的 commit。
- https://twitter.com/liruifengv/status/1737636700489470058
  - 可以创建一个 .git-blame-ignore-revs 文件，写入要忽略的 commit id。
  - 执行命令： `git config --local blame.ignoreRevsFile .git-blame-ignore-revs` 就好了
  - GitHub 也会自动读取 .git-blame-ignore-revs 文件
- 可以在服务端做一个 hook  如果没有通过 lint  的就拒绝

- ## 我也有个多repo的网盘git脚本... 用来没事fetch一下常用repo, 工作时少几秒fetch的等待, 心情会好一点点
- https://twitter.com/drmingdrmer/status/1734143991564902683
  - [watch and auto fetch/rebase/merge/push git-repo.](https://gist.github.com/drmingdrmer/07faee6c4f7c8e31da3c5210cfa04034)
