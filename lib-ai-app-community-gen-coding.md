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

- ## [How to tell cline must use recent documentation for a python lib? : r/CLine](https://www.reddit.com/r/CLine/comments/1nw95t9/how_to_tell_cline_must_use_recent_documentation/)
- The context7 MCP server is tailored made for this.
  - Add context7 mcp. Then add a global rule to fetch lastest docs before planning.

- Create your own documentation and put it in a docs folder. And then @ the file in your prompt. EZPZ

- is it going to create a rag or context injection?
  - Just context injection.

- ## [I tried vibe coding for 4 weeks, here’s why I’m dialing it back : r/vibecoding](https://www.reddit.com/r/vibecoding/comments/1nu8s3y/i_tried_vibe_coding_for_4_weeks_heres_why_im/)
  - And honestly? The first week felt incredible. I was in the zone, shipping features fast, and it felt like I was finaly coding for fun again.
  - But as the weeks went on, the cracks started to show.
- The Upside:
  - Super fast for prototyping.
  - Way less friction to just start building.
  - It did bring back that “hacking for fun” feeling.
- The Downside:
  - Code chaos: By week 3, I had no idea why certain functions worked or if they’d break something else.
  - Debuging nightmare: AI suggestions + zero structure = hours wasted chasing sily bugs.
  - Feature whiplash: I kept adding things randomly, which meant ripping out work a few days later.
  - Momentum drop: Without a roadmap, I started losing motivation once the shiny feeling wore off.
- What I Learned:
  - Vibe coding is amazing for exploration and quick hacks.
  - But if you actually want to scale a project, you need at least some structure (docs, tests, basic planning).
  - For me, the balance is: vibe code the prototype → switch to structured dev once the core idea works.
- So yeah… vibe coding was fun, but I don’t think I could rely on it for anything bigger than a proof of concept.

- Who said you should vibe code without a roadmap ?

- ## 🤔 [Hot take: ALL Coding tools are bullsh\*t : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nu6kjc/hot_take_all_coding_tools_are_bullsht/)
- We have these incredible language models—DeepSeek 3.2, GLM-4.5, Qwen 3 Coder—that can understand complex problems, reason through edge cases, and generate genuinely good code. And what did we do? We wrapped them in so many layers of bullshit that they can barely function.
- The Scam: Every coding tool follows the same playbook:
  - Inject a 20, 000 token system prompt explaining how to use tools
  - Add tool-calling ceremonies for every filesystem operation
  - Send timezone, task lists, environment info with EVERY request
  - Read the same files over and over and over
  - Make tiny edits one at a time
  - Re-read everything to "verify"
  - Repeat until you've burned 50, 000 tokens
  - And then they market this as "agentic" and "autonomous" and charge you $20/month.
- The Reality:
  - The model spends 70% of its context window reading procedural garbage it's already seen five times. It's not thinking about your problem—it's playing filesystem navigator. It's not reasoning deeply—it's pattern matching through the noise because it's cognitively exhausted.
  - You ask it to fix a bug. It reads the file (3k tokens). Checks the timezone (why?). Reviews the task list (who asked?). Makes a one-line change. Reads the file AGAIN to verify. Runs a command. Reads the output. And somehow the bug still isn't fixed because the model never had enough clean context to actually understand the problem.
- The Insanity:
  - What you can accomplish in 15, 000 tokens with a direct conversation—problem explained, context provided, complete solution generated—these tools spread across 50, 000 tokens of redundant slop.
  - And the worst part? It gives worse results. The solutions are half-assed because the model is working with a fraction of its actual reasoning capacity. Everything else is burned on ceremonial bullshit.
- The Market Dynamics:
  - VCs threw millions at "AI coding agents." Companies rushed to ship agentic frameworks. Everyone wanted to be the "autonomous" solution. So they added more tools, more features, more automation.
  - They optimized for demos, not for actual utility. Because in a demo, watching the tool "autonomously" read files and run commands looks impressive. In reality, you're paying 3x the API costs for 0.5x the quality.
