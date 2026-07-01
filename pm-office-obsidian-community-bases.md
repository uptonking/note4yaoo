---
title: pm-office-obsidian-community-bases
tags: [database, obsidian]
created: 2026-06-30T23:03:58.381Z
modified: 2026-06-30T23:04:11.000Z
---

# pm-office-obsidian-community-bases

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-showcase/examples
- ## 

- ## 

- ## 

- ## 

- ## [A Bases Template for Project Tracking or Task Management - Share & showcase  _202508](https://forum.obsidian.md/t/a-bases-template-for-project-tracking-or-task-management/104249)

# discuss-issues
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Migrating from Notion: How to get inline data tables without making every row a note? : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1u2t5n0/migrating_from_notion_how_to_get_inline_data/)
- Notion style is that every row is a note though. That’s how Notion operates.

- Obsidian doesn’t have a concept of mini databases embedded in a page. I went through this a couple of weeks, asked this sub and they set me straight. Bases are just different views of your sorted and filtered obsidian pages.

- I have a media base of marvel movies with files created by the Media DB plugin, that has files with just frontmatter sitting in a hidden attachment folder. So that is a way of doing what you ask… kinda

- ## [One base many views : r/ObsidianMD _202605](https://www.reddit.com/r/ObsidianMD/comments/1t20rfb/one_base_many_views/)
- I prefer to have separate bases for separate topics. But each topic base has multiple views to offer options for embedding or various contexts. If all of that would be in one base with many views, it would get messy quick

- I like to view multiple bases without having to switch from window to window. I ended up linking my bases ( w/ ![[FILENAME]] ) to an overview page instead, since you cannot attach properties to a base file.

- I use inline bases to filter each note linked to the note in which the inline base is (filtered by name of the note)

- ## [Starting Obsidian today - What folder structure works best with Home bases : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1pwfkuf/starting_obsidian_today_what_folder_structure/)
- Work in Obsidian before you worry about how to work on it or structure your system. Yes, changes take work, but until you have a use case and understand it, it’s putting your carriage before your horse to dwell on the “best system” for it.
  - I use a different system for every distinct vault I use, because each vault reflects a particular work space and mindset and workflow. I don’t need the same structure in my Digimon Encyclopedia as I do in my Conlangs, and even there: specific conlangs may have slightly different requirements to their language structure based on the features of that conlang.

- I’d take a step back first. You’re looking at a clean slate to your notetaking with a view to a simple structure. I’d argue that your notetaking should mirror what you want out of life

- ## [How do I recreate this in Obsidian? : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1uds99o/how_do_i_recreate_this_in_obsidian/)
  - 典型的多维表格
- bases don't work like databases in Notion. they fetch the notes you've already created, and you need to adjust the sorting and filtering to what you need. the base you showed here seems pretty easy to recreate in bases.
  - make a folder for your books, all the columns in your base are the Metadata, and then you make a base to make a table. you could even add the book covers as images and make a book gallery.
- A note per book is exactly how you should be using Obsidian. It's not messy at all, and is exactly how Obsidian is designed to work, out of the box. With a note per book and the properties for all of the metadata, that view you want can easily be done as a Base, no third-party plugins necessary.
- Just FYI, each of those was a note in Notion, too. Maybe you didn't use the note part, but it was a note.

- I'm using this plugin called Notion Bases for Obsidian, and it works great for me: https://github.com/bgarciamoura/obsidian-notion-bases-plugin

- ## [How to make obsidian bases beatiful, Notion style example? : r/ObsidianMD _202604](https://www.reddit.com/r/ObsidianMD/comments/1so8pj2/how_to_make_obsidian_bases_beatiful_notion_style/)
- Pretty Properties plugin. (Nvm)

- You're going to have to be good at CSS + HTML to achieve this without a plugin. I highly recommend reading through Bases-CSS-Guide. You're going to have to recreate this table view yourself with the classification based on the status/role to change colors.
  - The easiest method dataview which is a plugin. That way you can write embed inside the CSS you'd like. But if you're going to use plugins, might as well use Pretty Properties plugin.

