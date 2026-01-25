---
title: lib-aikit-ollama-community-janai
tags: [community, janai, large-language-model]
created: 2026-01-14T19:05:02.316Z
modified: 2026-01-14T19:05:15.969Z
---

# lib-aikit-ollama-community-janai

# guide

# draft

# xp-janai
- cons
  - 不支持直接使用已有的.safetensors文件

- 使用ollama或lmstudio的模型api时，需要关闭clash全局代理
  - http://localhost:11434/v1
  - http://localhost:1234/v1

- 
- 
- 
- 
- 

# xp-llamafarm

- 
- 
- 
- 
- 
- 
- 

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## [goal: Jan Desktop can use browser](https://github.com/janhq/jan/issues/6873)
  - Enable Jan to safely use a web browser via MCP (like BrowserMCP/ChromeMCP). 
  - Let agents navigate, read pages, click, or type with clear user consent.
  - ✅ 202601已支持

- ## 📌 [epic: Decouple cortex.cpp from Jan _202504](https://github.com/janhq/jan/issues/4906)
  - Decouple cortex.cpp from Jan, so that cortex.cpp acts like a model provider. It should not be affected when using other model providers.
- [epic: llama.cpp extension in Jan  ](https://github.com/janhq/jan/issues/4875)
  - This epic is to introduce new modle provider extension in Jan, this llama.cpp extension replaces legacy cortex.cpp which is deprecated.
  - Now all of the cortex.cpp features move to this extension such as: GGUF model management Hardware and engine variant control
- [goal: Jan Desktop uses llama.cpp and deprecates Cortex ](https://github.com/janhq/jan/issues/4941)
  - Integrate llama.cpp backend, by: Embedding llama-server via `std::process::Command`

- 
- 
- 
- 
- 
- 
- 

# discuss-roadmap
- ## 

- ## 

- ## 

- ## [Jan: Ollama integration for existing model support _202409](https://github.com/orgs/janhq/discussions/3629)
  - People store models they downloaded from Ollama. In Jan, we should let them run models they already downloaded. This is probably the most commonly asked feature from r/LocalLLaMA.

- just added a new provider and it worked

- ## [idea: MLX support · Issue · janhq/jan _202506](https://github.com/janhq/jan/issues/5485)
  - Jan does not currently support MLX as an inference engine
- Once we finish with the llama.cpp extension, I think supporting MLX won't be too difficult. We already bundle `uvx` with Jan.

# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🆚 [LM Studio no new runtimes since weeks..? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o4m7yt/lm_studio_no_new_runtimes_since_weeks/)
- Given Jan is actually open source and development is progressing more rapidly AND it's consistently more up-to-date, I don't see a reason to use LM Studio anymore other than nostalgia.
  - Do you know why Jan lags behind in making the latest models accessible through their model hub? GOtta give it to LM Studio for their super neat integration that lists models as soon as they appear on HF, whether you can run them or not...

- LM Studio gets kickbacks for promoting certain models in their model hub. For example, OpenAI paid them to promote the GPT-OSS rollout and it was one of the largest chunks of money they've ever made for anything they've ever done.
  - So Jan doesn't care as much about funneling people to their "hub" to download specific hand-picked models. I agree it's something LM Studio does much better and Jan could do better though. Until Jan allows actual search of Hugging Face and a similar compatibility screen to help new users, it will continue to be worse in this area.

- I was one of the first supporters of Jan and love to hear those great news. I saw that it is possible to import .ggufs into Jan, but with super large models such as GLM-4.6 that I downloaded through LMStudio, it is split into three .gguf files. Do you know how I can reuse them instead of re-downloading them?
  - cat model.gguf-split-a model.gguf-split-b model.gguf-split-c > model.gguf
  - [or on windows powershell] Get-Content model.gguf-split-a, model.gguf-split-b, model.gguf-split-c -Raw | Set-Content model.gguf -NoNewline
- If they're legitimately split models, I don't think that works. That method was for manual split.

- ## [Is it possible to use Jan AI server instead of LM Studio server in Obsidian Copilot? : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1f5vswt/is_it_possible_to_use_jan_ai_server_instead_of_lm/)
- You could also try changing Jan port to 1234 to attempt to use original (unchanged) LM Studio option. If Obsidian doesn't use any uncommon API features, maybe it could work.

- Yep, there's a local API server. In the left ribbon, click the icon right above settings. Turn on the server. Visit: http://127.0.0.1:1337 to verify (there should be an api playground)
  - Make sure you are on v0.5.3+

- ## [Jan vs LM Studio : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j7qol7/jan_vs_lm_studio/)
- LM studio does have Rocm support, but only for RX6800 or higer or newer variants(7600, 7600XT, 7800....).
- I recommend you to stay with LM Studio, which responds more quickly to newer models than other frontends. Jan was just a full of frustrating experience as I tried it.

- Check settings in Jan i think it doesn’t offload all layers to gpu fully by default

- ## [Jan. AI with Ollama (working solution) : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lsoflk/janai_with_ollama_working_solution/)
  - I already have lot of downloaded local llms in my system via ollama.

- Go to Settings > Model Providers
  - Click OpenAI
  - In API Key field add `ollama` as api key & in Base URL enter `http://localhost:11434/v1` equivalent endpoint.
  - In Models list you can see many already available models of OpenAI you can keep it or delete it (but it's optional)
  - In Models there is and option to add new model (there is plus icon), so click on it and add you local ollama model name in my case it was `qwen2.5-coder:14b` (to see available models with exact name run ollama list command in terminal)

- ## 🎯 [Jan now auto-optimizes llama.cpp settings based on your hardware for more efficient performance : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nvzeuh/jan_now_autooptimizes_llamacpp_settings_based_on/)
  - It works with Mac too! Although it is still experimental, so do let us know how it works for you.
  - We don't support MLX yet (only gguf and llama.cpp), but we will be looking into it in the near future.

- Can the Jan server serve multiple models (swapping them in/out as required) similar to Ollama?
  - You can definitely serve multiple models similar to Ollama. Although the only caveat is that you would also need to have enough VRAM to run both model at the same time also, if not you would need to manually switch out the model on Jan.
  - Under the hood we are basically just proxying `llama.cpp` server as Local API Server to you with an easier to use UI
- The manual switching out of the models is what I’m trying to avoid. It would be great if Jan could automatically swap out the models based on the requests.
  - We used to have this, but it makes us deviate(背离, 偏离) too much away from llama.cpp and make it hard to maintain, so we have to deprecate it for now.
  - We are looking into how to bring it back in a more compartmentalize way, so that it is easier for us to manage. Do stay tune tho, it should be coming relative soon!
- I believe this is what llama-swap does?

- What is the use case for a chat tool without RAG? How is this better than the llama.cpp integrated Webserver? 
  - Jan supports MCP so you can have it call a search tool for example
  - It can reason - use tool - reason just like chatgpt
  - As for the use case, it's the only open source AIO(All-In-One) solution that nicely wraps llama.cpp with multiple models
- You can actually run MCP that search your own files too! A lot of our user do that through Filesystem MCP that come pre-config with Jan
  - Any file over 5MB will flood the context and become truncated. It is not an alternative. 

- RAG is definitely on our roadmap, however, like other user has pointed out, implementing RAG with a smooth UX is actually a non-trivial task. A lot of our users don't have access to high compute power, so balance between functionality and usability has always been a huge pain point for us.

- I really wish Jan would be a capable RAG-system (like GPT4all) but with regular updates and support of any gguf-models (unlike GPT4all).

- What “All-In-One” practically means for Jan
  - Runtime + engine: includes llama.cpp (local inference) plus cloud provider options so you can run models locally
  - Model management / hub
  - UI: chat UI, model hub, model settings, downloads
  - Tool / integration layer: supports MCP
  - Server/API & multi-tenant features

- Does it support multi-GPU optimization?
  - Yes, it does!
  - It does handle multi-GPU setups, but not automatically yet. 
- I found the optimizer doesn't check if the model fits in a single GPU without layer offloading to CPU. It should put -1

- Does Jan allow one to create their own agents and/or agent routing?
  - Not yet, but soon! Right now, we only have Assistant, which is a combination of custom prompt and model temperature settings

- ## 🎯 [Jan now runs fully on llama.cpp & auto-updates the backend : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1mdy1at/jan_now_runs_fully_on_llamacpp_autoupdates_the/)
  - Jan v0.6.6 is out. Over the past few weeks we've ripped out Cortex, the backend layer on top of llama.cpp. It's finally gone, every local model now runs directly on llama.cpp.
  - Plus, you can switch to any llama.cpp build under Settings, Model Providers, llama.cpp (see the video above).
- We had different plans for Cortex, that's why we insisted on keeping it for a while, but maintaining it with the new plans became pretty tough. It just made more sense to support llama.cpp directly instead of going through an extra layer.
  - Well I'm glad the team changed direction. This more polished, cleaner, leaner, faster way of Jan development is bound to result in great progress!
- Cortex was the engine behind Jan. It ran on llama.cpp and worked kind of like an alternative to Ollama. We used to update it whenever llama.cpp got updated. Since we've changed our plans, we removed it with Jan v0.6.6.

- I see that the Linux version became 850MB lighter. Is that because of the Cortex removal?
  - Yes, Cortex removal is part of it. We also trimmed down the app by moving out unused dependencies like CUDA 11/12 and extra llama.cpp builds. 
  - Jan now fetches the right llama.cpp version after install, so no need to be bundled in the app itself, which makes the download much lighter
- Although it would be great to keep at least 1 version of llama.cpp, so the install would be portable.

- Does Jan allow selectively offloading model tensors to CPU? (For MoE models) If yes, I would migrate from LM Studio to Jan just for that!
  - oh - not yet, but we're adding it to the roadmap. Thanks for the request!
- this is the killer feature all the slick frontends are missing.

- Allowing ik_llama as a backend would be cool too!

- Llama cpp has so many options, there really should be a "custom arguments" option (input field that gets passed through to llama).

- Koboldcpp have this feature iirc

- Would be great if we could also use llama.cpp forks such as ik_llama.cpp or the Unsloth fork
  - llama.cpp forks: Each fork comes with its own changes, and integrating them cleanly would add a lot of maintenance overhead. We're keeping an eye on where things go, but sticking with official llama.cpp keeps Jan more stable for now.

- MLX support has been on the table for a while... it's something we revisit from time to time. We made several roadmap changes around it, but no final decision yet

- ## 🏠 [Jan got an upgrade to v0.6.0: New design, switched from Electron to Tauri, custom assistants, and 100+ fixes - it's faster & more stable now : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lf5yog/jan_got_an_upgrade_new_design_switched_from/)
  - [Release 0.6.0 · menloresearch/jan _20250619](https://github.com/menloresearch/jan/releases/tag/v0.6.0)
  - Switched from Electron to Tauri for lighter and more efficient performance
  - You can create your own assistants with instructions & custom model settings
  - Fully redesigned UI

- Tauri helps us bring Jan to new platforms like mobile. It's also lighter and faster, which gives us more room to improve performance in upcoming updates.
  - Tauri allows us to reuse our existing React and JavaScript codebase, which helps us move faster while keeping the design clean and modern. 
  - Qt and similar native toolkits don't integrate well with the web stack.

- Wails doesn't support mobile, and we're planning to bring Jan to mobile too - so we went with Tauri.

- As someone who is finalizing a port of a small app (atv-desktop-remote) from electron to tauri: If most of your code is in the renderer, the transition is easy. If you have lots of stuff in main.js, you’ll need to reimplement that in rust. The IPC line is still there (between main and renderer processes), you can move stuff around if you need to.

- what makes Jan different from / better than LM Studio? It seems you have same backend and similar frontend?
  - Jan is open-source 
  - We're experimenting with MCP support using our own native model, Jan-nano that outperforms DeepSeek V3 671B in tool use. It's available now in the Beta build.

- Been looking for some opensource UI for openrouter for a long time. It looks very promising, but I haven't figured out how to output reasoning yet.
  - reasoning output isn't supported yet - it's still on the todo list to check.

- Can we edit the responses?
  - No, you can't. why do you want to edit the responses?
- That's an easy way to steer the story in the direction you want it to go. Say, you draft a chapter and ask the model to develop the story; it starts well, but in the middle of generation makes an unwanted twist, and the story starts going in the wrong direction. Sure, you could just delete the response and try again, or try editing your prompt, but it is much, much easier to just stop generation, edit the last line of text, and hit "resume". So, editing AI responses is a must-have for writing novels.

- Jan supports OpenAI-compatible setup for APIs. So if it's empty, it won't work, even if the remote endpoint itself doesn't require one. We should add a clearer indicator for this, but in the meantime, try entering any placeholder key and see if that works.
  - Plus, Ollama doesn't support OPTIONS requests on all endpoints (like /models), which breaks some standard web behavior. We're working on improving compatibility.

- Jan doesn't work with Ollama llms out of the box is my biggest grip . Still unable to add ollama to Jan. Anyone succeeded?
- can it be used with lmstudio ?
  - i tried it and it doesnt work. not sure which one is wrong
  - jan is using OPTION request to list model while lmstudio only serve /v1/models on GET

- When using Ollama if the model does not fit in my GPU it will use the GPU and offload to the CPU but the same did not work with jan.
  - you can update the number of GPU layers manually in model settings (Model Providers -> llama.cpp).
  - We're planning to add automatic GPU offloading soon, once it's merged upstream in llama.cpp

- Please add MLX as a future inference engine

- The app is huge in size. I thought Tauri didn't ship the whole browser.
  - Totally fair. The app's size is due to the universal bundle - we're working on slimming it down soon.
  - Universal bundle on Mac means the app includes native code for both Apple Silicon & Intel Macs, so it's basically twice the size.

- I love Jan! Is there an option for it to autostart on boot with the API server enabled? I couldn't find any way to do that with the previous versions of Jan so I went with LM Studio for my backend unfortunately.

- Jan doesn't support chatting with files or image generation yet. We're going to add chatting with files feature soon. As for image generation, it's not available right now - we'll take a look at it as well.

- What do you feel differentiates your app from all the others? I keep downloading chat apps and they all pretty much offer the same functionality and interface. What is Jan's approach for separating yourself from the herd?

- Is chat history formatted into some portable standard?
  - We're using the same format as previous versions. It loosely follows OpenAI's thread structure but isn't a strict match. It's extension-based, so it can be replaced or exported to other formats if needed.

- on Linux Tauri uses WebKitGTK for now, so performance isn't as good as Chromium. We're refactoring to reduce app size, and once that's done, we'll look into bundling a better browser. Tauri gives us flexibility there, unlike Electron.

- ## [Cortex.cpp: llama.cpp Engine · menloresearch/cortex.cpp _202409](https://github.com/menloresearch/cortex.cpp/discussions/1156)
- We submodule llama.cpp
  - How we handle different llama.cpp versions (e.g. AVX, CUDA etc)
  - Documents which llama.cpp versions we bundle into Cortex/Jan
  - Switching logic for CPU/GPU inference

- ## [Are people not using JAN a lot? : r/LocalLLaMA _202408](https://www.reddit.com/r/LocalLLaMA/comments/1eza2kl/are_people_not_using_jan_a_lot/)
- I think that Jan still lacks a lot of “nice haves” that are present in LM Studio
  - Built in RAG support

- I'm Emre from Jan. Really appreciate this post - it's going to be super helpful as we keep improving Jan! Let me share a few things we're working on:
  - Improving Jan's performance across different hardware (with a new engine that is compatible with various hardware)
  - Revamping the new model hub, providing better
  - Experimenting with something that we'll share soon in homebrew.ltd, our R&D lab which is also the company behind Jan.
- Responding only to features and ideas without addressing the questions of struggling users is called exploitation(广告，宣传).

- Jan has a lot of potential, but is let down by its model management when it’s not the server. Please invest in Ollama and OpenAI compatible APIs. Jan has a lot of potential but not being able to simply connect to your server and select models from a list makes it a pain to use when you already have Ollama / OpenAI compatible servers other clients use.

- I don’t know if Im Studio has it, but I am waiting for tts and stt support in Jan. As for the online based tts it would nice to have different options like elevenlabs, oai whisper, google tts, amazon poly etc For a local tts it would be cool to have at least something that is friendly to limited hardware like piper.
  - Msty for example has implemented stt in the meantime. They just use oai‘s whisper api.

- It's probably due to the "competition" from other excellent easy-to-use software such as Koboldcpp, LM Studio, Ollama, etc. Additionally, Jan has historically been lacking in some functionality that the alternatives have. Maybe this is not the case anymore, as it was a few months ago I last tried Jan.

- I love using JAN but there are a few things that made me switch to openwebui.
  - First I need a more robust API. Running the same time as my threads. Why does it not let me chat in threads if I turn on the API? 
  - I also tried to do some simple things like get the currently loaded model and swap the loaded model for another one. I still have not been able to do this.
  - Why is there so many manual steps involved in adding a model that is not included in the hub? Can't we just provide the huggingface link and it pull the info it needs?
  - I could not find a way to add a custom extension. I want to add image generation using SearmUI. But I don't think I'm able to create extensions yet.
  - I would really love to come back to Jan but the features I need are already there on openwebui.

- JAN is poorly build and thought out unfortunately. 
  - They really need to address support of already existing GGUF models, new quantization types (IQ quants), proper and easy ways to switch prompt/system messages and have presets for things like ChatML, LLama 2/3/3.1, Mistral, etc.
  - Also things like longer context, Flash Attention, KV Cache, More useful debugging/error messages and proper Apple Silicon support is needed badly.
  - It generates a bunch of random and weird output on a lot of new models and quant types.
  - It's too bad that after all this time it is still very buggy and clunky.. I had high hopes for it

- jan has stopped supporting the WebUI, so browser functions are not available.

- ## [Jan: An open source alternative to ChatGPT that runs on the desktop | Hacker News _202403](https://news.ycombinator.com/item?id=39782876)
- GPT4All makes it annoyingly difficult to run any other than their "approved" models. I'd like to kick the tires on a whole host of random GGUF quantizations on Hugging Face, please.
  - I use text-gen-ui (Oobabooga) as a back-end and have it run with `--api` to use the front end of my choice.

- ## [Jan: an open-source alternative to LM Studio providing both a frontend and a backend for running local large language models : r/LocalLLaMA _202401](https://www.reddit.com/r/LocalLLaMA/comments/193m27u/jan_an_opensource_alternative_to_lm_studio/)
- A Big problem all these LLM tools have is that they all have their own way of reading Models folders. I have a huge collection of GGUF's from llama.cpp usage that I want to use in different models. Symlinking isn't user friendly, why can't apps just make their Models folder a plain folder and allow people to point their already existing LLM folders to it
  - This is salient(显著的, 突出的) criticism, thank you. At the core, we're just an application framework. We should not be so opinionated about HOW users go about their filesystem.
  - [/pr已合并 - epic: Better files & links · Issue · menloresearch/jan _202401](https://github.com/menloresearch/jan/issues/1494)

- Ollama being the biggest offender, with that fake docker syntax for modelfiles, model import and renaming using sha hashes.

- The Stable Diffusion UI variants also had this problem - until Stability Matrix came along and resolved a number of inconveniences with model management. Wonder if something similar could be viable here too.
  - invokeai 的选择文件也是一种方案

- Its why Koboldcpp just has a file selector popup, it doesn't make sense to tie people to a location.
  - Koboldcpp also has an OpenAI compatible server on by default, so if the main thing you wish for is an OpenAI endpoint (or KoboldAI API endpoint) with bigger context processing enhancements its worth a look.
  - Koboldcpp is a bit of a hybrid since it also has its own bundled QT UI. We also have GGUF support as well as every single version of GGML.

- This is the best example of why LLMs wont replace devs.
  - IMO, work is the tedious processes of begrudgingly implementing common design patterns. 
  - Did anyone building LLM frameworks/dev tools think they'd be building model library browsers drawing from itunes and calibre? If they're smart. How many people used itunes just because it had better browsing/searching than winamp? (Jumping back to hugging face for the model card and details is already less frequent.)
  - We all want different things.

- Is it better to use llama.cpp instead of LM Studio? 
  - Absolutely! KoboldCpp and Oobabooga are also worth a look. 
  - I'm trying out Jan right now, but my main setup is KoboldCpp's backend combined with SillyTavern on the frontend. 
  - They all have their pros and cons of course, but one thing they have in common is that they all do an excellent job of staying on the cutting edge of the local LLM scene (unlike LM Studio).

- It really needs a custom folder and scan directory function to incorporate already available local GGUF files. I also don't understand the weird implementation of needing a config/JSON file for each model. Why not just use the GGUF metadata and filename to determine the proper settings like other apps are doing?
  - local configs give you an ability to override specific parameters for every model - like to have a custom prompt, custom context length, rope settings etc. Without having local configs there would be no such place to put all your overrides. 
  - But of course no inference software should require them by default and should take everything it can from metadata (where applicable). 
  - And generate those Configs automatically only if you change some parameter from its default value.

- it's nice and simple, but as a consequence of being so new it lacks a lot of QoL stuff that I would expect with more mature apps. 
  - Also I find that the app loads/unloads LLM models into the RAM with every query, unlike LLMStudio which leaves it in RAM until you eject the model. I don't know which is better, but I am a bit concerned about that constant load on my computer.

- I don't like ollama. It keeps loading and unloading models Everytime you do Inference.

- It looks to have an openai API compatibility, wonder if I can use oobabooga textgen as a backend

- I am looking for a GUI that lets me set a -ve CFG without hassle. Does this GUI let me do that?

- Is it some kind of electron app bundled with llama.cpp? Can it be used as a web UI over network?
