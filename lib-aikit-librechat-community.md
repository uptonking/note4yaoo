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

- ## [Anyone running Open Webui with llama.cpp as backend? does it handles model switching by itself? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k5w6gg/anyone_running_open_webui_with_llamacpp_as/)

- llamacpp will not swap models by itself, but someone else mentioned, llama-swap is exactly for this use case.
  - In my setup I have more than one llama.cpp servers running at the same time, each with a small model.

- 🧑‍🏫 [Tutorial: Open WebUI and llama-swap works great together! Demo of setup, model swapping and activity monitoring. : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mon08l/tutorial_open_webui_and_llamaswap_works_great/)

- ## [OpenWebUI is the most bloated piece of s**t on earth, not only that but it's not even truly open source anymore, now it just pretends it is because you can't remove their branding from a single part of their UI. Suggestions for new front end? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nlkwr3/openwebui_is_the_most_bloated_piece_of_st_on/)
- If you want 0 bloat, then LLaMa.cpp’s server.exe gives you an extremely lean, no-nonsense interface.

- I love my librechat, full MIT license. 
  - If your in the discord you will notice large companies like Stripe have deployed it to their employees and government agencies are using it now too for low cost AI that is local hosted and secure. 
  - They kind of push their code interpreter and search/scraper solutions but you can easily replace those with whatever MCP you want.
  - I use Perplexity MCP and I use my AI nearly every day in a professional capacity
  - Lobechat I think its called seemed the best looking but its license is not what was looking for.

- The Code Interpreter bit is a bit annoying and the dual config files were for a long while a bit confusing for a lot of people but once you get past those it's very solid.

- Oobabooga has always been my favorite. 
  - It supports several backends, including transformers and llama.cpp, has a super configurable frontend with most backend options exposed, has a native OpenAI-compatible API endpoint, and the portable version has auto-install options for basically every major GPU platform. 
  - Not sure why people don't use it much anymore, as Oobabooga is still pushing meaningful improvements to support new model formats like GPT-OSS. 
  - If your target environment is a local network for a single knowledgeable user, it really can't be beat.