- The Simple Truth:
  - Just upload your fucking files to a local chat interface like LobeHub (Open Source). Explain the problem. Let the model think. Get your code in one artifact. Copy it. Done.
  - No tool ceremonies. No context pollution. No reading the same file seven times. No timezone updates nobody asked for.
  - The model's full intelligence goes toward your problem, not toward navigating a filesystem through an API. You get better code, faster, for less money.
- The Irony:
  - We spent decades making programming languages more expressive so humans could think at a higher level. Then we built AI that can understand natural language and reason about complex systems.
  - And then we forced it back down into the machine-level bullsh*t of "read file, edit line 47, write file, run command, read output."
  - We took reasoning engines and turned them into glorified bash scripts.
- The Future:
  - I hope we look back at this era and laugh. The "agentic coding tool" phase where everyone was convinced that more automation meant better results. Where we drowned AI in context pollution and called it progress.
  - The tools that will win aren't the ones with the most features or the most autonomy. They're the ones that get out of the model's way and let it do what it's actually good at: thinking.
  - Until then, I'll be over here using the chat interface like a sane person, getting better results for less money, while the rest of you pay for the privilege of context r*pe.

- Can you share the prompt & model used to generate this post? thxbye

- that's exactly what aider is doing. So there is one coding tool that is not bullshit?
- It doesn't have any tools and repo map is disabled with a single argument. 2k tokens for system prompt is nothing for modern models. However tool calling agentic tools are still more minimal then this because they can break down task into smaller steps and solve them separately in new context not connected to initial one.

- Qwen code (free 2000 api) has been an extremely valuable cli agent that I've been using geting it to do desktop tasks fast and raw. Its cost vs a human person per hour is still cheaper when you know the scope of the task. How big of a code base are you using that copy pasting is sufficient and all in a single file? Seems like you are a very basic end user or doing things with limited scope putting an entire framework into one file.

- models are stateless, so you are sending all initial context plus sliding context on each request. optimization can happen if it can output a summarized context that is still relevant for the next request.

- Integration at the IDE level allows the LLM to go find these links itself rather than putting the onus on you. It saves time.

- ## [Sometimes I feel like Architecture mode is a waste of tokens. Am I using it wrong? : r/RooCode _202509](https://www.reddit.com/r/RooCode/comments/1nmsu61/sometimes_i_feel_like_architecture_mode_is_a/)
  - I've seen many people saying how architecture mode is a life saver and it does wonders, however in my experience it hasn't yielded much results, here's why:
  - I generally do small incremental development steps. For example: 1- build the database schema, 2 - build the seed, 3- use the schema to builde api endpoints, etc. etc..
  - I feel like Architecture mode is great if you're trying to one-shot a small app with a not very detailed prompt. It designs the whole thing and then you switch to coding mode to build it. However the adjustment and debugging later is massive. Incrementally just ask for coding has made more sense to me so far.
  - Am I doing this wrong? How do you guys use architecture mode in your workflows to get good results?

- I've used it to build documentation if I'm writing a markdown file. But typically, I just go and use the ask mode.

- ## [Do local LLMs do almost as well with code generation as the big boys? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1naiud3/do_local_llms_do_almost_as_well_with_code/)
- You can run qwen 3 coder with 512GB M3 ultra easily.
  - Not the 480 though I dont think. Read and a few responses indicate that + context would need about 1TB of ram.
- The best model that's open source right now i think is still Qwen 3 Coder 480B; in my experience it codes pretty close to Sonnet 4 after having used both pretty extensively. But you're going to want it in 16-bit which would need about 1TB just to load. 

- Coding may be more sensitive, but anything above q6 is not really noticeable. 
  - Some of the best models are trained at q8 such as DeepSeek, Kimi and GLM 4.5. GPT OSS is 4 bit natively. I use gpt oss 120b every day for coding and I run it local. 
  - FP16 is for training. It has no place in inference.

- Absolute not. I have a Mac M3 Ultra 512gb, and it can run Kimi, Qwen480, Deepseek, GLM 4.5... but the thing most people don't understand is if you try and feed it a prompt with 100k tokens it's going to take 5-10 minutes just to process that, even if you get 20 t/s after that.
  - It's basically unusable for coding (which often times requires many prompts of larger context).