- ## [Bases : r/ObsidianMD _202604](https://www.reddit.com/r/ObsidianMD/comments/1sd4zfa/bases/)
  - Trying to understand how people are actually using Bases in Obsidian.

- Once I realized you can embed them in notes and scope them to pull data from the note they are embedded in to do queries and such, I was able to completely replace Dataview.

- I have a dynamic base that, when embedded into a note, reads the first tag of the note and then show a table of all notes with that tag.

- Right now I exclusively use tags + bases to organize my vault. Its really simple, but it works and is low friction. I tag my notes and have one base per tag which I usually embed into my home page for quick access.

- Each folder contains a "bases" file with the same name as the folder. This file typically displays all the notes from that folder in a list format. For notes about games, books, movies, and TV shows, they are displayed in a gallery format with covers.

- 
- 

- ## [Should I move to Obsidian Bases or Datacore, as a Dataview user? : r/ObsidianMD _202603](https://www.reddit.com/r/ObsidianMD/comments/1s3i73c/should_i_move_to_obsidian_bases_or_datacore_as_a/)
- In priority of preference
- Obsidian Bases
  - Why? Core Plugin, LTS
  - Why Not? Still missing some advanced features
- Obsidian Dataview
  - Why? 3.8 million downloads, lots of community support
  - Why Not? Not dynamic in live view
- Obsidian DataCore
  Why? You like complex scripts to setup a database
  Why Not? It's a Niche plugin that you either love or hate

- I use both because Bases have a fatal flaw which devs aren’t planning to mitigate: there’s no way to change cell size and adjust it to fit the contents. If you want accurate tables, use Datacore.

- It depends on how you've been doing things. I found I could replace most of my dataview tables with bases and it's way better/more streamlined, however I'm also using a lot of inline properties in my daily notes, which bases cannot pickup on, so I still have to use dataview for those tables.

- Data(View/Core) is obviously more flexible and powerful, but much harder to learn.
- Datacore uses a different syntax from Dataview. But will largely have the same features.

- Dataview has good documentation and there's a bunch of pre-made queries online. LLMs are somewhat trained on it at this point, so especially for dataviewjs queries, you can prompt your way there pretty easily. 

- ## [What are the best plugins in relation to bases already created for Obsidian so far? : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1pp25ul/what_are_the_best_plugins_in_relation_to_bases/)
- Virtual Content. You can add specific base views to files based on their property values without actually typing them in the note. It's great because if you want to change something in that base view, you can do it through the plugin settings tab and the change will happen in every file. Also, it doesn't alter the Markdown files.

- ## [Bases: data source from CSV instead of note properties? : r/ObsidianMD _202505](https://www.reddit.com/r/ObsidianMD/comments/1kw4yai/bases_data_source_from_csv_instead_of_note/)
  - Is there a way for a Base to grab data from a CSV (or other tabular-data format)?

- No. Because the core idea of bases, is presenting a view of MD files.. with smart query & filters based on those MD files. That’s it.

- I thought it was silly at first, but I’ve gone the thousands of notes route and haven’t had trouble yet. There’s a CSV/JSON importer plugin available to make a note per entry.

- SQLseal plugin is read-only, correct? I can't make changes to the table and have them write back into the csv file?

- ## [Obsidian Bases support in Flowershow (Alpha) : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1pevh7g/obsidian_bases_support_in_flowershow_alpha/)

- ## [Obsidian Bases — now available to everyone! : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mtxh52/obsidian_bases_now_available_to_everyone/)
  - Bases is a core plugin that lets you turn any set of notes into a powerful database. With bases you can organize everything from projects to travel plans, reading lists, and more.
  - Using a base you can view, edit, sort, and filter files and their properties. 
  - Each base can have several views, and different layouts such as tables and cards. 
  - Below is an example of table view where each row is a file, and each column is a property of that file.
- Bases are filtered and sortable Table and Card views of note Properties and Tags. It is a configurable "view" of various Properties of Notes in your Vault.
- A Base can be a standalone file (with a .base extension) and can be viewed directly or embedded like any other Note using the format ![[PathToNote]]
- Base code can also be embedded directly into a note to render the Base.

