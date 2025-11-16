---
title: lib-aisaas-pipeshub-community
tags: [community, pipeshub, rag]
created: 2025-11-16T15:34:14.297Z
modified: 2025-11-16T15:34:38.658Z
---

# lib-aisaas-pipeshub-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🤔 pipeshub: [Stop converting full documents to Markdown directly in your indexing pipeline : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1o261nz/stop_converting_full_documents_to_markdown/)
  - I've been working on document parsing for RAG pipelines since the beginning, and I keep seeing the same pattern in many places: parse document → convert to markdown → feed to vector db. I get why everyone wants to do this. 
  - You want one consistent format so your downstream pipeline doesn't need to handle PDFs, Excel, Word docs, etc. separately.
  - But here's the thing you’re losing so much valuable information in that conversion.
  - Our solution: Blocks (e.g. Paragraph in a pdf, Row in a excel file) and Block Groups (Table in a pdf or excel, List items in a pdf, etc). Individual Blocks encoded format could be markdown, html
  - We've been working on a concept we call "blocks" (not really unique name :) ). This is essentially keeping documents as structured blocks with all their metadata intact. 
  - Everything then gets stored in blob storage (raw Blocks), vector db (embedding created from blocks), graph db, and you maintain that rich structural information throughout your pipeline. We do store markdown but in Blocks
  - So far, this approach has worked quite well for us. We have seen real improvements in both accuracy and flexibility. For e.g. ragflow fails for these kind of queries (as like many other just dumps chunks to the LLM)- find key insights from last quarterly report or Summarize document or compare last quarterly report with this quarter but our implementation works because of agentic capabilities.
  - Do you think this should be an open standard? A lot of projects are already doing similar indexing work. Imagine if we could reuse already-parsed documents instead of everyone re-indexing the same stuff.

- Basically your new format "Blocks" is simply more extensive than "MarkDown" but the rest of the principle is the same. I would agree with you here, MarkDown is somewhat limited.
  - Docling has tried to solve same problem and is using actually DocTags and then converts DocTags to MarkDown when asked.
- Blocks isn't really a "format" like markdown. It's more of a schema/structure for storing content (which could be markdown, HTML, or whatever) alongside its metadata. Think of it as a container.
  - You mentioned Docling's DocTags - that's a perfect example! Docling has their own internal representation, then converts to markdown. LlamaIndex has theirs. Unstructured has theirs. The problem is they're all different. It's not easy to switch from one format to another, there is a learning curve for developers and there is zero reusability. What I'm proposing is a standard schema so these tools can interoperate.

- nice approcach, and we already have it in our lib https://github.com/managedcode/markitdown

- Consider carefully the tradeoff between using Docling and/or Docling Document format and rolling your own and maintaining it. What does your custom thing offer? Is it t really worth the effort?
  - There are some things missing in docling format (just to name a few - memory layout, semantic metadata extracted using LLM and VLM, relationships between blocks) which is why there is need of an open standard. Everyone is rolling out their own implementation which is not good.

- I felt this. Markitdown is pretty good, but only for structured documents such as docx. and xlsx. Sometimes I can save some time by converting to docx from pdf by using ocr based converters but it is still a very far cry.

- That is why i think RAG is useless. We need to have data in various formats, not just text. I have not seen any RAG that give out images. imagine an architect firms what to RAGed their drawings?
  - We haven’t tested it with architectural drawings yet, but we do support images embedded in PDF and DOCX files. When a user submits a query, we highlight the relevant images as well as the text.

- ## [PipesHub - Open Source Enterprise Search Engine(Generative AI Powered) : r/LangChain](https://www.reddit.com/r/LangChain/comments/1kr714l/pipeshub_open_source_enterprise_search/)
- How does this compare to SurfSense's RAG-as-a-service feature?
  - We’re building PipesHub as an enterprise-ready RAG platform with scalability, reliability, and high availability from day one. Unlike SurfSense, which uses federated search and depends on each app’s native search (so it struggles with unstructured data like files or attachments), PipesHub actually indexes both structured and unstructured data across all your tools.
  - Plus, PipesHub creates a rich knowledge graph that understands your organization—people, teams, and context—so it gives much more accurate answers. And every answer comes with pinpointed citations. If something comes from a PDF, we don’t just say “it’s in this file”—we scroll you to the exact sentence or paragraph.

