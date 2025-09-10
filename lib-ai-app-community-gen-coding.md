---
title: lib-ai-app-community-gen-coding
tags: [coding, community, large-language-model]
created: 2025-09-01T07:58:14.529Z
modified: 2025-09-01T07:58:29.058Z
---

# lib-ai-app-community-gen-coding

# guide

- tips
  - 🤔 模型选择: 不用纠结是否要用thinking/reasoning模型，参考成熟的方案来选架构和改进
    - thinking+coding(单模型方案) vs plan+coding(双模型方案), 可参考流行工具的默认值
  - 🤔 工具选择: 不必纠结于工具cline/aider, 模型能力提升后，工具里的体验也会自动提升
    - github copilot扩展开始支持本地model了
    - 甚至针对场景的微调模型，如ios/android, mobile-responsive
  - 🏠 continue.dev相对于cline/aider更擅长inline-autocomplete, 但架构设计可以参考rag/embedding/rerank

- leaderboard-coding
  - [SWE-rebench Leaderboard](https://swe-rebench.com/leaderboard)
  - [SWE-bench Leaderboards](https://www.swebench.com/)
  - [Aider LLM Leaderboards](https://aider.chat/docs/leaderboards/)
  - [LiveSWEBench](https://liveswebench.ai/)
  - [Evals | Roo Code](https://roocode.com/evals)

- leaderboard-pm
  - [LLM Rankings | OpenRouter](https://openrouter.ai/rankings?view=month)
# discuss-stars
- ## 

- ## 

- ## 

- ## [My experience trying out coding agents -- Qwen2.5-coder-tools/Sonnet 3.5 on Cline and Github Copilot agent mode : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ilza8m/my_experience_trying_out_coding_agents/)
  - trying out the preview copilot agent feature against cline using both a specialized version of Qwen2.5 through Cline and the Sonnet 3.5 (copilot API) through Cline and copilot

- For aider at least, benchmarks show the absolute best way to use it is with a reasoning model like r1 as the architect and sonnet 3.5 as the coder. Curious to see if that helps you and jumps over the usefulness / competency barrier for your usecase. 
  - Just `aider --architect --model r1 --editor-model sonnet` should work after configuring relevant APIs, I think?

- This is my exact experience, I have spend over 100 usd on API fees through OpenRouter, OpenAI and Deepseek and tried many models with both Cline and Roocode and you really get various results. Sometimes you can end up in endless loops trying to solve a problem no matter how many times you start a new task with the same LLM then you switch to another LLM and you can get past that point or you get a situation where it wants to go on another totally different tangent. Ive had similar issues with local LLMs and even still have issues with them even working with Roocode and Cline. Ive even tried Bolt.diy which is a fork of Bolt.new, similar issues. Ive started writing my own coder to hopefully solve a few of my concerns but its likely we will end up with the same issues.

- I’ve been having similar issues with all local models. I’m using Qwen-2.5-coder 7B on MacBook M3 Pro and I’ve come to the conclusion that Cline’s context size is too large to be performant. I use the same model with Continue.dev and everything works quickly.
# discuss-ai-coding-internals
- ## 

- ## 

- ## 

- ## 

- ## 🆚🏠 [why does cline not apply multiple agent approach? : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mtnwgp/why_does_cline_not_apply_multiple_agent_approach/)
  - Roo has default 5 agents, and has more agents in mode market, including code techear and document writer, that's cool when the modes are managed by orchestrator.
  - why does cline not take this way?

- This approach is a key difference from Roo. Personally, I operate in a plan/act mode, whether for feature development, debugging, or writing documentation.

- all the additional prompting can even create conflicts and reduce performance

- they're just different system prompts. you could switch your active rules files and get most of the way there. 

- ## [RooFlow, RooCommander, SPARC, etc. What frameworks are you still using? : r/RooCode _202508](https://www.reddit.com/r/RooCode/comments/1mz96of/rooflow_roocommander_sparc_etc_what_frameworks/)
  - A few months ago there was an explosion of frameworks coming out to improve RooCode - RooFlow, RooCommander, SPARC, etc. 
- I tried some of them, but then I realized I didn't need them.
  - Same, the native functionality (modes, to do lists etc) plus the models became a lot better so there is much less need for the (well appreciated!) bandages.
  - Nevertheless, sometimes I still take inspiration from it for a workflow or way of documenting. Orchestrator is good, but it very quickly goes to coder instead of researcher etc. Think before you do could be personal preference.

- I just use plain roo.. but only because I don’t need more (yet). Would be nice if there were presets for different tech stacks, like coder-node-react or coder-cplus coder-serverless etc. as I’m sure things for me would be smoother if I took the time to add guardrails around the stacks I’m using

- SPARC enabled me to do one complex project and taught me so much about system architecture/design. That being said, now that I developed my own understanding of how to architect, I no longer need it.

- ## 🧠🤼 [Should we deprecate Memory Bank? Looking for some feedback from the Cline Community. : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mu4lej/should_we_deprecate_memory_bank_looking_for_some/)
  - memory bank is a prompt that I wrote (and to some degree have maintained) over the last year or so. 
  - It's original purpose was to instruct Cline to create/edit/read these context files that gave it an understanding of the project and where it was headed. 
  - And to do this via a single prompt that any user could paste into Cline and have work out of the box.
  - Here are the main benefits I see: - keeps the agent on track - creates project context that persists between tasks - useful documentation across teams
  - However, it does bloat the context quite a bit. And with our most recent Focus Chain feature, I'm not sure where/how it fits.
  - What parts of Memory Bank are actually useful to you? What is not useful? What does the ideal version of Memory Bank look like for you?

- My favorite part of memory bank was the tracking of progress. It knew what was done. What still had to be done. How certain parts were set to work. Etc.
- is this not covered by the focus chain & its todo list?
  - Only for a task basis. The memory bank keeps the context about the whole project and work which has been done recently. It allows me to start a new task with a description of what's needed and in which parts of the repo. Cline will find everything necessary on its own (mostly), and I can refine it.
  - It's also super helpful when using plan mode or deep planning to basically get everything pulled into the task.

- Focus chain is for a single Cline task/conversation.
  - Memory bank is to share basis about the project, the service, the roles, , between Cline conversations, so I do not have to remind it about it everytime my task needs a lot of context to be shared.

- I stopped using the Memory Bank a while ago. It ate too many tokens and no model was very good at keeping it updated. Instead, I have a markdown file that I keep in Obsidian that I manually keep updated, and keep brief for the times when I think the AI needs some more context.

- I love the memory bank, and still consider it a major strength of Cline. The progress is my most used file by far, and I heavily rely on it. Though the product and project contexts are also both helpful.

- in my work, Plan leans heavily on Memory Bank.

- In terms of context usage, memory bank is wasteful, it's mostly the reason I do not use it anymore, though I still create manually specs files and use rules.

- Sharing context with another dev to take up can be super handy.
# discuss-coding-tools/tricks
- ## 

- ## 

- ## 

- ## 

- ## [What do you use on 12GB vram? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nd1tqf/what_do_you_use_on_12gb_vram/)
- Qwen3-coder-30B, qwen3-30b, gpt-oss-20b - you can keep the KV cache on GPU and offload MOE layers to CPU, and it will work reasonably fast on most modern systems.
- And you can bring some of those MOE layers back to GPU to really fill out the VRAM, which will also provide a great boost overall. 
  - Don't forget the `--batch-size` and `--ubatch-size` , make those 2048 or even bigger, which will provide much faster prompt processing but at additional VRAM cost which may require a compromise in context size, depending on what's most important. 
  - I have a machine with 11GB VRAM and I can get it to about 65k context with 2048 ubatch/batch size for Qwen30b MOE. I get about 600 t/s PP and maybe like 15t/s generation, which isn't bad at all. I kept all MOE layers on CPU to get that context and ubatch up though.

- ## [Just bought an M4-Pro MacBook Pro (48 GB unified RAM) and tested Qwen3-coder (30B). Any tips to squeeze max performance locally? : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1naqdl5/just_bought_an_m4pro_macbook_pro_48_gb_unified/)
- I use mlx with lm-studio. Look for DWQ mlx quants for best quality. Mlx will always be faster than a comparable gguf quant because it is native metal framework.

- You might want to try the unsloth fine tune of Qwen 3. It might perform better on local devices.
  - I’ve been digging into Unsloth’s fine-tune pipeline. Their Dynamic 2.0 quants deliver up to 2× speed, 70% less VRAM, and up to 8× larger context windows ! That makes running Qwen-3-Coder incredibly efficient on local machines like mine.

- ## 💡 [Recommendation for getting the most out of Qwen3 Coder? : r/LocalLLM _202508](https://www.reddit.com/r/LocalLLM/comments/1mrzi5x/recommendation_for_getting_the_most_out_of_qwen3/)
  - I was already running the model at the full context 262k with my setup. It was just slow. 
  - Now I'm experimenting with different versions and settings to find the best compromise/trade-off. 
  - Currently I'm testing `Qwen3-Coder-30B-A3B-Instruct-Q3_K_L.gguf` with 81k context, K/V Cache Quantization set to Q4_0 and I'm getting 110 tok/s at the start of the chat and still getting a rather respectable 40 tok/s with 55% of the available context used. I haven't done rigorous quality assessment on this yet though. It might be better than Quen2.5 Coder though.

- The cause of the slowness is large context sent to the model, typically 10-20k at the beginning. Have you measured your prompt processing speed? Usually, the issue is solved with prefix caching, vLLM supports it, llama.cpp to some extent, ollama has troubles with it, and I don't know about LLM Studio. 
  - K/V cache quantization Q4 may hurt model performance heavier then parameter quantization, I would not go lower Q8 for K/V cache.

- Keep tasks under 100k context including prompt and output. Reset once you go about that to avoid hallucinations.

- You may want to explore using Jupyter Notebook or JupyterLab with Qwen3 Coder. They offer integration with various coding languages and can handle larger scripts interactively.

- My 5090 runs at only 25 tks/s speed with 256k context, so the slowdown is normal

- ## 🤔 [Qwen3-Coder-480B Q2_K_XL same speed as Qwen3-235b-instruct Q3_K_XL WHY? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n7ket1/qwen3coder480b_q2_k_xl_same_speed_as/)
  - i am running two models and got unusual result of speed inference:
  - Qwen3-235B-A22B-Instruct-2507-UD-Q3_K_XL.gguf - got 23-24 token/s for 104GB model size from Unsloth
  - Qwen3-Coder-480B-A35B-Instruct-UD-Q2_K_XL.gguf - got 23-25 token/s for 180GB model size from Unsloth.

- Nope this seems about right
  - 22B @ 3bpw = ~8.25 GB of active parameters
  - 35B @ 2bpw = ~8.75 GB of active parameters
  - The ratios of the active / total parameters between Qwen 235B A22B and Qwen Coder 480B A35B changes such that coder requires less active parameters compared to its total size.

- Something similar happens to me. I'm running gpt oss 120B f16 almost at the same speed as qwen coder 3 30B Q4 in 3xMi50 32gb. 
  - GPT OSS 120B is 5.1B Active and natively Q4 even if youre running the fp16 weights. Qwen 3 Coder is 3B Active. OSS 120B will only be about ~20% slower aslong as you have enough vram to fit it so it doesnt have to fallback to system ram

- ## [Qwen 3 30B a3b on a Intel NUC is impressive : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1nbxkqh/qwen_3_30b_a3b_on_a_intel_nuc_is_impressive/)
- These models you're running are MoE, which makes them more CPU friendly, resulting in an increase in performance, they are built for local hardware without much potency, so that is expected.
  - I am running Qwen3-Coder-30B-A3B-Instruct-GGUF on 12vram and I can set 64k context window and I get 23t/s

- the speed is because at any given time activated parameters are only 3.3b, so computationally it's not like a 30b model, this is a clever thing about moe models.

- Also keep the Thinking and Coder models at hand. They could edge in situations where Instruct may not be able to solve.

- ## [Why does Qwen3-30B-A3B-Instruct-2507 Q8_0 work on my machine and no others come close? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1msy01r/why_does_qwen330ba3binstruct2507_q8_0_work_on_my/)
  - I'm surprised that having a machine with 8GB of VRAM and 32GB of RAM can run this LLM. Slow, yes, but it runs and gives good answers. Why isn't there another one like it? Why not a DeepSeek R1, for example?

- Because it's a MoE model, it's kinda like running a small model, during inference it first find which experts it should use and they're very small, it's quite different from running a dense model where it will go through all 30B params.
  - If you want similar models, look for gpt-oss 20b, Ernie 21b, SmallThinker 21b, those are MoE models too.
- MoE makes a huge difference. What I’ve noticed is that Qwen’s routing feels more efficient than a lot of other MoE setups, so even on low VRAM it doesn’t get bogged down as badly. Dense 30B models on the same hardware feel like night and day in comparison

- Is there anything in the name that gives away that it's a MoE?
  - yes the 30B is the total size, A3B = Active 3B, which means that only a part of model is active at time, like Qwen3 235B-A22B, but it's not a rule, gpt-oss 20B does not have it on the name, but if you search it's a 20B-A3.6B

- Dense 32B model, on the other hand, would be around an order of magnitude slower since in dense models active parameter count is equal to the total parameter count.

- ## 🤔 [Best coding model for 12gb VRAM and 32gb of RAM? : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1n7fn2t/best_coding_model_for_12gb_vram_and_32gb_of_ram/)
- when i tried qwen coder 30b with lm studio it was reaaaallly slow, if u find a way to optimize it let us know or maybe it's lm studio the problem
  - When I use chat directly in LM Studio with Qwen 3 coder 30b, it’s quite fast! I’m on RTX 3060 12Gb. However, when I hook it up to VS Code, via Continue plugin, it becomes a tad bit slow but still fine. Then, when I switch it to agent mode it just becomes unusable. 
- Switching to `Llama Server` feels like night and day for me. When I was using LM Studio, I tried everything, but it was mostly very slow.

- I've got 12tps on a single 5060ti on the same Qwen3-Coder-30B-A3B-Instruct-Q6_K model but with much smaller context 16K

- Don't go beyond 100k context window with these as they're useless above it, as I have them as daily drivers with capacity to run full context.
  - Alternatively balanced, yet faster, you have GPT-OSS-20B from Unsloth. Either quants will work due to how it was optimised, just choose one you can fit. Even with offloading it's an efficient performer.

- ## [Is it true that all tools like Cline/Copilot Agent/Roo Code/Windsurf/Claude Code/Cursor are roughly the same thing? : r/ChatGPTCoding _202505](https://www.reddit.com/r/ChatGPTCoding/comments/1kumywl/is_it_true_that_all_tools_like_clinecopilot/)
- Yes - it’s essentially a big prompt (32k context window) and their tools. There is no magic except some have different workflows
  - Different models, better or worse at what to put in the context, RAG approaches…but yeah it’s generally the same.

- There are mainly three category of Coding assistants:
- 1️⃣ IDEs or IDE plugins with subscription model
  - VSCode+GH Copilot; Windsurf. AI; Cursor. AI; etc
  - All this assistants use their own set of prompts and tools, so even when you select the same AI model you can get other results. 
  - This editos are "cheaper" because they provide a monthly fee, but they also do brokeage between you and the AI services provider, and within that brokerage they can fundamentally cripple how the AI is used to reduce the context and maximize their profit
- 2️⃣ IDEs or IDE plugins with Bring-Your-Own-Key
  - Cline/RooCode/Kilo, etc .
  - Same different as category 1 (different prompts, tools), but they use the API directly, not reducing the inteligence to save money
- 3️⃣ Command line interfaces
  - Claude Code, OpenAI Codex, Janito, Aider, etc
  - This are typically better for natural language programming (prompting more, coding less), because they operate directly on files without the overhead of providing the editor context, (which files are opens, which file tab is open etc).
- While the model itself available on each of this tools is important, the result can be quite different depending on the optimization of the tools.

- Subscription tools (Cursor, Windsurf) need to balance what you pay vs their inference costs, so they use caps, context optimization, and throttling to manage margins. That's not a bug, it's how the economics work.
  - Cline/ClaudeCode/Roo (Cline fork) use direct API access with zero markup or throttling. You pay more for inference, but get unfiltered model capability. Different tools optimize for different outcomes.
  - Many devs use both -- subscription tools for autocomplete, Cline/others for complex tasks where you want maximum AI capability.

- Cline has a vector db like cursor and Windsurf now, it’s free and open source and you can see it in the code.
  - I think its a terrible idea, because it adds complexity and local search for code, which is mostly structured wording, unlike the generic text which benefits from vectorizing.
- I have also seen this option being made by other colleagues at my job, I think overall this is a disputed topic. To index or not code using a vector db.

- no Cline does not have a vector db. We're actually very against the notion of it from both a performance and security perspective.
  - [Why Cline Doesn't Index Your Codebase (And Why That's a Good Thing) - Cline Blog _202505](https://cline.bot/blog/why-cline-doesnt-index-your-codebase-and-why-thats-a-good-thing)
- why is it calling indexes all over the place in the "new" context management while your post says its not indexing?
  - "Index" here refers to array positions for organizing conversation history in memory, not database indexing or vector embeddings -- it's just basic data structure navigation.

- ## [It is almost May of 2025. What do you consider to be the best coding tools? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k0nxlb/it_is_almost_may_of_2025_what_do_you_consider_to/)
- As for what we use on our team, we're doing some server work and a lot of work in Unity and building lots of tools. We largely use Cline or Roo Code for the editor and then Sonnet 3.7 and Gemini 2.5 Pro mixed in. 

- Aider + Gemini 2.0 are responsible for most of my github activity starting from February.

- I do not use any IDE/editor's AI feature for coding. They feel pretty much useless even with full context. My personal opinion is, a developer should fully understand their code before committing, AI powered editors destroys this habit

- I’ve had much better luck with keeping the AI open in a browser and chatting with it, then manually editing the code in an IDE. 
# discuss-local-coding
- ## 

- ## 

- ## 

- ## 

- ## [Qwen3-coder-30b issues with tool calls : r/unsloth _202508](https://www.reddit.com/r/unsloth/comments/1mi3yis/qwen3coder30b_issues_with_tool_calls/)
- The qwen3-coder uses a new format to structure the tool calls. The qwen team included a python script on the huggingface repo for parsing the tool calls (I think it was JSON vs XML or something). The original tool call parser in your inference engine (like llama.cpp) may not work with the new format yet, and by replacing the template you're essentially forcing the model to use the old format, which the inference engine already supports.
  - I'm no expert in LLM fine-tuning, but I think replacing the template might lead to the model not producing correct tool calls occasionally, since these weren't the format they were trained on. On the other hand, it's also possible that the model is smart enough to recognise the alternative format and works just fine.
- Switched to Beta branch of LM studio and it's working now. Thanks for pointing me in the right in the right direction

- ## [Tool Call Format from Qwen3 Coder 30B Not Recognized by Most LLM Coding Agents · Issue · lmstudio-ai/lmstudio-bug-tracker _20250801](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/825)
- Looks like LM Studio 0.3.21 Build 3 fixed the issue. Thanks

- [Feature Request: Support Qwen3 Coder 30B Local Model for Tool Calls · Issue · continuedev/continue](https://github.com/continuedev/continue/issues/6913)

- ## 🆚 what's the differences between the llm models below
- https://huggingface.co/Qwen/Qwen3-Coder-30B-A3B-Instruct  
  - Long-context Capabilities with native support for 256K tokens, extendable up to 1M tokens using Yarn
  - Parameters: 30.5B in total and 3.3B activated
  - Experts: 128
  - Activated Experts: 8
- https://huggingface.co/unsloth/Qwen3-Coder-30B-A3B-Instruct  
  - Unsloth Dynamic 2.0 achieves superior accuracy & outperforms other leading quants.
  - [Qwen3-Coder: How to Run Locally | Unsloth Documentation](https://docs.unsloth.ai/basics/qwen3-coder-how-to-run-locally)
  - We managed to fix tool calling via `llama.cpp --jinja` specifically for serving through `llama-server` ! If you’re downloading our 30B-A3B quants, no need to worry as these already include our fixes.
- https://huggingface.co/nightmedia/unsloth-Qwen3-Coder-30B-A3B-Instruct-qm468-mlx  
  - "qm468" in the name likely refers to the specific quantization configuration used.  
- https://huggingface.co/nightmedia/unsloth-Qwen3-Coder-30B-A3B-Instruct-qm468-hi-mlx
  - "high, " suggesting a different quantization setting or a variation 
- https://huggingface.co/mlx-community/Qwen3-Coder-30B-A3B-Instruct-4bit-dwq-v2
  - DWQ (Dynamic Weight Quantization), which significantly reduces memory usage while maintaining performance

- ## [PSA: Qwen3-Coder-30B-A3B tool calling fixed by Unsloth wizards : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mje5o0/psa_qwen3coder30ba3b_tool_calling_fixed_by/)
- Worth pointing out that it appears to have been fixed in relation to LM Studio.
  - Also worth pointing out that with LM Studio I get 1.75x - 2x slower performance compared to Llama.cpp, despite enabling flash attention, KV cache, etc. No idea why that is, but I definitely feel it when running the model. It also slows down dramatically as more context is added.

- It's not a real fix, but workaround forcing the model to use different tool call format (that llama.cpp handles) that is originally should use (xml instead of json formatted tool calls).
  - The proper fix (for llama.cpp-based workflows) is to update llama.cpp's internal tool call parsing to handle the new `<xml>` format, instead of forcing the model to use a different one.

- Got a chance to try out the updated Unsloth quants and it does seem to be improved. Not using a quantized KV cache with llama-server greatly improved tool calling for me and success rate of changes with RooCode.

- ## [Best really lightweight coding model for very basic questions? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n9faly/best_really_lightweight_coding_model_for_very/)
- Gpt oss 20b or qwen 30b a3b 2507 (thinking version), these aren't just coding models but they do well at coding and run fast on a CPU with enough system ram.

- ## [It's here guys and qwen nailed it !! : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m6qkse/its_here_guys_and_qwen_nailed_it/)
- on this chart Devstral Small really seems like the efficiency winner. Big numbers for a relatively small model. 
  - Devstral is the best model I can run with my VRAM poor system.
  - However, I've been playing with Qwen 3 coder for the last hour now that it's live on Openrouter, and it is really good. It's on a whole different level than latest Devstral.

- ## [OpenHands + Devstral is utter crap as of May 2025 (24G VRAM) : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kui17w/openhands_devstral_is_utter_crap_as_of_may_2025/)
- Devstral system prompt references OpenHands by name. 
  - It does not. I tried a few primitive tasks and it utterly failed almost all of them while burning through the whole 380 watts my GPU demands.

- Did you run devstral with default parameters in ollama? By default, it will be initialized to have context length of a mere 2048 tokens
- I check and I'm using default context length. All instructions just went straight out the window.
- That is one reason I switched away from ollama to llama.cpp, and run it on port 11434 and let it pretend to be ollama.
- Can you say a little bit more on how you have it pretend to be ollama?
  - It is essentially what is explained here https://github.com/ggml-org/llama.cpp/pull/12896 but it is not perfect. 
  - It is a bit backwards that ollama have custom api endpoints which llama.cpp need to implement because they add support for ollama but not the general openai compatible api endpoints.

- Ollama is so broke on devstral. When manually increasing context it would make the ram usage balloon to 50gb and then hang.
  - Switched to lm studio mlx devstral and set the context to the max and it works correctly
- If you do not adjust the KV cache in ollama then you're using full f16 by default which is why its taking 50GB to run devstral at 128k context.

- I need to dig into llama.cpp again, but can it run more than one model at once? Or will I have to build a reverse proxy for it?
  - There's llama-swap for that use-case. 
- I'm using it, it's good. Runs a few instances of llama.cpp llama-server with models for chat, embeddings and reranking and switches them as required by the API client.

- Ollama runs much better if you put the following lines in your environment variables and just leave it forever.

```sh
OLLAMA_CONTEXT_LENGTH: 32768

OLLAMA_FLASH_ATTENTION: true

OLLAMA_KV_CACHE_TYPE: q4_0
```

- Pretty sure they increased it to 4096 relatively recently. Still extremely small though.

- Qwen2.5-VL is not agentic and not good for coding assistant too, while Qwen3 is ok for agents but no vision support.

- From my experience it is very usable when running on my 4090 w/ 50k context window. Using unsloth dynamic q5. 
  - The only thing is that you need a more detailed prompting. 
  - Using w/ roo code. It is very important to use architect & orchestrator modes. Otherwise any bigger change hinders it's capabilities. IMO best local llm for coding

- I agree for Devstral-small. It's crazy bad.

- ## [Meet Mistral Devstral, SOTA open model designed specifically for coding agents : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kryxdg/meet_mistral_devstral_sota_open_model_designed/)
- Weird that they didn't include aider polyglot numbers makes me think they're probably not good. Unfortunately my suspicion was right ran aider polyglot diff and whole got 6.7% (whole), 5.8% (diff)
- The official system prompt has a bunch of stuff aobut OpenHands including `When configuring git credentials, use \"openhands\" as the user.name and \"openhands@all-hands.dev\" as the user.email by default` ... So yes seems specifically made to work with that framework?
  - [SYSTEM_PROMPT.txt · mistralai/Devstral-Small-2505 at main](https://huggingface.co/mistralai/Devstral-Small-2505/blob/main/SYSTEM_PROMPT.txt)

- This is amazing if it holds up to the benchmark in real life
  - It doesn’t. At least not in my real tests. Couldn’t get it to even update a css class using cline and roo. It doesn’t output the correct expected tokens from an agent

- [Qwen3-Coder is here! : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1m6qdet/qwen3coder_is_here/)
  - You’re right on Devstral, it’s a good model for its size, although I feel it’s not as good as it scores on SWE-bench, and the fact that they didn’t share any other coding benchmarks makes me a bit suspicious. The good thing is that it sets the bar for small coding/agentic model and future releases will have to outperform it.

- ## [Is MLX or GGUF better for Qwen 3 Coder on Apple Silicon? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mskd6u/is_mlx_or_gguf_better_for_qwen_3_coder_on_apple/)
- Mlx is faster. DWQ are maybe better in quality. GGUF are slow.

- It's fairly common for MLX to have multimodal support before GGUF. 
  - It's also fairly common for GGUF to have larger context windows released before MLX.
  - There are good reasons to use both, but typically MLX will be a tad more energy efficient with a few more tok/sec at the same bit depth.

- ## [Qwen3-coder is mind blowing on local hardware (tutorial linked) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n3ldon/qwen3coder_is_mind_blowing_on_local_hardware/)
  - qwen3-coder-30B is really impressive. 256k context and is actually able to complete tool calls and diff edits reliably in Cline. I'm using the 4-bit quantized version on my 36GB RAM Mac.
  - My machine does turn into a bit of a jet engine after a while, but the performance is genuinely useful. 
  - My setup is LM Studio + Qwen3 Coder 30B + Cline (VS Code extension). 
  - There are some critical config details that can break it (like disabling KV cache quantization in LM Studio), but once dialed in, it just works.

- The other one that shines on cline is Devstral small 2507. Not as fast as Qwen3-30b but equal if not a little better (in the way it plans and communicate back to you)
  - But yes, qwen3-30b best thing since web browsers.

- I find Devstral does a lot better than Qwen 30B Coder with thinking off. You need to let it ramble to get good answers but while I'm waiting, I would've got the answer from Devstral already.
- I don't think Qwen3-Coder comes in a thinking variant?
  - You're completely correct. Qwen3 30B Coder only has a non-thinking variant. I must have gotten the old 30B mixed up with 30B Coder when I was loading it up recently.

- why is Devstral so much slower than Qwen3 Coder even though it's smaller? I got 36tok/sec with Qwen3-Coder 30b (8bit quant), but I only get about 8.5 tok/sec with Devstral (also 8bit quant) on my Framework Desktop.
  - It’s a dense model. It’s slower but also smarter.
  - Devstral isn't an MoE model.

- ## 🤔 [Qwen3-Coder is impressive : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mssdfo/qwen3coder_is_impressive/)
- How does it handle long context?
  - It has 256 k context. Cline supports compression/summarization now for things exceeding that.
- I think at 125k context it has only 60% recall

- Plan or Act or both?
  - Both. I am too lazy to switch modes. Act all the way.
- Usually the solutions generated by act only are worse in my experience than if I did a planning / brainstorm session with the model first.
  - in my empirical experience/perception too. but that can be a biased by my usage style. i generally add at least a thing or two in its plan - and it works for me. 

- 🤔 Yeah it's excellent. I wish they had a version with reasoning.
  - “Reasoning” seems like mostly smoke and mirrors to me.
- Could you use something like sequential thinking MCP simulate that?
- The coding tools like cline and roo already prompt the model into reasoning. There’s no benefit of using a reasoning model with those.
  - That's not really how it works. You could tell 4o to "think step by step" back in 2024 (and I did), but that didn't turn it into O1.
- There's a huge difference between a system prompt and RL. But if you have a prompt that makes 4.1 reason like o1, lets hear it, that would be really interesting.

- Qwen3 coder performs good in terms of reasoning and complex problems. Only issue is context limit
  - That's when you use /smol or /newtask

- ## [Cline + Qwen3 coder is bliss for LocalLLM : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mt14x9/cline_qwen3_coder_is_bliss_for_localllm/)
- How much context window?
  - (I would max it out to 256k if you can)
- I’ve been using this combination successfully with a context window of 64k, 128, 256k on my Mac. Honestly I don’t notice too much of a difference, they all work darn pretty well. 

- I use unsloth/qwen3-coder-30b-a3b-instruct in LM Studio with its server enabled. I have 34GB VRAM across 2 cards, which is enough to fit the 26.34GB model in VRAM. 

- I also combined it with the new Archon Beta & the task planning + knowledge base makes this crazy powerful + keeps my context for enormous code bases down to below 128k tokens so lots of headroom not to mention reduces memory usage by around 60GB.

- ## [Qwen3- Coder 👀 : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m6mew9/qwen3_coder/)
- gemini flash works satisfactorily at 500k using Roo.

- The updated Qwen3 235B with higher context length didn't do so well on the long context benchmark. It performed worse than the previous model with smaller context length, even at low context. Let's hope the coder model performs better.
- I've tested a couple of examples of that benchmark. The default benchmark uses a prompt that only asks for the answer. That means reasoning models have a huge advantage with their long COT (cf. QwQ). However, when I change the prompt and ask for step by step reasoning considering all the subtle context, the update Qwen3 235B does markedly better.
  - That'd be worth a try, to see if such a small prompt change improves the (not so) long context accuracy of non-reasoning models.
  - The new Qwen coder model is also a non-reasoning model. It only scores marginally better on the aider leaderboard than the older 235B model (61.8 vs 59.6) - with the 235B model in non-thinking mode.

- ## [Local model for coding : r/ollama _202508](https://www.reddit.com/r/ollama/comments/1n0ht8x/local_model_for_coding/)
- Qwen3-coder B30A3 is really good and fast Works like a charm on my 4060ti 16GB
- I'm using hf.co/unsloth/Qwen3-Coder-30B-A3B-Instruct-GGUF: Q2_K specifically and even at that low quant, it's exceptional at coding and tool use.
  - Why are you going so low? Just offload the the inactive experts to CPU and only keep the active ones on the vram. Yes, it will be slower but also provide better quality as you will be able to run Q5 (or Q6) UD K XL with about 15t/s and a 32k context.

- Qwen3 is nice, but thinking part of it sucks - not good.
  - There are also models that have been adjusted to use tooling: hhao/qwen2.5-coder-tools maryasov/qwen2.5-coder-cline
- There is also the new qwen3 instruct variant, which doesn't think.

- ## [Best Way to Use Qwen3-Coder for Local AI Coding? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n4mo1r/best_way_to_use_qwen3coder_for_local_ai_coding/)
- (For local coding work) the lesson I learned is: Qwen3 Coder works very well as an autocomplete model.

- Cline and LM Studio is all you need.

- ## [two models big difference in how it converses/answers. ie Qwen3 30B A3B vs Qwen3 32B : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mkgv1l/two_models_big_difference_in_how_it/)
- The 30B A3B model is MOE model. The A3B tells you that it's 3B active. So you get the speed of a model like it was 3B but the intelligence of a 30B model.
  - Qwen3 32B is dense, not moe, and so it's slower.

- ## [Qwen3-Coder-30B-A3B in a laptop - Apple or NVIDIA (RTX 4080/5080)? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mwmi2n/qwen3coder30ba3b_in_a_laptop_apple_or_nvidia_rtx/)
- M2 Max 64 Gb here. 
  - I run Qwen3 30B A3B Q4 With llama.cpp, you’ll get around 50 TPS. 
  - If you run with MLX, 80TPS.

- ## [Why does Qwen3-Coder not work in Qwen-Code aka what's going on with tool calling? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mu3tln/why_does_qwen3coder_not_work_in_qwencode_aka/)
- That's just what happens when you have a fast-moving field and not much in terms of standards.
- The current situation is a bit of a mess. For whatever reason, OpenAI decided to release their new model with a Harmony format that, for the most part, no one asked for. This makes it a one-off system that every open-source LLM project has to support, especially if OpenAI doesn't release another model with the same format.
  - Similarly, Qwen also switched up their tool-calling scheme, but only for the latest coder version. To be fair, the current JSON tool-calling format is rather unforgiving, and quantized models are more likely to produce errors in the formatting. 

- Only LM Studio works, so they must have hacked around it, but it's closed source.

- ## 🆚 [GPT-OSS 20b vs Qwen3-30B-A3B : r/ollama _202508](https://www.reddit.com/r/ollama/comments/1mlgyct/gptoss_20b_vs_qwen330ba3b/)
- I use Qwen3-Coder over OSS because
  - A. Qwen3 models can be ablated to remove railguards for queries, while OSS can’t as easily.
  - B. I can run Qwen3-30b-a3b-abliterated Q6 on my 32gb gpu card fitting the entire model in that space. OSS has no quants available that work with ollama as of this moment. Which edge it just over into 1% CPU - 99% GPU which slows it way down.

- ## [Qwen 30B Instruct vs GPT-OSS 20B for real life coding : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mvbzvh/qwen_30b_instruct_vs_gptoss_20b_for_real_life/)
- I find GPT-OSS 20b way better for coding, especially in coding agents.  First it runs with 64k context window at 100+ tokens per second on 5060ti, where Qwen 30b would be way slower cause of size, around 40-45 tokens on my hardware. This makes huge difference especially for thinking model.
  - I've tried  https://huggingface.co/Qwen/Qwen3-Coder-30B-A3B-Instruct and it's sometimes better, but on some non trivial issues gpt20b beats it because of thinking on practice. Also this one has huge flaw, tool calling is not working at all, so it's pretty much unusable for now.
  - Qwen3 30b 2507 Thinking is cool one, it works and it's way better on simple tasks without context. The main issue with it it thinks too much. It can use 10k+ tokens for simple file edits in coding agents, context getting polluted very fast and on practice it's way slower then GPT-OSS 120b
  - I hope they will update Qwen coder, maybe will give dense model or thinking variant, but for now they are not really close to GPT-OSS.

- So that's the thing: for Qwen3-Coder they trained it to use a different tool calling format compared to the regular Qwen3! They switched from quoted JSON (Hermes format, I think that is called), to an XML based one. In theory this is better because it's less complicated to quote and so it survives better especially with quantized models. But support this new syntax does not exist in llama.cpp yet AND at least the small 30B seems to be a bit wonky with tool calling itself.

- Qwen 30b 2507 Thinking, works best , maybe Qwen 30B coder with thinking might perform even better but its not released yet.

- [Devs: Devstral VS Qwen3-30b/GPT-OSS? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mprb4d/devs_devstral_vs_qwen330bgptoss/)
  - qwen 30b coder is miles ahead for web development compared to dev and oss
  - Whereas gpt-oss is very good for general or research discussions oriented stuff like asking one-shot proof of prey-predator models or any complex system it’s really good. It’s power relies on reasoning high reasoning comes gives great result most of the time
  - gpt 20b. Omg it was a rocky start but with the latest lm studio + aider in diff mode. I'm confident to say that is my new go-to. It's the new hummer. Best of class.

- ## [Qwen Code + Qwen Coder 30b 3A is insane : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mfuiri/qwen_code_qwen_coder_30b_3a_is_insane/)
- Especially since 30A tool calling only works with Qwen-Coder. They decided to use XML for tool calling instead of JSON like all other models, so tool calling doesn't work in roo or cline.
  - Nodejs was shitting all over python for a decade and now the turns have tide
- Issue is they don't use XML, they use an invalid variant of XML: `<toolname=read_file><parameter=path>` ....

- Which tools are you calling? I have used it with RooCode and it was able to search my codebase, edit, create and read files. Wait, did you make sure to set the temp in RooCode? I know that I had problems until I changed it to 0.7.

- Roo and Cline use xml based tool calling so I wouldn't phrase it like that - Qwen was probably specifically trained for the Qwen Code prompt format

- Json is a terrible format for LLMs, it's incredibly token inefficient. I'll need to start using qwen-code.

- ## [Talking with QWEN Coder 30b : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mn00j3/talking_with_qwen_coder_30b/)
- Trust me even the biggest Models suck at Godot/gdscript

- Qwen3 Coder 30B A3B is capable of actually writing code in "agent" mode, but things like tool calling are extremely fragile and will fail for most people
  - I've had OK luck with the VS Code Cline plugin, the newest Ollama, and the Unsloth 4-bit XL quant, but literally all the other agent wrappers besides Cline failed to make tool calls 90% of the time
  - I've never seen any model in 32B size range that was amazing at code

- I had a similar experience with QWEN, While raw speed is appealing, reasoning depth and flexibility are more important than just token count.

- you should try qwen3 30b thinking. it is more accurate in such non-coding tasks.
- Actually Qwen3-30B-A3B-thinking-2507 is a way better than non thinking Version
- I have finished testing Qwen3-30B-A3B-thinking-2507, and I would say its answers are roughly on par with the OpenAI gpt oss 20b model

- I'm using the Qwen3-30B-A3B-instruct for coding. The coder seems to have more issues following the instructions of long prompts like in Roo.
  - Qwen Coder 30B is an instruct-tuned model, not a chat-tuned one, and I googled to search what means in more details.
  - Instruct-tuned models are optimized to follow direct, self-contained instructions in a single turn. 
  - Chat-tuned models, on the other hand, are trained specifically for conversational environments. They learn to remember previous messages

- ## [Installscript for Qwen3-Coder running on ik_llama.cpp for high performance : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1metf4h/installscript_for_qwen3coder_running_on_ik/)
  - After reading that ik_llama.cpp gives way higher performance than LMStudio, I wanted to have a simple method of installing and running the Qwen3 Coder model under Windows. 
  - I chose to install everything needed and build from source within one single script

- The random text issue could be because of flash attention, try disabling it. I had the same issue last week with Qwen 235b on my dual-GPU setup. My second GPU is also compute 6.1 (Quadro P5000).
  - Yep, can confirm the random text issue on both ik_llama.cpp and vanilla llama.cpp occur when `-fa` is enabled.
- I had it only with ik_llama.cpp tough, vanilla llama.cpp was fine with -fa

- My brain can't understand why lm studio doesn't implement ik llama or give us an option to run it.

- If you want faster especially with that nvdia 4070ti ...load the model with vllm on WSL in windows it will be a lot faster than llama.cpp/lmstudio probably around 5-6x faster for generation of tokens.
  - I know vllm is another fast inference engine, but I highly doubt the 5-6x claim. Do you have any benchmarks that show this?
- sorry meant to say 4-5x faster than tensorflow and about 25% faster than llama.cpp. 

- [How to run Qwen3 Coder 30B-A3B the fastest? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1mepr5q/how_to_run_qwen3_coder_30ba3b_the_fastest/)
  - lm studio will be trivially fast to setup. I run Qwen 3 Coder 30b-a3b locally. It works great with Cline.
  - For your reference. I run it (Q4-k-xl UD) on my 8600k 32GB Ddr4 with 4070 super desktop. I get about 10t/s at 4k tokens. Your laptop will probably be a lot slower than this.

- ## [I made a comparison chart for Qwen3-Coder-30B-A3B vs. Qwen3-Coder-480B-A35B : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1me4i2h/i_made_a_comparison_chart_for_qwen3coder30ba3b_vs/)
  - [qwen3-coder-flash-perf-comparison.html](https://gist.github.com/karminski/08d4952f61952b7aa32c89eff5924432)

- A dense 32B would make those gaps much smaller
  - And be ~ 10 times slower

- Qwen 30 A3B is so insanely fast (90tok/s on M4 Max silicon) that it seems more useful to just run it a few times and have it iron out errors as it goes. Needing to store 16x more parameters doesn't seem worth it tbh
  - I second that. And if you need something extraordinary you go to Qwen chat and ask Qwen3-Coder-480B for that specific piece of code.

- ## [Qwen3-Coder: Agentic coding in the world | Hacker News _202507](https://news.ycombinator.com/item?id=44653072)
- I currently use claude-code as the director basically, but outsource heavy thinking to openai and gemini pro via zen mcp. 
  - I could instead use gemini-cli as it's also supported by zen. 
  - I would imagine it's trivial to add qwen-coder support if it's based on gemini-cli.
- How was your experience using Gemini via Zen?
  - I just use it for architecture planning mostly when I want more info and to feed more info to claude. Tougher problems where 3 brains are better.

- what is the benefit of outsourcing to other models. do you see any noticable differences?
  - There are big gains to be had by having one top tier model review the work of another.
  - This is particularly useful in big plans doing work on complex systems.

- They also support Claude Code. But my understanding is Claude Code is closed source and only support Clade API endpoint. How do they make it work?
- Claude uses OpenAI-compatible APIs, and Claude Code respects environment variables that change the base url/token.
  - no it doesn't, claude uses anthropic API. you need to run an `anthropic2openAPI` proxy
- You can use any model from openrouter with CC via https://github.com/musistudio/claude-code-router

- ## 🚀 [Qwen3-Coder-30B-A3B released! : r/LocalLLaMA _20250731](https://www.reddit.com/r/LocalLLaMA/comments/1me2zc6/qwen3coder30ba3b_released/)

```sh
# Ollana is using standard gguf 
ollama run hf.co/unsloth/Qwen3-Coder-30B-A3B-Instruct-GGUF:Q6_K
```

- Interesting, no thinking tokens, but built for agentic coding such as Qwen Code, Cline, so assuming great for Roo Code.

- Qwen2 Coder wasn't so great for Roo Code and Cline. But Qwen3 is quite good in tools handling, and this is the key for successful integration with coding assistants. Fingers crossed.

- Does anyone know how 30B-A3B thinking compares to 30B-A3B-coder? The lack of thinking makes me somewhat sceptical that coder is better.
  - If you use Cline or similar you can set the thinking model to Plan role and the Coder version to Act role.

- No thinking only? Why's that?
  - they have a 480B-A35B thinking coder model in the works, they'll probably distill from that

- The only one that good both at code and writing is GLM-4, but it has nonexistent long context handling. Small 3.2 is okay too but dumber.

- [🚀 Qwen3-Coder-Flash released! : r/LocalLLaMA _20250731](https://www.reddit.com/r/LocalLLaMA/comments/1me31d8/qwen3coderflash_released/)
- I hope they still release a dense 30B+ coder. I don't trust tiny MoE models to output anything useful. Being lightning-fast is nice, but output quality is what matters the most for coding.

- a 30B-A3B MoE is poised to compete against ~10B dense models. It loses to Qwen3-14B for instance.
  - I think that's a poor observation, dense models are usually better than moes. In swebench verified with open hands scaffolding devstral small actually scores a little higher. Unfortunately this is the only benchmark I've been able to find that has both.

- ## [Is Qwen 2.5 Coder Instruct still the best option for local coding with 24GB VRAM? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kq029v/is_qwen_25_coder_instruct_still_the_best_option/)
- I'm just using the 30BA3B for everything. It's not the smartest, but it is fast and I am impatient. So far, it has been good enough for most things. If there's something it struggles with, I switch to Gemini Pro.
  - Once you get used to that speed it's hard to go back to a dense model in the 32B/30B size.

- QwQ is goated but you have to accept waiting 3 billion years of thinking before getting your output

- No, Qwen3 is better. 32B no-thinking or 30B-A3B with thinking.
  - 14B is also great with thinking, probably better than 30B-A3B, you can run it in Q5 or Q6, and you can fit so much context.

- Within 24G ram it supports only 2000 context size but for a normal Nextjs app it is too low. At least require 32k context size but then the memory requirement shoots up too.

- ## [What would you say are the best open models for code generation? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jyv6if/what_would_you_say_are_the_best_open_models_for/)
- Qwen2.5 coder, QwQ. Perhaps Mistral Small 24b.

- If starting from no code base, probably QwQ takes top spot due to its reasoning (thinking) steps.
  - For adapting existing code Qwen 2.5 Coder 32B, probably edges a little maybe.
  - Where the local models don’t include things like logging or type hints unless prompted (Python language), Gemini 2.5 Pro just did it without prompting.

- Ohhh something important for the local models. Make sure to configure them to get the best performance. (E.g. lower the Temperature setting to 0.5 or lower to achieve better performance for coding and maths)

- I really enjoy the directness of models that don't have reasoning. So for me that would be Qwen 2.5 32B Coder, Qwen 2.5 72B Instruct, Mistral Large 2, Deepseek V2.5, Deepseek V3-0324

- I use code models with Cline. DeepSeek V3-0324 (used through openrouter API) is much much better than Qwen Coder 32B/72B instruct. I can give it more advanced requests for implementations of various features, it's close in usability to Claude 3.7 Sonnet, it's a real workhorse. Qwen 2.5 72B Instruct which is my preffered local model as of now (I hope Qwen 3 will blow it out of the water soon)

- When searching for local model for code generation, take into consideration the context length that you can make it work at locally - I hit 40k ctx very easily even when working on single 500 LOC files.
- I expect context to be an issue. I'm currently thinking a lot about the RAG strategy (I have a lot of experience with RAG design but only for documents). I'm also pondering building an evolving graph database, which would help compile variables, functions, and classes since the files are highly structured.

- how do you like Cline? 
  - It's designed to work best with larger API-only LLMs, and it shows, so 14B LLMs for example have issues with using it's tools. I started off with Cline after doing some coding through chatting in the LibreChat UI, I didn't try other tools/extensions. 

- Qwen2.5-coder32b has been the best for me, but I can only run it slowly on my CPU, so I swap down to the Qwen2.5-coder14b that I can run on my 16gb GFX card.

- ## [What is the top model for coding? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m5x04m/what_is_the_top_model_for_coding/)
- Gemini 2.5 Pro now has a giant 2M token context, great code quality, and fewer “hallucinations, ” while GPT-4o is close to Claude with 1M tokens and strong integration. Both now rival or surpass Claude in many tasks. definitely worth revisiting. I use each AI for it's strengths per the task.

- ## 🧩 [What kind of Qwen 2508 do you want tonight? ; ) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mhbvig/what_kind_of_qwen_2508_do_you_want_tonight/)
- in the 30B-A3B size, there is Qwen3-30B-A3B-Instruct-2507, it's for general use. "Instruct" means it was trained for user-assistant conversations, like following instructions, not just text completion (unlike Base models).
  - Also, there is Qwen3-Coder-30B-A3B-Instruct, which is better for coding tasks (but could be worse at everything that isn't related to coding), also it supports FIM (Fill in the Middle) for code completion, and it's also "Instruct" so it can do the instruction following as well.
  - So "Base" usually means the model can only continue text.
  - "Instruct" means it can follow user's instructions (the `user` , `assistant` , `system` stuff).
  - "Coder" in Qwen models means it's a model for coding, trained on coding related stuff mostly.
  - Also there is Qwen3-30B-A3B-Thinking-2507. From what I understand, it's like Instruct but with thinking (with something like this before every reply: `<think>Okay, ...</think>` )
- So as I understand it, instruct models are specially trained to follow instructions better / adhere to them more?
  - Yeah, you could say that
  - I mean, you can think of an Instruct model as of a ChatGPT-like model, which can chat with the user. But models like that don't necessarily have that "Instruct" in their names.

- 14B and smaller are my only realistic options with high context
  - So far, my testing shows that the 30B-a3b-2507 (non-thinking) is on par or better than Gemma3 27B. If the new 14B delivers improvement on par with what the 30B-a3b-2507 achieved over its predecessor, then it would be in the same ballpark as Gemma3 27B since the old 14B and 30B-a3b—were already quite close in quality.

- [From Smooth Chatting to Precise Execution: differences between “chat” and “instruct” modes in large language models | by hengtao tantai | Medium _202405](https://medium.com/@zergtant/from-smooth-chatting-to-precise-execution-differences-between-chat-and-instruct-modes-in-9c6f73fc175e)
- “Chat” and “instruct” modes are two common interaction styles in large language models. 
  - These modes differ significantly in how they handle inputs and generate responses. 
- The “chat” mode aims to engage users in free-form conversation, simulating a chatting experience with an emphasis on fluency and coherence; 
- the “instruct” mode, on the other hand, focuses on understanding and executing specific user commands, striving for task accuracy and operational precision. 
  - They excel when the entire task and all requirements are included in one prompt, but they’re not designed to maintain context, handle back-and-forth exchanges, or interpret subtle hints over multiple turns.

- ## 🧩 [jukofyork/DeepSeek-R1-DRAFT-0.5B-GGUF · Hugging Face : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jiilot/jukofyorkdeepseekr1draft05bgguf_hugging_face/)
  - This model is hopefully going to speedup the 600B version
  - I tried this paired with Unsloth dynamic quant: there's a token mismatch, token 128815 exists there as "PAD_TOKEN", so you probably have to use the gguf tools found in llama.cpp to edit these existing models, the draft, or convert again if you're unsure of that 

- draft model means?
  - If you use a feature called speculative decoding, you load up your main model (eg Deepseek R1 671B) and a draft model (this 0.5B model).
  - The point is you can draft what the next few tokens/words should be and pass it to the main model to verify. 
  - This basically means a lot of filler tokens can be generated much faster by the smaller draft model, resulting in a significant performance improvement with no degradation in quality. The benefits get larger the difference between the main model and draft model in size. 
  - LM Studio has this feature built in and it’s best to watch it enabled. 

- I didn't understand, what this model does, and how should I use it?
  - It's like an inexperienced student that can come up with 10 ideas on the spot. But then the experienced teacher can say, hey wait, Idea no. 7 might not be that bad and is worth pursuing. This process is much faster than the teacher coming up with a new idea on his own. Basically verifying an idea is faster than coming up with a genuine good one for a teacher.
  - Because LLM inference is mostly memory bandwidth limited, you can evaluate multiple inferences in parallel for basically free

- I have wondered if an asymmetrical MOE could outperform speculative decoding. If the MOE had a large expert and a small expert, you could have the router send all basic English words to the small expert… then rejection would never happen.

- The draft model needs to be same architecture but smaller model.

- The problem with drafting MOE models is that the amount of weights increases if more tokens are calculated per pass. It won't be the same chosen experts for each token.

- ## [If you limit context to 4k tokens, which models today beat Llama2-70B from 2 years ago? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lzuaa3/if_you_limit_context_to_4k_tokens_which_models/)
- Codellama 70B was a fine-tune of Llama 2. Since then the only coder fine-tune above 70B was the DS 236B. So I'm assuming later models 70B and above have also been trained on coding datasets. Like Qwen 2.5 32B coder probably was fine-tuned on the same coding datasets used in their 72B. And that coder certainly beats codellama - codestral 22B did.

- Deepseek (R1 \ V3) at Q1 at 4k context shits on Llama2 70b any day of the week for whatever task your heart desires.

- ## [Qwen3 no reasoning vs Qwen2.5 : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kegrce/qwen3_no_reasoning_vs_qwen25/)
- Depends on the task. For code autocomplete Qwen/Qwen3-14B-AWQ nothink is awful. I like Qwen2.5-coder:14b.

- ## [Is Qwen2.5 Coder 32b still considered a good model for coding? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1iyuy62/is_qwen25_coder_32b_still_considered_a_good_model/)
- For performance on it can’t compare to closed source or the huge param models like Deepseek v3.
  - However it’s the only one a lot of people can run locally with a 24GB video card.
  - Personally, I mostly switched to using claude3.7 for general questions/code gen and qwen 2.5 7B for FIM and code completion.

- 🤔 I personally, prefer it to reasoning models of the same size just because when coding I am less eager to watch it ramble on, on how its going to answer and just want an answer. I think bigger and maybe even the same size reasoning models might give better answers but I am usually too impatient when coding to deal with all that.
  - Same here, I like the concept of reasoning models but I am also impatient 
  - Yeah, reasoning models like R1 are too bulky for chat-coding.

- it is weaker than bigger models, but it is better than codestral, except for context length. I am more than happy with 7b and 14b models; 

- For its size, it's the best.
  - DeepSeek R1 is 631B even with MoE, how can you compared to a 32B?
  - Sonnet API is $3 / million tokens. Also, how do you compare to a local model?

- while with some local models that you can run on a 24gb or even a 48gb setup are "good enough" for simple tasks, or even processing a lot of documents, or whatever, for coding assistants they are a toy compared to what is available. When you do anything serious they are more a waste of time than remotely helpful. You can compete with what you can get with $10 a month with GitHub copilot or services like that.
  - I'm still using local models for fun and learning, but it's hard to justify not using a cloud api like Gemini. 

- I am using it with continue VSCode plugin. Not bad.

- 32k context is not big enough. Need at least 4x for it to be really helpful.
  - Qwen coder 32b has 128k context
- People seem to ignore this fact, not only you can extend it to 128k, but it almost don't degrade (compared to other 128k models). Problem is, only VLLM support the YaRN rope configuration needed to extend it.
  - Also exllama supports it.

- QwQ is built on Qwen2.5-32B-Instruct and not Coder. (At least according to its HuggingFace page.)
  - Reasoning 32b models just kill my mbp unfortunately

- ## [Is qwen 2.5 coder still the best? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j2usb0/is_qwen_25_coder_still_the_best/)
- nothing has been released that really holds a candle to Qwen-Coder 32B that can be run locally with a reasonably modest hobbyist machine. 
  - The closest we've come is Mistral Small 24B (and it's community fine tunes, like Arcee Blitz) and Llama 3.3 70B (very good at coding, but wayy larger and questionable if it beats Qwen).

- CoT models think too much for coding IMO. I think they are good for optimizing your prompt though.
  - They might have a role for architecting. Like figuring out Rust traits is annoying and extra diagrams help as well. But for extra interns, no chain-of-thoughts please.
- I do this with Aider. R1 plans the code changes, Sonnet 3.7 writes the actual code based on it's output. It works really well.

- Do people prefer Qwen coder for coding compared to QWQ-preview or other COT models?
  - What are pros would you say? I tend to find the thinking models catch their logical mistakes more often which saves time when I double check what it gives me back. Is it just the speed or is it actually more accurate for you?
- Qwq just takes to long to get an answer for my taste.

- Gemma never been good at coding.
  - Hell even the largest Gemini models have never been good at coding.

- Still waiting for someone with much better hardware to add longrope v2 and a reasoning finetune to qwen 2.5 coder 32b. With reasoning and a ridiculous context window extension that thing would be beast mode for local coding. longrope 2
- Also Chain of Draft: Thinking Faster by Writing Less
  - It does not work. I've tried. No difference.

- I love how Claude 3.7 without reasoning beats gtp models with reasoning. The reasoning hype is a bit too much I think, and the way those models work feels like a step backwards and a little step forwards

- yep its still the best if you want to skip reasoning llms. Some of the reasoning llms are as good and maybe even better but at the cost of waiting for it to think which in my experience is 3 times longer wait as reasoning llms question everything even if they are cabable of spitting out an answer quickly.
  - Yes I think waiting for reasoning is not worth (right now).

- QwQ 32B model is the best for Local with same power as Deepseek R1 671B Model. But requres 46 GB VRAM and 64 GB RAM, to be able to run it.

- QwQ 32b is even better in coding on my experience.

- ## 🤔 [what are the challenges of fine tuning deepseek coder or codellama on a real world codebase? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n1mnbz/what_are_the_challenges_of_fine_tuning_deepseek/)
  - i’m curious about fine tuning code llms like deepseek coder or codellama on an actual messy real world codebase.

- It's probably not something you want to do. You might be better off with a RAG solution, but normal grep/search from tools like Claude Code or Codex works pretty well with good prompting.

- when you say fine tuning isn’t worth it, was that based on trying it yourself and running into issues, or more from comparing results with rag and prompting? 
  - I've fine tuned before, and I have also used RAG. I specifically fine tuned on newer specs/docs for the ESP32, since most of the LLM's at the time had older data
  - I mean it worked, I was able to improve things, but it was a big effort, and RAG ended up working just as well or better.
  - The problem is code changes quickly, doing a fine tune on giant models would be impractical, as soon as you start changing the code, the fine-tune is outdated. RAG is a better solution, but even just regular grep/code searches work pretty well.

- Stop expecting perfection or near-perfection and learn to work with "good enough" results. If 30B is good enough, then focus on the remaining portion that needs human intervention. You can't change the model behavior, but you can change the way you use it, and how you approach the overall problem.
  -  I have tried all sort of tasks from vibe coding, refactoring, disassembly. The key thing is that you need to know better/more than the AI to be an effective human. I found myself learning things that were beyond my reach previously, so even though the AI had objectively failed at the task assigned to it, through the process I learned enough to carry on the task with whatever meaningful results it had produced, and take the rest over the finishing line.

- ## [LocalLLM for coding : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1ku7zjs/localllm_for_coding/)
- Go for the highest number of parameters you can fit in vram along with your context, then choose the highest quant of that version that will still fit.
  - I find that the 32b models have issues with simple code … I can’t imagine a 7b model being anything more than a curiosity.

- Qwen2.5-coder 7B and 14B are both solid for local coding tasks.
  - Deepseek-Coder (6.7B or 13B): very strong with Python and general coding.
  - Code LLaMA 13B: great for code generation and reasoning.
  - StarCoder2 (7B or 15B): worth a try if you can stretch the limit a bit. Quite powerful.
  - Phi-2 (2.7B): super lightweight and fast for simpler tasks.

- Devstral is really good right now and IMHO it's better than qwen2.5-coder.

- ## [Devstral vs DeepSeek vs Qwen3 : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ksat42/devstral_vs_deepseek_vs_qwen3/)
- Devstral is not better than qwen3-32B in general-purpose tasks. I guess it was trained to be specific to that openhands particular agent.

- ## [AIDER - As I suspected QwQ 32b is much smarter in coding than qwen 2.5 coder instruct 32b : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j5ao2j/aider_as_i_suspected_qwq_32b_is_much_smarter_in/)
- I'm not clear if QwQ was 3x better or 3x more expensive
  - Both

- Qwen coder instruct 32b had 8% and that model is quite useful.
  - Now QwQ 20% in Aider is really a lot .. From my tests is quite good in coding ...of course is not level DP 670b or o3 mini yet .

- couldn't you combine QwQ 32B as the architect model and use Coder 32B as the editor model?
  - Except locally you have to load and unload the models all the time if you don’t have enough vram.

- ## [OpenHands-LM 32B - 37.2% verified resolve rate on SWE-Bench Verified : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jocz51/openhandslm_32b_372_verified_resolve_rate_on/)
- The model's performance isn't necessarily superior to other models in general. The thing is, that this model was specifically fine-tuned to work effectively with the OpenHands tooling system, similar to how a new employee receives training from a senior developer on company-specific tools, environment, and processes.
  - Because the model was deliberately trained to use the OpenHands tools more effectively, it can leverage this specialized knowledge to achieve better scores on the benchmark. so it will do great in any benchmark where it can use openhands, and probably not as great in benchmarks that it cant.

- It's annoying their comparison graph doesn't even include qwen2.5-coder 32b which this is based on.

- Since it's not documented anywhere, and I don't see anyone talking about it: This fine-tune breaks the underlying Qwen2.5-Coder's FIM. It's faintly present, but often goes off the rails and starts chatting. I don't think this result is surprising, but I wanted to check.
  - Outside of FIM, I cannot distinguish it from Qwen2.5-Coder-32B in my testing. The performance is virtually the same for everything I tried.
- have you tested it inside openhands? the whole fine tuning was to make it interact better with openhands, the fact that it didn't lose much outside of it is actually surprising.
  - Ah, got it. I only ran it via llama-server with the model's default configuration through the usual completion API.

- ## [Why has no one been talking about Open Hands so far? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ksfos8/why_has_no_one_been_talking_about_open_hands_so/)
  - What’s weird is that OpenHands has 54k+ stars on GitHub. For comparison: Roo Code sits at ~14k, and Cline is around 44k. So it’s clearly on the radar of devs. But when you go look it up on YouTube or Reddit—nothing. Practically no real discussion, no deep dives, barely any content.

- They used to be Open Devin. I think they started after Devin made a bit of a splash. Rebranding might have killed a bit of name recognition.

- The reason it has not been mentioned here is because the benchmarks for OH + local LLMs were not so good compared to cloud services.
  - The OH team recently released an OH fine tuned LLM based on Qwen2.5 and now Mistral jumped in. And there is a good reason for their decision.

- I wanted to try OpenHands, but they don't make it easy to run the thing outside docker on a POSIX environment. They also don't make it easy to setup with your own API. I gave up after about an hour and switched to Roo to test the model.
  - We're serious and the stars are real, but totally hear you on the install issues. We've tried to make it as easy as possible to set up with Docker, but getting it to work without docker is not as easy as it should be and we'll work on it.

- It's more difficult to setup, and after downloading like 20GB of Docker images, you need to spend $ on Claude 3.7 tokens or whatever SOTA models to actually get good results because you're stuck with the limited web app.

- it somewhat works with docker, but tools like LocAgent(which relies on external openhands_aci package), or file upload don't work for me. maybe it's just not mature enough yet

- I decided to check the product and have been sitting with the settings for the whole day. Installing docker and running it is not a problem, but no matter how hard I try, it does not want to connect to the local model, although in the console via curl the connection to it goes. Plus I created a 10 GB container, this is quite a lot, I do not understand why it requires such a crazy size, this is almost the size of the entire operating system.
  - I had a similar experience today. Running both LM studio and Open hands with more permissive networking settings allowed open hands to reach the LM studio web server.
  - So maybe give that a try? IIRC it's add `--host` to the `docker run` arguments and for LM studio it was update the setting to run the web server so it doesn't only resolve over localhost, and instead broadcasts over the machine IP.

- ## [Best coding models for Consumer Hardware : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ij1aaz/best_coding_models_for_consumer_hardware/)
- Qwen2.5-coder-32b is probably best, it’s great with code quality, speed and most coding use-cases.
  - DeepSeek-V3 & DeepSeek-R1 are probably the very best, but are very very slow on consumer hardware, not practical and should be reserved for very challenging assignments only.
  - If you want to alter existing code, Qwen2.5-coder-32b is probably your best bet.
  - If you want to generate from nothing, I’m not sure which wins from practicality perspective. (Possibly QWQ-preview-32b, Qwen2.5-coder-32b, llama3.3-70b or Qwen2.5-72b).
  - If you can handle the very very long completion time, DeepSeek-V3-671b and DeepSeek-R1-671b should be number 1.
  - DeepSeek-V3 can run on consumer hardware, if your available disk space is enough, but expect it to take 20mins or so to complete prompt outputs with the unsloth’s most Quantized model, if you use the SSD (I used Samsung Pro 990 NVMe) as additional RAM.
  - The DeepSeek-R1 time expands massively with the R1 model due to the additional thinking and tokens that it does. (Took 3hrs to create Flappy Bird game for me in Python, V3 took a little over 20min by comparison, about 0.5 t/s )

- Try qwen2.5-codder, even 0.5b version seems capable of producing useful code (if you keep it small, like scripts etc.)

- ## [Best LLM for Coding : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ijrwas/best_llm_for_coding/)
- double down on the qwen-2.5-codder, even 0.5b is usable for small scripts

- qwen2.5-coder:32b is the best you can run, though it won't fit entirely in your gpu, and will offload onto system ram, so it might be slow.
  - The smaller version, qwen2.5-coder:14b will fit entirely in your gpu

- what will be the suitable ram size for 32b
  - You'll need at least 24 GB vram to fit an entire 32B model onto your GPU.
  - Your GPU (RTX 4080) has 16 GB vram, so you can still use 32B models, but part of it will be on system ram instead of vram, so it will run slower.
  - You can also try a smaller quantization, like qwen2.5-coder:32b-instruct-q3_K_S (which is 3-bit, instead of 4-bit, the default), which should fit entirely in 16 GB vram, but the quality will be worse

- Is there anything I need to tweak for it to offload into system RAM? Because it always gives me an error about lack of RAM
  - No, ollama offloads automatically without any tweaks needed

- I tried qwen coder 2.5 u really need to use the 32b and q8 and it's way better than the 14b. I

- Roocoder which is based on cline is probably better. It's scary cause it can run in auto. 
  - you could leave it over night and it could fix the code or totally screw up and loop all night lol. 

- Run tests on the the q8 vs q6 vs q4. The 32b model is way better than 14b btw

- ## [Qwen-2.5-Coder 32B – The AI That's Revolutionizing Coding! - Real God in a Box? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gp84in/qwen25coder_32b_the_ai_thats_revolutionizing/)
- I've been using the Q4_0 gguf version of the Qwen2.5 Coder Instruct, and I'm pleasantly surprised. Despite the significant loss in quality due to gguf quantization—where the loss, although hoped to be negligible, is still considerable compared to full loading—it performs similarly to the GPT-4o-mini and is far better than the non-advanced free version of Gemini.
  - However, it still doesn't come close to GPT-4.0 for more complex requests, though it is reasonably close for simpler ones.

- It is currently 5th place on Aider leaderboard, above GPT-4o, but slightly worse than old Claude Sonnet 3.5 and o1, and quite worse than new Claude Sonnet 3.5.

- 32gb is a nice compact size. I may pull the trigger on a 48gb mac mini pro.

- Vllm absolutely smashes llama.cpp in speed
- Does LM Studio use Vllm behind the scene? I do know Ollama uses llama.cpp
  - LM Studio is also llama.cpp based

- ## [Best LLM Model for coding : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gkewyp/best_llm_model_for_coding/)
- just going by the basic rule of thumb.if you want the best model you can fit on your machine always going with q4 of larger model

- how this 32b can be better than 7b-coder tuned version?
  - coder finetunes are definitely better than there corresponding base models, but Due to the increased parameters, it is more accurate in first try and also adheres to prompt better and also understands the problem way better
- the 32b is a lot lot lot better for coding.

- The larger models can be smarter, but if you don't have the spare VRAM, it might not be able to look at your whole project.

- Someone suggested Codestral-22B-v0.1-IQ3_M in another thread, and Ive been using that one for coding ever since. Mostly for python. Its really good, way better than all other I have tried.
  - Most of the time it gives me run ready redesigns and code, quite impressive.

- ## [IMO the best model for agents: Qwen2.5 14b : r/ollama _202411](https://www.reddit.com/r/ollama/comments/1gh23zo/imo_the_best_model_for_agents_qwen25_14b/)
  - Today, I deployed Qwen2.5 14b and I find it's function calling, CoT reasoning, and instruction following to be fantastic. I might even say, better than GPT 4/4o. For all my use cases, anyway.

- how do you do function calling?
  - I use either langchain or the Vercel ai sdk for function calling personally

- This model is fantastic, I just tested it for coding as well and it is the only quantized model which detects SQL syntax error (e.g., missing of comma) despite being smaller than 10 GBs.

- ## [Appreciation post for Qwen 2.5 in coding : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1fn0a37/appreciation_post_for_qwen_25_in_coding/)
  - I have been running Qwen 2.5 35B for coding tasks. Ever since, I have not reached out to Chat GPT. Used Sonnet 3.5 only for planning.. It is local and it helps with debugging. generates good code
  - I am also impressed with its instruction following and JSON output generation. 

- The 14B model (Q8) was doing better than 35B (Q5) during my testing. But it was pretty smart overall.

- Sonnet for planning? Like how?
  - For the architecture and design of a solution. Also thinking through all the goods and bads about a particular design choice.

- Why not Qwen-Code?
  - Because I want the model to support other general purpose use cases too.

- ## [Best LLM right now for code generation? : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1b1tycl/best_llm_right_now_for_code_generation/)
- I’m confused, why is codellama-70b so bad on this leaderboard
  - Llama 70b feels more like a ESG score replenisher. Practically brain dead. Wonder if finetunes will uncover anything useful beneath 
- I haven't used it, but I heard it's been too censored and it affected its coding abilities. But who knows.

- ## [CodeLlama 70b censorship : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1anpi6c/codellama_70b_censorship/)
  - the response: I cannot fulfill your request as it goes against ethical and moral principles, and it is also illegal and potentially harmful.

- CodeLlama 70b have a prompt format issue. It make it spew censorship stuff
- Yeah, that model is quite censored indeed but its also very sensitive to its prompt template it seems

- This is a false positive, probably some sub classifier model needs to be adjusted.

- [Why is CodeLlama on huggingface so opinionated, biased and arrogant ? : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1b0ss2t/why_is_codellama_on_huggingface_so_opinionated/)
  - Probably because it was at some point a general model which was further trained for code. By using a word like "appropriate" you are probably triggering a lot of political/sociological/emotional thoughts which is suboptimal if you are trying to code.

- ## [Use self-hosted Code Llama 70B as a copilot alternative in VSCode : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1agerx0/use_selfhosted_code_llama_70b_as_a_copilot/)
- The gotcha is having hardware fast enough to run it at usable rates

- codellama fucks up and refuses a lot of work, I wouldnt focus on it too much until someone finetunes the base model for instruct
  - The model is fine once you get the new and complex prompt format right.

- It's a great idea on paper, but perhaps 70B is too big for most current consumer hardware.

- ## 🚀 [Today we’re releasing Code Llama 70B: a new, more performant version of our LLM for code generation  : r/singularity _202401](https://www.reddit.com/r/singularity/comments/1ae0rap/today_were_releasing_code_llama_70b_a_new_more/)
- is there a realistic way to run a 70B model on a 4090, with maybe 1-2 token/sec or better?
  - For Mixtral I get 5 token/s haven't tried an 70B (With 5 layers on CUDA and tensorrt). I am on DDR5 with a 7950X3D though. Ram speed seems to be the main issue.

- ## [Code Llama Released : r/LocalLLaMA _202308](https://www.reddit.com/r/LocalLLaMA/comments/1601xk4/code_llama_released/)
  - All models support sequence lengths up to 100, 000 tokens
- That could be made more nuanced. They support input context sequences of up to 100, 000 tokens. The sequence length of the underlying model is 16, 384.
- Can you help us newcomers understand why this is so exciting?
  - The context windows is basically the short term memory of the LLM. Larger window size allows "pre-initializing" it with more data. In this case a larger portion of your existing codebase can fit in, so it can provide more relevant answers and code-completion in that context.

- the key to the long context length is actually changing the base period!!! That was exactly the NTK scaling post here promoted, yet they didn't mention it at all. So they rushed out the linear interpolation paper to divert researchers' attention, but they secretly doing NTK

- [Codellama - Has anyone found "Codellama 34B Instruct" to be uncooperative? : r/LocalLLaMA _202308](https://www.reddit.com/r/LocalLLaMA/comments/160zxjd/codellama_has_anyone_found_codellama_34b_instruct/)
  - Just an update: issue appears to be definitely solved by using the correct parameters when loading and querying the model. 
  - Fortunately many of the popular frameworks like text-generation-ui are getting updates that use the correct settings for this new class of codellama models
# discuss
- ## 

- ## 

- ## [Are you using local LLMs to power Cline, RooCode, Cursor etc.? What is your experience? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ivhrbn/are_you_using_local_llms_to_power_cline_roocode/)
- I use Qwen Coder 14b/32b for code refactoring and Qwen Coder 3b for autocomplete with the Continue.dev extension for VSCode. It's not quite on par with Github Copilot or Cursor, but it works well enough.

- One nice feature of continue.dev is the drop down for selecting a model. I have qwen coder 7b or 14b running locally and a selection of models via Openrouter. When my local models isn't up to the task, it just takes a second to switch to something more powerful.
  - I have qwen coder 7b for auto complete and it does really well. The number of times it gets it right is kind of amazing.

- Most of these tools use a temperature of 0. Small local models need to be controlled to avoid looping. In tabbyAPI, you can force the temperature and other settings to what you please

- Deepseek Coder (and coder V2 Lite) is a very old weak model. Qwen2.5 Coder 7b is a starting point for a useful model. 

- ## [Aider's Architect/Editor approach sets new SOTA for AI code editing, achieving 85% pass rate : r/ChatGPTCoding _202409](https://www.reddit.com/r/ChatGPTCoding/comments/1fshzxl/aiders_architecteditor_approach_sets_new_sota_for/)
- This method separates code reasoning and editing tasks between two models:
  - Architect model: Focuses on solving the coding problem
  - Editor model: Translates the solution into well-formatted code edits
  - Best combination: OpenAI's o1-preview (Architect) with DeepSeek or o1-mini (Editor)
- If you look at the llm.logs in aider, the architect always writes out the code, the editor model will merge the code with the diffs. So the architect model does the entire thing with code output.
  - So if you are using o3mini, as architect, it is the main code generator as well, and if you are using Sonnet 3.7 as the editor model, it actually wastes the code generation powess of that model, because it only uses it to "Edit" the code back into your files.
  - This is where I'm confused on how it "architects". I would call it Code generator model, and a Code patch model.

- you're responding to a 7 month old comment. Even Paul G himself doesn't use Architect mode anymore!

- This is the way to do it. 
  - AutoGen did this years ago but it's a PITA. CrewAI is mostly OK but it's more designed for process instead of code generation

- ## 🤔 [Should I use reasoning for coding? : r/DeepSeek _202503](https://www.reddit.com/r/DeepSeek/comments/1jnzdb3/should_i_use_reasoning_for_coding/)
- no, Deepseek V3 writes code much better than R1.
  - In programming, R1 makes sense to use for planning, precisely..when you need to reason... 
  - That is, when you are planning something very complex, a model like V3 simply gets confused, wants clear instructions, is not very good with "but, however" .. then you use R1 which does the reasoning and spits out a sensible plan...then for the actual implementation, use V3 anyway...it is cheaper and if it is just about coding, it works better.
- If V3 is better why is R1 ranked higher for coding benchmarks? And why is it that the best coding models are all reasoning?
  - You are probably right and I expressed myself badly, although in my specific case V3 literally wrote better code than R1

- ## 🏠 [Has anyone successfully used "thinking" models for large coding projects? : r/ClaudeAI _202502](https://www.reddit.com/r/ClaudeAI/comments/1ifgtrz/has_anyone_successfully_used_thinking_models_for/)
  - The reason I ask is because I don't know if I'm just missing something when it comes to thinking models, but aside from the early code drafts and/or project planning. I just cannot successfully complete a project with them.
  - I'm starting to think that maybe models with this type of design paradigm just isn't compatible with complex programs given how many "reasoning" loops it has to reflect on, and thus it seems to constantly muddy up the context window with what it "thinks" it should do. Rather than what it is directed to do.
  - Everytime I try one of these models it starts off great, but then in a few hours I'm right back to Claude after it just becomes too frustrating.

- The problem I've observed was typically through using aider (where I have a $700+ in API costs from this project alone) where Claude incessantly recommends "improvements" that adds complexity and breaks things
  - But I noticed that happens significantly less when I use code mode in Roo Code
  - I think some of that rabbit-hole behavior might be due to the system prompt as I noticed Roo Code doesn't tend to "suggest" improvements that I never asked for.
  - The fundamental limitation IMO is that you really need to be fully capable of doing the entire project yourself without the use of AI. Then at that point AI becomes a force multiplier.

- I typically use reasoning models like you, then shift to Sonnet as wel

- For what it’s worth, this is the exact kind of workflow Aider (open source console-based dev tool) encourages.
  - Basically you use the thinking model to prototype the code (in Aider this is called “architect” mode), then when it comes to outputting actual code, you use a different “coder” mode that leverages a simpler chat model to write the code (like Sonnet, GPT4o). The chat model operates on the back of the notes and specs written out by the reasoning model to write the code to spec.
  - The Aider dev did a bit of research and iirc discovered this works better than just using the reasoning model for everything. And is obviously more affordable, too. It’s very interesting.
  - Anecdotally, this vibes with how I’ve used gen AI in my coding workflow before reasoning models even came to be. I’d write up a detailed technical spec of how it should be done, then let Claude or GPT4o write up the first draft of code, and iterate from there

- ## 🤔 [Why is Qwen 2.5 the most used models in research? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kyrhr7/why_is_qwen_25_the_most_used_models_in_research/)
- We tuned qwen 2.5 7b in our paper, general choice reasons - sota for their size, strong multilingual support, 7b variant is good for restricted compute resources while being smart enough for tasks. And no unexpected tricks are expected from the qwen team, like models are not overly tuned on some style/emojis in response, not overly guarded like early Gemma was etc.
  - For next experiments we want to try falcon h1 models and qwen3, but qwen3 being half thinking makes it harder to tune(you kind of need both reasoning and non-reasoning samples in your dataset), so choice will depend on how the data processing will go.

- For a while there it seemed like everything was Llama 2.

- May be related to how well it works with RL in general, so well that using random rewards increases the performance.. https://www.interconnects.ai/p/reinforcement-learning-with-random

- What I like about Qwen is that they come in all sizes. There is a Qwen model for every hardware.

- ## [Difference between Qwen2.5 and Qwen2.5-Coder for NON coding tasks? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i1jlop/difference_between_qwen25_and_qwen25coder_for_non/)
- 14b coder lose about 10% on mmlu and ifeval compared to 14b normal. 

- If you can go up to a larger model then I recommend Sky T1, it's a finetune of Qwen 2.5 32b non coder, so it has all of the non coder versions capabilities but is also better at coding than the coder version in my experience.

- ## [How much worse is Qwen2.5-Coder for non-coding tasks? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1inazl9/how_much_worse_is_qwen25coder_for_noncoding_tasks/)
- Qwen-Coder at least produces sensible output and tries its best, but in my experience is still a very poor model for this especially consider its size.

- About 4 LiveBench percentage points worse. I'd recommend switching models based on the task at hand.

- ## [Wow anthropic and Google losing coding share bc of qwen 3 coder : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1msrnqq/wow_anthropic_and_google_losing_coding_share_bc/)
- qwen coder is free
  - so people use anthropic and google models as architects, and then qwen coder for the coding
  - the result is qwen giving people free inference in exchange of anthropic and google outputs , to make next qwen better planner and more compatible to anthropic and google outputs
  - and the other result is anthropic and google losing income and power.

- Qwen 2.5 variants were already high on my capabilities tests, and qw3 is even better.

- GPT-OSS is a competent coder but it's vendor knowledge is waaay behind Qwen so 235b does out code it.

- 
- 

- ## 🧩 [What is the current best FIM model that I can run on a single 3090? Still using Qwen 2.5 Coder : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1miuctw/what_is_the_current_best_fim_model_that_i_can_run/)
- For the best Fill-in-the-Middle (FIM) performance on a 3090 with continue.dev, go with Codestral-22B due to its specific FIM optimization and official integration; 
  - for more complex, repo-level agentic tasks, Qwen3-Coder-30B is a strong alternative.

- I'm kinda new to this "FIM model" concept, is it the go-to type of model for code auto-completion? I am developing a auto-completion feature and I am trying to figure out if it'd be worth trying out FIM models. Also, is Qwen 2.5 Coder good?
  - 1. Yes
  - 2. You should indeed use FIM models. You can see continue.dev for an example: they have autosuggestion feature and recommends qwen coder in local deployment
  - 3. Yes, good enough for my needs

- ## [(Noob here) gpt-oss:20b vs qwen3:14b/qwen2.5-coder:14b which is best at tool calling? and which is performance effiecient? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mjz1ow/noob_here_gptoss20b_vs_qwen314bqwen25coder14b/)
- gpt is generally better at tool calling https://gorilla.cs.berkeley.edu/leaderboard.html
  - general knowledge is harder to gauge, ask it some questions in your field and see if it gets it right. Heard gpt-oss is bad at front end
  - Most importantly: Try it yourself. Also try the Qwen3 30b MOE, it's a little larger but the benchmarks place it close with the 20b MOE
