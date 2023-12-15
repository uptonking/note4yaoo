---
title: pm-office-notion-examples
tags: [examples, notion-database, notion-like]
created: 2023-12-15T18:16:08.060Z
modified: 2023-12-15T18:16:29.556Z
---

# pm-office-notion-examples

# guide

# popular

# extensions

# integrations
- https://github.com/infinitaslearning/notion-github-catalog /202312/js
  - https://infinitaslearning.notion.site/Notion-Github-Catalogue-ac2395eda37144e698e6b8faef1003c7
  - A github action that synchronises a Github repo data, including Backstage definition file information, with a Notion database
  - TL; DR ... you love the idea of https://backstage.io/ but think its way too complex to manage and operate, so just use Notion
  - This action will scan all of the Github repositories available to the provided token and update their information in the specified Notion database.
  - By default integrations cant access any content so you you must share your database (or the parent page / tree it is contained within) with the integration you created earlier to be able to access it.
  - This action expects each of your repositories to have a descriptor file format in the root of the repo in the form of a Backstage `catalog-info` file. This is because we are testing this approach against using Backstage directly, and wanted to leverage a format that perhaps has a chance of becoming a defacto standard.
# more
