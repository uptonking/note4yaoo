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
  - Once a property type is assigned to a property name, all properties with that name across your vault will use the same type.
- property types: Text List Number Checkbox Date Date & time Tags
- Obsidian comes with a set of default properties:
  - tags, aliases, cssclasses
- Frontmatter is a way to define properties by adding `YAML` or `JSON` at the top of the note.  
  - While we recommend using YAML to define properties, you can also define properties using JSON
  - Note that the JSON block will be read, interpreted, and saved as YAML.
- A few features are not currently supported in Obsidian:
  - Nested properties: To view nested properties, we recommend using the source mode.
  - Bulk-editing properties: For in-depth bulk editing outside of Properties view, we recommend using bulk-editing tools like VSCode, scripts, and community plugins.
  - Markdown in properties: This is an intentional limitation as properties are meant for small, atomic bits of information that are both human and machine readable.

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
  - Tags can't contain blank spaces. 
  - To separate two or more words, you can instead use the following formats: #camelCase #PascalCase #snake_case #kebab-case

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

## [The Architect's Guide to Obsidian Bases – Kabir Chugh's Website _202508](https://chughkabir.com/guide-obsidian-bases/)

- The transition to Obsidian's 'Bases' feature from platforms like Notion or Airtable requires a fundamental shift in perspective. These applications, while powerful, are built on a paradigm of structured, isolated containers. In contrast, Obsidian Bases operates on a principle of fluid, vault-wide querying. 
- The most common point of confusion when approaching Obsidian Bases is the term "database" itself. In the context of applications like Notion or Airtable, a database is a discrete, self-contained table or "base". One creates a "Books" database, and it contains only books. A "Projects" database contains only projects. Each entry is a record added to that specific container, and the data lives inside that silo.
- Obsidian fundamentally inverts this model. An Obsidian vault is not a collection of databases; the entire vault is the database. The 'Bases' feature does not create containers for data. Instead, it provides a powerful query engine to create dynamic, filtered "views" of all the notes that already exist across the entire vault. A more accurate mental model is to think of a .base file not as a database, but as a "vault views container".
- This architectural distinction is not a limitation; it is the system's core strength. In a siloed model, seeing connections across different data types requires building explicit, often complex, "relations" or "linked records". To see all science fiction content, one would need to link the "Sci-Fi" entry in a "Genres" table to individual records in the "Books" table, the "Movies" table, and the "Games" table.
- In Obsidian, this cross-contextual analysis is native. Because every Base queries the entire vault by default, a single view can be configured to show any note that meets the specified criteria, regardless of its "type" or folder location. 
- With the vault itself established as the database, the individual Markdown file becomes the fundamental record or "atomic note." All the structured, queryable data that Bases relies upon lives exclusively within the YAML frontmatter section at the very top of each file. 
- It is critical to understand that, by design, Obsidian Bases do not read, parse, or query the main content of a note. This means that inline data fields popularised by the Dataview community plugin (e.g., Rating:: 5) are invisible to the Bases engine. This constraint is not an oversight but a deliberate performance and design choice. It necessitates a disciplined and consistent approach to metadata management: if data needs to be sorted, filtered, or displayed in a Base, it must exist as a formal property in the YAML frontmatter.
- This symbiotic relationship offers the best of both worlds. The structured properties provide the robust framework needed for sophisticated data management, allowing for the creation of powerful organizational views that rival those in Airtable or Notion. Simultaneously, the unstructured body preserves the creative freedom and serendipitous linking that is the hallmark of a true second brain. One can manage a project with the rigor of a database while exploring the ideas within it with the freedom of a writer's notebook, all within a single file.

- The "vault view container" model of Bases presents a primary architectural choice in how to organize the .base files that generate these views. There are two main approaches:
  - The Atomic (Modular) Approach: This strategy involves creating a separate, highly-specific .base file for each distinct category of information. For instance, one would create Books.base, Movies.base, Projects.base, and Recipes.base. This approach offers maximum separation of concerns and conceptual clarity. Each file has a simple, unambiguous purpose.
  - The Container (Monolithic) Approach: This strategy involves grouping related categories into a single, broader .base file. For example, a Media.base could contain separate views for Books, Movies, Shows, and Music. A Productivity.base could house views for Projects and active Queries. This approach is more efficient for managing related data types and reduces the need to replicate similar filters across multiple files, a potential source of maintenance overhead.
- For the specified use cases, a Hybrid "Container" Approach is the most effective and elegant solution. This strategy leverages the strengths of both models:
  - Group related items into containers: Create a Media.base to house all consumption-related views (Books, Movies, Shows, Music). Create an Aspirations.base for Bucket Lists and Wishlists. This aligns the digital structure with the user's mental models, recognizing that these items are often facets of a single broader activity (e.g., "entertainment" or "goals"). This also allows for powerful, cross-cutting views within a single Base, such as a "Master To-Do List" that shows books to read and movies to watch.
  - Isolate functionally distinct items: Keep categories with unique properties and workflows in their own atomic bases. Recipes.base and Projects.base are prime examples. Their data models and the actions one takes with them are sufficiently different from other categories to warrant their own dedicated .base files.

