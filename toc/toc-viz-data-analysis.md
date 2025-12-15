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
- https://github.com/jupyterlab/jupyter-ai /4kStar/BSD/202511/python
  - provides a user-friendly and powerful way to explore generative AI models in notebooks and improve your productivity in JupyterLab
  - A native chat UI in JupyterLab that enables you to work with generative AI as a conversational assistant.
  - Local model support through GPT4All and Ollama, enabling use of generative AI models on consumer grade machines with ease and privacy.
- https://github.com/somethingreallycool123/CodeMate /MIT/202501/python/inactive
  - a Jupyter notebook extension that leverages powerful AI models for code assistance, debugging, and generation.
  - integrate with OpenAI, Anthropic Claude, Google Gemini, and Hugging Face.
  - Local Model Support: Run models locally using Hugging Face’s Transformers library.

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
  - [sqlcoder LLM support?  _202403](https://github.com/vanna-ai/vanna/issues/303)
    - I've used the 7b of sqlcoder via Ollama and found it to be extremely slow for some reason compared to models like mistral.

- https://github.com/Sinaptik-AI/pandas-ai /22.6kStar/MIT+EE/202510/python
  - https://pandas-ai.com/
  - PandasAI is a Python library that makes it easy to ask questions to your data in natural language.
  - PandasAI makes data analysis conversational using LLMs and RAG.
- https://github.com/aadya940/numpyai /MIT/202504/python/inactive
  - https://numpyai.readthedocs.io/en/latest/
  - natural language data analysis toolkit using NumPy and LLMs.
  - A Natural Language Interface for NumPy powered by LLMs. Empowering mindful data analysis using Generative AI.
  - Writes NumPy code for you based on your natural language queries.
  - Supports frameworks like sklearn and matplotlib for basic tasks.
  - Interactive debugging and re-tries.

- https://github.com/datalayer/jupyter-ai-agents /126Star/BSD/202511/python/ts
  - https://jupyter-ai-agents.datalayer.tech/
  - AI Agents for JupyterLab with MCP tools - Chat interface for intelligent notebook interaction, code execution, and workspace management.
  - The chat interface is built using Pydantic AI for robust AI agent orchestration and Vercel AI Elements for the user interface components.
  - By default, the Jupyter MCP Server is started as a Jupyter server extension, providing access to all Jupyter MCP server tools directly through the chat interface. This enables the AI agent to interact with notebooks, execute code, manage files, and perform various Jupyter operations seamlessly.
  - datalayer core似乎未开源
  - https://github.com/datalayer/jupyter-ui /MIT/202512/ts
    - https://jupyter-ui.datalayer.tech/
    - Jupyter UI is a set of React.js components that allow a frontend/webapp developer to build data products compatible with the Jupyter ecosystem.
    - The user interface delivers executable notebooks, cells, terminals, file browsers and allows the developer to manage a full integrated React tree instead of relying on iframes to display the Jupyter notebooks.

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
  - 🐛 
    - 在画完图表后的 `<Understand>` 部分，fastapi会突然停止接受llm输出数据，然后整个程序进入卡死/假死状态, 但vllm那边会正常输出完chat结果
    - 有时假死状态持续10min后
  - 定制的 DeepAnalyze-8B 模型不适合聊天对话，会乱说且loop，但适合执行数据分析任务
  - 未使用ai框架如langchain/graph, 基于简单的 python `while` loop 实现
  - Fully open-source: The model, code, training data, and demo of DeepAnalyze are all open-sourced, allowing you to deploy or extend your own data analysis assistant.
  - [feat: DeepAnalyze范式支持通用大模型开箱即用，新增主动提问与代码执行增强 _202512](https://github.com/ruc-datalab/DeepAnalyze/pull/65)
    - 🐛 实测在线ai有时会跳过`<Execute>`的执行代码而直接根据原数据捏造计算结果来凭空分析, 这一步如何增强正确性 
  - cd demo/chat && uv run python backend.py
    - npm run dev -- -p 4000
  - 🤔 数据分析基于文件系统实现，ai生成使用pandas操作数据的python代码并自动执行
    - 实测进行脏数据处理的工作很难自动化
    - 对模型的coding能力要求高
  - [添加 DeepAnalyze 详细部署教程文档_基于MacBook Air M4 · ruc-datalab/DeepAnalyze](https://github.com/ruc-datalab/DeepAnalyze/pull/16)
  - ❓ ai分析玩数据的结果如 `final_result.to_csv('category_price_performance.csv', index=False)` 在本地找不到保存的文件
    - 实测是lmstudio中模型的tool call都失败了, 所以实际并未执行代码
    - 是否通过sandbox进行文件io
  - 替代方案
  - https://github.com/modelscope/ms-agent/blob/main/projects/fin_research/analyst.yaml
    - You are a professional Data & Financial Analysis Agent operating inside an isolated Docker sandbox
    - You solve analytic tasks through systematic tool usage and step-by-step reasoning.

- https://github.com/DatarusAI/Datarus-JupyterAgent /226Star/MIT/202508/python/终端交互/inactive
  - A sophisticated multi-step reasoning pipeline powered by the Datarus-R1-14B-Preview model, designed for complex data science and analysis tasks. 
  - a powerful multi-step reasoning system that executes complex analytical workflows with step-by-step reasoning, automatic error recovery, and comprehensive result synthesis. 
  - 🐛 终端ux, 生成的不是通用code而是jupyter相关代码，还与定制模型绑定
  - This pipeline provides a robust framework for running iterative analysis tasks in isolated Docker environments with full Jupyter notebook integration.
  - We built this pipeline specifically for Datarus-R1-14B-Preview, our 14B-parameter language model that achieves up to 30% higher accuracy on AIME 2024/2025 and LiveCodeBench while emitting 18–49% fewer tokens compared to similar size models.
  - Multi-Step Reasoning: Executes complex workflows with step-by-step reasoning using Datarus model
  - Docker Integration: Isolated execution environment using Jupyter containers
  - Kernel Management: Direct kernel communication using jupyter_client for reliable execution
  - Built-in support for TensorFlow, PyTorch, and scikit-learn
  - Rich Console Output: Beautiful terminal output with syntax highlighting
  - Dynamic Port Allocation: Automatically finds available ports for Jupyter server
  - Automatic creation and management of Jupyter notebooks
  - Notebook Export: Save final notebooks for review and sharing
  - [DatarusAI/Datarus-R1-14B-preview · Hugging Face](https://huggingface.co/DatarusAI/Datarus-R1-14B-preview)
    - Datarus-R1-14B-Preview is fine-tuned from Qwen 2.5-14B-Instruct to act as a virtual data analyst, trained on full analytical trajectories including reasoning steps, code execution, error traces, and self-corrections.

- https://github.com/microsoft/TaskWeaver /6kStar/MIT/202512/python/inactive
  - https://microsoft.github.io/TaskWeaver/
  - The first "code-first" agent framework for seamlessly planning and executing data analytics tasks.
  - Unlike many agent frameworks that only track the chat history with LLMs in text, TaskWeaver preserves both the chat history and the code execution history, including the in-memory data. This feature enhances the expressiveness of the agent framework, making it ideal for processing complex data structures like high-dimensional tabular data.

- https://github.com/EduardTalianu/erag /202506/python/inactive
  - an AI interaction tool with RAG hybrid search, conversation context, web content processing and structured data analysis with LLM / GPT
  - Talk privately with your documents using Ollama or talk fast using Groq and others
  - Do AI powered Exploratory Data Analysis (EDA) with AI generated Business Intelligence and insights on excels and csv

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

- https://github.com/dataease/SQLBot /4.8kStar/GPL+LOGO/202512/python/ts
  - https://sqlbot.org/
  - 基于大模型和 RAG 的智能问数系统，对话式数据分析神器
  - 开箱即用：仅需简单配置大模型与数据源，无需复杂开发，即可快速开启智能问数
  - 依托大模型自然语言理解与 SQL 生成能力，结合 RAG 技术，实现高质量 Text-to-SQL 转换
  - 易于集成：支持多种集成方式，提供 Web 嵌入、弹窗嵌入、MCP 调用等能力；能够快速嵌入到 n8n、Dify、MaxKB、DataEase 等应用

- https://github.com/loglux/SQLAIAgent-Ollama /202506/python/inactive
  - A powerful SQL AI agent built with Phi Data that helps you interact with your databases through natural language conversations.
  - https://github.com/CodewGPS/SQLAIAgent /单文件

- https://github.com/gd03champ/llm4sql /MIT/202404/js/inactive
  - a project aimed at integrating LLMs with SQL databases
  - [I've built a project that integrates LLM with DBMS ( Finally ). : r/opensource _202404](https://www.reddit.com/r/opensource/comments/1btvjrj/ive_built_a_project_that_integrates_llm_with_dbms/)

- https://github.com/FalkorDB/QueryWeaver /AGPL/202511/python/ts
  - an open-source Text2SQL tool that converts plain-English questions into SQL using graph-powered schema understanding

- https://github.com/advenimus/databoard /NonOpen
  - [Built a free local-first data visualization app for SQL/CSV/Excel - zero cloud, zero telemetry : r/BusinessIntelligence _202511](https://www.reddit.com/r/BusinessIntelligence/comments/1p0n6s6/built_a_free_localfirst_data_visualization_app/)
  - Completely offline - works on airplanes, no internet required
  - Power BI Desktop is free (and works offline), license is only needed when you publish in Service
  - PowerBI is cheap and is all in one solution. Go for features that PowerBI and Tableau have and dont have

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
