---
title: lib-saas-activepieces-docs
tags: [activepieces, docs]
created: 2025-03-31T17:39:05.894Z
modified: 2025-03-31T17:39:21.066Z
---

# lib-saas-activepieces-docs

# guide

# overview

# docs

## Flow

- Flow consists of two parts, trigger and actions
  - Any Activepieces flow is a vertical diagram that starts with a trigger step followed by any number of action steps.

- Trigger
  - various types of triggers available, such as Schedule Trigger, Webhook Trigger, or Event Trigger based on specific service.
- Action
  - Actions come after the flow and control what occurs when the flow is activated, like running code or communicating with other services.

- Action Steps are connected vertically. Data flows from parent steps to the children. 
  - Children steps have access to the output data of the parent steps.
  - Step 3 can access data produced by Steps 1 and 2 as they’re its parent steps. This step can produce data but since it’s the last step in the flow, it can’t be used by other ones.

​

- Dropdowns and some other input types don’t let you select data from previous steps. If you’d like to bypass this and use data from previous steps instead, switch the input into a dynamic one using this `(x)` button

- If you can’t find the data you’re looking for in the Data to Insert panel but you’d like to use it, you can write a JSON path instead. `{{step_slug.path.to.property}}`

- draft/publish: The changes you make won’t work right away to avoid disrupting the flow that’s already published. 
  - You can edit a flow as many times as you want in draft mode.
  - The published flow will be immutable and cannot be edited.
  - If you try to edit a published flow, Activepieces will create a new draft if there is none and copy the published version to the new version.

- 
- 
- 
- 
- 

# more
