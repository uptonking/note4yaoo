---
title: lib-editor-app-community-version-history
tags: [collaboration, database-design, version-control]
created: 2024-07-18T15:51:29.786Z
modified: 2024-07-18T15:52:38.176Z
---

# lib-editor-app-community-version-history

# guide

- search-keywords
  - office/document track-change/version-history
# discuss-stars
- ## 

- ## 
# discuss-diff
- ## 

- ## [draftable - Show HN: Diffs of Word documents, designed for humans | Hacker News _201305](https://news.ycombinator.com/item?id=5662214)
- Office 2013 brings some powerful compare options for Word and Excel:
  - Compare (included in Word by default) http://office.microsoft.com/en-us/word-help/compare-is-under...
  - Spreadsheet Inquire (need to enable an included COM add-in which requires . Net 4) http://office.microsoft.com/en-us/excel-help/what-you-can-do...

- Word already has this capability through their track changes feature. You can even use it to open two documents and see a third document showing what has changed.
  - Doesn't provide many more features than piping antiword to your favorite text-based diff-tool. Only difference i've managed to find is that with draftable you get formatted headers.

- Pictures added or removed are not shown. Changed formatting is not shown. Text modified in text boxes is not shown.

- ## [ChangeDetection, monitor any website change | Hacker News _202309](https://news.ycombinator.com/item?id=37348162)
- I've used https://urlwatch.readthedocs.io but this definitely seems much easier to use—though possibly not quite as powerful regarding page filtering. But at least ChangeDetection supports jq which is already quite a nice feature in that department.

- https://visualping.io does a nice similar job and is free for moderate personal use.

- Curious how this handles sites behind CloudFlare using bot detection.
  - It’s not too difficult to get past cloudflare using puppeteer. Being normal is the key.

- ## [Ask HN: How do you track copy changes on websites/emails? | Hacker News _202404](https://news.ycombinator.com/item?id=40046670)
- I have been using urlwatch for years, I have a cron run daily which will send a diff of the page(s) via email. You can also use it for checking local file changes and more.
- https://github.com/thp/urlwatch /202410/python
  - Watch (parts of) webpages and get notified when something changes via e-mail, on your phone or via other means. Highly configurable.
  - The change notification will include the URL that has changed and a unified diff of what has changed.

- This is how I’ve had the most success in the absence of a CMS. Automate dumping of the website text into Google Docs/Sheets and have people edit those.

- Ours are all stored and managed in the CMS/DAM we use, which happens to be Adobe Experience Manager. When the email service renders an email, it calls the CMS endpoint which returns the html with handlebars style template placeholders. That endpoint is heavily cached so not too worried about the mail service hammering it.

- For websites, there's a bunch of hosted services for this, like VisualPing or ChangeTower or Sken.io or BrowserStack. It's often called "visual regression testing".
  - You can also do this yourself with something like Playwright: https://playwright.dev/docs/test-snapshots
  - For email templates, they usually create a HTML version hosted online somewhere too, don't they? You can probably use the same tools for those if they're publicly accessible.
# discuss-git-office
- ## 

- ## 

- ## 

- ## [Using Microsoft Word with Git | Hacker News _202008](https://news.ycombinator.com/item?id=24302896)
- I never trust the received file's "track changes", always compare to the latest version I've sent -- and it is extremely common to find a change that wasn't mentioned/discussed, and somehow magically "accepted" or otherwise not tracked in the other side's "track changes". Whenever I point these out, I always got a "oh, yes, forgot about that one"

- Most serious document creators don't want to branch and merge, instead they want to pass on the document through a series of stages. They want statistics on when, what and why of each stage. And at any point of time the document is in one definitive stage not scattered across emails/folders/versions/forks.

- I think the issue is that parallel workflow is a bridge too far for the current legal profession. They do sequential and they like it. A tool that makes the sequential workflow better will gain more ground than one that tries to change the process whole hog.
  - I have worked on several hundred of these types of contract processes in the last few years, and you are absolutely correct: sequential is where it's at for these situations. I have, however, encountered a few situations where time was an issue so I had two or three different versions out to different parties at the same time, and then merged the proposed changes where possible and sent out alternate versions where the changes differed. That process was... not fun, and could definitely use a more coherent workflow than manual merges or Word's built in merge features.

