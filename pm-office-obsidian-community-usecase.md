---
title: pm-office-obsidian-community-usecase
tags: [obsidian, usecase]
created: 2026-07-05T14:58:10.113Z
modified: 2026-07-05T14:58:20.129Z
---

# pm-office-obsidian-community-usecase

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-feat-project/task
- tips
  - properties: people, task/event, dateStart/end, status, priorty

- ## 

- ## 

- ## 

- ## [TaskNotes 4.10.0 and TaskNotes Workflows companion plugin : r/ObsidianMD _202606](https://www.reddit.com/r/ObsidianMD/comments/1tu4qv9/tasknotes_4100_and_tasknotes_workflows_companion/)
  - this release exposes a new Obsidian-internal TaskNotes runtime API. The new API allows other plugins to respond to TaskNotes events (like the completion of a task, or the beginning of time tracking), and to manipulate your tasks.
  - I would love to see more plugins that inter-operate with TaskNotes. 
  - Leveraging this API, I've published alongside this release a "companion" plugin for Tasknotes, TaskNotes Workflows. TaskNotes Workflows integrates with TaskNotes to enable automatic task-transformation or other actions based on task events
  - TaskNotes 4.10.0 also introduces "materialized occurrences" (see the spec). This allows recurring tasks to create a new note for every occurrence.

- ## [Thoughts on TaskNotes as an Obsidian Projects replacement? : r/ObsidianMD _202510](https://www.reddit.com/r/ObsidianMD/comments/1nzohdm/thoughts_on_tasknotes_as_an_obsidian_projects/)
- I'm loving the flexibility of note-per-task from TaskNotes, and think the combination of the plugin features with things like Bases can be VERY powerful.

- The one note per task wouldn't be an issue in my case, because Projects already forced you into using one note per task. For day to day small tasks, it may be a bit painful depending on the case, but I don't have a workflow set for those, do no big deal either.

- I wanna use TaskNotes and I wanna use colors to show importants. 

- ## [For those using taskNotes who feel a page(md file) per task is a lot, what approach do you use for todo lists? : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1pjoup1/for_those_using_tasknotes_who_feel_a_pagemd_file/)
  - I think of those file being created anytime a task is made via taskNote. I wish we could decide to not make it a file if it’s some quick task and not something that’ll have detailed steps or info to put in that note.
- For me the Advantages of the task notes plugin are bigger then the disadvantage of using separate files for each task. Since tasknotes uses yaml properties to store task meta data and a tag to identify tasks it improves portability and uses less 'workarounds' then the tasks plugin additionally It is just more aligned with bases then the inline tasks .
  - Shopping lists are the only reason why i would prefer inline tasks but i decided that i can use a different free app for that.

- I have similar concerns: I write tasks directly into project notes, so they have context and all relevant infos. There simply is no need to have a separate file for them. But on the other hand - aside from that thought - I love TaskNotes for the integration into bases and all the other features.

- I like the approach of Projects, Sections and Tasks...similar to todoist. Each project and section gets their own pages and each task is just a to-do.

- I have the same issue. The plugin is so well written and feature-rich, that I'd like to use it for all my tasks (also the smaller ones), because then I'd also be able to TaskNotes Calendar Feature for those.
  - Currently: It's very easy to promote a regular task to a tasknote-task. If it were equally easy to demote a tasknote-task (that has no note info) to a regular task, it would completely cover our needs. Then we'd simply run such a step in our file containing smaller tasks and get he best of both worlds.

- ## 🆚 [Task Notes or Task Genius : r/ObsidianMD _202509](https://www.reddit.com/r/ObsidianMD/comments/1ngsxh6/task_notes_or_task_genius/)
- Task Genius is flexible: you can have a project note where you index all your tasks, create custom views, and even integrate it into different databases, but only for PCs. It allows filters (complete, pending, etc.) for all your notes in general, quick capture, and connection to Google Calendar/iCal, although that part is a bit annoying. It also offers views such as Canva, Inbox, horizontal calendar, timeline, and more. For me, it's ideal because I centralize my tasks in a single note or in the daily note, and I move the important ones to Calendar.

- in tasknotes, what is the context field for? I have not been able to figure that out.
  - It’s a GTD (Getting things done) concepts where u seperate tasks by context (i.e: @desk, @home, @phone .. etc) so you can easily when a certain context is available for example u are planning to go to the to a mall or the shopping center in your city you can see all the @shopping-mall context tasks and be reminded on all the things i can do there
- I use it to assign to users (not context). So my context entries are people. The idea is tasks often occur in a location.

- I've become a big proponent of TaskNotes. Why?
  - One note per task. I was initially not a believer in the "one-note-per-task" approach, but I've found that it works really well. Context can be pulled into each task from different parts of the vault and all tasks are neatly stored in a separate folder. Links to the task can be pulled into my daily agenda as needed.
  - Natural language task entry. The natural language task entry in TaskNotes is also great. I don't find myself clicking into calendars and other settings boxes as I can just mention those details in natural language during the task entry and it parses it amazingly well.
  - Project features. I like that after linking a task to a project note, the plugin automatically pulls all project tasks into the project note without having to manually create queries etc.
  - Plays well with Obsidian Bases. 

