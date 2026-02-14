---
title: lib-ai-app-community-model-format
tags: [format, large-language-model, protocol]
created: 2025-10-10T02:44:12.470Z
modified: 2025-10-10T02:44:49.634Z
---

# lib-ai-app-community-model-format

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-ai-chart/flow/viz/sql 📊
- ## 

- ## 

- ## [text2sql的工程项目大家有没有最优解 _202602](https://linux.do/t/topic/1614141)
  - 要求 text2sql 足够准，涉及多表联查，多轮对话纠正，可以生成 echarts 图表展示；
- 💡 一种思路是参考bi项目的ai功能设计

- 目前没有什么通用的方案， 主要原因是因为业务的 sql 表千奇百怪、各种各样、甚至有一些业务自己都不知道什么语义， 还是需要根据库表的实际场景来分析

- 所以要做数据治理， 要做大量的工程化

- ## Parsing line charts is a hard task for VLMs
- https://x.com/jerryjliu0/status/2020228625191330028
  - VLMs are generally fine at coarse visual understanding, but they have a hard time reasoning about precise coordinates. Ask most VLMs, even though tuned to chart understanding, to parse a line chart to a table and they will struggle.
  - We tested over a few samples. Docling’s new granite-vision model, gemini 3 flash, gpt 5.2 pro, and a v0.1 of our own chart parsing (which is in beta and rapidly evolving).
  - Out of these, most models fail, and sometimes miss the entire chart correctly. gpt 5.2 pro is closest but spends an absurd number of tokens reasoning through each point. Our own parsing is actually quite good, though of course, there’s still some things we need to do to get to 100% accuracy.

