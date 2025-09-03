---
title: lib-aikit-librechat-community
tags: [community, large-language-model, librechat]
created: 2025-09-01T05:52:53.238Z
modified: 2025-09-01T05:53:05.266Z
---

# lib-aikit-librechat-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-open-webui
- ## 

- ## 

- ## 
# discuss-librechat
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🔌 [Enhancement: Custom Plugins (Langchain Tools) as External Modules - Dependency Injection · danny-avila/LibreChat _202404](https://github.com/danny-avila/LibreChat/discussions/2557)
  - According to the documents (make_your_own.md), adding a new plugin to Librechat requires modifying the repository files including `handle_tools.js, index.js, and manifest.json` .
  - If anyone wants to implement their own plugin, they have to fork the repository and manually keep up with the updates, git conflicts, and breaking changes.
  - An alternative approach would be having Librechat to look for external Langchain tools and do the imports/exports automatically (specially once manifest.json goes away).
  - Honestly, I can't think of any clean way to implement this.

- I've thought a lot about this and know of a way, but I want to retire the old way of handling plugins and build it from the ground up anyway. I would implement this first for Assistants, then a new agent system that is also compatible with other endpoints (Anthropic, google, etc.)
  - The Assistants endpoint is most of the way there for dependency injection of tools.
- 202405: The current plugins system will be discontinued in favor of something more modular, including using different LLM providers.

- ## [Artifacts not loading _202507](https://github.com/danny-avila/LibreChat/discussions/8583)
  - I'm running LibreChat through Docker on my local machine
  - I saw that there is a new tutorial for creating a static browser server for sandpack to work. But as I'm running this locally and did have (until recently) it running well
- If running sandpack locally, you would also need to run: LibreChat-AI/codesandbox-client
  - Both that repo and the tutorial you shared are for learning/dev purposes. Ideally you would have your own HTTPS API acting as a CDN for the static files serving for both templates
- I set this all up and got the same issues. After several hours of debugging I opened it in safari and all was fine. I had a chrome specific issue which was blocking the calls. Refreshed cache and all started working again.

- Your bundler container should be in the same network as your LibreChat container. For example this is in our docker compose

- [Artifacts not generating using code sabox _202507](https://github.com/danny-avila/LibreChat/discussions/8729)

- ## [Artifact functionality in chat  _202504](https://github.com/danny-avila/LibreChat/discussions/6987)
  - The artifact system is very sensitive to any other errant text an LLM may place just before the artifact tags begin. Is it possible to have LibreChat ONLY look for the `:::` to determine when to display the Artifact window? And just ignore plain text above that as part of the chat message?

- The artifact block is being enclosed with triple-backticks, which is not the correct format. This can be improved through prompting, instructing the LLM not to do so (mileage with artifacts in general will vary by how smart the LLM is).
  - Yes precisely—I've written several agent instructions to avoid it and none work with smaller models + LibreChat because of this issue of LibreChat only honoring the first markdown it sees

- ## 🤔 [LibreChat Artifacts Preview not showing · danny-avila/LibreChat _202501](https://github.com/danny-avila/LibreChat/discussions/5393)
  - I have beta enabled for artifacts, per image below, but not window pops up to preview code.
  - I have tried different models none of which seem to trigger the Artifacts preview pane.

- 👷 实测可以在本地运行code artifacts的模型包括 mistralai/devstral-small-2507
  - prompt1
    - use code artifacts. use react and javascript to create a simple personal profile landing page: homepage shows a big welcoming greeting
  - ❌ 不能触发artifacts sandbox preview的prompt
    - use code artifacts. use react and tailwindcss to create a minimal personal profile landing page: homepage shows a big welcoming greeting, then shows 2 example personal projects

- I noticed it only works for me if I use Sonnet. So it might not work for local models via Ollama. Can you or anyone confirm with a local model, please?
  - Smaller models tends to have difficulties following the (very long) artifacts prompt, try manually giving it a simplified version of the prompt

- SOLUTION: I'm running LibreChat (self-hosted in Docker) + LM Studio + Mistral Small 24b 4bit MLX flavor (because I'm on an M4 with a single GPU with only 48GB VRAM + 64GB RAM) and using a greatly simplified instruction in a LibreChat Agent
  - I should add that apparently Mistral has artifacts in their online chat interface, so maybe it's no surprise that their open source model worked pretty easily when requesting artifacts.
  - I attempted this with their dedicated Codestral 22b model [MLX flavor] and it kept putting the actual "artifact" headers inside the normal code block
  - Update: Got a smaller ~10GB MLX flavor codestral-22b-v0.1-mlx-3 working as well. Moving the Artifact prompt into the system instructions in LM Studio made this work every time. For some reason, these smaller local models just don't receive or ignore the Artifact prompt sometimes otherwise (ie: it doesn't show up in developer logs in LM Studio if being sent by LibreChat).
  - PS: I also increased the context length in LM Studio (default is around 4, 000 and I pushed it closer to 8, 000) just in case. Not sure if that helped or if it was the simplified prompt in general.

