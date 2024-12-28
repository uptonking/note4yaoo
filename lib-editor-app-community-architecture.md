---
title: lib-editor-app-community-architecture
tags: [architecture, community, editor, text-editor]
created: 2024-12-28T19:10:41.691Z
modified: 2024-12-28T19:11:01.446Z
---

# lib-editor-app-community-architecture

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [NotepadNext: A cross-platform reimplementation of Notepad++ | Hacker News _202204](https://news.ycombinator.com/item?id=30959025)
- Efficiently handling large text files requires extra special care.
  - ~2x memory looks like a naive implementation of just allocating an std::string from heap for each line. Due to heap fragmentation and various overhead it would quickly blow up.
  - ~1x memory looks like just reading the entire file into RAM (that would still be slow).
- A truly efficient implementation would never need to load the entire original file in RAM.
  - It would just need to remember the binary offset of each line in a way that combines random access and reasonably fast insertion/deletion (e.g. K-fold trees). You can even keep everything beyond the top-level directory in an temporary on-disk file, so your RAM usage could be less than 1MB with nearly instant performance.
  - The efficient implementation is tricky, error-prone, and involves handling a solid amount of corner cases, which is beyond the amount of hassle a typical hobbyist developer is willing to go through.
- > To know the offset of each line, you'll need to load the entire file from disk.
  - No. You will need to read the file, not load it all at once in memory. And for a sequential scan, you need very little memory at any one time.

- With a 64-bit address space, you're probably better off just mapping the entire file into memory, not specifically loading it all. Let the OS swap in and out the pieces you need as you access it (and build your index of line offsets or whatever other structures you need).
- The big advantage to mapping is that you only read from disk the portions of the file you need, and only when you need them. Disk access is monumentally slow, so this can be a big win: if you don’t need to access all of a large file, or don’t need to access it all at once, mapping saves you very expensive operations or spreads them out over time.
  - The problem with that for a text editor is that probably the first thing you want to do is process the line endings. So you’re just going to access the entire file, right away, as fast as possible anyway.
  - The problem with that for a text editor is that probably the first thing you want to do is process the line endings. So you’re just going to access the entire file, right away, as fast as possible anyway.

- Why not just use mmap() or the Windows equivalent?
  - Let me rant for a bit because I've dealt with the following: Another downside is you'll get people complaining about memory usage despite mmap only paging in what's needed.
  - Mmap is a brilliant way to have the os handle which parts of the file actually reside in memory but you'll seriously have to deal with users that know only enough to be dangerous complaining that your app uses gb of ram when it's merely mapping a file into virtual address space to allow the os to page as it sees fit.
- Because then all your edits have to go directly into the file, so you have no real "save" flow unless you make a swap file for every file and then mmap that (which can be an appropriate approach, to a degree). Then all your caching and memory use subject to OS I/O and filesystem concerns, and you can't optimize for specific use. And inserting or deleting the middle of the file means shifting all the bytes after it.
  - I could think of a reasonable implementation for Linux that would use mmap and fallocate, but it wouldn't "just" be an mmap, as the swap file would still need to represent a rope or a gap buffer or something else of the sort for efficient editing.

- 
- 
- 