- ## [Anybody tried Codellama-70B, SQLCoder-70B; SQLCoder-7B? And Alphacodium framework? And perplexing HumanEval scores : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1ajwhc8/anybody_tried_codellama70b_sqlcoder70b_sqlcoder7b/)
- SQLCoder is not instruction fine-tuned yet! You will probably get better results with [this prompt](https://raw.githubusercontent.com/defog-ai/sqlcoder/c167d340ad16b925f87eef5530474c5a9405abce/prompt.md) for the 70b, and with your metadata in this format

- ## [Best way to build a private Text-to-SQL app? : r/LangChain _202509](https://www.reddit.com/r/LangChain/comments/1n7ra5q/best_way_to_build_a_private_texttosql_app/)
- My advice, do some data engineering on the tables and columns. Be ambitious, but careful. Don't try to have a solution that will answer every possible tricky questions.
  - first advice : Start slowly, test, and add tables progressively.
  - In our case, when made specific views in which we pick what selected fields we want to publish to the app.
  - When you have something working, add some more views.
  - Views give you a lot of flexibilities.

- Based on experience the only way for you to make this work is to basically study Prompt Engineering. Providing a very vague prompt would not be sufficient to provide you the correct answer. I bet for sure that the users would think that the thing your building is like ChatGPT that would provide info and data on its own.

- If the SQL part is part of your equation, I am doing the natural language to SQL right now and I have learned a few things—
  - first, that SqlCoder as an LLM is not giving me better results than DeepSeek (both self hosted on a consumer PC with a 5080 and 16G VRAM). 
  - Second that descriptions of tables etc. (our schema was well documented with comments on what tables and columns mean) are all but worthless! 
  - And finally that natural language requests connected to the SQL that satisfy them are gold!
- I'm working with natural language to SQL. Yes, sqlcoder did not work for me either, so I had to shift to llama3:instruct which is far better.

- ## [We benchmarked 19 popular LLMs on SQL generation with a 200M row dataset : r/dataengineering _202505](https://www.reddit.com/r/dataengineering/comments/1khsiwd/we_benchmarked_19_popular_llms_on_sql_generation/)
  - we tested how well different LLMs generate SQL queries against a large GitHub events dataset.
  - We found some interesting patterns - Claude 3.7 dominated for accuracy but wasn't the fastest, GPT models were solid all-rounders, and almost all models read substantially more data than a human-written query would.
  - https://github.com/tinybirdco/llm-benchmark /202512

- Generating SQL against a curated dataset is not super useful.
  - I think what most people (or at least the business) want out of llms is the ability to interpret a complex data model (that might not even fit in a context window) and generate complex queries that require joins across multiple tables.

- This echoes my experience experimenting with text-to-sql using OpenAI a couple of months back: they are next to useless for all but the simplest queries against the simplest relational models. You seem to have made it easy for them by only providing a single table for querying. Imagine how bad they are in scenarios where they have to produce queries for more complex models.

- dang and this is only one flat table — 99% of SQL users are trying to query relational dataset directly

- ## [I have tested all the popular coding assistant for data science, here's what I found : r/datascience _202503](https://www.reddit.com/r/datascience/comments/1jo2gxt/i_have_tested_all_the_popular_coding_assistant/)
  - I setup a test to find the best AI coding assistant to help with Data Science task.
  - The result is a bit surprising for me: None of the popular AI agent works for data science. Although the demo looks gorgeous, Google Gemini in Colab fail pretty bad. But there are some tools that has potential and some are already a bit useful.
  - [The Best AI Coding Agent for Data Science and Machine Learning _202503](https://medium.com/@DangTLam/the-best-ai-agent-for-data-science-and-machine-learning-march-2025-20a3cfee836d)

- Gemini has repeatedly in my experience been the worse of all the AI agents.
  - Used to be the same but 2.5 pro kinda changed my mind
- Came here to say this. I shit on flash alllllll the time, it was unusable. But pro 2.5 is now my go to. Certainly easier to use than o3 mini.

- TLDR; There’s no perfect AI assistant for data science and ML — yet.

- A big problem with any of these tools is the data is not cleaned or curated for use by LLMs. An MCP only provides access to db functions; but each dataset has it's own relationships, semantics, and domain knowledge baked in.
  - What would be amazing is a tool that used LLMs to scan the data and developed a metadata layer for it. I think that would make the outputs so much better.
  - I think something like getanswerlayer.com is trying this, and I've seen others too. So much happening here, I think we'll see a lot of progress this year

- Why are you so tied to Jupyter notebooks? Why is that a requirement for DS workflows?
  - Seriously, I’m not happy with jupyter, but I haven’t found anything even close.

- DS require more thought process which present LLM are not capable of

- ## DeepAnalyze-8B, the first agentic LLM designed for autonomous data science, capable of automatically completing the end to end pipeline _202510
- https://x.com/Dr_Singularity/status/1981010771338498241
- If tools like this can generate full research reports on their own, the next big question is: who’s building the framework for agents to take real-world actions from those insights? I keep seeing mentions of @GetActionModel and #LAM wondering if that’s where the space is headed?
  - What @getactionmodel is doing with LAMs runs in parallel, building agents that don’t just analyze but act, reason, and coordinate on-chain. When AI can think and do, acceleration becomes inevitable.

- ## [MermaidMistral: A Work In Progress Model for Flow Maps : r/Oobabooga _202401](https://www.reddit.com/r/Oobabooga/comments/192qb2c/mermaidmistral_a_work_in_progress_model_for_flow/)
  - I'm an unemployed recent college graduate aspiring to specialize in fine-tuning AI models and build useful software around AI.
  - During my brief stint at Bito AI after graduating college, I developed an AI Documentation Agent that creates code documentation and flow maps for an entire codebase using Code2Flow which I further developed to use Mermaid js to support more programming languages. Customer Feedback revealed that GPT-4 struggles to reliably produce mermaid.js syntax with function calls that have parameters especially when the parameters are strings, hindering reliable flow chart generation for code documentation. I implemented retry logic to address inaccuracies, before proposing the idea of training a model for this scenario.
  - In the past few weeks, I dedicated my time to handcrafting MermaidMistral on HuggingFace as a Proof of Concept, demonstrating that small models can specialize in tasks overlapping with the original base model's latent abilities from only a small, diverse set of manually created Python-to-mermaid flow map examples using Mermaid Flow Map Web Editor Online
  - MermaidMistral_v2 which is a merge of all of my MermaidMistral Variants into one model which seems to be even better at creating knowledge graphs from input.

- 
- 
- 
- 
- 
- 
- 
- 

- ## 👾 i want to extend markdown syntax to support rendering charts like pie/line/bar/...
  - are there any existing extensions for markdown charts? 
  - especially for llm output with markdown charts, are there any experiments and solutions?

- tips
  - vega-lite json to markdown

- For integration, plugins like `markdown-chart` for `VuePress` allow you to enable multiple chart libraries (including Chart.js, ECharts, and Mermaid) simultaneously within your documentation site
- There are plugins (like markdown-it-chart or vuepress-plugin-chart) that allow you to write JSON configurations for these libraries directly in Markdown.

- When generating charts with LLMs, the challenge is not just the syntax, but how to render it reliably in a chat interface (streaming) and handle errors.
- A. The "Code Block" Pattern (Standard Solution)
  - Most production LLM apps (ChatGPT, Claude, open-source UIs) use this pattern
  - Prompting: Instruct the LLM to "Output the chart using Mermaid.js syntax inside a markdown code block."
  - Parsing: On the frontend, use a Markdown parser (like react-markdown or markdown-it).
  - Component Mapping: Write a custom component for the code block renderer.
  - Extension: Use `rehype-mermaid` or write a custom components prop for the code block.

- [Google Gemini](https://gemini.google.com/app/51914f331eb6f22c)
- chart visualization support is achieved not through an intrinsic, universally recognized Markdown syntax, but rather through the use of fenced code block extensions. 
  - These specialized blocks serve as containers for Domain-Specific Languages (DSLs)—such as Mermaid—or declarative JSON specifications—such as Vega-Lite or Chart.js—that are interpreted by dedicated client-side JavaScript rendering engines. 
- The universal, pragmatic mechanism adopted for integrating complex, structured visualization data into Markdown involves leveraging the fenced code block
  - This shifts the role of the Markdown processor from a passive translator of text to an Active Content Loader that initiates client-side JavaScript execution. 
  - This architectural shift significantly increases implementation complexity, introduces client-side dependencies, and creates portability risks, as rendering success is entirely dependent on the specific processor supporting the required extension (e.g., mermaid, chart, or vega-lite).

- Mermaid's DSL allows users to define complex structures, such as flow charts, sequence diagrams, and pie charts, through highly structured, yet expressive, plain text. The syntax is designed for readability and requires minimal overhead compared to writing a full JSON specification
  - However, the analysis shows that Mermaid's core strength lies in generating diagrams that illustrate relationships and flows. Line and bar charts, common in statistical reporting, are often approximated using the flow chart (graph) or Gantt chart syntax for timeline visualizations. 
  - This is a crucial distinction: Mermaid is optimized for Process Documentation (sequence, flow, mind maps) rather than complex statistical plotting.
  - While simple, the Mermaid DSL is syntactically strict. Configuration details, such as themes, layout algorithms (dagre, elk), and specific rendering options, can be managed using a frontmatter configuration block within the fenced code.

- Vega-Lite is recommended for advanced users tackling complex calculations, custom time filters, nested aggregations, and unsupported visualization types like scatter or Sankey charts.
  - Vega-Lite specifications are declarative JSON objects, often simplified using HJSON (which allows optional quotes, comments, and missing commas). The specification dictates the visualization by mapping data fields to visual encoding channels (e.g., x, y, color)
  - Vega-Lite supports a rich variety of statistical visualizations, including complex line charts with markers, varying size/dash attributes, and slope graphs. 
  - Due to its statistical sophistication, Vega-Lite is deeply integrated within the data science ecosystem through language bindings like Altair (Python), ipyvega (Jupyter), and Julia bindings.

- Chart.js's integration into Markdown typically involves a custom extension that wraps the Chart.js configuration JSON—a structure detailing type, data, and extensive options—within a language-specific fenced code block 

- [Le Chat](https://chat.mistral.ai/chat/25d895f6-22de-40cc-9569-73d1054dcfb4)
  - R Markdown is a variant of Markdown that integrates R programming code chunks to generate statistical plots and charts using R libraries such as plotly and rCharts. 

- Ditaa: ASCII art-based diagrams converted to images, supported in some Markdown editors.

- PlantUML uses its own domain-specific language and typically requires a command-line tool or integrations within build tools (like Maven) or IDEs (like IntelliJ) to generate static image files such as SVG or PNG 
  - This differs from Mermaid's client-side, dynamic rendering approach.

- A primary technique for guiding LLMs to produce chart-ready Markdown involves the use of carefully constructed system prompts or specific instructions within the user's query.
  - This approach leverages the LLM's ability to follow instructions and mimic patterns it has learned during its training, provided those patterns (in this case, Mermaid syntax) were sufficiently represented in its training data or can be effectively described in the prompt.

- ## [Graphing visualization options : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1kziili/graphing_visualization_options/)
  - My hope is to use a prompt like "Show me how many creative ways the data file can be visualized as a scatter plot" or "Creatively plot the data in row six only as an amortization using several graph types and layouts"...
- Describe the data (list of columns and descriptions if name is not obvious). Write a prompt to provide step be step guide to build charts and tables in graphana / kibana / excel. Should work in most of the cases. You can also ask it to generate code for a Jupyter notebook

- ## [Markdown-ui v0.2: Let AI output charts using React/Svelte/Vue in realtime : r/ChatGPTCoding _202509](https://www.reddit.com/r/ChatGPTCoding/comments/1n6jng1/markdownui_v02_let_ai_output_charts_using/)
  - For v0.2 I’ve included support of chart widgets using the beautiful chart.js, allowing users to plot line, bar, pie and scatter charts by specifying data in the familiar csv format.
  - Under the hood markdown-ui uses web components. Some people have expressed the wish for a vanilla JS implementation, this is still being considered

- ## [Diffusion model for generating infographics : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lkuzya/diffusion_model_for_generating_infographics/)
- HiDream somewhat can generate infographics. But the text for description 80% accurate

- as far as I'm aware there's not any open source models currently trained for this kind of a thing. Its completely a feasible thing to do thought, but you'll have to use flux models for it as sd1.5 and sdxl dont handle text or graphs really. ChatGPT's image generation currently works really well for this use case though.

- ## [Charts generation : r/OpenWebUI _202502](https://www.reddit.com/r/OpenWebUI/comments/1iicoec/charts_generation/)
- Ask it to generate mermaid diagrams and it will render them automatically. Mermaid.js supports all kinds of graphs, charts and mind maps. I use it for this purpose constantly, it’s awesome for architectural diagrams

- which LLM are you using?
  - Any works
  - O1-mini, qwen2.5 and deepseek all returned basically the same

- A couple pointers:
  - You do need to be somewhat explicit in your prompt with "generate a mermaid.js diagram..."
  - Also, in my experience, smaller models have difficulty doing this often and just wind up producing something that looks like it should have been to create a mermaid diagram but never did.

- Mermaid.js. Md files and thing like obsidian are used. Like the git pages graphs and flowcharts.

- ## [Vision models that can read charts correctly? : r/LocalLLaMA _202403](https://www.reddit.com/r/LocalLLaMA/comments/1bm7wsz/vision_models_that_can_read_charts_correctly/)
- Better to convert the charts into textual data for LLMs than use a LMM.
  - This is what I've been doing. Whenever my data analysis bot spits out a chart, it also pulls the data (or a sample in the case of a busy scatter plot) in tabular form. I eventually want to be able to understand papers and notebooks, which communicate alot with data viz.
  - 可参考comfyui在图片中嵌入数据的方式

- 🤔 LLMs aren't particularly good at size or proportion. They're good at classification. "This is a dog" is a lot easier than "This rectangle is 10 units long"

- ## [Discussion: Best Way to Plot Charts Using LLM? : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1foph33/discussion_best_way_to_plot_charts_using_llm/)
  - how are you plotting charts or graphs? 
  - Currently, I am using structured output from the LLM with the data and sending it to the frontend to plot with Plotly React. In my current approach, I get the data from an API and then pass it to the LLM, which formats the data and the structure for the chart. However, this is currently slow.
  - I've seen chat2plot use a dataframe with the data, querying it from the LLM and then structuring the output, but it only uses the dataframe to plot the chart. The LLM never directly accesses that data, just pass the structure with the filters
  - What approach do you recommend for handling chart generation in this kind of setup?

- Apparently Phi 3.5 Vision is good at this. There is also ChartGemma.

- I had decent luck asking an LLM to write some code for matplotlib

- I asked the LLM to generate JavaScript code to display the chart using plotly. It worked OK however it took 20 to 30 seconds. When it has to generate a lot of tokens for the JavaScript on the json data, it takes a while. I have to think about how to optimize the main reason for going to the LLM is that I can ask the type of the chart the color, the style everything in natural language. I just got it working now. I had to figure out a way to optimize.
- Do you pass your data to the LLM? I think except for the framework and library we are doing the same
  - Yes. I pass the data to the LLM. I think that slows down. I should only pass the data schema and let the llm generate the JavaScript and the I have to embed the json after the llm process.
  - An alternate approach would be predefined chart format and llm pick the chart type and field/series based the user question. This will make it faster. But this will lack flexibility.

- What I did is, I asked the llm to output a chartjs codeblock. And in the frontend, since we are rendering it as a codeblock, when the language is chartjs. I use the chartjs renderer, boom. I get dynamic plots.

- ## [PlantUML vs Mermaid? : r/ExperiencedDevs _202504](https://www.reddit.com/r/ExperiencedDevs/comments/1k7ki6k/plantuml_vs_mermaid/)
- I like how mermaid diagrams are rendered on GitHub.com, always add them to my README.md files.
  - I thought, plantuml is doing the same. Atleast on gitlab both works
- only for gitlab. GitHub needs additional tooling last time I checked

- I use PlantUML+CoPilot to draw UML diagrams. For system diagrams I usually use draw.io

- PlantUML is better for the simple reason that you can render as ASCII art and nothing beats that.
  - Jokes aside, from a point of writing both work fine. PlantUML is more feature rich and more complex.
  - Mermaid is simpler. So it's also supported in more default setups like GitHub or Obsidian.

- I use PlantUML in markdown for most everything--it's extremely flexible with lots of different kinds of diagrams.
  - Though it's a bit more limited, Mermaid is more user-friendly, and more likely to be implemented as a plugin in whichever editor you're using.

- ## [MermaidMistral: A Work In Progress Model for Flow Maps : r/Oobabooga _202401](https://www.reddit.com/r/Oobabooga/comments/192qb2c/mermaidmistral_a_work_in_progress_model_for_flow/)
- MermaidMistral_v2 which is a merge of all of my MermaidMistral Variants into one model which seems to be even better at creating knowledge graphs from input.
  - Recently this model was made private as it's currently being fine-tuned in collaboration. These partners have provided proprietary code to enhance the model's ability to generate detailed flow diagrams for system design documentation. 
  - Due to the specialized nature of this data and our commitment to confidentiality and model integrity, MermaidMistral_v2 will remain private for the time being.

- ## [Any open-source models for generating diagrams? : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hhmgnl/any_opensource_models_for_generating_diagrams/)
  - I know existing LLMs can do this, but they frequently get the syntax wrong or hallucinate elements of the diagram. Wondering if there's an open-source model that’s especially good at this task.
- LLMs that are good at coding are also quite good at creating MedmaidJS and PlantUML diagrams.
  - I usually use the BigAGI frontend for this since it auto-renders both types of diagrams directly within the chat.
- Even smaller LLMs manage to output mermaid quite ok, syntactically that is. But they tend to hallucinate. So you might have to carefully craft your prompts in order for it to work properly. In general favor bigger models. Or use claude sonnet, which should be your most capable option overall.

- Look into using Qwen, but give it an example of the diagram in the prompt for consistency.

- You can use ToDiagram for diagramming any json data.
# discuss-ai-graphics-gen 🖼️
- ## 

- ## 

- ## 

- ## [nano banana生成的图片转可编辑矢量图的工具 ](https://linux.do/t/topic/1398790)
  - 我目前的方法是用第三方api生成4k的图片，然后导入到illustrator里面进行描摹处理。gemini官方默认最高生成的是2k，导入之后处理会很糊
- 只能生成svg然后导入sketch或者 illustrator 编辑，banana直出图片色彩文字，组成过于丰富，直接转svg，遵循效果很差，所以不如直出svg
  - 生成 svg 那用的就不是 banana 了，那是 gemini3

- 个人体验如下：工具使用的vetor Magic，生成的时间较长，最后的输出图片支持.ai的格式，方便之后在ai里面更改。基本能做到失真较少，算是比较好用的一个免费工具
  - [安利一个图片转svg的方案Vector Magic ](https://linux.do/t/topic/1157197)

- ## [Any good open-source model for SVG image generation? : r/svg _202505](https://www.reddit.com/r/svg/comments/1kx8jhy/any_good_opensource_model_for_svg_image_generation/)
- AFAIK no. I think anyone using generative AI to create vector art or vector illustrations is using something like Stable Diffusion to make vector illustration looking PNGs, then converting them to vector.

- I did some more research, found one that gives 20 free credits to generate SVG images, the images look pretty cool. https://svgmaker.io

- ## [I tested various models' ability to generate SVG unicorns. : r/singularity _202502](https://www.reddit.com/r/singularity/comments/1ixe5yu/i_tested_various_models_ability_to_generate_svg/)
  - 3.7 sonnet was initially a bit dissapointing here, but after giving it another attempt it's definetly the best one.

- we need to start with an SVG Benchmark test when new AIs come out 
  - They can perform the "most difficult human exams" but they can't do a simple 2D vectorized image.

- ## [Can Flux Models generate SVG images? : r/StableDiffusion _202409](https://www.reddit.com/r/StableDiffusion/comments/1fcsy8x/can_flux_models_generate_svg_images/)
- Text to image models produce images. They can produce vector-style graphics, which you can often run through a vectorizer for passable results.
- Illustrator has a text-to-vector feature, but I'm not sure what it's doing in the background. I assume it's doing a text-to-image-to-vector.

- It might sound counterintuitive, but your best bet might be fine-tuning an LLM (such as Llama 3.1) on a big dataset of text prompts with SVG outputs.

- SVG-like images yes, actual SVGs no. There are no AI vector solutions yet, even Adobe's AI vector thing is arguably also auto vector using Illustrator or whatever.

- Inkscape is open source and can convert images to SVG vectors.
# discuss-md-table/excel/csv 📈
- ## 

- ## 

- ## [[D] Why is table extraction still not solved by modern multimodal models? : r/MachineLearning _202503](https://www.reddit.com/r/MachineLearning/comments/1jnjfaq/d_why_is_table_extraction_still_not_solved_by/)
- These tasks (and other precise image-based tasks) are a pretty common problem:
  - Text has a lower information density per character compared to numerical data. In the encoding stage LLMs/VLMs do well with text or general images as semantic meaning is still retained even with somewhat incorrect representations given by the Text/Vision encoder. The same cannot be said for numerical values, where a single incorrectly interpreted digit can drastically change meaning.
  - VLMs can have issues with geometric problems. 
- When I did OCR, the important aspect was consistency. A traditional multi-stage OCR process was used as it was much easier to identify which part of the process would errors appear (and either flag/correct). End-to-end multi-modal models can have a 99% correct extraction, but determining why (and when) that 1% occurs is the hard part, when so many things could have gone wrong (resolution too low? table borders too thin? text too close to border? etc).
  - Which is why if you're going to do this, I suggest setting up a workflow and fine-tuning separate models for specific tasks.

- I think this will remain a niche for a few more years, because models have to be explicitly finetuned on certain documents. For example this startup finetuned on all common government invoices and most common b2b shops too. They will always outperform general LLMs because of their datasets

- If the table is really THAT clean you could extract the layout with traditional computer vision (opencv...). Then you'll need some OCR (deep learned or not) to read whats inside each box.

- ## [A R&D RAG project for a Car Dealership : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pgvkae/a_rd_rag_project_for_a_car_dealership/)
  - [This AI Brain Turns Messy Data to Dollars (Full Build + Code Provided) - YouTube _202512](https://www.youtube.com/watch?v=DJKVwo2mk-k)
  - https://neurafirst.com/ai_resources/content
  - https://drive.google.com/drive/folders/1Lk7Bxtc0hwFdpBYCsiwFBQXdWr9CBenv?usp=drive_link
  - Tldr: I built a RAG system from scratch for a car dealership. No embeddings were used and I compared multiple approaches in terms of recall, answer accuracy, speed, and cost per query. Best system used gpt-oss-120b for both retrieval and generation. I got 94% recall, an average response time of 2.8 s, and $0.001 / query. The winner retrieval method used the LLM to turn a question into python code that would run and filter out the csv from the dataset. I also provide the full code.
  - Since my background is AI R&D, and that I did not see any full guide about a RAG project that is treated as R&D, I decided to make it. The idea is to test multiple approaches, and to compare them using the same metrics to see which one clearly outperform the others.
  - The idea is to build a system that can answer questions like "Do you have 2020 toyota camrys under $15, 000 ?", with as much accuracy as possible, while optimizing speed, and cost/query.
- For the retrieval part, I compared 5 approaches:
  - Python Symbolic retrieval: turning the question into python code to be executed and to return the relevant documents.
  - GraphRAG: generating a cypher query to run against a neo4j database
  - Semantic search (or naive retrieval): converting each listing into an embedding and then computing a cosine similarity between the embedding of the question and each listing.
  - BM25: This one relies on word frequency for both the question and all the listings
  - Rerankers: I tried a model from Cohere and a local one. This method relies on neural networks.
  - I even considered in-memory retrieval but I ditched that method when I realized it would be too expensive to run anyway.
  - After getting a somewhat satisfying recall with the 1st method (around 78%), I started optimising the prompt. Main optimizations which increased the recall was giving more examples of question to python that should be generated. After optimizing the recall to values around 92%, I decided to go for the speed and cost. That's when I tried Groq and its LLMs. Llama models gave bad results. Only the gpt-oss models were good, with the 120b version as the clear winner.
- Concerning the generation part, I ended up using the most straightforward method, which is to use a prompt that includes the question, the documents retrieved, and obviously a set of instructions to answer the question asked.
- So what I did is that for the final answer, I used LLM-as-a-judge as a 1st layer, and then human-as-a-judge (e.g: me lol) as a 2nd layer, to produce a score from 0 to 1.
  - Then to measure the whole end-to-end RAG pipeline, I used a formula that takes into account the answer score, the recall, the cost per query, and the speed to objectively compare multiple RAG pipelines.
  - I know that so far, I didn't mention precision as a metric. But the python generated by the LLM was filtering the pandas dataframe so well that I didn't care too much about that. And as far as I remember, the precision was problematic for only 1 question where the retriever targeted a bit more documents than the expected ones.
  - As I told you in the beginning, the best models were the gpt-oss-120b using groq for both the retrieval and generation, with a recall of 94%, an average answer generation of 2.8 s, and a cost per query of $0.001.

- This feels less like a RAG system and more like an agentic text-to-query tool operating over tabular data. The LLM is effectively generating executable filters, which puts it closer to an AI agent than a retrieval pipeline. Also, giving the model direct authority to emit Python that you then run is unsafe in any real deployment unless it's constrained by a DSL, sandboxed, and validated. The results are interesting for a narrow use case, but framing this as R&D in RAG is a stretch, it’s more of a structured-data agent experiment than a RAG study.

- Try using bm42
  - I feel like all methods involving term frequency wouldn't work here because questions like "Do you have black sedans under 25, 000 miles ?" need filtering. And I don't see how term frequency could have a mechanism for that.

- ## [Pandalyst-13B-V1.0 released!!! Your first local LLM for mastering data analysis using pandas. : r/LocalLLaMA _202309](https://www.reddit.com/r/LocalLLaMA/comments/16v5aj4/pandalyst13bv10_released_your_first_local_llm_for/)
- 7B is uploading https://huggingface.co/pipizhao/Pandalyst-7B-V1.1 
  - This 7b version is trained based on Codellama-python-7B, and achieve competitive performance with our 13B !!! (witch was trained on wizardcoder-python-13B)

- how to make it read charts? E.g. Excel sheets.
  - In fact, we don't need the model to see the entire table of data.
  - In our implementation, we just feed the model the description of the table, as well as the type and enumeration value of each column, and we found that the model can handle the contents of the table well.

- can it return json reliably?
  - In the V1.x version, our model was trained to return the answer as a string reliably.
  - Responses in json format will be considered in the V2 version.

- ## [LLM recommendations for working with CSV data? : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1ktzdrd/llm_recommendations_for_working_with_csv_data/)
  - Is there an LLM that is fine-tuned to manipulate data in a CSV file? 
  - I've tried a few (deepseek-r1:70b, Llama 3.3, gemma2:27b) with the following task prompt: In the attached csv, the first row contains the column names. Find all rows with matching values in the "Record Locator" column and combine them into a single row by appending the data from the matched rows into new columns. Provide the output in csv format.
  - None of the models mentioned above can handle that task... Llama was the worst; it kept correcting itself and reprocessing... and that was with a simple test dataset of only 20 rows.
  - However, if I give an anonymized version of the file to ChatGPT with 4.1, it gets it right every time. But for security reasons, I cannot use ChatGPT.
  - So is there an LLM or workflow that would be better suited for a task like this?

- Can’t you ask an LLM to give you python code to do that?
  - Yes. Asking any LLM about CSVs is asking for trouble. If you care about accuracy and repeatability, always use code to answer such questions. Use an LLM to generate such code.

- For structured data it is often easy to generate code and then analyse it using that code. Or you can put it in a db and use text to sql for analysis.

- I’m not sure you need an LLM to do this. Feels like something a python script could achieve. Perhaps get an LLM to help write the script?

- ChatGPT is using a library like Pandas. What it does really is passinng your data to Pandas, and creating a query. Is not an easy task to do locally.

- ## [Which LLM is best at understanding information in spreadsheets? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l1lqdm/which_llm_is_best_at_understanding_information_in/)
- I think you need to make the LLM write code to process the spreadsheet. Something like:
  - Read top n rows, summarise as plain text, so the basic structure of the file is in context.
  - Have the LLM plan what operations it needs to perform.
  - Have it write and execute python code, reading the data into variables in memory and doing work on them.
  - Python code to write back out to a spreadsheet, or summarise totals in plain text, etc.
- llms have near zero comprehension of a bunch of numbers in rows. They can barely manage simple addition, if they're lucky, but ask them to write code and they're pretty close to solid (you still likely need somebody who's not code-illiterate to give it a once- over and make sure it hasn't done something silly)

- Have LLM build the formulas you need for Excel/Google sheet.

- There are MCPs out there that can spin up a small python environment to do data analysis. just provide a code executor tool to your model, tell it about the spreadsheet's schema and tell it to write and execute python code to do the analysis.

- Claude is GREAT at Excel, it's one of the rare instances when letting it create on its own at the outset means improved output later, because it built the formulas. Human created spreadsheets may contain eccentricities in the formulas and formatting that will roadblock later accurate data extraction.

- ## 🤔 [LLM has trouble understanding tabular data (.csv) relationships with RAG : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1hymyky/llm_has_trouble_understanding_tabular_data_csv/)
  - I'm currently having trouble getting a LLM to understand relationships in a table using RAG
  - One idea was to turn this into a text document and sentences such as "alice is 1 year old and her favorite color is blue." But since i have quite a bit of data (~10k rows), I was wondering if anyone else had something better. 

- One solution that can work for advanced cases is to use the LLM to generate a query (sql, pandas...) instead of the answer. This way you will be able to also extract more complex relations. 
  - Generating a query for this is easy, while putting everything into the context window for the llm to calculate it will not work.

- As mentioned by others you’re better off using a tool that enables the LLM to generate pandas or sql queries on the table. E.g you can have a look at the TableChatAgent in Langroid 
  - https://github.com/langroid/langroid/blob/main/examples/data-qa/table_chat.py /MIT/202510/python
    - lightweight, extensible and principled Python framework to easily build LLM-powered applications, from CMU and UW-Madison researchers

- ## 🧪 [Which Format is Best for Passing Tables of Data to LLMs? : r/LLMDevs _202510](https://www.reddit.com/r/LLMDevs/comments/1nw3jha/which_format_is_best_for_passing_tables_of_data/)
  - For anyone feeding tables of data into LLMs, I thought you might be interested in the results from this test I ran.
  - I tested how well an LLM (GPT-4.1-nano in this case) could answer simple questions about a set of data in JSON format. I then transformed that data into 10 other formats and ran the same tests.
  - I wanted to understand whether how you format a table of data affects how well an LLM understands it.
- [Which Table Format Do LLMs Understand Best? (Results for 11 Formats _202509)](https://www.improvingagents.com/blog/best-input-data-format-for-llms)
  - markdown kv: 60.7%
  - xml: 56.0%
  - yaml: 54.7%
  - html: 53.6%
  - json: 52.3%
  - markdown table: 51.9%
  - csv: 44.3%
  - If you make heavy use of tabular data, consider testing whether transforming that data into a different format gives you improved accuracy.
  - Consider markdown tables when you need a balance between readability and cost.
  - Be wary of defaulting to CSV or JSONL - these common formats could hurt your system’s accuracy.

- Markdown-KV was markdown with "key: value" (KV) pairs, like this:

```md
# Employee Database

## Record 1

\`\`\`
id: 1
name: Charlie A0
age: 56
city: New York
department: Operations
salary: 67896
years_experience: 7
project_count: 1
\`\`\`

## Record 2

\`\`\`
id: 2
name: Grace B1
age: 59
city: Mumbai
department: Marketing
salary: 47248
years_experience: 0
project_count: 43
\`\`\`

```

- That's not a table format, it's a map format for each row, but thanks for the tip anyways! Best table format: do not use table to format your data.

- It’s interesting that your bespoke Markdown-KV outperforms established formats like JSON and YAML despite presumably having far less training data.
  - I suspect the markdown headers act as positional fences that constrain the attention mechanism's search. Once the model finds the right record, relevant values are bounded between headers rather than scattered across 1000 records.

- Short answer: for real apps, generate SQL and let the DB do the work; only stuff rows into context or a vector index when you must.

- Parquet is a binary columnar format, so the model can’t parse it directly. You’d still need to convert it into a text format like JSON or Markdown, etc.

- I worked out how to ingest CSV files and turn into an index which builds a knowledge graph. You can tag demographics, filter by age, gender whatever the data has. Is this cool or useless?

- what about nested json? is there value in converting it to markdown?
  - [Which Nested Data Format Do LLMs Understand Best? JSON vs. YAML vs. XML vs. Markdown _202510](https://www.improvingagents.com/blog/best-nested-data-format)
    - yaml: 62.1%
    - markdown: 54.3%
    - json: 50.3%
    - xml: 44.4%
    - effects varying by model
    - YAML is a good default if you don’t know which format your specific model prefers
    - Avoid XML for large-scale nested data in LLM contexts
# discuss-output-structured
- ## 

- ## 

- ## 

- ## [JSON makes llms dumber? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j9rc6r/json_makes_llms_dumber/)
- I had the same hypothesis, on my tests it was the same, but on smaller models json worked better than yaml, I suppose it's becase of the amount of json data in training dataset, but to find out I needed more resources I hadn't.

- Pretty well known issue, documented by Anthropic and others. Try for yourself to write valid code inside valid JSON objects, it takes a lot more effort to handle quotes and escape characters.

- It seems models like XML more then other output formats (except Markdown, but markdown is a lot harder to parse).

- ## [LLM Output Formats: Why JSON Costs More Than TSV _202412](https://david-gilbertson.medium.com/llm-output-formats-why-json-costs-more-than-tsv-ebaf590bd541)
- JSON is the default choice for many, but it’s a serious token hog. It can use twice as many tokens as other formats for the same data.

- The main reason to explore alternatives to JSON is to reduce the number of tokens used, which reduces costs and response times.

- It’s worth noting that JSON is often the only option if you want to use an LLM provider’s ‘structured data mode’ or some other structure-enforcing package like Guardrails or Outlines. I predict that this will change with time. As more LLM-based apps make it into production and developers turn their attention to optimizations like minimizing token usage, LLM providers will respond by supporting more format options for structured data.

- ## [Structured outputs can hurt the performance of LLMs : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hcj0ur/structured_outputs_can_hurt_the_performance_of/)
- Whenever using structured outputs, also leave the model space to output some "unstructured" content in a form of descriptions, comments etc. It reduces the pressure of improbable token sequences and you can use it for some fancy logs.
- Do you have an example of that?
  - Include a comment or description fields into structured output schemas allowing for a short free-text flow.
  - `{ description: "1 sentence explaining the reasoning behind your choice", ... }`

- This still mess with the performance though cause there are enforcement ongoing. Please free text regex enforcement can be quite slow. I find using 2 prompt work better with first prompt let it freely generate an answer

- I found that adding a `reasoning` field to an output schema object improves results. 
  - And I simply add this mixin to almost every model intended to be used as the `output_schema` for structured output.

- I definitely have found this to be the case, at least with all the major commercial models and the big OS ones. It's still super useful to have structured outputs, of course, but good advice I've seen is to informally structure the output (e.g., "include a short summary section and grade between 1 and 100 at the end of each review") and then use a second model to structure the informal output into JSON.
  - I just it meant as an example of structured output (summary and grade) that would be relatively easy to parse with a secondary model.

- I've also noticed that if I ask the model to output what I want in proper XML tags (no attributes, just simple tags - with hierarchical relationship), the performance is generally better than 100% constraining to JSON/Pydantic. I let it output whatever other text it wants to outside the tags, and it seems to like that.
  - Works especially well with the Claude models, but also a lot of open source ones. My theory is that a lot of training data likely had xml tags, html, etc. in it, so it's probably most familiar with this structure.
- Nice. I hope OpenAI eventually makes for more flexible constrained decoding because right now you only can produce JSON. Then you could try other formats, and see if that makes a difference.

- Claude really likes XML, but I've found llama3-405b is hit or miss with same prompts. Llamas like JSON.

- I do the same. Let the model output in whatever format it is compelled to, I just ask it to do so in a meaningful structure and dictate what information needs to be included, then I pass that output to a second LLM call to coerce the data into the required final form

- If the model is good at following instructions, just tell it to output the data you need, then use a second pass to turn the answer into structured outputs, or like other's mentioned leave room for unstructured content.

- It was debunk(揭穿：揭露) by dotxt Bullshit article by trashy researcher https://blog.dottxt.co/say-what-you-mean.html
  - Our study reveals that structured generation constraints significantly impact LLM performance across various tasks.
  - The source for this claim was three sets of evaluations they ran that purportedly showed worse performance for structured generation (”JSON-Mode” in the chart) compared with unstructured (”Natural Language”/NL in the chart).

- Function calling and classification are not the only use cases of structured outputs. Some good examples here: https://python.useinstructor.com/examples/#quick-links

- ## [What's the BEST local LLM for JSON output, while also being smart? : r/LocalLLaMA _202408](https://www.reddit.com/r/LocalLLaMA/comments/1ex6ngu/whats_the_best_local_llm_for_json_output_while/)
- Any LLM can do strictly correct structured JSON output if you use a backend that supports constrained generation.
  - I use Mistral 0.3 personally, EXL2 with aphrodite-engine and outlines
  - Remember that you still need to prompt the LLM well and give examples, but these tools will all make sure what you get back matches a pydantic schema.

- Run 2 agents 1 for queries and 1 for post processing in json
- You could use 2 models instead of one, the first model can be any model really, just don’t tell it to output json, then you can use the nuextract model to put everything into a nice json

- One way to work around it is to use a two step process; one to reason freely, and then one to capture that reasoning into the constraint required.

- Don't forget a recent paper stated that forcing an LLM to output a JSON will greatly decrease it's quality
  - The paper was about processing code in JSON, not forcing a JSON output (two different things)
- You two may be talking about different papers. 

- ## [Every Way to Get Structured Output from LLMs | Hacker News _202406](https://news.ycombinator.com/item?id=40713952)
- Structured output should not be assumed is limited to JSON. Claude performs very well with XML, as it has been trained with it, so there's no real need to put in extra work. Not XML as in conformant, schema-compliant XML, just XML as delimiters.
  - Give it examples and instructions in tags, ask it to output in tags, and force it to return early by completing for it. (Assistant: `<output>` ).
  - When you think about it, it makes a lot of sense. Even if the output is chatty, parsing it is easy because you're not looking for `}` which may or may not match an opening {, instead you're looking for `</output>` which is much easier to parse for.

- XML is also a great option, but there are a few trade offs:
  - XML is a many more tokens
  - regardless of if you're looking for `} or </output>` its really a matter of "does your parser work".

- the main one is that most people don't own the model. so if you use openai / anthropic / etc then you can't use token masking. in that case, reprompting is pretty much the only option

- We just use openai function calls (tools) and then use Pydantic to verify the JSON. When validation fails we try the prompt again.
  - Same here. I send a JSON schema along with the prompt to ChatGPT as function_call and then verify with NodeJS + Ajv against the same schema again.

- we use claude in production and have a 95%+ accuracy returning valid json

- Are there fine tuned models that perform better for structured / parsable outputs?
  - llama.cpp has a feature to constrain output to the provided grammar, such as https://github.com/ggerganov/llama.cpp/blob/master/grammars/...

- ## [Best format for structured output for smaller LLMs? XML/JSON or something else? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i5k5qw/best_format_for_structured_output_for_smaller/)
  - I'm wondering which format is the best and easiest to follow for smaller models?

- Given that most function calling APIs are built on top of JSON, I'd say JSON gets more training.
  - are you talking about smaller models, or frontier models as well? In my tests all the larger models write extremely accurate XML.

- Also, wasn't there a paper posted here a ~week ago showing how constrained decoding hurts intelligence?
  - If your model is good enough, constrained decoding will not reduce the performance of the model, because it is just predicting the next token, which is equivalent to writing the prompt manually. For small models, you should not expect it to do anything correctly.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What's the best format to pass data to an LLM for optimal output? : r/Rag _202511](https://www.reddit.com/r/Rag/comments/1oo3fg8/whats_the_best_format_to_pass_data_to_an_llm_for/)
  - I’ve been testing different methods for feeding structured and semi-structured data into open-source LLMs(mostly open-source), trying to find which formats produce the most accurate and contextually aware results.
  - Has anyone done systematic testing or found reliable patterns in how LLMs interpret various data formats?

- I recently ran some tests on several non-open-source models, aimed at seeing which of several formats of some structured data they understood best: https://www.improvingagents.com/blog/best-nested-data-format
  - Results varied considerably between models/providers, so results with any specific open source model could be different again.

- It can be model dependent. Some models like markdown. L, some like bulleted lists (dashes), numbered lists, and XML. Even though it doesn’t get mentioned as much as it used to, XML is still the safest bet across all models (Gemini and Anthropic models still strongly prefer it). Only problem is XML is a verbose structure.
  - One way to get a clue as to this is to look at the papers published by whoever created the model. They usually have prompts in the appendix of the model release papers.

- The real shift is when you need the LLM to take an action based on the data. Trying to get it to parse raw text and then format an API call is a nightmare.
  - we lean heavily on function calling for this at eesel AI. It basically forces the model to give you a structured output you can actually use reliably. It's way less flaky than prompt-based formatting for complex tasks.

- [What's the best format to pass data to an LLM for optimal output? : r/PromptEngineering _202507](https://www.reddit.com/r/PromptEngineering/comments/1mb80ra/whats_the_best_format_to_pass_data_to_an_llm_for/)
  - chatgpt likes markdown, claude likes xml

- ## [LLMs pose an interesting problem for DSL designers | Hacker News _202506](https://news.ycombinator.com/item?id=44302797)
- The title should be "DSLs pose an interesting problem for LLM users".
  - "Everyone can code now!" -> "Everyone must learn a highly specialized set of techniques to prompt, test generated code, etc."

- authoring DSLs is something LLMs can assist with better than most programming tasks. LLMs are pretty great at producing code that's largely just a data pipeline.

- We're making a prompting DSL (BAML https://github.com/BoundaryML/baml) and what we've found is that all the syntax rules can easily be encoded into a Cursor Rules file, which we find LLMs can follow nicely. DSLs are simple by nature so there's not too many rules to define.

- I recently had to work with the robot framework DSL. Not a fan. I hardly think it's any more readable to a business user than imperative code either. Every DSL is another API to learn and usually full of gotchas. Intuitiveness is in the eye of the beholder . The approach I would take is transpiling from imperative code to a natural language explanation of what is being tested, with configuration around aliases and the like.

- In an initial experiment, I found that LLMs could translate familiar shell scripting concepts into Hypershell syntax reasonably well. More interestingly, they were able to fix common issues like type mismatches, especially when given light guidance or examples. That’s a big deal, because, like many embedded DSLs, Hypershell produces verbose and noisy compiler errors. Surprisingly, the LLM could often identify the underlying cause hidden in that mess and make the right correction.
  - This opens up a compelling possibility: LLMs could help bridge the usability gap that often prevents embedded DSLs from being more widely adopted. Debuggability is often the Achilles' heel of such languages, and LLMs seem capable of mitigating that, at least in simple cases.
  - More broadly, I think DSLs are poised to play a much larger role in AI-assisted development. They can be designed to sit closer to natural language while retaining strong domain-specific semantics. And LLMs appear to pick them up quickly, as long as they're given the right examples or docs to work with.
- Your experience with Hypershell points to an interesting possibility: LLMs as DSL translators rather than replacements. This could actually democratize DSLs by lowering the learning curve while preserving their domain-specific benefits. The real opportunity might be DSLs optimized for both human semantics and machine translation.

- Using an LLM to generate code is not an easily traceable and explainable process. Using a DSL to same ends is. PL research has yet to meet explainability in AI head on.

- ## 📈 [Which table format do LLMs understand best? | Hacker News _202510](https://news.ycombinator.com/item?id=45458455)
- I was curious enough to have Codex create a similar benchmark: https://github.com/jcheng5/table-formats
  - I was so surprised by gpt-5 getting 100% that I ran it again with 1000 samples. It got 999 correct, and one wrong.
  - gpt-5 also got 100/100 for both CSV and JSON.

- The test really needed to be run on multiple data sizes (50, 100, 500, 1000, 5000). The more token efficient formats would probably eventually overtake the token heavy ones due to context pollution. All this test really says is what performs best for 1 particular model at one particular context length.

- Curious to reproduce across models, I made a comprehensive eval based on your post and ran it against 30 models
  - As you can see it's near 100% recall across all formats for a good chunk of frontier models, with a few (curiously, mostly Claude) failing at basic prompt adherance ("Return just the number") but still returning the right answers. 
  - The major failures are from Mistral Medium, Llama Maverick, Llama 3 70b Instruct, Mistral Nemo, Gemma 3 12b It, GPT 4o/4.1 Mini etc.
- Based on these limited tests, here's the leaderboards on formats FWIW:
    CSV: 84.25%
    Markdown Table: 82.65%
    YAML: 81.85%
    JSON Lines (jsonl): 79.85%
    Markdown key-value: 79.83%
    Pipe-delimited: 79.45%
    Natural language summary: 78.65%
    JSON: 77.73%
    HTML table: 75.80%
    XML: 73.80%

- IMO the biggest takeaway really is: Use the best model you can reasonably afford, then the format chosen will matter less. The cheapest 100%-coverage models are Gemini 2.5 Flash and Deepseek Chat V3.1 FWIW. However, if you have no control over model, then use CSV or Markdown Table as these have highest chance of success.

- I wonder how this compares to a more agentic approach where the LLM composes SQL queries to answer the questions, for example.
  - Yeah I mean for many real world scale datasets you don’t want to blow the whole context window on a massive markdown file. Instead you can provide a tool that presents the data as a SQLite database. In my testing Claude code seems very capable of answering questions via SQLite queries or even `head` and `grep` on CSV files.
- 💡 This was exactly my thought. Rather than feed the table directly to the LLM, build agents that extract the data and have the LLM act on the extracted data items. Then it’s a preference issue.

- It highlights an important but often downstream problem. In real-world pipelines, the bigger issue comes before this: extracting tables from PDFs or scans without breaking their layout. Once the structure is lost (merged headers, nested cells, footnotes, etc.), no data format can fully recover it.
  - Check out LLMWhisperer from Unstract —> it preserves table and layout fidelity when converting documents for LLM use. 

- Can someone explain why one would want to use an LLM to read tabular data? This is something even trivial code could do while using far fewer compute and energy resources.
  - I want this for after the code has run and returned results. Often when you use code to answer questions about a table, the result is in the form of a smaller table. I'd like to know how small that table needs to be before you can rely on the model being able to make reliable observations about it.

- This is a bit silly way to use LLMs to process tabular data. In reality, you'd ask it to write functions and execute them. First you'd ask it to create a type definition from the table, then ask it to create functions to process the data.
  - "Write a function to find years of experience by name? Return just the number, e.g. '12'."
  - It works much better, and it can single-shot many of the processing requirements just from type definitions it can infer from the data.
  - This way it's easier to stick to tabular formats that have easy reading libraries, like with TypeScript/JavaScript JSON, and with Python, maybe CSV...

- We ended up making middleware for LLM 'tools/functions' that take common data/table formats like CSV, Excel and JSON.
  - The tool uses an LLM to write code to parse the data and conduct the analysis to return back to the LLM. Otherwise, we found pumping raw table data into a LLM is just not reliable, even if you go to the effort to conduct analysis on smaller chunks and merge the results.

- We've experimented with different formats for feeding data to LLMs and markdown tables usually work pretty well. JSON is more structured but harder for the model to parse visually.
  - CSV works okay but you lose a lot of context about what the columns actually represent. The model performs better when it can 'see' the structure clearly.

- a table inherently has a 2D spatial structure, while Large Language Models (LLMs) are optimized for processing 1D sequential text. This creates a fundamental mismatch between the data representation and the model’s input format.
  - Most existing pipelines address this by preprocessing the table into a linearized 1D string before passing it to the LLM — a question-agnostic step that may lose structural information.
  - Instead, one could retain the original table form and, when a question is asked, feed both the question and the original table (as an image) directly into the VLM. This approach allows the model to reason over the data in its native 2D domain, providing a more natural and potentially more accurate solution.

- I've found that xml is surprisingly good for llms when it comes to table extraction in production. I only found out when I send the raw xml storage format to benchmark again various flavours of everything else. XML turns out to the best format for tables that have more than three levels of nesting.

- I’ve been using YAML data for tables for a while now, and had pretty good results.

- There are other studies on this topic with similar results across LLM systems:
  - Y. Sui, M. Zhou, M. Zhou, S. Han, and D. Zhang, “Table Meets LLM: Can Large Language Models Understand Structured Table Data? A Benchmark and Empirical Study, ” in Proceedings of the 17th ACM International Conference on Web Search and Data Mining, Merida Mexico: ACM, Mar. 2024, pp. 645–654. doi: 10.1145/3616855.3635752.
  - C. Pang, Y. Cao, C. Yang, and P. Luo, “Uncovering Limitations of Large Language Models in Information Seeking from Tables, ” June 06, 2024, arXiv: arXiv:2406.04113. doi: 10.48550/arXiv.2406.04113.