- Establishing a consistent, vault-wide "Universal Data Language" through a master property schema is therefore not optional; it is the foundation upon which the entire structure rests.
  - a master schema should define all properties used across the vault, specifying their name, data type, the note types they apply to, and any allowed values. This document becomes the single source of truth for the vault's data model.

- While Bases operate primarily on properties rather than file location, a minimal and logical folder structure provides essential organizational scaffolding and prevents the vault from becoming a chaotic flat list of files. This structure should support the workflow, not dictate it. A recommended minimal setup is:
  - 00-System/: A folder for templates, .base files, and other system-related notes.
  - 01-Projects/: A dedicated folder for all notes with type: Project.
  - 02-Media/: A container for all media-related notes (Books, Movies, etc.).
  - 03-Life/: For Recipes, Aspirations, and other personal management notes.
  - 04-Knowledge/: For Queries and general-purpose notes that feed into projects.
  - 05-Attachments/: A central repository for all images, PDFs, and other non-markdown files.

- The true power of this architecture is realized through automation. The Master Property Schema must be enforced to maintain data integrity, and the most effective way to do this is with templates. Using a community plugin like Templater, one can create a template for each note type. When a user triggers the creation of a "New Book Note, " for example, the Templater plugin will create a new file and automatically insert the complete YAML frontmatter block with type: Book and all other relevant properties from the schema, pre-filled with placeholders.

- One of the most powerful, yet often overlooked, features of Obsidian Bases is the ability to create filters that are relative to the note in which the Base is embedded. This is achieved through the this.file object, which refers to the properties of the host note itself. This allows for the creation of highly contextual, self-updating dashboards that are far more dynamic than a static .base file.

- A common practice in Obsidian is the creation of "Maps of Content" (MOCs)—manually curated notes that serve as indexes or tables of contents for a specific topic by listing relevant wikilinks. While effective, MOCs require constant manual upkeep. As new notes are created, they must be manually added to the relevant MOCs.
  - Obsidian Bases can entirely automate this process, creating "Dynamic MOCs" that are always up-to-date. Instead of a manual list of links, a MOC note can embed a Base configured to query the vault for all notes related to that topic.

- A well-designed system must also be maintainable. The longevity of this architecture depends on three key practices: schema evolution, data integrity, and leveraging Obsidian's core principles.
Schema Evolution
As workflows change, the need to add, remove, or modify properties is inevitable. When a change is required, the first step is to update the central "Master Property Schema" document. This ensures the official definition of the vault's data language remains current. For implementation, changing properties across a large number of existing files can be tedious. Community plugins like "Linter" or scripts using "Templater" can be configured to perform bulk operations, such as adding a new default property to all files in a specific folder or renaming an existing property across the vault.

Data Integrity
The system's reliability hinges on the consistency of the data within the properties. The primary defense against inconsistency is the rigorous use of templates, as outlined in Section 2.3. However, errors can still occur, and periodic audits are recommended. A powerful data integrity tool can be built using a "Utility" Base. For instance, a view with the filter "where type is empty" will instantly surface any notes that were created without being assigned a proper type, allowing for quick correction. Another view could filter for projects where due_date is in the past but project_status is not "Completed, " flagging items that need attention. These simple audit views are essential for maintaining a clean and reliable dataset.

Backup and Longevity
Finally, the most critical aspect of future-proofing is data ownership. The entire system described here is built on top of local, plain-text Markdown files. Unlike cloud-based platforms where data is stored in proprietary formats on company servers, this Obsidian architecture ensures that the user retains complete control and ownership of their knowledge. The .md files and .base files are human-readable and can be backed up, version-controlled with tools like Git, and migrated to any future system with minimal effort. This adherence to open formats is the ultimate guarantee of the system's longevity, ensuring that the meticulously structured knowledge built today will remain accessible and valuable for decades to come.

- The success of this system rests on three foundational pillars:
  - A Paradigm Shift to "Vault View Containers": Understanding that Bases are flexible windows into the entire vault, rather than rigid data silos, is paramount. This enables the synthesis of information across diverse categories, fostering a more holistic understanding of one's knowledge.
  - The Centrality of a Universal Schema: A disciplined, consistent approach to metadata via YAML Properties is non-negotiable. The establishment of a Master Property Schema, enforced through automated templates, is the critical mechanism that ensures data integrity and the reliable functioning of all views and filters.
  - A Hybrid "Container" Architecture: Strategically grouping related data types into monolithic .base files (like Media.base) while isolating functionally distinct workflows (like Projects.base) provides the optimal balance of efficiency, clarity, and scalability.

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