- [PSA: Some Clarity on Bases : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mvfoys/psa_some_clarity_on_bases/)

- Yeah at first glance I thought it was like a built in spreadsheet for any data but it's more like my notes are the rows.
  - Notes are the rows (records).
  - Properties are the columns (fields).
  - A Base is a view that renders the rows and columns. What displays in the rows and columns is controlled by Filters and Property selection.

- I think the core plugin Bases only works with YAML properties or explicit file metadata (created date, modified date, path, etc). It does work with inline tags, but not Dataview inline properties (the propertyname::value syntax you allude to). I think the devs have said that this is technically feasible and so a community plugin could be used to access Dataview properties, but I haven't seen one yet.

- ## [Obsidian bases are great, but is making a separate note for each item practical? : r/ObsidianMD _202509](https://www.reddit.com/r/ObsidianMD/comments/1nq0mci/obsidian_bases_are_great_but_is_making_a_separate/)
  - I really like Obsidian bases in terms of automation, customization and overall look. It's pretty and functional. 
  - However, there are cases where making a note for each entry can be a bit excessive. Do you think it's possible to have multiple items from one note?
  - Example use case: movies to watch, games to play. Say you want to have 200 entries, do you really have to make 200 notes? If you make lists like this you end up with potentially thousands of empty notes (besides the metadata).

- The Bases core plugin is not a database. It provides filtered views, generally based on Properties. If you need true database functionality, Obsidian might not be the right solution.
  - The idea of Bases is to provide a managed jumping-off point to dig deeper. (Heck, a Base is, arguably, a Map of Contents.) The way that Bases' Table and Card views aggregate information amps up Obsidian's capabilities, so how the data (notes) are handled behind the scenes really depends on what you are trying to do.

- Why not both? For example, I’ll create a note for each book that I want to create a note for. I separately have a note called “Books consumed” that just has a bulleted list of books that I’ve read by year, which may or may not link to a note.

- This is why I still use dataview, too, not only bases. For some notes I need to collect pieces from notes that contain many things.

- Remember Base is just a view and not a database. It doesn't change anything nor depends on how your notes are made. It just style so to speak what's already in your vault (for simplicity sake).
  - So write and organize your notes however you want. Experiment to discover what works for you, and it might be the same or different for each use case. You can always tweak and change.
- Yes, Base doesn't display the content of a note, rather it displays the properties or YAML.

- In some cases Dataview is still a better fit (and probably Datacore, although this is still unexplored territory for me) if you want to use the note's contents instead of the YAML frontmatter properties.

- This has me thinking that the community could use a plugin that converts each line in a table into a note with metadata, and then generates a Base for those notes with the same look as the original table. Then you can start modest and there's no FOMO of not starting it as a Base. Because you're right, a lot of knowledge management starts smaller than what a Base is.

- ## [Obsidian Bases | Hacker News _202508](https://news.ycombinator.com/item?id=44945532)
- 
- 
- 
- 
- 
- 
- 
- 

- ## Obsidian Bases can be exported to CSV or copy-pasted anywhere — as Markdown, or even into your favorite spreadsheet app
- https://x.com/kepano/status/1927501007480582467
- 
- 

- ## [Introduction to Bases | Lobsters _202505](https://lobste.rs/s/nxroup/introduction_bases_obsidian_help)
- but when you really lock-in with bases or obsidian plugins like tasks and dataview, you really rely on thing, not being that easily to replicate if obsidian would go paid or something else.

- This is very interesting. In 2019 I wrote a small hack using Pandoc that parsed a Markdown file and:
  - Detected tables and dumped them into a SQLite database.
  - Detected SQL code blocks, run the SQL on the SQLite database and replaced the code block with the query results as a table.
  - I was obviously inspired by Notion (2016) and Coda (2019). I still think that the slow death of Access and similar tools, the abuse of spreadsheets, and a couple of other factors are a severe drag on global productivity. Easy CRUD on relational databases is an overlooked problem
  - I wanted to start a similar project based on some more modern lightweight markup language (such as Djot) and likely on some Datalog variant, but I stalled

