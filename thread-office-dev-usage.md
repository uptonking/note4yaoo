---
title: thread-office-dev-usage
tags: [office, thread]
created: '2021-01-14T13:17:05.456Z'
modified: '2021-01-14T13:17:38.972Z'
---

# thread-office-dev-usage

# pieces
 

- ## After 6 years of writing in markdown, I've finally mastered the basic markdown table syntax
- I was recently exposed to AsciiDoc table syntax.  It’s…exotic.
- this is why I use HTML for everything. I already know it!

- ## No matter how many times I've written a markdown table, I still have to look it up literally *every* time
- https://twitter.com/Una/status/816511597355077632
- I see it as a failing of HTML that we can't just write `<table src=data.csv></table>` natively.
- no idea what editor you use, 
  - but if it's @code, use markdown-shortcuts ext <-- Tables, fenced codeblocks, nested lists, oh my.
- Save yourself the trouble! I found `csvtomd` on GitHub
  - Never used tablesgenerator ever since.

- ## Read file from local directory in Javascript
- https://stackoverflow.com/questions/19842314/read-file-from-local-directory-in-javascript
- as far as I know this is not possible in JavaScript due to security concerns.
  - If it were, a web page could grab any file on your file system without your consent or without you knowing.
  - A user must be given the option to choose a file from their file system knowingly.
- This is not really possible or recommended for security reasons.
  - If this is only being used on your personal computer or for testing reasons, you can add an option for your browser to allow file access, 
  - `--allow-file-access-from-files`
- It is not possible to access the users file system.
  - However with the `FileSystem` API you can get a temporary or persistent private file system where you can store stuff for you application (cached images for example). 
  - You can then combine this API with the `File` API to allow the user to drag and drop files to your application from the users files.

- ## Do not use FileReader to show local file during uploading it to the server. 
- https://twitter.com/sitnikcode/status/1060157747038208000
- FileReader will copy the whole file to JS memory as a string.
- Use `URL.createObjectURL()`. 
  - It will return short blob: URL with a link, which you can use in `<img>`.

- ## For self-publishing eBooks from Markdown - are there nice alternatives to using a complex LeX toolchain?
- https://twitter.com/alexellisuk/status/1349693214782074882
  - `MD <> LeX <> PDF` is a complicated toolchain with native components and comes out like an academic paper.
- Pandoc is quite popular for this. It can generate pdf, and epub/mobi files as well
  - It's also a huge pain when exporting to PDF with needing LaTeX plugins and lots of native tools.
- If just starting, you could check out AsciiDoc. 
  - Similar-ish to Markdown but has nice support for exporting to PDF, EPUB, MOBI, etc.
  - I'm pretty fluent in markdown - what toolchain do you use to get the AsciiDoc to PDF? And how good is it for eBooks?
    - I used AsciiDoc and pandoc. Worked pretty well, but O'Reilly took care of all the formatting etc. Pandoc also handles markdown.
  - I have been using Pandoc, which is where all the issues are because the MD to PDF uses Lex to convert/generate. Did you ever do any local preview/generation?
    - Sometimes, but to get it to look right I had to run it through the O'Reilly webapp. I assumed with the right templates I could local generation to look as good.
- Ugh, that's exactly the problem I've been having lately. 
  - I resorted to just paying for Leanpub Premium for now. 
  - I write everything in Markdown, then just add the Markua extensions on top. 
  - Leanpub does all the heavy-lifting across PDF, ePub and mobi
  - The added benefit of the Premium option is that I can keep pushing changes to a GitHub repo, and LP will automatically generate unlimited previews each time.

- ## I'd want to be able to read the file's meta, and be able to find all .mp3 files on my PC
- https://twitter.com/trevorblades/status/1155144570251780096
- You might need to implement some kind of file upload mechanism to handle local files on your PC. 
  - Howler accepts base64 data URIs
  - so you could use a file input and handle the uploaded file using the FileReader API
