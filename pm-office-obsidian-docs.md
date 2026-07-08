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
  - When you insert a template into the active note, all the properties from the template will be added to the note. Obsidian will also merge any properties that exist in your note with properties in the template.

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

## formulas/functions

- Functions are used in Bases to manipulate data from properties in filters and formulas. 
- Bases functions follow JavaScript behavior. 
- Formulas allow you to create calculated properties in Bases using data from other properties. 
  - Calculate values, add prices, compute totals, or perform math operations.
  - Manipulate text, combine strings, change case, or extract substrings.
  - Work with dates, calculate time differences, format dates, or determine deadlines.
  - Apply logic, use conditional statements to display different values.
  - Process lists, filter, sort, map, or aggregate list data.

- 
- 
- 
- 
- 
- 
- 

# docs

- 
- 
- 
- 

# blogs

## [How I use Obsidian — Steph Ango ](https://stephango.com/vault)

- I use Obsidian to think, take notes, write essays, and publish this site. This is my bottom-up approach to note-taking and organizing things I am interested in. 
- In Obsidian, a “vault” is simply a folder of files. This is important because it adheres to my file over app philosophy. If you want to create digital artifacts that last, they must be files you can control, in formats that are easy to retrieve and read.
- Rules I follow in my personal vault for consistency:
  - Avoid splitting content into multiple vaults.
  - Avoid folders for organization.
  - Avoid non-standard Markdown.
  - Always pluralize categories and tags.
  - Use internal links profusely.
  - Use YYYY-MM-DD dates everywhere.
  - Use the 7-point scale for ratings.
  - Keep a single to-do list per week.

- I use very few folders. I avoid folders because many of my entries belong to more than one area of thought. 
- Most of my notes are in the root of the vault, not a folder. If a note is in the root, I know it’s something I wrote, or relates directly to me.
- My notes are primarily organized using the categories property. Categories display an overview of related notes, using the bases feature in Obsidian. 

- References where I write about things that exist outside my world. Books, movies, places, people, podcasts, etc. 
- Clippings where I save things other people wrote, mostly essays and articles.
- Attachments for images, audio, videos, PDFs, etc.
- Daily for my daily notes, all named YYYY-MM-DD.md. I do not write anything in daily notes, they exist solely to be linked to from other entries.
- Templates for templates.
- Categories contains top-level overviews of notes per category (e.g. Books, Movies, Podcasts, etc).
- Notes contains example notes.

- I use internal links profusely throughout my notes.

- Almost every note I create starts from a template
- I have a template for every category with properties at the top, to capture data such as:
  - Themes/topic — grouping by genre, type, topic 
  - Dates — created, start, end, published
  - People — author, director, artist, cast, host, guests
  - Locations — neighborhood, city, coordinates
  - Ratings — more on this below

- A few rules I follow for properties:
  - Property names and values should aim to be reusable across categories. 
  - Templates should aim to be composable, e.g. Person and Author are two different templates that can be added to the same note.
  - Short property names are faster to type, e.g. start instead of start‑date.
  - Default to list type properties instead of text if there is any chance it might contain more than one link or value in the future.

- This site is written, edited, and published directly from Obsidian. To do this, I break one of my rules listed above — I have a separate vault for my site. I use a static site generator called Jekyll to automatically compile my notes into a website and convert them from Markdown to HTML.
# more
