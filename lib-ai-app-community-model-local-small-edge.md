---
title: lib-ai-app-community-model-local-small-edge
tags: [ai, community, large-language-model, local-first, mobile, phone]
created: 2026-01-23T13:08:23.483Z
modified: 2026-05-28T20:48:22.013Z
---

# lib-ai-app-community-model-local-small-edge

# guide

# local-models
- local-hardware
  - [Hardware – Hugging Face](https://huggingface.co/hardware)

- local-model
  - [GPU Poor LLM Arena - a Hugging Face Space by k-mktr](https://huggingface.co/spaces/k-mktr/gpu-poor-llm-arena)

- https://github.com/fiveoutofnine/whatcanirun /202603/ts
  - https://whatcani.run/
  - Find the best local models based on real data
  - https://x.com/fiveoutofnine/status/2038728823861367233
    - whatcani.run is based on real runs submitted by people
    - canirun.ai provides estimates across a wider variety of models and devices
    - it filters all submissions by CPU + GPU + RAM, and so far that's the only model that has any benchmark data submitted for it

- https://github.com/AlexsJones/llmfit /MIT/202603/rust/ts
  - https://www.llmfit.org/
  - Hundreds of models & providers. One command to find what runs on your hardware.
  - A terminal tool that right-sizes LLM models to your system's RAM, CPU, and GPU. Detects your hardware, scores each model across quality, speed, fit, and context dimensions, and tells you which ones will actually run well on your machine.
  - Ships with an interactive TUI (default) and a classic CLI mode. Supports multi-GPU setups, MoE architectures, dynamic quantization selection, speed estimation, and local runtime providers (Ollama, llama.cpp, MLX, Docker Model Runner).

- https://github.com/outsourc-e/bench-loop /MIT/202605/python
  - https://bench-loop.com/
  - Local-first CLI for benchmarking LLMs on real hardware — quality, speed, reliability, and a real multi-turn agent loop.
  - BenchLoop is a local-first CLI + web app for benchmarking LLMs running on your own hardware. 
  - It scores models across seven repeatable suites — quality, speed, reliability, agentic tool use, coding, instruction following — and gives you receipts: per-task outputs, latency, token counts, machine info, scores.
  - No accounts, no telemetry, no API keys. Your model, your machine, your numbers.
# discuss-stars
- ## 

- ## 

- ## 
# discuss-browser-ai
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🧭 [Chrome's Local AI Model in production (Gemini Nano) 41% eligibility, 6x slower and $0 cost : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qkph45/chromes_local_ai_model_in_production_gemini_nano/)
  - reading about Chrome's built in AI model (Gemini Nano 1.8b) and tried implementing it, this is my story.
  - Google ships Chrome with the capability to run Gemini Nano, but not the model itself.
  - Multiple models, no control. Which model you get depends on an undocumented benchmark. You don't get to pick.
  - ~1.5-2GB download. Downloads to Chrome's profile directory. Multiple users on one machine each need their own copy.
  - On-demand. The model downloads the first time any site requests it.
  - Background download. Happens asynchronously, independent of page load.
  - Think of the requirements like a AAA video game, not a browser feature.
  - Inference Performance:
  - Gemini Nano (on-device)	7.7s
- 👀 At p99, Nano hits 52.9 seconds while Gemma is at 2.4 seconds. Worst case for Nano was over 9 minutes. Gemma's worst was 31 seconds.
  - prompt-processing 速度太慢
- What Surprised Us
  - No download prompt. The 1.5GB model download is completely invisible. No confirmation, no progress bar. Great for adoption. I have mixed feelings about silently dropping multi-gigabyte files onto users' machines though.
  - Abandoned downloads aren't a problem. Close the tab and the download continues in the background. Close Chrome entirely and it resumes on next launch (within 30 days).
  - Local inference isn't faster. I assumed "no network latency" would win. Nope. The compute power difference between a laptop GPU and a datacenter overwhelms any latency savings.
  - You can really mess up site performance with it We ended up accidentally calling it multiple times on a page due to a bug..and it was real bad for users in the same way loading a massive video file or something on a page might be.
- By the numbers, there's no reason to use Gemini Nano in production:
  - It's slow
  - ~60% of users can't use it
  - It's not cheaper than API calls (OpenRouter is free for Gemma)
- We're keeping it anyway. I think it's the future. Other browsers will add their own AI models. We'll get consistent cross-platform APIs. I also like the privacy aspects of local inference. The more we use it, the more we'll see optimizations from OS, browser, and hardware vendors.

# discuss-small-llm-hot
- ## 

- ## 

- ## 

- ## 

- ## [MiniCPM5 1B (now open source) benchmarks are kind of absurd : r/LLM _202605](https://www.reddit.com/r/LLM/comments/1tp1135/minicpm5_1b_now_open_source_benchmarks_are_kind/)
  - 1.08B params, tops the Artificial Analysis Intelligence I ndex for every open model under 2B, and somehow beats Qwen3.5 2B which has literally double the parameters.
  - The whole thing is Apache 2.0 with weights, training data, and deployment code all published.
  - Quantized to INT4 it sits at 0.5GB, so you can run it on a phone. 131K context window, standard LlamaForCausalLM architecture, so Ollama, vLLM, llama.cpp, all the usual stuff loads it with zero custom setup.

- They are far from useless. Intention classification, keyword generation, text summary, named entity recognition, moderation, memory and retrieval etc... They are absolute necessity if you do serious agentic stuff...
# discuss-local-hardware
- ## 

- ## 

- ## 

- ## [香橙派+MiniCPM-V-4.6, 本地化的极致小模型推理方案 - LINUX DO _202605](https://linux.do/t/topic/2241870)
  - 这次轮到手头的这个国产小板子（香橙派AI Pro，昇腾310B芯片）。由于国产生态问题，其实这个板子很少有人去适配模型
  - 20TOPS版本大概2000块，8T版本更便宜，只要899。折合一下FP16算力差不多也有1080TI水平了，用的unified memory, 24GB内存。最近没啥人折腾，还是要祭出天才程序员，这次不是写CUDA，而是写AscendC自定义算子，把MiniCPM-V-4.6支持起来。
  - 一个完全从零写的 C++/AscendC 推理引擎, 把 MiniCPM-V 4.6 跑在 Orange Pi AIPro 20T 板载的 Ascend 310B NPU 上。 文本和图像对话都完全跑在 NPU 上, Python 端只在 CPU 上做 tokenize 和图像预处理, 推理热路径完全不依赖 torch_npu。
  - 通过三轮 cube unit / 自定义 kernel 工作, 单 batch 解码从 2.88 → 5.90 tokens/s(~2×), 跑的是完整 24 层 hybrid 线性 + full attention 模型(hidden 1024, vocab 248094, fp16)

- 这是个边缘计算的板子吧？其实我没想明白它的家用场景。 如果只是低功耗长期运行的话，理论上ESP32+glm flash免费api就可以实现可用了，效果还会好点。

- 这速度看起来还不如3*2T=6Tops的rk3588

- 310p的性能依托，堪称昇腾界的k80，胶水核心，推理能力依托，严肃要求换成930，天才程序员一晚上才把驱动什么的打好，官网甚至没说驱动不支持高版本内核

- 我的macmini m4 丐版 部署过几个本地模型后 发现基本没有什么可用性, 还是老老实实买套餐

- 昇腾一直就不支持高版本linux内核……都是坑

- ## We’re launching @huggingface Hardware: → trending GPUs & CPUs  _202605
- https://x.com/julien_c/status/2057084823097794772
  - nvidia: 45%
  - amd: 5%
  - apple: 16%
  - cpu: 32%

- from tracking public training logs, A100s still dominate open-source runs by a wide margin. the interesting part is consumer GPUs — 4090s and M-series are quietly becoming the fine-tuning workhorses. real bottleneck for most people isn't compute, it's VRAM. wonder if your data shows the same split

- The reverse would be great too: input my hardware (GPU + VRAM) and get the best models I can run locally right now, with quant suggestions.

- 
- 
- 
- 

# discuss-local-llm-usecases
- resources
  - [Use Cases | Claude](https://claude.com/resources/use-cases)

- https://github.com/Ashfaqbs/TinyLLM-usecases
  - When Small LLMs Win
    - Tool/function calling - Mapping user intent to a function name + arguments
    - Intent classification - Routing queries to the right service
    - Query parsing - Extracting structured data from natural language
    - Simple Q&A with tools - Answering questions by calling APIs
    - Edge/IoT deployment - Running AI on devices with no internet
    - High-throughput pipelines - Processing thousands of requests per second
    - Privacy-sensitive workloads - Data never leaves your infrastructure
    - Development and testing - Fast iteration on AI pipelines without API costs
  - When You Still Need Large LLMs
    - Complex multi-step reasoning across long documents
    - High-quality creative writing or content generation
    - Tasks requiring deep world knowledge
    - Nuanced understanding of ambiguous instructions
    - Multi-modal tasks (vision + text + audio)

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What are the main uses of small models like gemma3:1b : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qhf451/what_are_the_main_uses_of_small_models_like/)
- Prompt decomposition to filters, routing, basic chat 'sentinel' for stuff like filtering, spelling correction to save tokens etc.. LOTS of uses as part of a system. They're great (and super efficient) for small tasks.

- I fine tuned gemma 270m to extract/find sensitive data in text or code. It worked great in my llm proxy security app. 

- Classifiers mostly

- ## [What do you use Gemma 4 for? : r/LocalLLaMA _202605](https://www.reddit.com/r/LocalLLaMA/comments/1t4zca8/what_do_you_use_gemma_4_for/)
- Gemma trounces Qwen for my handwriting analysis and general vision tasks at the very least. I also appreciate Gemma in chat significantly more than Qwen (qwen is cold and calculating even with system prompt modifications/nudging I've found though I have gotten it to be better lately with further modifications).
  - Gemma also produces quality outputs with far less thinking than Qwen. Qwen can think forever before responding.

- The only things I use llms for are coding and JP->EN translation, for agentic coding its a nobrainer, Qwen is much better than gemma with tools, for JP->EN translation its also a nobrainer, Gemma is much better (at least in the genre of text I translate from—hentai and porn tweets)

- Qwen3.5/3.6 are really good at video analysis, better than Gemma4
  - Gemma4 is considerably better as a voice agent, Qwen does not follow instructions for conciseness as it seems it wants to be "too helpful" and spends a lot of time listing options and things which it is explicitly told not to. Gemma4 follows instructions perfectly and is better assistant overall IMO.

- ## [Why don't more people or companies run local LLMs rather than using APIs? : r/LocalLLM _202605](https://www.reddit.com/r/LocalLLM/comments/1t3vts9/why_dont_more_people_or_companies_run_local_llms/)
- I can't speak for many other companies, but at my company we have a policy to prefer external enterprise solutions over local/custom/on-premise solutions.

- Higher up front cost and difficulty sourcing GPUs

- They are still under aws spell - cloud is cheaper, better, faster. I've had that told to me, even on a CPU intensive applications, where aws marks up at least 10x over on-prem

- uptime, redundancy, infrastructure cost, maintenance cost, man hour cost, liability for all the previously mentioned etc.

- ## [What are people using Local LLMs for (beyond coding) : r/LocalLLM _202604](https://www.reddit.com/r/LocalLLM/comments/1sz59g6/what_are_people_using_local_llms_for_beyond_coding/)
- Roleplaying

- News aggregation. Weather monitoring. Novel writing. Schedule keeping.
  - Book-keeping (gnucash alternative to SAAS quickbooks et al that put financial info in cloud server security danger). "But you just use a pc for that." The AI is for budgeting and forecasting for a small business.

- In the last couple weeks, besides general info, here are some things I've asked Local LLMs to do:

Help with writing. Not creating it but spell checking, grammar, coherence, and helping me convey exactly what I am trying to say... like finding that word on the tip of my tongue that I'm trying to think of.

Pulling transcripts from long YouTube videos and giving a synopsis

Generating images using ComfyUI, sometimes with OpenWebUI to mimic the cloud LLMs

Image analysis (vision)... for example:

Took a photo of items in a "junk drawer, " and it listed everything in it.

Took photos of my bookshelf, and it listed all the books.

Analysing logs from my home DNS queries for suspicious activity.

Created a beautiful custom Grafana dashboard in one shot to monitor devices in my homelab.

Asking questions and doing comparisons against long PDF documents: e.g. Health and Auto Insurance

Instead of auto-accepting "Terms of Service" I'll now copy and paste, and ask if there are any catches or if it's pretty standard

Use with the Smart Composer plugin in Obsidian to compose and analyse notes

- For basic web search, creative writing, and exchanging ideas, Gemma 4 31B has been great.  I also use Gemma 4 31B and Qwen 3.6 27B for image reasoning when privacy is the priority. 

- uncensored models, + AI costs gonna be explode in future, most people using online tools for coding will learn it in hard way

- ## [Do 2B models have practical use cases, or are they just toys for now? : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s5bztk/do_2b_models_have_practical_use_cases_or_are_they/)
- The 2B size is practical for: classification, routing, summarization of small inputs, function calling with well-defined schemas, and anything where the output format is constrained.
  - They are genuinely useful for structured tasks.

- As everyone put it, 2B is great for recognizing patterns, but what makes them amazing is also the fine-tuning capabilities! If you want to standardize something, then a team of 2B models with specific fine-tuned goals will outperform any generalized model in efficiency, where you can tune up the accuracy.

- ## [Small model (8B parameters or lower) : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1s4zhlx/small_model_8b_parameters_or_lower/)
- So decompose your problem first into clear, small, steps, then automate everything with code that you can, only call the model when you need it, and only with the exact context and tools that it needs for a step.

- Scraping HTML - works great - but takes some trial and error to get it to work but cheaaaapp, can run beautifully without quantization on 5060ti 16gb (run schematron 8b)

- I'm currently filtering a huge 6.8mill dataset of scraped roleplay forum posts and a specialized 8B model is plenty to do fast batched checks of "is this post in-character", 46 posts per seconds on 2x3090.

- I've mostly seen small models work best for lightweight stuff, summaries, quick Q&A, basic doc/image analysis, and simple local assistants. They’re surprisingly decent, but consistency and deeper reasoning usually start to fall off once context gets longer or tasks get more layered

- ## [Cheap LLM vs Local LLM : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1s00zby/cheap_llm_vs_local_llm/)
- Find the model you are thinking of running locally and subscribe to it with API calls. Compare if it is good enough. You likely will prefer the state of the art models.

- Use cheap APIs for: orchestration / planning steps, anything that needs strong reasoning or large context. One bad step in an agent chain can waste all the previous steps, so it's worth paying for quality there.
- Use local for: the repetitive subtasks - classification, extraction, reformatting, tool-call routing. A Qwen3 8B handles these fine and you get zero latency overhead, no rate limits, and no surprise bills when your agent accidentally loops.
- The hybrid approach works best: frontier model as the "brain" that plans, local model as the "hands" that execute the simple stuff. You can cut API costs 60-70% this way while keeping quality where it matters.

- 5070ti, Tried qwen 9b, moved to 27b. Usable but a lot of debugging because agents wouldn’t execute multi step tasks properly.

- ## [Are local LLMs better at anything than the large commercial ones? : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1rtpqqo/are_local_llms_better_at_anything_than_the_large/)
- They are better at privacy. That is a thing.

- NSFW models are better

- Latency - some models (e.g., at openrouter) get overloaded and take 10-30s to respond. For long responses, they will still "win" but for short responses, local can be better.

- all frontier models set you either with temporary loose limits to lock you in, hour/weekly limits that drive you nuts or paying big bucks to get what you want. Local models gives a piece of mind, even if they're not as capable

- ## [Finally found a reason to use local models  : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rp48hx/finally_found_a_reason_to_use_local_models/)
  - I have a static website with about 400 pages inside one sub directory. I wanted to add internal linking to those pages but I was not going to read them and find relevant pages manually.
  - So I asked claude code to write a script which will create a small map of all those mdx files. The map would contain basic details for example, title, slug, description and tags. But not the full content of the page ofcourse. That would burn down my one and only 3090 ti.
  - Once the map is created, I query every page and pass 1/4th chunk of the map and run the same page 4 times on a gemma3 27b abliterated model. I ask the model to find relevant pages from the map which I can add a link to in the main page I am querying.
  - At first I faced an obvious problem that the tags were too broad for gemma 3 to understand. So it was adding links to any random page from my map. I tried to narrow down the issue but found out the my data was not good enough.
  - I asked claude code to write me another script to pass every single post into the model and ask it to tag the post from a pre defined set. When running the site locally I am checking whether the pre defined set is being respected so there is no issue when I push this live.

- You’re missing out on a significantly easier and cheaper way to do this! Use an embedding model. My go to is https://huggingface.co/google/embeddinggemma-300m but anything should work fine. They will naturally generate the exact sorts of connections you’re looking for. They’re significantly faster than anything generative and can probably do just as well. Look into RAG with a vector DB, it fits your use case very well. To me, it sounds like you’re doing document clustering. You might want to look into that cause you might be able to significantly improve the results you’re seeing!

- This here is what I like to see. Experiment, learn, share

- Instead of stopping the script manually, you should set your GPU power limit to 50-70%, whatever your PC can handle longterm during those temperatures. You can do similar things with the CPU, lowering the max frequency by a slight amount can already cut the power consumption in half.

- Embeddings won’t directly insert inline links. Use them to fetch the top 10 nearest pages for each article, then pass only those candidates plus the source article to an LLM and ask it to return max 3 inline link edits as JSON. So the pipeline is: embed all pages once -> cosine top-k retrieval -> optional rerank with tags/categories -> LLM chooses exact anchor text and sentence placement -> script patches the markdown.

- ## [Local LLM Performance: Testing OpenClaw with 2B/4B models via llama.cpp? : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1qzykqy/local_llm_performance_testing_openclaw_with_2b4b/)
  - Has anyone here experimented with "tiny" models in the 2B to 4B parameter range (like Gemma 2B, Phi-3, or Qwen 4B)?

- I have tested it in the 2-12b param range and it is literally unusable, it isn't even able to respond properly to the very first "wake up my friend" prompt.

- I managed to get it going with qwen3-4b-thinking-2507 on a 6gb rtx 3050. It took about 3 minutes to respond to hello. It’s unusable.

- I have a Lenovo Legion 5 notebook with 16GB RAM, a Ryzen 5 5600H, and a 3070 notebook GPU. I didn't use llama.cpp directly but used Ollama.
  - Download qwen3:4b-instruct-2507-q8_0.
  - Install OpenClaw on the VM and complete the setup.
  - Tool Calling: Seems to work fine.
  - Performance: 30 seconds to execute the command "Create a file named HelloWorld on my desktop". 10 seconds to respond to "Hello".
  - It is not the fastest, but it works well for me. You could also host the model on your main PC and use an old device in the same network to run Linux with OpenClaw

- ## [I benchmarked 22 local models for OpenClaw agent tool calling on RTX 3090 — Qwen 2.5 Coder 32B (Oct 2024) still beats every 2025-2026 model, including Claude Sonnet 4.5 : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rmkqco/i_benchmarked_22_local_models_for_openclaw_agent/)
  - I run OpenClaw as my daily AI agent (Telegram, email, CRM) on a self-hosted RTX 3090. I tested 24 models (18 dense + 6 MoE) on what actually matters for agents: tool calling, multi-step workflows, bilingual FR/EN, and JSON reliability. 
  - Setup: llama.cpp, 65K context, KV cache q4_0, flash attention.
  - https://github.com/Shad107/openclaw-benchmark
- Qwen 2.5 Coder 32B (Q4_K_M) wins at 9.3/10 — a model from October 2024 beats every 2025-2026 model
- It also beats Claude Sonnet 4.5 API (8.6/10) on pure agent execution
- Reasoning models (R1 Distill, QwQ, OLMo Think) make terrible agents — thinking ≠ doing
  - Reasoning models can't agent. R1 Distill (4.0), OLMo Think (3.4), QwQ (7.3) — they waste tokens thinking when the agent needs to act.
- MoE with small active params can't handle multi-step — fast but unreliable
- Magistral Small 2509 is the dark horse — best multi-step (9/10), perfect French

- another fucking bot, can we just ban for mentioning qwen2.5 at this point

- ## [Local agent - real accomplishments : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1rgw4yk/local_agent_real_accomplishments/)
- I’m doing complicated parsing of texts and information heavy texts and books. I regularly run into being blocked by copyright on online models so run a 8b qwen locally with a 14b for further refinement. I’m churning through 50 pages an hour at the moment in an amd 7900

- The future is LocalLLM and open claw, in any future form. The thing we are currently seeing, large companies having their models sign a deal with administration, to be able to invade anyone privacy or even - life. Everyone will need their own AI Agent, locally, to defend them

- ## [Is Local LLM the next trend in the AI wave? : r/LocalLLM _202602](https://www.reddit.com/r/LocalLLM/comments/1r0swmh/is_local_llm_the_next_trend_in_the_ai_wave/)
- I mean local is always going to be limited by your gear - to have a ‘good’ local LLM you’re talking 5k minimum to have something reasonable and really 10k+ to get something that is significant value add
  - I mean even with OpenClaw there are a ton of reviews basically saying it is near useless without hooking it up to one of the large models.

- Local LLMs are much less capable with 16-24GB GPU memory limit. We need cheap GPUs with like 128GB memory.
- Remember to factor in electricity too 

- I think it could be a business for a while. I just don't know how to find clients. LOL There's bound to be people who want local llms but don't know how to do it.
  - Finding clients for niche tech like local LLMs can be tough, especially if cold outreach is not your thing. Try looking for communities where small businesses or devs vent about AI challenges and jump in to share your knowledge. Tools like ParseStream can help by tracking those discussions across multiple platforms so you do not miss any real opportunities to help.

- ## [Anyone here actually using AI fully offline? : r/LocalLLM _202602](https://www.reddit.com/r/LocalLLM/comments/1qwjgj4/anyone_here_actually_using_ai_fully_offline/)
- I run vLLM in docker for inference and use the API to connect various services. Which is what everyone does. You’re not going to get anything different from anyone if you’re speaking only about inference.

- You have different options, easist is LM Studio as already mentioned, search for the Model on huggingface which suits your GPU (fast response) or your RAM (slow response). Then there is Ollama which also runs locally and you can search for Models on ollama Web Page and how to. Then there is openwebUI which is Local Web UI which runs locally and Access to UI via Browser and it Looks more Like ChatGPT but you have the control, you can combine this with ComfyUI to generate images too but it’s more complicated. There are many other options available and above one are just a tiny bit of Tipps and easy ways.

- My use cases are coding. consulting, and community organizing.

- I batch process documents to create summaries as part of an automated workflow, I want to keep everything local for privacy reasons. I've used the API of a local install LM Studio and it was easy to set up and worked well, but now I use llama.cpp with my own code as I have more control over it.

- Try Localai.io. You’re able to run basically any model and the docker configuration isn’t the most complicated. Works offline in your terminal. I sometimes will finetune with a LoRA in a CoLab notebook and use my new model with localai. Then also you can API to practically anything. Cheers

- ## [Getting OpenClaw to work with Qwen3:14b including tool calling and MCP support : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qrywko/getting_openclaw_to_work_with_qwen314b_including/)
  - I got local tool calling working on Qwen3:14b with ~40 tools, accessible through WhatsApp. 
  - OpenClaw is an AI assistant framework that supports multiple messaging channels. It talks to its LLM backend via an OpenAI-compatible API (/v1/chat/completions).
  - Why a bridge instead of adding tools directly in OpenClaw? OpenClaw supports custom tools natively. You could write each MCP tool as an OpenClaw extension. But I have multiple apps that need the same tools: OpenClaw for WhatsApp, Engram (my personal knowledge system), Jan.ai, etc. Writing each tool as a per-app extension means duplicating everything. With the bridge as a shared MCP layer, you configure your tools once, and any OpenAI-compatible client gets them. Just point it at :11435 instead of :11434.
  - I tested both qwen3:8b and qwen3:14b on an M4-series Mac Studio with 64GB of RAM
  - The 8b model is 3-5x faster but basically treats every message as a new conversation when there are 40 tool schemas in the context. OpenClaw sends the full message history (confirmed via logging: messages=16), so the problem isn't missing context. The model just can't follow it alongside those massive tool definitions.
  - Verdict(裁定，判决): qwen3:14b. Quality over speed for now.
  - The patch code is available as a GitHub Gist. Running this as a daily driver via WhatsApp and it's surprisingly capable for a 14b model.

- I am having looping tool call issues with glm 4.7 flash 8bit running on lm studio with mlx. I just ask open claw ‘use browser to open google.com’ and it goes into a loop. I have tried all sampling combinations but nothing works. Please help

- ## 🤔 [Why we went desktop and local-first for agents 6 months ago : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qr5v9d/why_we_went_desktop_and_localfirst_for_agents_6/)
  - We’ve been thinking a lot about first principles when building agent project, and one conclusion we keep coming back to is this: The first thing you should optimize for is the agent’s capability ceiling.
  - From that perspective, a desktop-first agent architecture makes a lot of sense. A few reasons why:
- Context access
  - If you want agents to be genuinely useful, they need real user context. On desktop, an agent can natively and seamlessly access local files, folders, running apps, logs, configs, and other artifacts that are either impossible or extremely awkward to reach from a purely web-based agent.
- Permissions equal intelligence
  - Powerful agents need powerful permissions. Desktop agents can read and write the local file system, control native software like IDEs, terminals, browsers, or design tools, and make system-level calls or interact with hardware. This isn’t about being invasive, but about enabling workflows that simply don’t fit inside a web sandbox.
- Web parity without web limitations
  - A desktop agent can still do everything a web agent can do, whether through an embedded Chromium environment or via browser-extension-style control. The reverse is not true: web agents can’t escape their sandbox.
- An often overlooked point is that desktop agents run on user-owned compute. Browsers, terminals, and local tools all execute locally, which significantly reduces backend costs and makes high-frequency, long-running agents much more viable.
- This line of thinking is what led us to build Eigent, the opensource alternative to cowork

- ## [现在高智商人群都是如何利用AI的?(咨询贴, 疑问句) _202507](https://linux.do/t/topic/779052)
- 我有时候写东西没思路了，会让AI给我多列几组提纲，然后从中选一组满意的，自己开始拓展写
  - 很少用它生成长文，太长了它就会有幻觉，甚至跑题，而且也不符合要求它做的原意

- 和网页版的区别是你可以用不同的提示词让ai去做不同的事情，比如翻译，归纳，润色邮件。

- 知识库坑更大……新技术层出不穷不说，都不成熟。单一个rag就够研究好久, 然后高质量的数据源又从哪来, 来了以后又如何处理这些数据片, 断最后才到高质量的ai能不能组合这些数据，得到你想要的东西几个都是大坑，都不完美，要达到生产力感觉甚至差得远。

- 帮你提升效率，自己核心竞争力保持住就可以了，搞钱才是王道 其他都是虚的

- ## [What are you building with sub-4B LLMs in early 2025? Real-world use wins? : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qewdza/what_are_you_building_with_sub4b_llms_in_early/)
- Been running a Qwen 2.5 3B on my Pi 4 for basic home automation - it parses voice commands from my cheap USB mic and controls lights/temp through Home Assistant API. Nothing fancy but beats yelling at Alexa when the internet's down
  - Works surprisingly well for stuff like "turn off bedroom lights" or "what's the temp upstairs" - just had to keep the vocab simple and train it on my specific device names

- a Raspberry Pi monitors IP cameras and sensors. A tiny LLM processes live feeds in real-time to detect intruders, leaks, or hacks alerting you via push notifications or automated responses (e.g., locking doors).

- We used https://huggingface.co/unsloth/gemma-3n-E4B-it-GGUF for an on premise Graph-RAG System and it worked pretty well. The Model showed promising results in not hallucinating with the right prompt and context.

- I previously looked at them for simple classification tasks, I am now using FunctionGemma in a Mobile App I am building as a function caller/info extractor where a LLM call is way overkill.

- ## [Why aren't more people using local models? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oj7ts7/why_arent_more_people_using_local_models/)
- Two reasons that I could think of:
  - Average consumer HW isn't just there yet to run something universally useful
  - Consumer mindset forbids to start doing things on your own
  - free time
  - Most people probably don't have the time, willingness or patience to get into the matter just far enough for using local models. The average user has no clue about how to compile llama.cpp and is also not intrigued to get into this. Things have changed a lot since the 80's.

- The problem with edge devices is simple. Battery life. Yeah, I can use a local model on my phone, and yeah, it works mostly relatively well. But I'm not willing to lose 20% of my battery on a short conversation

- Because graphics cards cost a kazillion dollars and you need 10 of them to get claude quality which is good enough but nothing less is..

- Because it's a huge pain in the ass and requires decently expensive hardware to do well.

- I love using local models and it's a great feeling having control over my privacy but honestly it's a fuckton of work. If you just wanna chat and load up LM Studio it's fine but if you want more you basically have to build everything yourself. Research mode, STT and TTS, RAG, MCP or tool use. All these are small building blocks you have to integrate yourself. It really gets messed-up if you also want these in your native language other than english. When showing my setup to my normie friends everyone quickly comes to the same conclusion.

- ## [We tried to automate product labeling in one prompt. It failed. 27 steps later, we've processed 10, 000+ products. : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qcsmww/we_tried_to_automate_product_labeling_in_one/)
  - We built an AI agent to localize imported food products for a retail client. The task sounds simple: extract product info, translate it contextually (not Google Translate), calculate nutritional values for local formats, check compliance with local regulations.
  - First attempt: one detailed prompt. Let the AI figure out the workflow.
  - Result: chaos. The AI would hallucinate numbers even with clean images. It would skip steps randomly. At scale, we had no idea where things broke. Every error was a mystery to debug.
- So we broke it down. Way down. 27 steps.
  - Each column in our system handles one thing: Extract name/weight/desc/...
- What changed:
  - 1. Traceability. When something fails, we know exactly which step. No more guessing.
  - 2. Fixability. Client corrects a number extraction error once, we build a formula that prevents it downstream. Errors get fixed permanently, not repeatedly.
  - 3. Consistency at scale. The AI isn't "deciding" what to do. It's executing a defined process. Same input, same process, predictable output.
  - 4. Human oversight actually works. The person reviewing outputs learns where the AI struggles. Step 14 always needs checking. Step 22 is solid. They get faster over time.
- The counterintuitive part: making the AI "dumber" per step made the overall system smarter. One prompt trying to do everything is one prompt that can fail in infinite ways. 27 simple steps means 27 places where you can inspect, correct, and improve.
  - We've processed over 10, 000 products this way. The manual process used to take 20 minutes per product. Now it's 3 minutes, mostly human review.
  - The boring truth about reliable AI agents: it's not about prompt engineering magic. It's about architecture that assumes AI will fail and makes failure easy to find and fix.

- This is case with 90% of real world AI use for non coding currently. It always requires human quailty control and intervention.

- Good example of human in the loop. I've been talking with my CEO about how the best use of LLM's at least for the foreseeable future will be wtih humans in the loop. The problem will always be getting humans to actually do the human in the loop process as the error rate begins to plummet.

- same attempt and result I had. Found Nemotron nano solved any output quality issues once it was all broken down.

- ## [Llama 3.2 1B Instruct – What Are the Best Use Cases for Small LLMs? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i4cfpz/llama_32_1b_instruct_what_are_the_best_use_cases/)
- Llama 3.2 1B Instruct can work as speculative decoding model for Llama 3.2-11B/90B or 3.3-70B.

- Code completion and autocomplete

- With a bit of fine tuning they can be really good at task specific things, including structured output (do not try llama 1b for structured output without fine tuning).
  - Long term my hope is local models built into the OS, with small task specific Lora adapters. iOS is doing it, but not open to 3rd parties yet.

- For research it's nice to have a dirt cheap model to prototype datasets when evaluating LLMs I usually use 8B for that though

- ## [Real world use cases for small LLM on edge devices : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1ffzsy0/real_world_use_cases_for_small_llm_on_edge_devices/)
- Small local models can make many factual mistakes, because it's impossible to compress the entire world model into 2 GB. However, they can be great analyzers (for their size) of the existing text.
  - Summarizing news articles, extracting insights from long web pages, finding a fact that you're searching for in a long text (a book?) and so on. Imagine it as a personal assistant in daily activities.

- Function calling. If it can do basic language to function translation, this is a perfect use. So it allows human voice or text interaction with complicated systems that would otherwise require custom coding. Also, text to structured responses, like using embeds or RAG to return well-defined SQL queries that might result from a wide variety of human specifications.

- All of these tasks involve LLM now, and are simple enough that they can be done on edge. In fact, most of them already do. Sure a cloud service can also do them, sometime better, but with a recurring cost that scale with usage. Most business that sell hardware, and user that buy it, will prefer the fixed upfront cost for R&D that small model.
  - OCR
  - Live transcription and translation
  - Summarization
  - Autocorrect
  - Basic voice control

- Analysis of secured data in offline mode . Maybe finance data , healthcare data , research data. Embed it on drone and check for suitable usecases

- ## [The curious case of Qwen3-4B (or; are <8b models *actually* good?) : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1p76wtf/the_curious_case_of_qwen34b_or_are_8b_models/)
  - how good are the smaller models at answering some of the sort of questions I might ask of them, chatting, instruction following etc?
  - I ran each model's output against the "council of AI elders", then got GPT 5.1 (my paid account craps out today, so as you can see I am putting it to good use) to run a tally and provide final meta-commentary.
  - The results, per GPT 5.1: GPT-OSS 20B and Qwen 3-4B emerged as the strongest overall performers. Mid-tier models like DeepThink 7B and Qwen 2.5 7B produced competent technical content but struggled severely with the style transform, while Phi-Mini 4B showed the weakest combination of accuracy, coherence, and instruction adherence.
  - The results align closely with real-world use cases: larger or better-trained models excel at technical clarity and instruction-following, whereas smaller models require caution for detail-sensitive or persona-driven tasks, underscoring that the most reliable workflow continues to be “strong model for substance, optional model for vibe.”

- I’m using qwen3-4b 2507 instruct for simple tasks such as meeting summarization, keeping track of to-do’s and the likes. So far, it has performed quite well

- ## [My Journey to finding a Use Case for Local LLMs : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1p1xy0q/my_journey_to_finding_a_use_case_for_local_llms/)
  - I have a lot of phone pictures of recipes, and a lot of inherited cookbooks. The thought of gathering the ones I really liked into one place was daunting. The recipes would get buried in mountains of photos of cats (yes, it happens), planes, landscapes etc. Google photos is pretty good at identifying recipe images, but not the greatest.
  - I landed on qwen3-vl:8b. It was able to take the image (with very strict prompting) and output the exact text from the image. I did have to verify and do some editing here and there. I was happy
  - I then turned to GPT-OSS:20b since it is newer, and asked it to convert the recipe text to json-ld recipe schema compatible format.
  - Now I can take a pic of any recipe I want, run it through the qwen-vl:8b model for OCR, verify the text, then have GPT-OSS:20b spit out json-ld recipe schema text that can be imported into the mealie database. (And verify the json-ld text again, of course).
  - I'm not using any system prompts at this time. Here is the prompt

- You could now take this even further and query it with a prompt on your cell phone.

- My use case is that I use local vlm to the content of the download file, then rename following the format I define and use bash script to route it to the its dedicated folder. Now every time a file is downloaded, it is renamed and route to its location automatically.
# discuss-local-llm-xp/tips
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🧭 [Google Chrome secretly installed Gemma 3 and 4 on a billion PCs and Macs, it's called weights.bin, a 4gb file for your RAM. : r/LocalLLM _202605](https://www.reddit.com/r/LocalLLM/comments/1t6vhyx/google_chrome_secretly_installed_gemma_3_and_4_on/)
- You don't need to delve into chrome://flags. Settings -> System -> On-device AI

- Gemini Nano, not Gemma. Not new. Chrome has had this for a while. It powers the prompt API and no, it doesn't send anything back to the mothership.
  - Prompt API allows websites to use the LLM via JavaScript. For translations, summary, voice decoding etc.

- If you still use chrome, you don’t mind about bloat and spyware so whats the point?

- my weights.bin file date shows up as 31-Dec-1979 5:00pm version ...seems very strange
  - That's just a placeholder or epoch date used by the file system. Happens when the file metadata is corrupted or missing.

- [4GB "Gemini Nano" model GGUF anyone? : r/LocalLLaMA _202605](https://www.reddit.com/r/LocalLLaMA/comments/1t72aui/4gb_gemini_nano_model_gguf_anyone/)
- Gemini Nano is based on a custom variant of one of the smaller Gemma 4 models. It was mentioned in some Google/DeepMind blog post when Gemma 4 came out.
  - Still not Gemma 4 afaict

- It you can use it locally by writing javascript in the browser

```JS
const session = await LanguageModel.create({ outputLanguage: "en" });
const reply = await session.prompt("what model are you");
console.log(reply);
```

- You can test it with: chrome://on-device-internals

- ## [关于大模型对于中文字数的理解  - LINUX DO _202603](https://linux.do/t/topic/1773860)
- 反正玩酒馆的时候发现，AI并不能掌控自己到底输出多少字，更有效的prompt是要求大概的tokens数或每一段落大概多少多少字，一共字数在哪个范围。大模型只能估算，没办法实际去计数。

- 是的. 只能给区间. 大模型好像默认只能发散, 聚拢必须要通过推理.

- ## [Small LLMs seem to have a hard time following conversations : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1rn7362/small_llms_seem_to_have_a_hard_time_following/)
- 4B quants might be the bigger culprit(问题的起因; 罪犯) than the model size here. Especially if the KV cache is quantized as well.

- Use a structured prompt. Instead of a raw copy-paste, wrap the chat in XML tags. It helps the degraded 4-bit attention mechanism focus on the actual logic

- Another option is write a quick python script to break conversation into chunks and clear context between each chunk. Small model focuses on one chunk at a time and writes a short “compressed” summary for itself. Then the final instantiation of the model just looks at all the summaries.
  - Or alternatively you could use something like GPT-5-mini over API (if conversation not sensitive) to do the original large context summarization then pass it off to a smaller local model. 5 mini is so cheap you would have to purposely trying to run up your bill to be surprised. I use it for OpenClaw and end up paying a few bucks a month typically.

- ## [3 weeks of running qwen2.5:14b in an agentic loop - context management is where everything breaks : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1rcdicv/3_weeks_of_running_qwen2514b_in_an_agentic_loop/)
  - I've been running qwen2.5:14b locally for about 3 weeks as part of an automation pipeline - not chatting with it, but using it to actually do things: read files, make decisions, call tools, write outputs. The hardware part worked fine. What I completely underestimated was context management.
  - The problem isn't that local models are bad at long contexts. Qwen handles 128k tokens on paper. The problem is what happens to quality as you fill that window. Around 60-70% capacity, the model starts ignoring things it read earlier. It doesn't fail loudly - it just quietly forgets constraints you set at the top of the prompt. You get plausible-looking output that misses requirements you specified 10, 000 tokens ago.
  - I caught this because the pipeline was producing outputs that were technically correct but violated a formatting rule I'd set in the system prompt. Took me two days to figure out it wasn't a logic error - it was just the model not "seeing" the beginning of its own context anymore.
  - The fix that actually worked: aggressive context pruning between steps. Instead of one long running context, I reset between major task phases and re-inject only what's essential. It felt wrong at first - like I was throwing away useful state. But the consistency improvements were immediate and obvious.
  - The other thing I didn't expect: streaming matters for pipeline latency in a non-obvious way. If you're not streaming and you're waiting for a 2000-token response, you're blocking everything downstream. Obvious in hindsight, but I had batch mode on by default and it was creating weird bottlenecks.
  - The model itself is genuinely good. On structured reasoning tasks with a clear prompt, it rivals what I was getting from API calls a year ago. The failure modes are just different from what you'd expect if you've only ever used it interactively.

- yeah this tracks hard with what we've seen. we run a similar setup and the context degradation thing is real, it's so subtle too because the outputs still look reasonable until you realize key constraints from your system prompt just evaporated.
  - one thing that helped us beyond pruning was adding a lightweight "context health check" between steps. basically a quick validation pass where the model confirms it can still recall the 3-4 most critical constraints before proceeding. catches the drift way earlier than waiting for bad outputs.

- Either using multiple agents with specific roles like summarizing and replying fixes this, or using memory like a library to craft a reasonable context for the model.

- I’ve noticed something similar across near enough every model (instruct/thinking) I have used regardless of (harness/scaffolding).
  - Around 60k to 90k tokens into agentic coding, the likelihood of success diminishes significantly.
  - Much better to kill it and start a new session. 
  - Another alternative is to consistently break a large problem into smaller pieces and run those smaller pieces in their own session.
  - TLDR - avoid exceeding beyond 60k tokens in a single agentic coding session window.
  - Break the problem down and use multiple sessions under 60k tokens instead.
  - use plan mode to build markdown files, so that the independent session builds with integrate properly.

- ## Something that’s remarkable easy and high ROI now:
- https://x.com/GrantSlatton/status/2025311598735491250
  - When I write a really tricky algorithm in our codebase, I can have my LLM whip up a pretty HTML / JS visualizer to give future readers a visual intuition for it, 3blue1brown style, and commit that to the repo alongside the algo

- Interesting but now you have to maintain both the visualisation and the logic and keep them in sync. If i dont understand anything in a codebase i just ask it to visualise it on the fly, imo that is a better approach

- have you tried beautiful mermaid diagrams? someone should turn it into a way to create it into movies/slideshow so you can get introduced to a large codebase by navigating it and then have that section of the codebase be narrated to you and then visually shown

- ## 我觉得 AI 编程的发展有些像现在的编译器，普通人不需要关心它的实现，
- https://x.com/dotey/status/2019918867812757556
  - 只要用高级语言描述清楚自己想要的，编译器会帮助把编程语言编译成机器代码；以后人类用自然语言，AI 翻译成编程语言，人类不需要关心其中的细节，只要验收结果就好
- 编译器的输出是确定的，但LLM不是
- chatgpt以后就类似于Windows，是操作系统，你用软件完全不应研究内部咋实现的

- 完全同意编译器这个类比。但现在的关键瓶颈不是AI翻译能力，而是人类描述需求的精度。我做产品用 Spec 驱动开发（先写文档再写代码，文档: 代码比 3.6:1），发现越精确的 Spec 给 AI，出来的代码质量越高。自然语言编程的前提是结构化自然语言。

- 代码逻辑的复杂度不会消失，计算机发展的过程就是不断提高抽象层的过程。

- 宝玉老师是前端吧。后端或者服务型是要跑很多年的，不是什么月抛年抛的
  - 大部分没有复杂业务的curd没有任何护城河。复杂点的云计算，openstack k8那一坨，大家都玩了这么多年了，gayhub上一大堆。
- 你们眼里的后端就是云计算和crud吗？

- ## [I admit it… I underestimated the quality of local models : r/ClaudeCode _202602](https://www.reddit.com/r/ClaudeCode/comments/1qwkyx6/i_admit_it_i_underestimated_the_quality_of_local/)
  - The context size you can configure in the Windows app for Ollama has a global impact on the VRAM used by the models, and because of that I had basically made models like QWEN3-CODER or GPT-OSS:20b unusable.
  - Today, by chance, a friend told me I was wrong and to reduce the context to 48 KB and try again with the two models I mentioned above.
  - Surprise… they now run at 100% GPU, and despite the smaller context, they’re really making me change my mind.

- 48K context handles most coding tasks fine. Bigger windows don't automatically mean better output... there's a well-documented attention curve where models track info best at the start and end and lose grip on stuff buried in the middle.
  - But the thing nobody here is bringing up is KV cache. Ollama supports KV cache quantization now (q8_0), and that's what actually eats your VRAM as context grows, not the model weights. With q8_0 you get roughly half the KV cache memory cost with almost no quality loss.
  - So the real question isn't what context size to pick. It's whether you're tuning context size and cache precision independently. For small app work, 32K context with q8_0 KV quant on a 20B model is probably the sweet spot. Enough window for a full file plus surrounding context without starving the model of compute.

- ## We've been exploring the value of letting agents use CLIs vs just navigating a REST API directly. 
- https://x.com/dhh/status/2012543705161326941
  - The smartest models can do without a CLI, but take longer and cost more. Even small models can succeed when given CLIs. But the puck keeps moving!
- AI does better with CLIs because it's a human interface. It's designed with self-discovery in a logical way. 

- We realized this very early on. Our first party integrations with Ci providers are clis we purpose built for our vertical agent workflows. Mcps are terribly inefficient even if tools are lazy loaded for multi turn agentic conversations

- Everyone who’s been early to using coding agents, figured this out a few months ago

- Yeh my personal assistant is all CLI driven (a cli for open code to use, so I say "Plan out my day" and it goes and uses it to do that).  Super useful.  At @agentuity , we've really had to make sure our sdk, api's, and CLI are FOR agents as much as developers. Mindshift change.

- Using the same CLI for both humans and agents turned out to be surprisingly practical.

- The CLI abstraction buys you something else too: versioning. REST APIs change endpoints, parameters, auth flows. A stable CLI surface means your agent skills don't break when the underlying API shifts. That durability matters more as you scale agent count.

- This is why I recently converted my Basecamp MCP connector to a Basecamp CLI.

- ## [I benchmarked 7 Small LLMs on a 16GB Laptop. Here is what is actually usable. : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pzxtnr/i_benchmarked_7_small_llms_on_a_16gb_laptop_here/)
  - I tested Qwen 2.5 (14B), Mistral Small (12B), Llama 3 (8B), and Gemma 3 (all 4-bit quants) to see which ones I could actually run without crashing my laptop.
  - Qwen 2.5 (14B): The smartest for coding, but it eats 11GB System RAM + Context. On a 16GB laptop, if I opened 3 Chrome tabs, it crashed immediately (OOM).

- They are all ancient models by llm age so its kinda an invalid test. The king of low spec ram is mamba2 and sliding window attention. Try Granite 4, or Nemotron Nano 2

- I'm not considering 1-2 tokens/s "usable". Even 10 tokens/s is barely usable for the most part.

- ## [I'm curious whether people ask for the model's name in their prompts when testing on LMArena (ChatBot Arena). : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jtfzci/im_curious_whether_people_ask_for_the_models_name/)
  - After all, by doing this, users can know the names of the models being A/B tested beforehand, which could bias the ongoing test to some extent.

- Models never know a thing about themselves; no serious LLM user in 2025 will ask model about itself.

- well, the model's output might not be correct at all: deepseek sometimes call itself gpt. so you never now who these models actually are.

- ## [Hard lesson learned after a year of running large models locally : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pvxq2t/hard_lesson_learned_after_a_year_of_running_large/)
  - I’m running everything off a workstation with a single RTX 3090, Ubuntu 22.04, llama.cpp for smaller models and vLLM for anything above 30 B parameters.
  - My goal has always been to avoid cloud dependencies and keep as much computation offline as possible, so I’ve tried every quantization trick and caching tweak I could find.
  - The biggest friction point has been scaling beyond 13 B models.
  - My takeaway so far is that local first inference is viable for small to medium models, but there’s a hard ceiling unless you invest in server grade hardware or cluster multiple GPUs.
  - Quantization helps, but you trade some quality and run into new bugs.
  - For privacy sensitive tasks, the trade‑off is worth it; for fast iteration, it’s been painful compared to cloud based runners.

- vLLM works great if model + context fit into VRAM, but it doesn't do CPU offloading well - use llama.cpp for anything that spills over to RAM.

- instead of trying to use "smarter bigger" models to achieve whatever youre trying to achieve, its more reliable to use multiple parallel instances (via vllm for example) of smaller model that can communicate with each other in distinct roles to create a system that produces accurate results.

- You can also rent a card in the cloud for near local inference.

- ## [Useful patterns for building HTML tools _202512](https://simonwillison.net/2025/Dec/10/html-tools/)
- https://x.com/vista8/status/2003803470449787263
  - 用大模型两年做了150个工具。这不奇怪，强的是他只用单页HTML做！
  - 一个 HTML 文件，打开就能用，不需要安装，不需要注册。
  - 他特别强调 "不要用 React"。 因为 JSX 需要构建，这会让整个流程变得麻烦。 保持简单，就是保持可维护。
- 优势也很明显：
  - 可以直接从 ChatGPT 或 Claude 里复制粘贴出来
  - 扔到 GitHub Pages 上几秒钟就能用
  - 不需要 npm，不需要构建步骤
  - 两年后还能打开，不会因为依赖过期崩溃
- 状态存在哪里？ 没有后端数据库怎么办？Simon 有两个办法：
  - 把状态存在 URL 里。 比如，他做了一个 24x24 的图标编辑器，你画的图标直接编码在 URL 里。这样你可以收藏，可以分享，打开链接就能继续编辑。
  - 把关键的信息存在 localStorage 里。 比如 API key 这种敏感信息，不能出现在 URL 里，也不能发到服务器。 localStorage 让数据只存在用户的浏览器里。 他还用 localStorage 做自动保存。 写字数统计工具时，每次输入都会保存，这样不小心关掉标签页也不会丢内容。
- CORS（跨域资源共享）听起来很技术，但理解它很重要。
  - iNaturalist 可以查动物的观察记录
  - PyPI 可以获取 Python 包的信息
  - GitHub 的公开仓库内容都可以直接获取
  - Bluesky 和 Mastodon 的 API 也很开放
  - Simon 甚至用 GitHub Gists 来持久化数据。 因为 Gist 的 API 支持 CORS，你可以做一个纯前端工具，把用户的数据保存到他们自己的 Gist 里。
- 文件不需要上传 `<input type="file">` 不只是用来上传文件。 JavaScript 可以直接读取文件内容，在浏览器里处理。
- Python 和 WebAssembly 这是最让人兴奋的部分。 Pyodide 让 Python 可以在浏览器里运行。
  - 不是玩具级别的运行，是真正的 Python，包括 Pandas 和 matplotlib。
- Tesseract OCR、SQLite、图片压缩库，这些原本用 C 或 C++ 写的软件，现在都能在浏览器里跑。
- 这些工具真可以解决问题。更重要的是，这种方式让你能快速实验。想法到原型可能只需要几分钟。不用担心部署，不用担心维护，不用担心成本。
- 怎么起步尝试？ 一个 GitHub 仓库，开启 GitHub Pages。 然后就可以开始了。 用 ChatGPT 或 Claude 生成一个工具，复制粘贴到仓库里，几秒钟后就能在网上访问。 不需要完美，不需要复杂。 从一个解决你自己问题的小工具开始。 然后慢慢积累，慢慢改进。 两年后你可能也会有几十个甚至上百个这样的工具。 每一个都在某个时刻帮到你，每一个都让下一个更容易做出来。
- 这就是 HTML 工具的魅力：简单、实用、可持续。

- ## [Senior engineer struggles with learning LLMs foundations : r/LLMDevs _202512](https://www.reddit.com/r/LLMDevs/comments/1plxnq0/senior_engineer_struggles_with_learning_llms/)
  - I've been using ollama and openai to create some interesting side projects and to learn more about LLMs, but I think I'm hugely lacking solid foundations. Please provide me with a structure learning material for a senior engineer with some knowledge of LLMs, thanks
- Andrej Karpathy’s series on YouTube and Stanford’s CME course on LLMs and Transformers which is published to YouTube for free.
  - I had a quick look at the Stanford's course and I think it's exactly what I needed, thanks

- You need to learn four critical things
  - Your agent's core product logic is the prompt/instructions you send to an LLM. You will be spending time here with domain experts too to construct good instructions so that the model aligns to your policy. There is no magic bullet. You iterate and evaluate until you are satisfied. Making investments in evals is worth it.
  - If you want to build an agentic application, then you need to expose tools to different models. These are essentially APIs that you have today, both internal or external which the model will instruct you to run and return its results as string. 
  - There are two agentic loops, one is called the inner loop where you agent interacts with an LLM until the LLM is done (stop_reason=finish). There is an outerloop which runs to route traffic to/from agents (if you have a multi-agent architecture), ensure that only good traffic is reaching your agents and that if multiple agents need to be engaged it would be handled outside your core product logic.
  - You need exceptional observability to know what happens, how things fail, etc. And you need to account for different models in your stack so that you can easily improve performance, and/or latency and/or cost.

- ## [和AI对话，不要使用“你” ](https://linux.do/t/topic/1293395)
- AI 大神 Karpathy 分享了一个反直觉的观点：跟大模型聊天时，不要使用 “你” 这个字，也就是不要把它们当 “人”。
  - Karpathy 指出，这种问法其实是在给 AI 降智。因为 LLM 本质上并没有自我意识，它更像是一个拥有海量知识的模拟器。
  - 当使用 “你” 这个字的时候，比如问 “你的看法”，模型就会立刻被触发一种特定的人格嵌入。
  - 它会强行让自己扮演一个礼貌、安全但有点无聊的 AI 助手。这时候它吐出来的往往是那些四平八稳、滴水不漏，但实际上没啥深度的车轱辘话，也就是大家常说的 “Al 味”。
  - 相反，Karpathy 建议我们要转变思路，要想解锁 AI 真正的实力，就把 AI 当成模拟器用。
  - 举个例子，不要问 “你怎么看”，而是要设定具体的情境和角色。你可以问 “如果是三位资深产品经理坐在一起讨论这个功能，他们会提出哪些尖锐的批评”，或者 “请以一位诺贝尔经济学奖得主的视角分析这个现象”。
- 评论区也有不少高手补充，不仅要少用 “你”，也要少用 “我”。
  - 因为当你表达 “我觉得.” 的时候，AI 为了讨好用户，往往会顺着你的话说，这就导致了所谓的阿谀奉承现象，而不是基于客观事实给出答案。
- 下次写提示词的时候，试试戒掉 “你” 和 “我” 这两个字。让 AI 去模拟那些具体的专家、团队甚至反方辩手，你会发现它的回答质量能提升好几个档次。

- 那么比如 “你是一个物理学领域专业人士”、“你是一个穿小裙子的算法高手”、“你是一个猫娘” 的 prompt，到底该不该用呢？以前我看很多人鼓励在需要特定工作场景时这么做，这里面有你，但是指定了人格的类型
  - 我也在想这个问题，可以改写成 “作为一个 xxx”，“扮演一名 xxx”，然后后面全部用祈使句试一下
- “你” 的话感觉是已经指定了一个人，而用 “请以” 的话感觉会从该领域中每个人不同视角来思考，可能会更全面一点？

- 省流，多用角色扮演法。 此事在脑筋急转弯中亦有记录。 非思考模型你直接提问 脑筋急转弯类型的题目 大多模型很可能被欺骗。 但你强调这是脑筋急转弯， 让他去扮演类似领域的高手， 即使是非思考模型也能破解陷阱

- “你是一个专业的 swift 程序员”  →  “请作为一个专业的 swift 程序员，xxxx” 这么理解对吗

- 这些技巧直接调用 api 效果最明显吧？网页版的大模型和其他工具里调 API，基本都预设了角色。即使不用第一二人称，效果提升也不大吧？

- ## [8 local LLMs on a single Strix Halo debating whether a hot dog is a sandwich : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pdh0sm/8_local_llms_on_a_single_strix_halo_debating/)
  - https://github.com/lemonade-sdk/lemonade
  - Lemonade v9.0.6 came out today, making it really easy to run many models at the same time... and this is the best demo I could think of. Hope it makes someone laugh today!
  - This is a Ryzen AI MAX 395+ (aka Strix Halo). The models are between 3 and 8B parameters (size on disk is visible at the start of the video).
  - Lemonade is a free and open local LLM server made by AMD to make sure we have something optimized for AMD PCs. Today we released a new version that lets many LLMs run at the same time.
  - I made this quick HTML/CSS/JS app to demo the capability. It loads 8 LLMs, has them share a chat history, and then keeps prompting them until they vote yes or no on the user's question.
  - In the backend, there are 8 llama-server processes running on the Strix Halo's GPU. The web app talks to lemonade server at http://localhost:8000, and then lemonade routes the request to the right llama-server process based on the model ID in the request.
  - I thought it was funny the LLMs couldn't come to a final decision on this question. Just like people!

- A tie? That's no good. There should have been 9 LLMs, like the Supreme Court.

- Are they debating each other? Seems like they don’t spend much time disagreeing. I want to see one where they are forced into consensus or it doesn’t end (or maybe time it out and score it then)
  - There’s 5 rounds of debate. First round they are supposed to give a hot take. Rounds 2 and 3 they’re supposed to react to each other (shared chat history). Rounds 4 and 5 they’re supposed to vote.

- ## ["We're in an LLM bubble, not an AI bubble" - Here's what's actually getting downloaded on HuggingFace and how you can start to really use AI. : r/LlamaFarm _202512](https://www.reddit.com/r/LlamaFarm/comments/1pb2wr2/were_in_an_llm_bubble_not_an_ai_bubble_heres/)
  - Encoder-only models (BERT family) account for 45% of HuggingFace downloads, nearly 5x more than decoder-only LLMs at 9.5%. 
  - Every one of these model families exists because someone realized the "one model to rule them all" approach was failing for their use case
  - This is "Mixture of Experts" at the application level. Many small, specialized models working together instead of one massive model trying to do everything.

- ## [What broke when you tried to take local LLMs to production? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p91p4k/what_broke_when_you_tried_to_take_local_llms_to/)
- Ollama broke a lot of the time because we dev’d on a Mac but pushed production to nvidia. Switching to vllm has largely solved this and pushed it to more of an interface rather than model problem.

- Hosting several Models on one GPU is always really annoying with vLLM. You basically have to fiddle with the memory utilisation until all models fit. There is no clean way I found to calculate memory usage. You just have two tweak, boot, look at the logs and repeat. And even if you got all models to fit, vLLM sometimes crashes with cuda out of memory exceptions when loading the models since there seems to be a peak in memory consumption on boot up.

- Why doesn't anyone mention tabbyAPI/exllamav3? It's much more memory-efficient than AWQ, also it loads quicker, and the quantization is more optimized. Also K/V cache can be quantized between 2 and 8 bits seperately (=more room for context)

- ## [Why do you use open-source LLMs ? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p16kxx/why_do_you_use_opensource_llms/)
- Freedom. I can do whatever I want without having my data stolen.

- The benefit of open source LLMs for me is that you can access the internal layers to do things like attention injection, intermediate layer feature extraction, attention map extraction, token-wise early stoppage, adaptive layer skips, conversion to latent attention, conversion to mamba or gated delta net hybrid etc
  - This is it. Intervening mathematically in something that can talk like a human is an otherworldly experience. I do it almost every day and it makes me feel like an alchemist tinkering with a homunculus. There’s nothing else like it. Most other intellectual activities feel shallow by comparison.

- I just think it's very cool to have a summary of the vast wealth of human text and knowledge in a 30GB file on my computer.

- I want to own my capabilities. I don’t want my coding skills to be tied to some external service that I have zero control over.

- ## [What do you use local LLMs for? What is your use case? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1ms4gmz/what_do_you_use_local_llms_for_what_is_your_use/)
- They are best used for small context tasks like classification/sentiment, asking it summarize, pull out keywords, grammar, etc.
  - Not for long conversations or complex tasks, but system prompt, user request, and then get a single response.
  - For example, I've been experimenting with a local LLM checking chat messages for rule-breaking in a Discord server, flag the suspicious once, and then I checked the flagged messages and take action myself.

- I used it to generate a synthetic dataset for training my first neural network, with successful results.

- Structured data extraction from private documents (millions of documents)
  - We have produced an annotated dataset of a few thousand records. We used this to fine tune a model and evaluate performance. We are getting >0.98 F1 score which is a margin of error we are willing to tolerate given the scale and time saved... It's for a very specific type of short documents. Our extraction pipeline has multiple extraction and validation steps.

- Data extraction and classification.

- ## [What are you using your local models for ? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oz6k5j/what_are_you_using_your_local_models_for/)
- Confidential research. In SillyTavern. Just yet with a quantized Skyfall-31b from Drummer, apparently some blend of Mistral Small or whatever. It's fun.

- Qwen3-VL-30B-A3B-Thinking is heating my home by processing video. I've posted about it before but llm-ffmpeg-edit.bash handles the logic & llm-python-vision-multi-images.py handles sending the images/frames to the LLM backend.
  - I was using Mistral 3.2 (24B dense) before Qwen3-VL got support. The speed increase from 24B -> 30B-A3B has been incredible, while maintaining accuracy.

- I'm bound by the legal terms of my employment to not discuss the technologies we use there, but am free to talk about my personal use-cases.
- STEM research assistant -- I give it my technical notes (usually physics and/or math) and a question, and get back helpful replies. My go-to is Phi-4-25B, and when it's not smart enough I escalate to Tulu3-70B, sometimes Qwen3-235B pipelined with Tulu3-70B.
- Creative writing -- Cthulhu-24B, Big-Tiger-Gemma-27B-v3, or Valkyrie-49B-v2. Mostly sci-fi (space opera or Murderbot fanfic).
- Evol-Instruct and synthetic dataset generation or augmentation -- again, mostly Phi-4-25B or Tulu3-70B, though recently I have been using Valkyrie-49B-v2 to bulk up a RAG database of technical troubleshooting advice/solutions. To my surprise Valkyrie is a lot better at this than Tulu3-70B, even though they are derived from similar models (Tulu3 from Llama-3.1, Valkyrie from Llama-3.3-Nemotron-Super-49B-v1.5 which in turn is based on Llama-3.3).
- Persuasion research -- studying the capacity for LLM inference to change people's minds. Big-Tiger-Gemma-27B-v3 is excellent at this.
- Wikipedia-backed RAG for general question-and-answer. I use Big-Tiger-Gemma-27B-v3 for this as well.
- Describing images so I can index them in a locally hosted search engine. Qwen2.5-VL-72B is still the best vision model I've yet used, but I haven't had a chance yet to compare it against Qwen3-VL-32B. I am hoping Qwen3 is better, despite having fewer than half as many parameters.
- I also run an IRC bot for a technical support channel, which is mostly GOFAI-driven but I've been working on a plugin for it to be RAG/LLM-driven too. That, too, uses Big-Tiger-Gemma-27B-v3.
- Recently I've been trying to use Phi-4 (14B) as a synthetic dataset rewriter, to salvage low-quality inferred data I would normally prune from the dataset. I read a paper suggesting even very small models (4B) are effective at this. So far my results have been mixed. I've been meaning to try Tiger-Gemma-12B-v3 as well; possibly Phi-4 just isn't the right model for this.
- GLM-4.5-Air for slow inference of entire programming projects (which I don't do much, since I don't want my coding skills to atrophy) or to find bugs in my own code.
- Qwen3-Coder-REAP-25B-A3B for fast FIM code inference. The model doesn't have to be smart to figure out what my "for"-statement is going to look like, but it does need to be fast enough that it can suggest a completion before I've finished typing the "for"-statement myself. I use the REAPed version of this model so that it fits in my GPU's VRAM (at Q4_K_M); the original 30B-A3B didn't quite fit.
- I'm also tentatively using Phi-4 as a judge, comparing two replies to the same prompt and telling me which is better. It's early days yet, for this project, and it might not be the right model for this. We will see.
- Sometimes I use Big-Tiger-Gemma-27B-v3 or Phi-4 (14B) for language translation (mostly Spanish to English, but sometimes German or Russian to English). Overall Big Tiger is better at this, though Phi-4 does surprisingly well, and is better than Big Tiger at taking situational context into account with its replies. It's also a lot faster than Big Tiger, which is sometimes important for translation tasks.

- ## [Are any of you using local llms for "real" work? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1otnj2k/are_any_of_you_using_local_llms_for_real_work/)
- The most "real" work I've done is that Qwen3-VL-30B-A3B-Thinking is currently going through videos 10-seconds at a time. 
  - Based on the bot's True/False boolean output a wrapping program keeps track of what segments `<thing I'm looking for>` is within. At the end, we're done using Qwen3-VL and the wrapping program uses the segment information to use FFMPEG to make a clipped version where `<thing I'm looking for>` should always be present.
  - A general example is you could have the bot look for every explosion in an action film. Maybe it considers muzzle flash from a gun to be an explosion, not technically wrong as far as I know. So you could prompt that it should only be explosions not from gunfire and try that.

- I use an LLM, a scraper to fetch security vulnerabilities (CVEs), and an internal API that lists my running services, and the LLM generates a daily report for me about whether any of the software I'm running might have been mentioned.

- Using qwen3 vl to parse vids to extract car plate numbers snd other vehicle markings

- I used a local LLM and a vector database to help me with my corporate taxes. I first fed all past 3 or 4 years of expenses along with their categorizations (meals, fuel, office supplies etc.) into a Postgres PG Vector database and embedded the data using the Nomic model. I then classified several hundred transactions for the past tax year using this vector set of data to categorized the transactions.

- I use nvidia/Llama3-ChatQA-1.5-8B to index 2M similar insurance docs using ollama. I load the index into Meilisearch and sell access to it. I did this after a trip to micro center and a little over $3k.

- I use them as zeroshot NER/Classification models. They're pretty decent at it out of the box. Training isn't too complicated, but for small repetitive tasks, they're often good enough.

- ## [Why we shifted to Spec-Driven Development (and how we did it) : r/ClaudeCode _202511](https://www.reddit.com/r/ClaudeCode/comments/1op8b6i/why_we_shifted_to_specdriven_development_and_how/)
  - Over the last few months we came up with our own Spec-Driven Development (SDD) flow that we feel has some benefits over other approaches out there. 
  - Specifically, using a structured execution workflow and including the results of the agent work. 
- In short: you design your docs/specs first, then use them as input into implementation. And then you capture what happens during the implementation (research, agent discussion, review etc.) as output specs for future reference. 
- The cycle is:
  - Input specs: product brief, technical brief, user stories, task requirements.
  - Workflow: research → plan → code → review → revisions.
  - Output specs: research logs, coding plan, code notes, review results, findings.
- By making the docs (both input and output) first-class artifacts, you force understanding, and traceability. The goal isn’t to create a mountain of docs. 
  - The goal is to create just enough structure so your decisions are traceable and the agent has context for the next iteration of a given feature area.
- First, worth mentioning this approach really only applies to a decent sized feature. Bug fixes, small tweaks or clean up items are better served just by giving a brief explanation and letting the agent do its thing.
- How we implemented it (step-by-step)
  - Define your prd.md **:** goals for the feature, user journey, basic requirements.
  - Define your tech_brief.md: high-level architecture, constraints, tech-stack, definitions.
  - For each feature/user story, write a requirements.md file: what the story is, acceptance criteria, dependencies.
  - For each task under the story, write an instructions.md: detailed task instructions
  - To start implementation, create a custom set of commands that do the following for each task
  - Commit these spec files alongside code so future folks (agents, humans) have full context.
  - Use folder conventions: e.g., project/story/task/requirements.md, …/instructions.md etc. So it’s intuitive.
- Bonus: If you want a tool that automates this kind of workflow opposed to doing it yourself (input specs creation, task management, output specs), I’m working on one called Devplan that might be interesting for you.

- Bmad does exactly this: https://github.com/bmad-code-org/BMAD-METHOD

- have you tried any of BMAD, GitHub/Spec-kit or Privacy-AI/spec-kitty for a community fork with extensive git worktree support

- ## [Which model do you wish could run locally but still can’t? : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1omoodc/which_model_do_you_wish_could_run_locally_but/)
- It's not really about particular models at this point. I'm way more interested in the local infrastructure around it. The main thing I'm still missing is simple knowledge-base integration for something like Open-WebUI. I would really like to just point the front-end at my local Kiwix-server and a 1TB-eBook collection, let it index to its heart's content for a few weeks and then have any model be able to reference and integrate all those information.

- Qwen3 Omni, how come no one is talking about a 30B model that can do video and speech?

- Something which I can install with just a dmg or exe file please
  - I tried a couple but I am not tech savvy and had to install a lot of other stuff to my laptop

- For me, it’s not that it’s a single model I can’t run… it’s the fact that I can’t run multiple models.

- ## [What's the missing piece in the LLaMA ecosystem right now? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o5dh3v/whats_the_missing_piece_in_the_llama_ecosystem/)
  - For me, it's the data prep and annotation tools. The models are getting powerful, but cleaning and structuring quality training data for fine-tuning is still a major, manual bottleneck.

- Training-Data is the biggest issue for local ecosystem right now i think. There is so many datasets, but who knows about their real quality.
  - For me personally, finetuning an LLM is like 500x harder than a diffusion model, simply due to the lack of tooling. Unsloth is nice and all, but i dont want to run fucking Jupyter Notebooks, i want something akin to kohya_ss with as many of the relevant hyperparameters exposed.
- Hardware accessibility is only secondary. If you have a small Model, e.g. the Qwen3 0.6B full finetune should be possible on local hardware. If that proves to be effective, renting a GPU machine somewhere for a few bucks shouldnt be the issue.

- llms are very bad at image recognition, give it a civ or other strategy game screenshot and it gets nearly everything wrong.

- Benchmarks. There has been little to no progress in the past two years regarding how LLMs are evaluated. It’s still mostly huge catalogues of questions with predetermined answers. That’s a very poor system for testing intelligence.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