- TaskNotes does not work for me. I write Tasks into notes where they fit into the context. Tasks can easily be collected into nice lists afterwards. 
  - I know this comment is older, but to add that TaskNotes supports inline tasks quite well, and in my opinion much better than the Tasks plugin. If you write a normal (inline) task into the meeting note, TaskNotes will add a small icon behind it. If you click on it it will „import“ the task and generate a TN. I am not sure if you have to activate it in the TN settings. 

- ### [Task Notes vs Task Genius Pros and Cons : r/ObsidianMD _202602](https://www.reddit.com/r/ObsidianMD/comments/1qzzcv0/task_notes_vs_task_genius_pros_and_cons/)
- The main difference is their philosophy.
  - TaskNotes creates a note per task, with all what that implies: you can have attachments, version history, details, metadata, visualization of where said task appears via backlinks, etc. On the other hand, you might end up with lots of files (that you can archive / delete / merge / etc. in the future).
  - Task Genius enhance the visualization of your tasks with extra fields added to the tasks themselves. For example, it adds something like "[||||----]" for progress bars on your tasks. This makes managing metadata, details about tasks, etc. harder because you only have that task line as the context and then everything else is the note itself (other tasks, text, etc. not specific to the task).
  - Both work with the tasks plugin, but you don't need it. And both leave functional tasks if removed. Both provide better visualization of tasks.
  - I'd say that you have to check what works better with what you have and how you manage your workflow. But the main difference is one note per task or keep the view of tasks in a note along with other contents not 100% related to the task itself.
- They have different philosophies. You'll end up with extra text in your task description and with one note per task... It doesn't make much sense to me. But nothing prevents you from testing if it makes sense in your use case. I'd recommend putting the task title in a property as task Genius will change it and you probably don't want your note getting renamed all the time...

- TaskNotes has been immensely helpful, I love how it creates widget-like kanbans at the bottom of, say a project note with all the tasks associated with said project. And works the same for subtasks associated with a given task. Couldn't be happier with it after trying sooo many others. 

- my favorite is tasknotes. It was the last one I tried because I thought having a note per task would be overkill, but I like the views, the scheduled date, estimated duration, etc. The natural language input is great.

- 
- 
- 
- 
- 

- ## 🚀 [TaskNotes - Using frontmatter to track tasks : r/ObsidianMD _202506](https://www.reddit.com/r/ObsidianMD/comments/1l0e0iu/tasknotes_using_frontmatter_to_track_tasks/)
  - a plugin that uses YAML frontmatter to manage tasks, daily notes, and time tracking in Obsidian.
  - Creates tasks as individual markdown files with structured YAML metadata (status, priority, due dates, contexts, time tracking), 
  - Provides calendar views with visual indicators for tasks and daily notes, 
  - Supports recurring tasks with instance tracking, 

- Looks interesting, although I enjoy making a task in a note on the fly and then using the Tasks plugin to roll everything up. I think a note per task can slow a person down, but that is just my opinion. Bases is an excellent addition to the Obsidian tool chest, but I will be avoiding using it just for the sake of it

- Last year, I created a lot of DataviewJS and some other scripts to do something similar. There are a lot of uses for storing a task as a note. You can add notes to a task, attach a document, and transform a task into a project with the tasks in the note. It will be great to use with Bases
  - Classic TiddlyWiki had a powerful task/project management system because of the use of notes as tasks. I'm using Org-mode for tasks now, and it's quite powerful. The batch editing feature sold me on it. But I will test this plugin and give you feedback!
# discuss-feat-cms/crm
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-cases
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-files
- ## 

- ## 

- ## 

- ## 

- ## [Cloudflare Drop | Hacker News _202607](https://news.ycombinator.com/item?id=48836233)
- Does nobody read the fineprint(小号字体部分)? By submitting, posting, or publishing your content, suggestions, enhancement requests, recommendations, feedback, information, data, or comments (“Content”) to any Website or Online Service, you are granting Cloudflare a perpetual, irrevocable, worldwide, non-exclusive, royalty-free right and license (with the right to sublicense) to use, incorporate, exploit, display, perform, reproduce, distribute, and prepare derivative works of your Content.
  - This is standard boilerplate for hosting companies so they don't run into issues putting your content on distributed CDNs, or if things are in their logs, etc.
  - Vercel, Netlify, Fly.io all have the same "legal-ese".
- Netlify made this 10 years ago... they even copied the name

- I doubt this is a real safety issue. You can already sign up for a free cloudflare account and deploy it for free, on your own, on a free workers.dev domain. The friction removal here isn't going to meaningfully change the security / amount of malicious content.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