- ## [Is there a way to use 2 models at once? Deepcoder nor phi-4 doesn't generate use tool available to it's disposal just tells user what to do. Like an interpretation model. : r/RooCode _202504](https://www.reddit.com/r/RooCode/comments/1k936cu/is_there_a_way_to_use_2_models_at_once_deepcoder/)
- A lot of models don't do tool calling natively. 
- Try Qwen2.5-Coder 14b can do

- ## 🤔 [getting lost in the speed of model updates. What is best for the planning phase, what is best for the coding phase : r/CLine _202502](https://www.reddit.com/r/CLine/comments/1iji10g/getting_lost_in_the_speed_of_model_updates_what/)
- Here’s an Aider blog post making the rounds stating that R1 for Architect and Sonnet for Editor (roughly equivalent to Cline’s Plan/Act I believe) is their new SOTA for their polyglot benchmark.
  - [R1+Sonnet set SOTA on aider’s polyglot benchmark | aider _202501](https://aider.chat/2025/01/24/r1-sonnet.html)

- A common pattern is:
  - DeepSeek R1 for Planning (R1 is a reasoning model)
  - 3.5 Sonnet for Acting (3.5 Sonnet is best coder)
  - DeepSeek V3 is also solid for coding

- Reasoning model to architect the solution, standard/cheaper model for execution

- TLDR: For cost efficiency: I would use R1 for the architect and whatever the best Gemini model is for coding as the editor

- ## [Which model combinations have you tried for the best performance (also cost rationally) in Plan and Act mode, especially working with memory bank in a large project? : r/CLine _202503](https://www.reddit.com/r/CLine/comments/1j8e7ji/which_model_combinations_have_you_tried_for_the/)
- If you're looking at the Aider LLM Benchmarks for coding stuff, the best value for tricky coding tasks right now is using DeepSeek R1 for plan-mode and Claude 3.5 Sonnet for act-mode. If you're doing something simpler, DeepSeek Chat V3 is a cheaper option.

- I've been using Gemini 2.0 flash for planning/architecture and then implementation with Claude 3.5 sonnet. I don't really know if I get better results than with deepseek, but I had so much waiting time with deepseek r1 it was practically unusable. 

- I see a lot of people advocating for using Claude for act mode and another llm to plan. The issue I have with this is that the plan stage uses a relatively small amount of tokens compared to act, so you aren't really saving much money relative to using Claude for everything.

- ## [Is Plan / Act Conceptually Broken or am I using it wrong? : r/CLine _202503](https://www.reddit.com/r/CLine/comments/1jd9nuf/is_plan_act_conceptually_broken_or_am_i_using_it/)
  - I really liked the idea of Plan and Act modes, especially using a cheap model (R1) for planning and reserving premium model (Sonnet) for Act mode, however......
  - by having these two modes in the same chat and switching between them you end up carrying massive amounts of context/message history (which was cheap to accumulate with planning model) into your messages with your 'Acting' model, and the costs suddenly jump up for every message.
  - if you were providing the Act mode with an actual plan it shouldn't need all that historical context, it should be given something far more distilled, with just enough context to complete the task you are asking of it
  - I think theres great potential in this plan/act division but I think its currently not modelled correctly in Cline - I guess Im essentially suggesting this should be 2 agents instead of 1..... with the 'Act' agent able to feed back to the 'Plan' agent and ask for more info etc.

- I think you might be using it backwards. You're supposed to use a smarter model to do planning and then pass that plan to a smaller model to execute.
  - I experimented this weekend switching back and forth between a cheaper model and a more expensive model for act and plan. I think the current version of Cline needs some tuning still.
  - The feature is going to save a lot of cost once it's dialed in. But right now I've found doing it manually gets great results.

- Not a smarter model. A reasoning model. R1 architect and Claude coding is top of the list in terms of price/performance and is very close to the top in pure performance

- In times when you use prompt caching, it makes little sense to use different models in my opinion. But yes, use the best model for planning

- act mode shares the cache from plan mode, it preloads the plan (you can test this by having a chat with plan mode, switch to act and asking it what it knows about xyz)
  - So all you do is get the best language model for your task (aka Opus for coding) to explain to you a plan, how to implement, best implementation principles, and examples of code etc.
  - then switch to Act where you're using a cheaper model, and tell it do the thing. this way you will get the claude-3-5-haiku-20241022 model to make some surprisingly acceptable code for peanuts.

- Plan, chat with it until you happy then save to MD. Load MD in act and do the job.
  - You can extend this with Roo, it has sub tasks which run in separate context and return result to main task
  - Subtasks are not silver bullet but its very handy addition

- Can Cline write to Memory Bank without going into Act mode?
  - Yes it can. Its md files
  - We save it in MD so we can reset context and you can edit it a bit before running code/act mode

- I don’t switch back and forth. Just Plan once, the act until the task is done. You can give it feedback in act. I use Somnet for both, because the cost isn’t more than paying someone else to do it.

- ## [Strategy for Coding : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1nf8o7d/strategy_for_coding/)
  - Qwen 3 Coder can benefit from the thinking output of another model. If you copy/paste your prompt and the thinking output from something like Qwen 3 Thinking, it seems to perform better than simply giving either the prompt alone.

- Wonder if you could fake it in the prompt by asking Coder to write a document discussing the problem and creating a to do list before anything else
  - sorta but it's not as good as actually using another qwen. the other qwen doesn't even have to be that big

- I guess you're not using a tool like Cline where you enter into Plan or Act mode.
  - Plan mode lets you chat to the LLM (I prefer a thinking one instead of instruct) about the requirements. During this mode, it can ask to look at files in the project to generate a better plan. The final part of Plan Mode is asking the User if they want to proceed with the generated plan and enter Act Mode.
  - In Act Mode, will perform creating files, updating files, deleting. And can also run/validate the code if you configure your rules properly.
  - Another cool thing about cline is you can actually have two different LLMs for the Plan and Act modes. In Plan mode, i'll leverage Qwen3 4B thinking for rapid back and forth on the requirements. Then when Act mode is enabled, use Qwen3 Coder 30B A3B to consume the plan and do the work.

- ## [What is your system prompt for Qwen-2.5 Coder 32B Instruct : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gqagzg/what_is_your_system_prompt_for_qwen25_coder_32b/)
- Start your system prompt with You are Qwen, created by Alibaba Cloud. You are a helpful assistant. - and write anything you want after that. Looks like model is underperforming without this first line.

- for the 7B version, my Qwen coder suddenly started working better with LM Studio blank preset. Increased the context length, lowered temperature to 0.2, works great.
  - any system prompt made the generation worse. That said, any errors in prompt seem to break something, but that's probably the 7B model only.

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
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [New to local, vibe coding recommendations? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nh16ft/new_to_local_vibe_coding_recommendations/)
- I still prefer Aider. Their system messages are under 2k. Crush is like 10k iirc. Idk about cursor/roo.
  - Sure it's not agentic but I prefer going one step at a time with the bot. Plenty of /undo's and /clear's.

- Keep using Cursor. 12GB VRAM is too low. The Vibe code part starts around 16GB but BARELY.

- ## 🧑‍🏫 [Engineer's Guide to Local LLMs with LLaMA.cpp and QwenCode on Linux : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nhh1v1/engineers_guide_to_local_llms_with_llamacpp_and/)
  - I will share my local AI setup on Ubuntu that I use for my personal projects as well as professional workflows (local chat, agentic workflows, coding agents, data analysis, synthetic dataset generation, etc).
  - Compile LlamaCPP on your machine, set it up in your PATH
  - Use `llama-server` to serve local models with very fast inference speeds
  - Setup `llama-swap` to automate model swapping on the fly and use it as your OpenAI compatible API endpoint.
  - ntegrate local AI in Agent Mode into your terminal with QwenCode/OpenCode
  - Test some local agentic workflows in Python with CrewAI 

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
- gpt-oss is MOE 20b/3b active, so it (should be) faster. You can try it yourself to make sure it's right on your system
