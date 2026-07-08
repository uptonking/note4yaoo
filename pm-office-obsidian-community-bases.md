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

- ## [Is there really not any way to make bases query something smaller than a file? : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mxlibf/is_there_really_not_any_way_to_make_bases_query/)
- Obsidian has always considered notes to be the smallest unit. You cannot assign tags to blocks, you cannot assign properties to blocks, you cannot meaningfully link from a block to a note (the backlink shows the note, not the block), and you can only link to a block as part of a note.

- It’s simply not a block based editor - it’s file system based. That has always been the opinionated take. You can look into anytype if you want something like that, it’s much more rigid tho.
# discuss-showcase/examples 🌰
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [BASES - Relative Progress Bars | LeanProductivity _202601](https://blog.sascha-kasper.com/BASES---Relative-Progress-Bars)
  - [BASES - Absolute Progress Bars | LeanProductivity _202601](https://blog.sascha-kasper.com/BASES---Absolute-Progress-Bars)

- ## [A Bases Template for Project Tracking or Task Management - Share & showcase  _202508](https://forum.obsidian.md/t/a-bases-template-for-project-tracking-or-task-management/104249)

# discuss-issues
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Bases: Open in Source Mode (Easy access to '.base' YAML file/view) - Feature requests - Obsidian Forum _202507](https://forum.obsidian.md/t/bases-open-in-source-mode-easy-access-to-base-yaml-file-view/103196/6)
  - Provide an option to view the YAML (“source”) view of a .base file. There’s currently an option to show the file in explorer, and I use that to then open the file in VS Code, but I’d like to have a way to switch between YAML and GUI view similar to other Markdown files in Obsidian.
  - workaround: right-clicking on the .base file, showing it in explorer, and opening it in a different editor.

- ## [Bases: Renaming (or deleting) a property in properties view should update all affected bases - Feature requests - Obsidian Forum _202508](https://forum.obsidian.md/t/bases-renaming-or-deleting-a-property-in-properties-view-should-update-all-affected-bases/104914)
  - 2种场景都很合理

- ## [Provide API access to the results of Bases view - Developers: Plugin & API - Obsidian Forum _202601](https://forum.obsidian.md/t/provide-api-access-to-the-results-of-bases-view/110660)
  - Bases is a fantastic first‑party way for users to define cohorts of notes. Allowing plugins to get a list of notes from a Base without the plugin being implemented as a Base view would significantly expand what plugins can do with Bases.
  - Many plugins implement their own query language, search system, or filtering to compile lists of notes, which requires users to re-write their custom filters across plugins. If users could point such plugins to a Base#view, they could reuse a native feature of Obsidian instead.

- ## [Bases are great, the Bases API will make them fantastic : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mxatpc/bases_are_great_the_bases_api_will_make_them/)
  - I've really enjoyed exploring how Bases can change up how I display certain kinds of data in my vault, especially views of related data. They feel familiar as someone moving over from Notion, even though I'm doing more with inline tags and the Tasks plugin versus individual files for everything.
  - But once the Bases API is available and plugin authors can start hooking into it, I think we're going to see some really fantastic ways to use it and its interface. Specifically imagining dynamic Bases views of Task data, rather than using the inline queries and functions.
  - Maybe even outputting Dataview results into a Bases-styled table with sorting, dynamic filters, and other functionality?

- A pretty simple one honestly. If I'm viewing a Base, I want to be able to click new note, and have tags or things applied automatically. Or when I set up the properties it moves the note to the right folder etc. Right now it just goes in the root etc and requires manual moving.

- Does Dataview currently have an API ?
  - It appears to! Even an integration that renders dynamic Dataview queries would be neat, but probably ways to take advantage of connecting the two at the API layer
# discuss-properties/schema
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Some people here using "object types" for every notes to mimic AnyType structured data? : r/ObsidianMD _202510](https://www.reddit.com/r/ObsidianMD/comments/1oina9c/some_people_here_using_object_types_for_every/)
  - I'm testing (for now successfully) organizing my Obsidian vault more like Anytype meaning, assigning an “object type” to every note.
  - Each note has an Object property, and each Object a template (optional). For instance, I have currently Project, Project file, Server, Subscription, Task objects, Person object types. etc. when i add a new note, I select the right type and the right template.
  - The big advantage of that is that anything in my vault is "Typed", it's a full and formal data-model that can evolve with time. I feel more confortable with that rather than just using tags, which often lead to a big mess.
  - I noted also - and it was not planned - that my graph view looks a lot better because each note is linked to a object type which can be of a different color. Therefore, it makes a more logicial clustering without even using tags in the graph view.
  - Final consideration: Obsidian is extremely powerful. AnyType is a good product because it helps to formalize everything, but I had absolutely no difficulty to reproduce this in Obsidian, very intuitively, and the new Bases feature is really wonderful. I even have a table with all my object types and their template(s).

- Are you just assigning it as a property? Or are you using something like the fileclass/Metadata plugin or something else? The idea is appealing.

- Yup, I do something similar. I use “Web Links” for bookmarks (terminology from Capacities), “People”, “Projects” and a few others; each are notes in a top level directory of the same name with a Base in the folder as well to list, sort, etc.
  - I found Metadata Menu really helpful for this; I configured it to understand the structure of properties I want in each folder and use that to ensure a new file has the right properties. My use cases are pretty light at the moment so I haven’t built templates; I just make a new file on the right directory and use Metadata Menu to inject the desired properties.

- I do exactly the same. And I also have a script that validates all objects conform to a given schema (like making sure person has a worksFor attribute and stuff like that.)
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Bases List View has Potential as Checklist : r/ObsidianMD _202511](https://www.reddit.com/r/ObsidianMD/comments/1oy8n71/bases_list_view_has_potential_as_checklist/)
- Checklists are my last use case for Dataview, I'd like to get everything unified under Bases but I can't do checklists (to-do, shopping, etc)

- I managed to find a workaround to add clickable checkmarks to the card views of the databases, using the QuickAdd plugin. I'm sure it can also work for the list view.

- I use the Table view as a checklist. Not quite as clean as List view, but I use it for projects with multiple steps/statuses and it works great.

- ## [Can a base have properties? : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mzae8p/can_a_base_have_properties/)
  - is it possible to add properties to a .base file? I want to create a base of bases to organize my notes, but I want them to have covers for the card view, but that seems to be impossible.

- Just embed the base file into the note. You can even have it pull a specific view every time as well.

![[basefile.base #heading name]]

- Is there a difference between just embedding a base file in a note with the double brackets, and using the code black with base (as you had said)? 
  - Not much, except there will be no additional file, and link in your graph view, if the base is inside a code block. I myself have separate files I embed but if I ever had a need for, say a base of bases, I'd go down that road instead of having multiple duplicate markdown notes that only exist to embed a base.

- ## [How to group bases by month _202601](https://forum.obsidian.md/t/how-to-group-bases-by-month/109597)
- Make a Properties formula that’s [Created.year, Created.month]. Then group by that formula.

- [Group by year in bases : r/ObsidianMD _202602](https://www.reddit.com/r/ObsidianMD/comments/1r355n3/group_by_year_in_bases/)
# discuss-internals-bases
- ## 

- ## 

- ## 

- ## 

- ## [Bases: data source from single CSV, JSON, special markdown file instead of note properties - Feature requests - Obsidian Forum _202508](https://forum.obsidian.md/t/bases-data-source-from-single-csv-json-special-markdown-file-instead-of-note-properties/103622)
- This feature request is legitimate but the background is wrong. Obsidian does not read every file every time. There are multiple layers of caches (in memory and on disk). 
  - I still think that if you have a very large database with complex queries you are better off using a different product.

# discuss-dataview/datacore
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Obsidian bases with inline fields? : r/ObsidianMD _202508](https://www.reddit.com/r/ObsidianMD/comments/1mwsbuk/obsidian_bases_with_inline_fields/)
  - I'm guessing the new bases feature doesn't work with Dataview's inline fields?
- You're correct. Inline fields is an unofficial feature from an unofficial (but hugely popular) plugin. You should be using only top-level YAML frontmatter properties if you want official support. There are community-made scripts out there to go through your notes and convert inline fields to properties. There's also tools out there to convert inline fields to properties as you type them.

- The issue for me with switching to properties is that links aren't supported there. For example, I can have an inline field with text like "I met [[josh]]". If I move it to the properties, it doesn't consider the current note and "josh" to be linked. Unfortunately my solution was duplication. Since I want to preserve linking, I have a script that copies the value of the inline field to the property so that I could have both linking and using it in bases
- I must be missing something because when I use the [[Link]] format in a property it does link them. I can see it in the local graph and the Rich Foot plugin.
  - It only works if the field is just the link without any additional text. So [[josh]] would work, but not "I met with [[josh]]"
- A workaround could be to use aliases if it's just a single link. [[josh|I met with josh]]
- You can also use a list property with multiple linked entries

- ## [Obsidian Bases by Block, Sentence, Checklists rather than full file : r/ObsidianMD _202603](https://www.reddit.com/r/ObsidianMD/comments/1s3rke0/obsidian_bases_by_block_sentence_checklists/)
- Bases is limited to note-level data, so it won’t pick up individual blocks like that.
  - For block-level queries (tasks, tagged lines, etc.) you’ll want Dataview or Datacore.
  - Bases ≈ metadata, Dataview/Datacore ≈ actual content inside notes.

- Datacore is a metadata index - it stores information about every page, section, block, list item, canvas file, and other file in your vault in an internal database which can be quickly searched for generating nice-looking views. You access this metadata using the query language, and then compile it into useful views using the embedded views.
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