- ## [Obsidian Bases | Hacker News _202505](https://news.ycombinator.com/item?id=44058972)
- They are using a yaml file with `.base` extension for this.
  - I believe their `.canvas` format is also just JSON.

- Bases seem like a great alternative to Dataview but better supported and with simpler syntax than literally writing inline JavaScript for more complicated stuff.

- Are there any good ways to attach files to notes? I often want to tie a memo or email to a note but have not found a convenient way.
  - Default way is drag and drop which adds a copy of the file to your attachments.
  - Another way is to put a file reference into your note (in a link). Your file stays where it is and you have a link to it in a note. Links are opened by default apps as per your OS config.

- ## 📈 [Obsidian 1.9.0 (early access): Introducing Bases! Turn any set of notes into a powerful database. : r/ObsidianMD _202505](https://www.reddit.com/r/ObsidianMD/comments/1ks0ebr/obsidian_190_early_access_introducing_bases_turn/)
  - Introducing Bases, a new core plugin that lets you turn any set of notes into a powerful database. With Bases you can organize everything from projects to travel plans, reading lists, and more.
  - All the data in a base is backed by your local Markdown files and properties stored in YAML. 
  - To support Bases, we're introducing the `.base` file format and syntax.

- Is this `.base` an open source file format that can work outside of Obsidian also?
  - All the data in a base is stored in your Markdown files. You can also export a view to CSV or copy the content as a plain Markdown table. Any app that can read/edit Markdown files can interoperate with Bases.
  - The `.base` file stores the query information, like SQL or Dataview. It is a new open format based on YAML. It can also be used in code blocks similar to Dataview.
  - You can edit .base files in any code editor, and the format is completely open for any app to implement.
- Maybe Im misunderstanding but why have two files? and not just use frontmatter to contain the YAML like format for base query info, and the body of the markdown for the data?
  - It's not two files, it's one base file and an arbitrary number of markdown files. Bases use your existing markdown files.

- Does this kill Dataview?
  - Base will probably be more useful for standard database things, just showing stuff in tabular form. Possibly even editing the stuff on the spot? That'd be helluva useful. I use Dataview for much more advanced purposes, so Dataview will probably stay.
- I think this will more completely replace DB Folder than it does Dataview, but, like you said, it's going to replace many of Dataview's common use cases.
- Not at all but mostly. When this see the light of day I will move my journaling to base!
  - bases isn’t gonna run JavaScript. It’s not gonna do inline psuedojs functions.
- Nope, this more likely to kill "Projects" plugin. Dataview is still way more flexible, relies on text queries vs UI clicking around + works with tasks and inline properties. 

- o7 dataview kanban and projects ur time has come but ur time was well served
- I use Dataview in ways that it's barely table-based anymore, so I don't think its time has come yet. Unless Base can go jam multiple values together in one cell, formatted to my liking.
- whether there will be anything like in-line bases yet.
  - There is. The docs mention embedding bases into notes as well as inline “code block” bases

- Kanban still works plenty well and it is in MD format, not Yaml disguishes as MD so still this cannot replace kanban for me.
  - any property you add to a markdown file is stored as yaml. The YAML portion is just a comment in the source markdown file in of itself? So it’s still markdown. This can easily replace Kanban. Confirmed that this works with note properties

- inline properties is the biggest thing missing for me currently. Until Properties are properly viewable in Publish, I still have a need for inline values, which means DB Folder will be have a place in my setup for the time being.
  - Since inline properties were a concept from Dataview, and Obsidian doesn't support them in the core product or core plugins, I bet this will have to come as a community plugin like you said.

- Currently you can edit the base file directly in any code editor. But yes, perhaps at some point it would make sense to have something like "source mode" for base files.

- You can also create Bases as codeblocks within existing Markdown notes, which is how I mostly expect to be using the feature (how I use Dataview today). In that case, you can see and work with the code directly without opening in an external editor.

- Can the Base file also query text inside the note itself? like collecting open checkboxes under a specific header of a note?
  - Currently no.
