---
title: pm-office-obsidian-docs
tags: [docs, obsidian]
created: 2026-06-30T17:32:45.003Z
modified: 2026-06-30T17:32:52.416Z
---

# pm-office-obsidian-docs

# guide

# overview
- A vault is a folder on your file system which contains notes and an .obsidian folder with Obsidian-specific configuration. 
  - A remote vault is a copy of your local vault that is maintained with Obsidian Sync. 
  - The remote vault data is updated based on changes to local data.

- Reading view shows your note without Markdown syntax, offering a clean, readable format for focused review.
- Editing view lets you make changes to your note. 
  - Editing mode defines, how Markdown is displayed. You can choose one of two Editing modes: Live Preview or Source mode.
  - Live Preview shows formatted text inline while hiding most Markdown syntax. When your cursor enters formatted content, the underlying syntax becomes visible for editing.
  - Source mode displays all Markdown syntax exactly as written. Use it if you prefer plain text or need precise formatting control.
  - To switch to Source mode, press Ctrl+E, 此状态下properties不会显示为yaml格式，仍是wysiwyg

- Properties define additional information about a note, such as a due date or author.
  - Properties allow you to organize information about a note. 
  - Properties contain structured data such as text, links, dates, checkboxes, and numbers. 
  - Once you add a property, a row will appear at the top of the file with two inputs: the property name and the property value.
  - property types: Text List Number Checkbox Date Date & time Tags
  - Once a property type is assigned to a property name, all properties with that name across your vault will use the same type.
- Frontmatter is a way to define properties by adding YAML or JSON at the top of the note.  

- An alias is a type of property that defines alternative names for a note.

- A link references another note or file. 
  - An internal link points to a file located in the current vault. 
  - An external link points to a location outside the vault, typically a web page.

- Embedding means replacing a reference to external content with the content itself, for example to include an image in your note.  

- An attachment is an accepted file format that was created outside of the vault and added later.
  - By default, attachments are added to the root of your vault. You can change the default attachment location under Settings
  - You can import Accepted file formats, or attachments, to your vault, such as images, audio files, or PDFs. 
  - Attachments are regular files that you can access using your file system. 
  - Attachments can be embedded.
  - You can download an attachment directly to your vault, for example if you import from your browser, or from other apps that saves files directly to your file system.

- A tag is a word that starts with a hash (#), for example #book. Tags are primarily used to find related notes.

- Templates is a core plugin that lets you insert pre-defined snippets of text into your active note.
  - You can add dynamic information to your templates, using template variables. 

- A snippet, or CSS snippet, changes the appearance of Obsidian, just like a theme. 
  - Unlike themes, you can apply multiple snippets at the same time.
- A theme changes the appearance of the Obsidian app using CSS. You can override parts of a theme using snippets.

- Obsidian Publish lets you host notes and various media types, including images and video clips, with a limit of 4 GB per site. 

- 
- 
- 
- 
- 

# [obsidian-flavored-markdown](https://obsidian.md/help/obsidian-flavored-markdown)
- Obsidian supports CommonMark, GitHub Flavored Markdown, and LaTeX.

- Obsidian supports HTML to allow you to display your notes the way you want, or even embed web pages. 
  - Obsidian does not render Markdown syntax inside HTML elements. This is an intentional design choice for performance optimization and to keep parser complexity low when managing large documents.
  - HTML blocks must be complete and cannot contain blank lines within them. 
- To embed a web page
  - Some websites don't allow you to embed them. Instead, they may provide URLs that are meant for embedding them. 
  - `<iframe src="INSERT YOUR URL HERE"></iframe>`
  - Embed a tweet `![](https://twitter.com/obsdmd/status/1580548874246443010)`

- 
- 
- 
- 

## obfm-elements

- Internal link
  - Link to a page: [[Embeds]].

- Embeds
  - Embed another file
  - ![[Plugins makes Obsidian special for you]]

- Callout
  - written as a blockquote, inspired by the "alert" syntax from Microsoft Docs.

```markdown
> [!INFO]
> Here's a callout block.
> It supports **markdown** and [[Internal link|wikilinks]].
```

- Comment
  - Use `%%` to enclose comments, which will be parsed as Markdown, but will not show up in the preview.
  - some methods of converting Markdown notes, such as Pandoc, have limited support of Markdown comments. In those instances, you can use a `<!-- HTML Comment -->` instead.

- Highlighting
  - Use two equal signs to ==highlight text==.

- Diagram
  - uses Mermaid to render diagrams and charts.

- Footnote
  - Here's a simple footnote, [^1] and here's a longer one.[^bignote]
  - You can also use inline footnotes. ^[notice that the carat goes outside of the brackets on this one.]
  - Inline footnotes only work in reading view, not in Live Preview.

- Links
  - Obsidian URI links can be used to open notes in Obsidian either from another Obsidian vault or another program.
  - [Link to note](obsidian://open?path=D:%2Fpath%2Fto%2Ffile.md)
  - By default, due to its more compact format, Obsidian generates links using the Wikilink format.
  - If interoperability is important to you, you can disable Wikilinks and use Markdown links instead.
  - Even if you disable the Wikilink format, you can still autocomplete links by typing two square brackets [[. 
  - Autocomplete functionality switches to a simpler result algorithm when the vault reaches 10, 000 items to maintain optimal application performance.
  - While you can link to any of the Accepted file formats, links to file formats other than Markdown needs to include a file extension, such as [[Figure 1.png]].
- We do not support links to specific parts of quotations, callouts, and tables.
- Change the link display text 
  - Use link display text when you want to customize how a link looks in a specific place.  
  - If you want to set up an alternate link name that you can reuse throughout your vault, consider using an alias instead.
  - Use aliases when you want to refer to the same note using different names throughout your vault.

- Math
  - uses Mathjax

- 
- 
- 
- 
- 

# bases
- All the data in Obsidian Bases is stored in your local Markdown files and their properties. 
  - The views are described by the Bases syntax, which can be saved as a .base file or embedded in code blocks within your Markdown files.

- There are three kinds of properties used in bases:
- Note properties are only available for Markdown files, and are stored in the YAML frontmatter of each note. 
- File properties refer to the file currently being tested or evaluated. File properties are available for all file types, including attachments.
  - Use the this object to access file properties. What this refers to, will depend on where the base is displayed.
- Formula properties, defined in the .base file itself (see above).
  - Formulas allow you to create calculated properties in Bases using data from other properties.

- Functions are used in Bases to manipulate data from properties in filters and formulas. 
  - Bases functions follow JavaScript behavior. 

- 
- 
- 
- 

# docs

# more
