---
title: lib-office-joplin-community
tags: [community, joplin, note-taking]
created: 2024-01-28T20:54:33.031Z
modified: 2024-01-28T20:54:44.482Z
---

# lib-office-joplin-community

# guide

# discuss-stars
- ## 

- ## ©️ [Crowdfunding Joplin Server license? - Lounge - Joplin Forum _202108](https://discourse.joplinapp.org/t/crowdfunding-joplin-server-license/19891?page=2)
- the Joplin Server license is different from the rest of the project - it's a "Free for Personal Use Only" license and it disallows commercial use.

- ## ©️ [RFC: Switch to AGPL license for Joplin Server? - Development - Joplin Forum _202104](https://discourse.joplinapp.org/t/rfc-switch-to-agpl-license-for-joplin-server/16529)
  - The idea is to prevent a company from taking the software, improve it and sell it as a service, without contributing anything back to the original project. It's still however possible to self-host the service and I suppose even modify it, as long as it's not for commercial purposes.
  - I think I will switch to that license for Joplin Server
  - For now, the desktop, mobile and CLI apps will remain MIT.

# discuss-not-yet
- ## 

- ## 

- ## [Export to Textbundle - Features - Joplin Forum _202309](https://discourse.joplinapp.org/t/export-to-textbundle/32524)
  - I would like to renew the 2021 request (Support TextBundle files? 
- Just look at TextBundles Apps-list:
  - Agenda, Bear, Craft, eBookBinder, FSNotes, Go Edit, Gazer, Highlights, iThoughts, Keemark, Marked 2, MarkMyWords, MindNote, Myary, Note-C, One Jotter, Paper, Smartdown II, Taio, Textbundle Editor, Ulysses, WordPress, XMind: ZEN, Zettlr.

- it wouldn't make sense to support this since it's not widespread enough. It's also Apple-only (weirdly enough) and has been discontinued for about five years.
  - If you want to share a note in an open format, export it as HTML. We do the same as Textbundle (all resources are in the file) except that it works everywhere including mobile as long as a browser is available.

- I wasn't aware that the HTML export encapsulated the images in the file. That would definitely be a more open format. I'll check it out.

- Joplin plugins are also well suited for custom workflows such as this one since you could get the data out in exactly the way you want to, although that requires some development work.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🏘️ [A beginner question about Joplin (I'm coming from Obsidian) - Support - Joplin Forum _202301](https://discourse.joplinapp.org/t/a-beginner-question-about-joplin-im-coming-from-obsidian/29166/7)
- Joplin stores all your notes on your computer. 
  - The notes are stored in a sqlite database in the configuration folder for the software. 
  - However at any time you can export some or all your notes and there are several options. Two of these options are "MD - Markdown" and "MD - Markdown + Front Matter".
  - The reason Joplin uses Markdown and has these export options is to ensure that a user's data is not tied up in some proprietary format
- Joplin stores the images/attachments in a `resources` folder that is found in the same folder as the database file.
  - You can, or you open in a SQLite DB browser 17 and explore or query it like any other database.

- ## 🚀 [Joplin Server pre-release is now available - Development - Joplin Forum _202101](https://discourse.joplinapp.org/t/joplin-server-pre-release-is-now-available/13605)
- The first release of Joplin Server is now available as a pre-release
  - You will need Joplin v1.6+ clients
  - At this point, this server allows you to sync any Joplin client with it, as you would do with Dropbox, OneDrive, etc. So in that way, it's not essential. 
  - Long term, the goal is to add collaboration features

- ## [Options/Configuration should show storage location_201711](https://github.com/laurent22/joplin/issues/7)
- where the files are located
  - On Windows: `C:\Users\YOUR_NAME\.config\joplin-deskop` .
  - On macOS and Linux: `~/.config/joplin-desktop` . /home/yaoo/.config/joplindev-desktop/database.sqlite
  - For the terminal app, it's under the directory "joplin" instead of "joplin-deskop"

- ## 🆚️ [What do you do differently in Joplin in comparison to other note taking apps? - Lounge - Joplin Forum _202004](https://discourse.joplinapp.org/t/what-do-you-do-differently-in-joplin-in-comparison-to-other-note-taking-apps/7886?page=3)
- I have been using BoostNote, then boostnote.next for a few years. Now the legacy is discontinued, and the .next version is pushing heavily and constantly for paid cloud storage, I have been looking for alternatives.
- Joplin seems to have much of it:
  - tree-like organization which can be re-arranged simply
  - export of entire tree structure
  - keyboard oriented workflow
  - actual support for dropbox through integration instead of working on file level
  - android support
- There are some things I will miss dealry on the way out:
  - Adinmotion markdown (for "NOTE", "WARNING" etc sections
  - better themes

- I use typora as an external Editor on Mac and Win10 Works like a charm and has a mix of layouted text and Tags that appear when you need to see them.

- Evernote has some cool things such as thumbnails in the note list but, to me, that is a kind of “cosmetic” feature that I can live without.

- ## [Joplin – An open-source note taking and to-do application with synchronisation | Hacker News _202307](https://news.ycombinator.com/item?id=36611355)

- 🆚️ How does it compare to obsidian?
  - Having started with Joplin, the three things that took me away were the (at the time) lacking mobile support, periodic syncing collisions, and probably most importantly, their non-standard file format.
  - There was a tool that could extract files into standard markdown format, then repack them, but the overhead was tiring, and meant a few key environments lacked access, namely when I was accessing a server from the rack, and when the mobile app acted up
  - Obsidian has better community plugin support, better sync (paid) and stores plain text files instead of using a DB. Most importantly the mobile app (at least for iOS) of Obsidian is 1:1 with the desktop app.
- I tried a few, but (nearly) default Obsidian won me over by simplicity, ease-of-use.