- Pretty crazy but I was able to get a really small model to correctly output the Artifact as well by reiterating things in the chat prompt. 
  - `mistral-nemo-instruct-2407@4bit` (it's a 12B model very compressed to under 7GB file size)
  - Small models seem to ignore the LibreChat Agent Instructions unless you call them out explicitly. Or for some reason they never even receive the LibreChat Agent Instructions unless you mention it in the chat prompt 

- [Artifacts fail to render when using chatgpt-4o-latest model ](https://github.com/danny-avila/LibreChat/discussions/7081)
  - It's an issue with the LLM,  `chatgpt-4o` is really no good here. Try using gpt-4.1 instead

- ## 🔡 [feat: Code Artifacts by danny-avila · Pull Request · danny-avila/LibreChat _202408](https://github.com/danny-avila/LibreChat/pull/3798)

- [Code Artifacts _202409](https://github.com/danny-avila/LibreChat/discussions/3970)
- artifacts is not implemented for bedrock yet. I will get to it today.
- Can we have a list of where artifacts are implemented? i am using a local Ollama instance and managed to get it work by chance only once, at this point i assume that it depends on the model i am using? Sadly i cannot remember which one i was using that one time it worked.
- 👷: It all comes down to prompting. Unfortunately, for most open source models, the current required format for artifacts is a bit too "advanced" for consistent output, which is why the "smarter" models, i.e. claude, gpt-4, etc, will perform more consistently

- ## 🧊 [feat: Code Interpreter API and Agents Release by danny-avila · Pull Request · danny-avila/LibreChat _202412](https://github.com/danny-avila/LibreChat/pull/4860)
  - Following this update, users can utilize the new Code Interpreter API: code.librechat.ai/pricing
  - This pull request first appeared in librechat-1.8.9

- [feat: Code Interpreter API for Non-Agent Endpoints by danny-avila · Pull Request · danny-avila/LibreChat _202504](https://github.com/danny-avila/LibreChat/pull/6803)

- ## 🧊 [Enhancement: LibreChat Agents · Issue · danny-avila/LibreChat _202408](https://github.com/danny-avila/LibreChat/issues/3607)
- > code interpreter is not available yet. What do you plan to add ? Maybe code interpreter would only be available through official openai agents, which means that we would need to opt for an open source equivalent, like open interpreter ?
  - 👷202410: Unfortunately, this is not a simple problem. I'm happy to say after months of work, I've built something that will be highly compatible with LibreChat, to run code in a safe and secure manner, running many different languages (not just python or javascript), with the ability to work with and generate files, and scalable to many users. 
  - On open interpreter: it would be one of the least secure ways of doing this, and it's not scalable. It's mainly meant for a single-user environment.
- I would like to comment here for the first time that Code Interpreter functionality won't be open source. 
  - with this particular feature, I would like to protect the source code as it came from months of research, frustration, and trial and error, to build something truly effective and seamless across many use cases and principally for the use case of LibreChat Agents. I believe this would also give LibreChat a "competitive" edge 
  - My decision was also due to the fact that packaging this solution would significantly bloat the current tech stack, and with less compatibility across systems, thereby creating more maintenance overhead, not to mention the increased bandwidth.

- ## [GPT4 Code Interpreter in LibreChat with GPT4 and other versions of GPT · danny-avila/LibreChat _202308](https://github.com/danny-avila/LibreChat/discussions/796)
- my plan as of now is to use dominic's project, "codeinterpreter-api": https://github.com/shroominic/codeinterpreter-api
  - Rather than reinvent the wheel, and it's the best solution I've used.

- You can try this simple plug-in I made : https://github.com/ronith256/Code-Interpreter-LibreChat
  - It is very much in beta, and does not sandbox the python env.

- ## [Open-interpreter integration? · Issue · danny-avila/LibreChat _202310](https://github.com/danny-avila/LibreChat/issues/1010)
- Open Interpreter (as in using the actual open interpreter library) could be easy but not scalable. A more scalable solution is harder to implement

- ## [Is it possible to use a free code interpreter in librechat instead of their paying API? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m2543n/is_it_possible_to_use_a_free_code_interpreter_in/)
- As a tool call maybe?

- ## [Connecting LibreChat to a local LM Studio, which hosts a Mistral 7B. _202402](https://github.com/danny-avila/LibreChat/discussions/1836)
- 🌰 This is what I used in my librechat.yaml for Mistral in LMStudio
  - Note: in LMStudio you need to enable the "server mode" since it's disabled by default
  - removed "user_provided" and replaced it with a dummy key