- Git for Word doesn't make sense because software applications can be edited independently because of abstractions -- you can't have different people changing different parts of a Word document without ANY idea of what each other is doing the way you can in software. You can't change the tone in one section to conversational in isolation.

- Typical workflow with word documents required mutiple people reviewing, commenting, and merging or rejecting the comments. Microsoft Word's change tracking, comment, and review features are adequate for most people.

- ⚖️ if you're using libreoffice write you can save your file as a flat odt file (.fodt), which gives you a version-controllable format
  - Yes, it definitely has its limitations. It used to store everything on one line without breaks if I recall correctly. With a little bit of work to ensure stability of numbering, FODT and related flat ODF formats could be really usable with version control.

- Just use Markdown (or similar markup language) and a tool like pandoc to convert to word if necessary.

- ## 🤔 [Ask HN: “Git” for Microsoft Office? | Hacker News _202005](https://news.ycombinator.com/item?id=23245552)
- A couple years back I built this: 
- https://github.com/tomashubelbauer/modern-office-git-diff /js
  - It is a pre-commit script which unpacks Office XML into text contents and tracks that alongside the source file. This way you can consider the binary to be a source of truth, but with each commit you also get a textual diff showing what changed content-wise. More or less
  - This is achieved using a PowerShell script which unpacks the ZIP file to a tracked directory, formats the XML files for nice diff and tracks the formatted files as well.

- An underused feature in MS Word is 'Compare documents' - It's under the Review tab on the ribbon as 'Compare'. It allows you to do a 'diff' style compare on two Word documents - it's invaluable for working out what changed between versions if the place you are working at doesn't have any other document tracking systems.

