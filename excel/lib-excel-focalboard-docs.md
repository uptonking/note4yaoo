---
title: lib-excel-focalboard-docs
tags: [docs, focalboard]
created: 2022-03-16T20:45:20.467Z
modified: 2022-08-21T09:56:59.220Z
---

# lib-excel-focalboard-docs

# guide

- resources
  - [Focalboard: alternative to Trello, Asana, and Notion](https://www.focalboard.com/)
# docs
- Mattermost Boards enable your team to manage projects and tasks via a familiar Kanban board structure.
  - Keep everyone in your team and organization in the loop to stay on schedule with clearly defined tasks, owners, checklists, and deadlines. 
  - Keep everything your team needs in one place, including documents, images, and important hyperlinks.

- [Overview](https://docs.mattermost.com/boards/overview.html)

- A board is a collection of cards to help you manage your projects, organize tasks, and collaborate with your team all in one place.
  - Boards can be displayed and filtered in different views such as kanban, table, calendar, and gallery views to help you organize your work items
- A board contains cards, which typically track tasks or topics, and views, which define how to display the cards, or a subset of them. 
  - Views can display cards in a board, table, calendar, or gallery layout, optionally filtered and grouped by a property (e.g., priority, status, etc).

- Cards are used on a board to track individual work items.
  - It’s not currently possible to move cards between boards. This functionality will be supported in a future release.

- [Work with cards](https://docs.mattermost.com/boards/work-with-cards.html)

- A card consists of:
  - A set of properties: 
    - **Properties are common to all cards in a board**. 
    - Board views can group cards by `Select` type properties into different columns.
  - A list of comments: 
    - Comments are useful for noting important changes or milestones.
  - A set of content: 
    - The content of a card can consist of Markdown text, checkboxes, and images. 
    - Use this to record detailed specs or design decisions for an item for example.
- Drag cards from one column to another to change their `group-by` property.
- For sorted boards, dragging a card to a column will auto-sort it using the specified sort settings.

- Card grouping is only available in **board** and **table** views and you must have at least one `Select` or `Person` property on your board for grouping to work.

- card supports a wide range of fully customizable property types:
  - Text
  - Numbers
  - Email/Phone
  - URL
  - Select/MultiSelect
  - Dates
  - Person/MultiPerson
  - Checkbox
