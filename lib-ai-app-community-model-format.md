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
# discuss-md-table
- ## 

- ## 

- ## 

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

- ## [What's the best format to pass data to an LLM for optimal output? : r/PromptEngineering _202507](https://www.reddit.com/r/PromptEngineering/comments/1mb80ra/whats_the_best_format_to_pass_data_to_an_llm_for/)
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