- How do you guys handle tabular data, both csv/xlxs type and tables embedded in pdfs?
  - We try to detect all the tables in a file first — sometimes there are multiple tables in one Excel sheet, just separated by empty rows or columns. 
  - Once we identify a table, we run it through the AI model which figures out the headers and rows. The AI then converts the each table row into a clean paragraph format(Denormalized using headers and row cells), which we use for generating embeddings. 
  - We also store metadata like header and row info for citation purposes. 
  - There are a few more steps in the pipeline, but that’s the gist of how we handle tabular data.
- What kinds of use cases does that kind of parsing and indexing support? At best, with amazing semantic enrichment and supremely tuned search algorithm, you can retrieve some facts or numbers. But more complex analyses (filtering, aggregation, pivot) are off the table, no?
  - Rows themselves are incomplete without headers and what table represents(sometimes context from previous rows also). This method of indexing ensures that the retrieval works fine.
  - There are few other things that are also evaluated as part of the pipeline, like Categorization, Sub-categorization and Entities detection(detecting relationships between entities is also in the process). All of these things, ensure when the user does query, we are able to accurately retrieve correct table/records.
  - As for more advanced analysis like filtering, aggregation, or pivots — those will be handled at query time. We're building out a deep research agent to support complex use cases and eventually more complex analyses will be added in couple of months.

- ## [PipesHub - The Open Source Alternative to Glean : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kgwy2m/pipeshub_the_open_source_alternative_to_glean/)
- If you can convert the script output into any standard file format like .txt, .pdf, .csv, .xlsx, .docx, .html, or even .md, PipesHub can easily pick it up(with automatic sync from connectors like Google Drive) and index it through our AI pipeline. This way, even scattered script outputs can become part of your organization’s searchable knowledge base.

- 🆚 How does this compare to Onyx? It doesn't look like you have as many connectors. 
  - Yes, we build our connectors with exact permissions as the source app and handle both user and user group access.
  - Our platform is an end-to-end multi-agent system where search is just one part of the workflow. Our indexing layer serves as the context foundation for agents, but agents themselves require much more than just access to search.. they need tools, actions, and the ability to interact with other agents.
  - Another key difference is how we approach indexing. When we index data, we capture and understand the relationships between multiple data points. For example, with a Jira ticket, indexing is not just about the ticket itself.. it also includes comments, attachments, and descriptions, and the relationships among them. This relational understanding is crucial for high accuracy (Agents need full context not just chunks) and is missing in some of the other platforms.

- [PipesHub - The Open Source Alternative to Glean : r/Rag](https://www.reddit.com/r/Rag/comments/1kgy501/pipeshub_the_open_source_alternative_to_glean/)
  - Unlike Glean and most other tools that only cite documents, PipesHub gives pinpoint citations—like exact paragraphs in PDFs/DOCX or row numbers in XLSX/CSV—so humans can instantly verify AI answers and also scroll to the exact location in the document. Onyx currently doesn’t leverage Knowledge Graphs, which we’ve found essential for accurate and contextual responses. 
  - Also, several cutting-edge features are in the pipeline and coming out shortly. 
  - Onyx is search platform where as PipesHub is an end to end Multi-agent platform that developers can use to build Agents that need enterprise context to answer queries and tools to perform actions and automate workflows
  - What does it use for vector storage? I saw in the docs you can set an s3 bucket for storage- does that mean it uses pgvector?
    - We use Qdrant. S3 bucket(Storage service) is used for storing things like Document Summary, Text layered OCR document and more

- [PipesHub - Open Source Enterprise Search Platform(Generative-AI Powered) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1l2afie/pipeshub_open_source_enterprise_search/)
- 1) How many documents can it ingest and is there a practical limit? 2) Can it mingle its search results with those from the open Web - e.g. you feed it a list of 3, 000 website URLs, it goes and downloads those sites and ingests them as well?
  - PipesHub is built to be highly scalable and fault-tolerant — it can handle millions of documents without issues.
  - Support for ingesting content from the open web (like a list of URLs) is coming soon! You’ll be able to crawl and index any webpage as part of your search.