- Technically, tracked changes and SharePoint. But in practice, you’d rather send the changes to the project owner via carrier pigeon.
  - I’ve looked into what it would take to make a git style system for docx (since it’s just zipped XML, right, and the file format was a nightmare whenever an edit was made. 
  - Someone smart should take a look at it, as there would be a massive market for a DVCS for Office files. Imagine a world where every bill in Congress was committed to a central repo so the whole world could see the changes, or where someone in your team wants to play with the formatting on a shared requirements document without breaking the page you’re writing on. It would be a boon for productivity.
- I don't see any evidence that the average Office user is clamoring for it. Even comparatively crude systems like Track Changes aren't used in my experience as often as they could be, and those are a hundred times easier for non-technical people to wrap their minds around than a Git-like system would be.
  - I suspect that part of the reason this problem is so intractable is that it's really two problems. The first is actually tracking the changes to the underlying document, which, as you note, is hard enough by itself. But then on top of that is the second problem, which is that you'd also have to come up with an interface that could make the power of a Git-like system comprehensible to non-technical users. And you'd need to solve both problems to have a product that would actually be ready to take to market.

- 🌰 For procedure-style documents, I co-founded a company called ProcedureFlow that allows change requests but for hyperlinked flowcharts. My inspiration was 100% GitHub/pull requests. We found that a lot of organizations store procedures in document form which change all the time. So, the purpose behind our product is to move away from a document into a format that easier to use/change/track.
  - A procedure is made up of many flows that are linked together. Everyone that uses the procedure views the "live" flows (like a master branch). Each user gets their own branch which we call a "draft". In a draft, a user is free to make any changes they want (add/delete/modify flows) and then submit all the changes for approval. Approving the change request then merges the changes into the "live" for everyone else to see/use. I even went so far as to build side-by-side diff of the flowcharts, rebasing/merging with live, and conflict resolution.
  - It's simplified in the UI so the terminology isn't 100% like git. But, one of our biggest hurdles though is actually teaching users how this works why it's better than the current mode of document locks/real time editing. And when our customers "get it", they really fall in love with the concepts and why it's better

- Use sharepoint, office365, and Teams. It versions, it supports collaborative editing, no more mailing things around, and so on.

- Most office folks require version history rather than version control -- not many are likely to need to branch, merge, pull, push -- and Office365 definitely supports the former.
  - this is different from "Track Changes" in older version of office -- which still exists but is more for visual diffing. Version history only stores snapshots.

- We're working with LibreOffice, but MS also supports OpenDocument. The quality of the XML produced by these programs is extremely poor. LibreOffice, for example, changes the name of every (or nearly every) automatic style every time you save, which makes it very hard to use the diffs. Also ODS doesn't stride formula references when you repeat rows, which baffles me.

- I wish there was a git blame for office.

- ## [Show HN: Version Control for Microsoft Word | Hacker News _201706](https://news.ycombinator.com/item?id=14552140)
- Slight aside (since LibreOffice != Word, and XML diffs are still horribly messy):
  - If you save your LibreOffice documents in flat XML format, (e.g. fods, fodt instead of ods, odt), placing them under version control becomes slightly less annoying — the diffs become at least _potentially_ human readable.
- Word can also save in flat XML format, but it's really verbose (really just a listing of all the document parts).

- I tried doing something like this a couple of years ago by embedding an actual git repository inside a docx or ODF file. Unfortunately, most popular word processing suites back then trashed the git directory instead of leaving it alone (as they should, according to the standards)
  - I did something similar: I built a tool in Python called musdex to use in git (or any other VCS) hooks to extract the zip file that a docx/odf file is before commits and recombine them on pull/merge (essentially treating the docx/odf as something of the build product of the repo). Run an xml lint tool on the XML in them and you get decent diffs.
# discuss
- ## 

- ## 

- ## ⌛️🎞️ [CodeTour: VS Code extension to record and play guided walkthroughs of codebases | Hacker News _202103](https://news.ycombinator.com/item?id=26488610)
- A killer feature would be doing semantic analysis to attach steps to AST nodes instead of lines. EG a class or function.
  - Without this it seems tours could be broken/outdated very quickly in active code bases.
- 💡 IMHO this is much better solved with a literate programming approach where the tour content lives inside the code as comments. Then as code is refactored and changed it's very obvious that the related docs and tour data has to change too.
  - some files don't necessarily support comments (e.g. JSON/image)
  - Additionally, after speaking with a bunch of folks, there are definitely teams that weren't interested in "polutting" their code with comments
  - That said, I totally agree with the value of a literate programming-based solution. But there may also be some nice properties to a "side car" file as well, and so I'm primarily trying to explore how well we could make that work, in a resilient and easy-to-maintain way. We'll see how it goes
- > there are definitely teams that weren't interested in "polutting" their code with comments
  - Add an extension feature that toggles (hides/shows) those comments maybe?

- Not an equivalent of literate programming. Here you can jump to arbitrary files at arbitrary points, in literate programming your code must flow from top to bottom linearly, which is most of the times impossible to achieve.

- How do CodeTours handle drift as the code base changes?
  - They have a GitHub Action to monitor this

- 🔒 how is user privacy handled? Is data about the repo sent externally? I assume this would primarily be useful for OSS projects and not private or internal/confidential projects?
  - When you record a tour, it simply creates a JSON file that can be committed/maintained as part of the associated codebase. Then, when someone takes the tour later, they're simply "reading" that file locally in their editor, and so no data about the codebase is ever sent externally.

- I'm hoping that some day it'll be possible for my coworkers to follow a CodeTour without installing VS Code.
  - That's exactly the issue we had at the office. So someone in our team built https://github.com/doctolib/code-tours-github we use it to help new joiners get into the codebase!

- CodeLingo’s playbooks are an approach to solve that type of problem https://playbooks.codelingo.io/p

- 🆚️ This seems really cool but my immediate thought is that it might be pretty fragile compared to just screen recording.
  - Create the tour, then screen record playing through it. Two birds one stone.
  - 💡 conversely, a screen recording does not allow for easy maintenance as this plugin does with its tours.

- Does anyone know of any package similar to this for emacs?
  - For vim I use the CodeReviewer plugin to capture comments for files. I modified it to use differently named comment files and to jump to the file locations from the comment line. I am planning to include support for hierarchical comments or referring other comment files from within one. Also the problem of tracking code changes or referring to a certain git commit is still there - in clearcase it can be easily done with a reference to the branch, but not sure how to do it in git.

- ## [Hey Dropbox, why can't I compare file versions like this? | Hacker News _202003](https://news.ycombinator.com/item?id=22221265)
- Am I missing something? This already exists in Google Docs. Much easier to implement when the doc is database-backed (recording every keystroke for OT) vs file-based.
  - Yeah, the thing is, you can't do this in a file-format-agnostic way (you need to know what a Word doc or an Excel sheet is), which makes the file system layer the wrong level of abstraction to consider.
- The diff when database-backed is still going to be file-format specific because a text-based document will not be stored in a DB identically to a spreadsheet.

- Etherpad was acquired by Google in 2009 and a fork of Etherpad, Hackpad, was acquired by Dropbox in 2014. Both projects got folded however: Etherpad into Google Wave, and Hackpad into Dropbox Paper.

- Git supports configuring different diff programs for different file types. And there are tools to diff docx etc.

- Cloud word processors like Zoho Writer & Google Docs already have version comparison features. But this idea of a sliding time traveler for documents is very intuitive!
  - Also Zoho Writer has a combine feature, that lets you upload a docx and combine it with another docx - with the changes highlighted as tracked-changes. Pretty handy for comparing docx files.

- ## [On Building Git for Lawyers | Hacker News _202411](https://news.ycombinator.com/item?id=42137391)
- This person is 100% correct that git will never see adoption outside the tech industry.

- Git is a tool built around the needs of software developers. Because git is too complicated and branching, though in principle, would make sense in some situations, is actually pretty difficult to manage (especially for binary documents).
  - Also, they do use version history built into tools like Sharepoint/Office, or the document itself.

- "git for x" is overrated. Git can compare binary diffs like Word files by using custom diff drivers and external text conversion tools. Git allows you to configure a process where these files are converted into a readable format for diffing.

- google docs has a very nice version control
- Google Docs is a step in the right direction but has several limitations.
  - Lawyers don't want everyone holding the pen at the same time. Specialists want to make their changes and have them reviewed in isolation from other's changes. Think of a redline like a pull request. You don't want other people's changes in your work when it's getting reviewed.
  - Google Docs breaks down when even a single person drafts outside of it. See the section of my essay about why lawyers will never stop using Word. Even if you managed to get an entire firm using Google Docs, it still wouldn't work because they need to exchange drafts with external parties.

- ## [Ask HN: Best way to version control your notes or documents? | Hacker News _202302](https://news.ycombinator.com/item?id=34690171)
- I recently switched from using Google Docs to storing my notes in Markdown/Git and making them available just to myself via Docusaurus on a private Gitlab Pages repo.

- I tried using git for general note taking and I hated it. I used Foam, which is markdown inside of VSCode synced to Git, accompanied with GitJournal which allows you to update the same markdown files from a mobile device.

- For plaintext documents in Emacs the diff command is useful but enabling the fossil-mode has more steps, and Fossil has extra plumbing for ticketing and webui.

- ## 🌵 Introducing Projects for Replit Teams. _20240718
- https://x.com/Replit/status/1813713645882515570
  - We’re sick of decade-old version control systems. Git is unapproachable to non-engineers and makes it hard for everyone else to start contributing.
  - When you create a project, you'll get a clean dashboard that shows the active forks of your main Repl and who’s currently coding on your team. 
  - When starting a new feature or prototype, you can easily make a fresh fork and jump between versions from the Workspace header. Once you’re happy with the changes, you can easily integrate them back in one click. 
  - Projects are backed by Git under the hood, but we’ve flattened the learning curve.

- If you made it so that everyone on the team could see the same inputs/outputs in the AI pane that would be very cool.
  - Replit AI chat is collaborative! you can see messages your teammates sent and how the AI replied

- I'd guess they are using their multiplayer tech that doesn't have merge conflicts. I'm sure there are edge cases where intents are lost. They do have more information than git does when merging, probably as far as near keystroke level, when files were edited/added/deleted, and more.
