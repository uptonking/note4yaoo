---
title: toc-viz-data-analysis
tags: [data-analysis, toc, viz]
created: 2021-05-23T18:45:22.333Z
modified: 2021-05-23T18:45:59.139Z
---

# toc-viz-data-analysis

# popular

- LineUp.js /42Star/BSD/202105/ts
  - https://github.com/lineupjs/lineupjs
  - https://lineup.js.org/
  - https://lineup.js.org/app
  - 依赖d3、lodash、reflect-metadata、lineupengine
  - LineUp is an interactive technique designed to create, visualize and explore rankings of items based on a set of heterogeneous attributes.
  - https://github.com/sgratzl/lineup-lite
    - LineUp-lite is an extension of the excellent react-table library for rendering beautiful interactive table visualizations based on the LineUp ranking visualization technique.

- UpSet.js /33Star/AGPLv3/202102/ts
  - https://github.com/upsetjs/upsetjs
  - https://upset.js.org/
  - UpSet.js is a JavaScript re-implementation of UpSetR to create interactive set visualizations for more than three sets. 
  - The core library is written in React but provides also bundle editions for plain JavaScript use. 
  - The UpSetJS React component is implemented as a pure functional component solely depending on the given properties.
  - [UpSet: Visualizing Intersecting Sets](https://jku-vds-lab.at/tools/upset/)
  - [upset live demo](http://vcg.github.io/upset/)
# viz-ai
- https://github.com/vanna-ai/vanna /21.7kStar/MIT/202511/python/ts
  - https://vanna.ai/
  - Chat with your SQL database
  - Streaming Responses — Real-time tables, charts, and progress updates
  - Enterprise Security — Row-level security, audit logs, rate limiting
  - Charts (Plotly visualizations)
  - Any LLM: OpenAI, Anthropic, Ollama, Azure, Google Gemini, AWS Bedrock, Mistral, Others 
  - Any Database: PostgreSQL, MySQL, Snowflake, BigQuery, Redshift, SQLite, Oracle, SQL Server, DuckDB, ClickHouse, Others 
  - Your Auth System: Bring your own — cookies, JWTs, OAuth tokens 
  - Your Framework: FastAPI, Flask

- https://github.com/Sinaptik-AI/pandas-ai /22.6kStar/MIT+EE/202510/python
  - https://pandas-ai.com/
  - PandasAI is a Python library that makes it easy to ask questions to your data in natural language.
  - PandasAI makes data analysis conversational using LLMs and RAG.

- https://github.com/StructuredLabs/preswald /4.3kStar/apache2/202507/python
  - https://www.preswald.com/
  - Preswald is a static-site generator for building interactive data apps in Python. 
  - It packages compute, data access, and UI into self-contained data apps that run locally in the browser. 
  - Built on a WASM runtime with Pyodide and DuckDB, Preswald enables portable, file-based apps that are fast, reactive, and shareable.
  - Code-based. Write apps in Python, not in notebooks or JS frameworks
  - File-first. One command creates a fully-packaged `.html` app
  - Built for computation. Use Pyodide + DuckDB directly in-browser
  - Reactive engine. Only re-run what's needed, powered by a DAG of dependencies
  - Local execution. No server. Runs offline, even with large data

- https://github.com/CodePhiliaX/Chat2DB /24.7kStar/apache2/202504/java/ts/inactive
  - https://chat2db.ai/
  - AI-powered app builder that creates professional applications in minutes, no coding required

- https://github.com/ruc-datalab/DeepAnalyze /2.2kStar/MIT/202511/python
  - https://ruc-deepanalyze.github.io/
  - 你的AI数据分析师，自动分析大量数据，一键生成专业分析报告
  - DeepAnalyze is the first agentic LLM for autonomous data science. It can autonomously complete a wide range of data-centric tasks without human intervention
  - Entire data science pipeline: Automatically perform any data science tasks such as data preparation, analysis, modeling, visualization, and report generation.
  - uv run python backend.py
    - npm run dev -- -p 4000
  - 🤔 数据分析基于文件系统实现，ai生成使用pandas操作数据的python代码并自动执行
    - 实测进行脏数据处理的工作很难自动化
    - 对模型的coding能力要求高
  - 🐛 
    - 在画完图表后的 `<Understand>` 部分，fastapi会突然停止接受llm输出数据，然后整个程序进入卡死/假死状态, 但vllm那边会正常输出完chat结果
    - 有时假死状态持续10min后
  - 定制的 DeepAnalyze-8B 模型不适合聊天对话，会乱说且loop，但适合执行数据分析任务
  - Fully open-source: The model, code, training data, and demo of DeepAnalyze are all open-sourced, allowing you to deploy or extend your own data analysis assistant.
  - [添加 DeepAnalyze 详细部署教程文档_基于MacBook Air M4 · ruc-datalab/DeepAnalyze](https://github.com/ruc-datalab/DeepAnalyze/pull/16)
  - ❓ ai分析玩数据的结果如 `final_result.to_csv('category_price_performance.csv', index=False)` 在本地找不到保存的文件
    - 是否通过sandbox进行文件io
  - 替代方案
  - https://github.com/modelscope/ms-agent/blob/main/projects/fin_research/analyst.yaml
    - You are a professional Data & Financial Analysis Agent operating inside an isolated Docker sandbox
    - You solve analytic tasks through systematic tool usage and step-by-step reasoning.

- https://github.com/eosphoros-ai/DB-GPT /17.7kStar/MIT/202511/python/华人团队
  - http://docs.dbgpt.cn/
  - https://www.yuque.com/eosphoros/dbgpt-docs/bex30nsv60ru0fmx
  - 一个开源的AI原生数据应用开发框架
  - 通过开发多模型管理(SMMF)、Text2SQL效果优化、RAG框架以及优化、Multi-Agents框架协作、AWEL(智能体工作流编排)等多种技术能力，让围绕数据库构建大模型应用更简单，更方便
  - 私域问答&数据处理&RAG
  - 支持自然语言与Excel、数据库、数仓等多种数据源交互，并支持分析报告。
  - 围绕大语言模型、Text2SQL数据集、LoRA/QLoRA/Pturning等微调方法构建的自动化微调轻量框架, 让TextSQL微调像流水线一样方便。
  - 支持自定义插件执行任务，原生支持Auto-GPT插件模型，Agents协议采用Agent Protocol标准

- https://github.com/Canner/WrenAI /13kStar/AGPL/202511/python/ts
  - https://getwren.ai/oss
  - GenBI (Generative BI) queries any database in natural language, generates accurate SQL (Text-to-SQL), charts (Text-to-Chart), and AI-powered business intelligence in seconds
  - Semantic Layer: MDL models encode schema, metrics, joins
  - support Ollama

## viz-charting

- https://github.com/geodaai/openassistant /MIT/202510/ts
  - https://geodaai.github.io/openassistant/
  - https://www.npmjs.com/package/@openassistant/plots
  - OpenAssistant focuses on providing a rich set of AI tools for spatial data analysis and GIS tasks. 
  - v1.0.0 is framework-agnostic and can be integrated with any AI framework of your choice
  - Spatial Analysis Tools: Comprehensive suite of GeoDA tools for spatial statistics, LISA, Moran's I, spatial regression, and more
  - DuckDB Integration: Powerful in-browser SQL queries with DuckDB WASM 
  - Ready-to-use components for ECharts, Vega-Lite, Kepler.gl, and Leaflet visualizations.
  - AI Framework Agnostic: Works with Vercel AI SDK, LangChain, Anthropic, and other popular AI frameworks.

- https://github.com/whoiskatrin/chart-gpt /3.6kStar/apache2/202308/ts/inactive
  - text to beautiful charts within seconds
# data
- https://github.com/antvis/data-set
  - state driven all in one data process for data visualization
# data-tools
- https://github.com/tellery/tellery
  - Tellery lets you build metrics using SQL and bring them to your team. 
  - Metrics are defined consistently and constantly updated, no longer scattered across tools, and recreated with no oversight.
# viz-examples
- https://github.com/houshanren/hangzhou_house_knowledge
  - 2017年买房经历总结出来的买房购房知识分享给大家
- https://github.com/ayuer/shanghai_house_knowledge
  - 2020年11月在上海买房经历总结出来的，启发来自这位同学2017年做的杭州购房分享