- I don’t like Ooba because it has a trash user interface but I support it generally as free and open source software. 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [[openidStrategy] only requests to HTTPS are allowed · danny-avila/LibreChat _202507](https://github.com/danny-avila/LibreChat/discussions/8310)

```diff
     openidConfig = await client.discovery(
        new URL(process.env.OPENID_ISSUER),
        process.env.OPENID_CLIENT_ID,
        clientMetadata,
        undefined,
        {
          [client.customFetch]: customFetch,
+         execute: [client.allowInsecureRequests],
        },
      );
```

- [Disable need for HTTPS during development? _202411](https://github.com/panva/openid-client/discussions/716)
  - In case someone else runs in the observation that the flag `allowInsecureRequests` is marked as deprecated: The reason is to highlight the fact that you shouldn't have to use it.
  - Instead, use it only in development or other non-TLS environments where you are absolutely certain it is secure enough. The default should be HTTPs, though.

- ## [Using LibreChat in a corporate environment (Azure or self hosted) _202311](https://github.com/danny-avila/LibreChat/discussions/1207)
- I'm also interested in custom branding as a feature.

- ## [[Enhancement]: "Bring-your-own" Local MCP servers _202505](https://github.com/danny-avila/LibreChat/discussions/7268)
  - I would like to see LibreChat provide a built-in mechanism for seamlessly connecting local MCP servers (or local companion apps) to a centrally deployed LibreChat instance.
  - A browser-based approach alone can’t directly connect the remote server to localhost. Enabling local MCP servers or companion apps, similar in concept to tools like GetMCP (but free), would let each user securely handle local operations while still benefiting from LibreChat’s LLM capabilities. 
  - This mirrors how Claude Desktop manages local file access by running an MCP server on the user’s machine.

- Claude Desktop is actually running MCP servers very similar to LibreChat. The user runs Claude Desktop, and it runs the MCP processes on their machine. You can achieve the same local "capabilities" by running LC locally.
  - However, there may not be much more work involved here, if you can use this project in conjunction with LibreChat: https://github.com/srbhptl39/MCP-SuperAssistant
  - we can take look at that project I linked for the proxying parts, since that's what it does, it may indeed go overboard with script injection via the extension.
- I'm aware that LC locally is quite similar to Claude Desktop, which is already amazing. Limitations arise when deploying it on scale to many users (where LCs strenghs are).
- I think you could do this with something like ngrok. 
  - 1. Locally start an MCP server running on port X.
  - 2. Locally start ngrok and get an ngrok URL that maps to your local MCP server on port X.
  - 3. Do some kind of config in your LibreChat session in the browser to give it the ngrok URL so your browser session can use that URL to contact the locally running MCP server.
  - It would be cool if LibreChat could automatically do 1 and 2 but that's probably out of scope. I think 3 seems like it could be quite useful, though for lots of applications besides just this question. 
- Cool idea! Also sound a little like my companion App Idea. The Companion could handle the local MCP stuff (file permissions etc.) and the ngrok connection.

- I just recently got this working for our Shopify instance and we want to open source the parts that aren't LC related and hopefully incorporate it into LC core.
  - this is an example of it talking to my local folders using the example Filesystem MCP server from the MPC repo.
  - This does not require NGROK, it actually connects to the frontend through a "tunnel" which the frontend acts as a bridge to the backend using the frontend's auth. This way it can better use horizontal scaling in the future. The Tunnel and Web App are authenticated with each other too, so you don't have a random site looking for this on your machine and using it without your permission.

- ## 📡 [2025 Roadmap · danny-avila/LibreChat _202502](https://github.com/danny-avila/LibreChat/discussions/5960)
  - [LibreChat 2025 Roadmap](https://www.librechat.ai/blog/2025-02-20_2025_roadmap)
- Basically, the cloud-hosted version will just be the same open-source app you can already self-host. We're not planning to take away or restrict any features from the self-hosted version because of the cloud offering. 
  - Everything you can do now for free when self-hosting will stay free. 
  - All planned features on the roadmap are planned to be open-source.
  - ⚖️ no plans to change the open-source license of LibreChat (MIT License).
  - The only exception is the Code Interpreter API service – that's already a premium thing, and it'll stay that way.
  - The cloud version might eventually have some paid tiers (maybe for extra storage, resources, managed stuff, etc.), but the features will mirror what's available in the project repository.

- MCP Marketplace / Store as seen in Cline & 5ire

- One idea I still have would be some image playground within Librechat that can use Black Forest Labs API to generate and modify like on replicate playground or midjourney edit function.

- 🤔 Are there plans for supporting OpenAI's new Responses API which will also replace the Assistants API.
  - 👷 Nope, we have our own agent framework: https://www.librechat.ai/docs/features/agents
  - And Assistants API will officially be deprecated following this announcement
  - Responses API is just another layer on top of completions so it can actually be used with LC Agents framework quite nicely without being its own independent thing like the Assistants API component.
- Are you referring to OpenAI's deprecation of Assistants, or you are announing LC Assistants will be dreprecated?
  - Both. [[Enhancement]: Support for OpenAI's new Responses API · Issue · danny-avila/LibreChat _202503](https://github.com/danny-avila/LibreChat/issues/6364)
  - OpenAI announced last week a new Responses API that contains the feature set of the Chat Completions API and replaces the Assistants API (the latter is now deprecated and will be sunseted mid-2026).
  - Azure already announced that they provide this API day one and considering OpenAI's position on the market, we can expect that it will become an industry standard as is the Chat Completions API today.

- I'm using librechat within my company as the main chat applications for my employees (50). there are some features listed on the roadmap which makes it even better.
  - Admin features
  - Folders in chat & agents
  - Agent Sharing with groups
  - Memory
  - Deepresearch
- these are all already being worked on:
  - Admin features
  - Agent Sharing with groups
  - Memory (completed)
  - On Deep Research, the Web Search tool was inspired by multiple papers on the topic
# discuss-tools/extensions
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [I’ve opened a new PR that adds a Chart Toggle option to agent configs, allowing agents to render inline ECharts-based charts directly in conversations. _202507](https://discord.com/channels/1086345563026489514/1397726855632785500)
  - [Chart integration by rohitpathak21 · Pull Request · danny-avila/LibreChat _202507](https://github.com/danny-avila/LibreChat/pull/8634)
  - When enabled, agents can return a strict ECharts option JSON wrapped in a `:::chart{}` block, and it gets rendered seamlessly in the chat UI.
  - The idea is to make it easy for anyone using LibreChat to plug in their own data tools, scripts, or APIs that generate structured data — and have that data instantly visualized as charts in the conversation flow

- 🏠 Just a thought: maybe this could be generalized into a broader "rich message" system (kind of like Rocket. Chat's cards/buttons or Slack blocks). For example, a JSON block that renders a form asking "Do you want to see the chart?" with Yes/No buttons, and routes the response back to the agent.
  - This would also align well with MCP/tools/thinking setups during a chat — since you have to render something structured anyway (not just plain text) to give some information to the user... Having a common rendering layer for buttons/forms/charts/etc. feels like a natural next step. What do you think?
- What you suggested is actually super cool. A generalized rich message system with buttons, forms, and charts sounds like a great direction, especially for tool-based or agentic workflows like MCP. I’d love to see something like that in LibreChat.
  - Right now though, I’ve tried to keep the implementation pretty simple and aligned with the existing structure. I based the chart feature loosely on how `artifacts` are handled (though this is nowhere near as complex), just to make sure everything fits into the current codebase without too many changes.
  - I definitely think your idea is worth exploring further, but I feel like it would need a solid plan and quite a few changes under the hood. I’d probably need to sync up with the repo owner first to understand what kind of direction or roadmap they have in mind, and how “rich” they’d actually want this to be.

- For generic "rich-text" uis with forms, buttons etc. a colleague of mine recently linked me this project: https://github.com/idosal/mcp-ui
  - It's react based and features a server and client side library/sdk.
# discuss
- ## 

- ## 

- ## 

- ## [Setting BAN_VIOLATIONS=false has no effect on login violation bans _202509](https://github.com/danny-avila/LibreChat/discussions/9527)
  - Setting `BAN_VIOLATIONS=false` works as expected for violations such as `NON_BROWSER_VIOLATION` , but seems to have no effect on `LOGIN_VIOLATION` .
  - Additionally, when an IP is banned for Too many login attempts, please try again after 5 minutes, this ban does not seem to be logged anywhere.

- [BAN_VIOLATIONS=false doesnt have any effect · danny-avila/LibreChat · Discussion #3914](https://github.com/danny-avila/LibreChat/discussions/3914)
  - LOGIN_MAX and LOGIN_WINDOW, adjust as desired.

- ## [LibreChat can't be self-hosted in any commercial way even internally, because of MongoDB SSPL? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nn449p/librechat_cant_be_selfhosted_in_any_commercial/)
  - I want to run it but it seems, it's complicated way to say they backed by MongoDB right? Because you can't self host it and then you need to pay anyway and give them your data.

- there are MongoDB compatible options that aren't Mongo, such as FerretDB. AWS has DocumentDB with a MongoDB compatibility layer, for a hosted instance. So even if your legal interpretation is right, claiming that Librechat can't be self hosted because of the license is still wrong.

- The SSPL applies if you are making mongo itself available to your customers, not if you are using it to back an application you are making available to your customers.
  - Would have to look at what surface LibreChat exposes, for instance, a vector db is probably part of the customer facing feature set from LibreChat, presumably mongo is just for data storage and query, could be any database.

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
