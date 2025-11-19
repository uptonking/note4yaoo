---
title: lib-viz-mermaid-dev
tags: [charting, flowchart, mermaid]
created: 2025-11-19T17:49:45.753Z
modified: 2025-11-19T17:50:09.072Z
---

# lib-viz-mermaid-dev

# guide
- pros
  - 图表类型丰富, 除流程图外，还支持 kanban, gantt, Timeline, Mindmap, pie, xy(line/bar), Quadrant, git-branching, radar, Treemap, ...
- cons
  - ?
- features
  - ?
- who is using #mermaid
  - github README
  - integrations: 
- resources
- mermaid-models
  - https://huggingface.co/mermaidchart/models
  - https://huggingface.co/mermaidchart/merged-mermaid-7b  /202509
# draft
- streamable chart spec: 类似mermaid支持逐步添加关系, 可逐步添加折线/条形/扇形
# dev-xp

# ai-mermaid
- prompts
  - [The ChatGPT prompt list for Software Engineers: Prompts to generate software diagrams in Mermaid _202405](https://medium.com/@martin-jurran/chatgpt-prompt-list-for-software-engineers-prompts-to-generate-software-diagrams-in-mermaid-deaf2f373104)
  - https://github.com/fladdict/llmermaid
    - LLMermaid is a framework that enhances the capabilities of Large Language Models (LLMs) by integrating markdown-style diagram charts.

```
Write the Mermaid code for a sequence diagram describing a process. Flowchart diagrams in Mermaid start with "sequenceDiagram". Stricly follow this format:

sequenceDiagram
  Alice --> John: Hello John, how are you?
  John  --> Alice: Great!
  Alice --> John: See you later!

Only use the provided information. 

- write mermaid code for this workflow:  user login with email
```

# more
