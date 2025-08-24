---
title: lib-aigc-image-comfyui-community-diffusers
tags: [comfyui, community, diffusers, image]
created: 2025-08-23T06:44:39.345Z
modified: 2025-08-23T11:42:36.444Z
---

# lib-aigc-image-comfyui-community-diffusers

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [Execution Model Inversion · comfyanonymous/ComfyUI _202408](https://github.com/comfyanonymous/ComfyUI/pull/2666)
  - This PR inverts the execution model -- from recursively calling nodes to using a topological sort of the nodes. 
  - This change allows for modification of the node graph during execution. 
- This allows for two major advantages:
  - 1. The implementation of lazy evaluation in nodes. or skip evaluation
  - 2. Dynamic expansion of nodes. This allows for the creation of dynamic "node groups". Specifically, custom nodes can return subgraphs that replace the original node in the graph. This is an incredibly powerful concept.

# discuss-comfyui-diffusers
- ## 

- ## 

- ## 

- ## [Chroma - Diffusers released! : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lepqtg/chroma_diffusers_released/)
  - I look at the Chroma site and what do I see? It is now available in diffusers format! for v38

- What is the diffusers format good for?
  - A1111 was based on LDM. ComfyUI at one point supported diffusers but then dropped it.
  - Diffusers is really good for making things easy to edit and run, but it expects that the person running it has an 80GB graphics card in a server somewhere. Most research papers will provide code modifications compatible with diffusers library, but it gets ported to other engines to work in UIs. I think SD. Next is the only UI that supports full diffusers pipelines these days.

- 👷: ComfyUI was never based on diffusers. It's a horrible library but I can't hate it that much because it's so bad that it's responsible for prematurely killing a lot of comfyui competition by catfishing(鲶鱼, 网络骗子) poor devs into using it.
  - There is some code in comfyui that auto converts key names from diffusers format to comfyui format for some loras and checkpoints but that's it.
- I was under the impression that at one point it included nodes to handle diffusers models
  - there are nodes for it https://github.com/Limitex/ComfyUI-Diffusers You can still use all ten billion diffusers compatible models with it.
- invokeai is a failed startup and their downfall started when they made the mistake of switching to diffusers.
  - They raised 3.75 million dollars over 2 years ago and their execution has been so bad that they let multiple one man projects (A1111, ComfyUI at the time) with zero funding beat them.
  - They are currently trying to raise another round of funding but are failing. You can easily tell things are not going well on their end because development is slowing down and they are no longer implementing any open models.

- The diffusers pipeline in sdnext is a joy to use and well implemented , comfy is a mess .

- Diffusers doesn't do everything because it doesn't need to, python is modular and those things already exist. But the best thing about Diffusers is it is standardized, once a problem is solved with it, you only need to translate. It is a solid foundation.

- diffusers is transformers but for text to image and text to video models. People love to harp on it but no one has ever maintained a diffusion model library the size of diffusers. Having your project in diffusers is important because basically every small research lab uses it for prototyping various implementations because it's accessible, much like transformers.
  - People love to shit on it just like they love to shit on transformers -- but it just works across platform and is easy to hack on.

- That's an implementation problem, SDnext uses diffusers and it's offloading is great, you can get the resource usage at least as low or even lower than any other UI.

- InvokeAI mentions diffusers. The main complaint on that tool is that it doesn't support safetensor (or if it does, it needs to convert it to chkpt/diffusers and save it to cache).
  - Invoke uses diffusers library for its model handling calls, but doesn't use diffusers pipelines to run inference. It has supported safetensors for a long time, and hasn't required conversions to diffusers for almost 2 years now. 

- ## [Standalone Diffusers vs ComfyUI inference speed : r/StableDiffusion _202410](https://www.reddit.com/r/StableDiffusion/comments/1g4xq2r/standalone_diffusers_vs_comfyui_inference_speed/)
- comfyui doesn't use diffusers, he implements his own modeling / attn processor code or copies the upstream impl for eg. SDXL or Flux

- ## [Is Diffusers worth learning? Or stick with Comfy? : r/StableDiffusion _202412](https://www.reddit.com/r/StableDiffusion/comments/1h3r670/is_diffusers_worth_learning_or_stick_with_comfy/)
- 👷: Diffusers is a bad library, there's a reason I didn't use it for ComfyUI and why no notable SD interface uses it. InvokeAI is the only notable SD interface that used it but I learned recently that they are transitioning away from it.

- It's much more useful to learn one comfyui api or forge api. Forge has a much cleaner api, but it's less flexible. There's just a lot of vram optimization that forge and comfyui do that are tedious to replicate.

- With Diffusers i can run in one pass: txt2img, img2img (another checkpoint), Face fix, Upscale - it does work on 4Gb VRam. With Comfy UI it is literally impossible. Only when I saw what is possible with custom implementation, I realized how sh1tty all those "Web UIs".

- From my small experience (i built backend using diffusers, FastApi).
  - What is good - very simple to use.
  - What is bad - it is bugged. Nobody will help you, you will learn diffusers code as your own.
  - While core Comfy UI code has advanced smart VRam management which allows it to run on low end GPUs. "Custom nodes" are literally horrible bug collection, forget about any logic.
  - Even though Diffusers has some bugs, it cannot compare vs Comfy UI nodes hell.

- I went pretty deep into diffusers, at a certain point you just hit a wall in terms of usability. There’s a reason even the pros use Comfy. Also plugins/extensions are very clearly defined with direct links to git, so you can decide for yourself. The top extensions are ranked accordingly.

- Experienced programmer that likes to tinker. So I made this: https://github.com/dkackman/diffusers-helper

- ## 🆚🤔 [Why diffusers results are so poor comparing to comfyUI? Programmer perspective : r/StableDiffusion _202504](https://www.reddit.com/r/StableDiffusion/comments/1k06zzd/why_diffusers_results_are_so_poor_comparing_to/)
  - I’m a programmer, and after a long time of just using ComfyUI, I finally decided to build something myself with diffusion models. 
  - My first instinct was to use Comfy as a backend, but getting it hosted and wired up to generate from code has been… painful.
  - I’ve been spinning in circles with different cloud providers, Docker images, and compatibility issues. A lot of the hosted options out there don’t seem to support custom models or nodes, which I really need. Specifically trying to go serverless with it.
  - So I started trying to translate some of my Comfy workflows over to Diffusers. But the quality drop has been pretty rough — blurry hands, uncanny faces, just way off from what I was getting with a similar setup in Comfy.
  - I saw a few posts from the Comfy dev criticizing Diffusers as a flawed library, which makes me wonder if I’m heading down the wrong path.
  - Now I’m stuck in the middle. I’m new to Diffusers, so maybe I haven’t given it enough of a chance… or maybe I should just go back and wrestle with Comfy as a backend until I get it right.

- I spent a long time chasing that rabbit hole once, and I assure you the results are identical if you are using identical settings, but not all settings are commonly exposed to users and the defaults are not always the same.
  - For instance, DDIM sampler has an `eta` input variable that some UIs will default to 1, but diffusers sets it to 0 unless you intentionally define it. Pony models specifically do not perform well on 0 and will give mushy results, but other architectures and finetune groups handle it fine.
- The difficulty with diffusers is not how it runs the model. At the end of the day, every backend eventually calls the same model forward pass and gets the same noise predictions. 
  - But the stuff around that, memory management, model storage, download cache, etc. can make it cumbersome to use directly in other apps. It's designed to make things convenient and easy to write quick scripts, assuming you are running on a research server with unlimited VRAM and 10GB download speeds. 
  - Comfyanonymous is a dev with strong opinions, and they wanted to create a more editable pipeline environment than diffusers allows normally. Both approaches are fine, and neither one is inherently flawed.

- I think InvokeAI uses diffusers for all generation and the quality is fine.

- In ideal case comfy generated image and diffusers generated image should be the same for the same model, seed, sampler, number of steps, LoRA strength etc.
  - I'd start with simplest workflow failure case and look for issues: e.g. often specific trainer script LoRA-s are not loaded at all for specific models (e.g. Flux1. D LoRa from ostris/ai-toolkit vs kohya-ss/sd-scripts may have different key names and just not load or some similar problem) - these issues can usually be quickly solved once identified.
  - Without more specific information the only suggestion is to browse the diffusers issues, e.g. searching for comfyui there to get a feel for the typical problems/solutions: https://github.com/huggingface/diffusers/issues?q=comfyui

- ## 🆚 [From ComfyUI to Diffuser Pipeline, why so many differences? : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1ewpcfg/from_comfyui_to_diffuser_pipeline_why_so_many/)
  - I've tried to replicate the generation process with Diffusers, using same LoRAs and same schedulers but the results are really different. ComfyUI generation quality is much better than Diffusers pipeline, even with same parameters.
  - It's no matter of seed, I know that one is CPU generated and the other is GPU generated. But with Diffusers the LoRAs seam to do not works well. I see a lot of artifacts or no prompt following.

- I noticed the same result. Somehow comfyui is giving better results has better prompt understanding and quality

- the samplers implementation and parameters are different, diffusers do not work with long prompts. if you make minimal example with raw python code and use short prompts - result will be same, it the output of the ML model after all.
# discuss-comfyui-like
- ## 

- ## 

- ## [InvokeAI's alternatives? : r/StableDiffusion _202405](https://www.reddit.com/r/StableDiffusion/comments/1d4jbsp/invokeais_alternatives/)
  - It lacks a lot of important features for composition: such as layers, color filters and even integration with other AI image processors for segmentation-based selection/masking.

- Invoke was really good for a while, but their refusal to add models like SC because they don't like the license is a bummer. The infinite canvas was such a game changer for me, but going to ditch it in the near future and learn the damn comfy one because it supports like every model type ever. I can train them all in one trainer, so I need a UI that can use them all to match it.

- Anyone who uses SD for work, or as a very serious hobby, should just bite the bullet and learn to use ComfyUI. It is not the easiest thing to use and has a learning curve, but it can do anything you want if it is doable with SD at all.
  - ComfyUI is the "official" (along with StableSwarmUI, which uses ComfyUI as the underlying engine) UI for SAI products. comfyanonymous works at SAI.
  - Almost without exception, all new techs appear first on ComfyUI. 
  - So if you like to play with shiny new toys, it is better to use ComfyUI (or StableSwarmUI if you want a friendly UI).
  - For example, support for new models such as Cascade, SD3, PixArt, CosXL all appear first there (and some are still not supported with A1111). Same with fancy options such as AYS, PAG, IPAdapter, Faceid, etc.

- Not as comprehensive but I use NMKD Stable Diffusion GUI locally. Its ok but it hasn't gotten an update in months. It doesn't have any of those newer features but it is fast


- 
- 
- 
- 
- 
- 

- ## [What comes closest to ComfyUI for LLMs? : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1e8k7q8/what_comes_closest_to_comfyui_for_llms/)
- make comfyui custom node. it is super easy. or there are some LLM node for comfyui, so you can use them.
  - What we need to complete the whole thing is a comfy node to run other comfy workflows as a sub-process.

- I think comfyui can do LLM too

- ## [ComfyUI for LLMs : r/comfyui _202412](https://www.reddit.com/r/comfyui/comments/1hgfy3g/comfyui_for_llms/)
- Why not make these into comfyui nodes if you love it so much?
  - We considered this but soon realised that Comfy is quite opinionated for diffusion
  - However, when we place LLM workflows at the highest priority, the ideal product in our view differs from Comfy significantly.
  - We would want to define the type of the output of a node in runtime.
  - Support more natural interaction with code: let LLMs execute code. This needs a python runtime/sandbox in the backend.
  - Support long running agentic workflows
- but every one of those functions is a (third party) node already in Comfy.
  - alternative view interfaces for gathering props in a sidebar have been done
  - ANY type nodes support variable outputs.
  - there are sandbox python executors, e.g. https://github.com/chrisgoringe/cg-use-everywhere
  - looping is still clunky as it basically relies on you iterating over files in a folder (e.g. json configs, text files or images) with each queue, but it's doable. if/else is easier (see Comfyui-Logic)
  - not sure what "long running" means here but I think a goal of Comfy is to get a stable environment that can churn for days or weeks on end.

- For future reference, I would probably be interested in a couple of nodes that can send input to one of these LLM workflows, and then have the results of the LLM workflow sent back into the next comfyui node

- Do you have some sort of bridge or API to interact with comfyui WFs?
  - While, this can be done currently using a python code node that calls the comfy workflow via comfy's API, but i agree that a proper node for this would be better.

- How does this stack up against Flowise or N8N?
  - In contrast to these two you mentioned, we offer built-in 
  - 1) evals, 
  - 2) prompting techniques like few-shot prompting and best-of-N sampling, 
  - 3) we’re close to releasing a self-improving pipeline feature (eg. using DSPy), which isn’t a current focus of those other tools.

- For anyone looking for a custom node solution within comfy that can use ollama/lmstudio etc have a look at Plush. Works great.

- Can you make a multi-agent workflow with it?
  - Yes, you can include a subworkflow into a larger workflow and also have different models and prompts for each node in the graph.

- What is the difference between dify and yours?
  - we focus on having evals built into the editor and we also support some nodes with certain prompting techniques like Best-of-N sampling that Dify doesn't support right now.
# discuss-image-generator-tool
- ## 

- ## 

- ## 

- ## [General AI Workflow Like ChatGPT Image Generator : r/comfyui _202504](https://www.reddit.com/r/comfyui/comments/1jxtqq9/general_ai_workflow_like_chatgpt_image_generator/)
  - What I'm asking is more about a general system that can take a prompt (including images) and generate an appropriate workflow automatically.. kind of like ChatGPT’s vision model does.

- You can imagine that the ChatGPT's vision model is designed to understand prompts and then "create" the corresponding workflow.

- Comfy Copilot can help you build workflows based on chat prompt: https://github.com/AIDC-AI/ComfyUI-Copilot

- Actually I never heard of anything like this and I think this would be a clever way of achieving what you want. I would personally try training a ML model by using a dataset text —> vector space —> cyclic node based graph. Very interesting subject I will think about it 

- Something using an LLM for "thinking", Flux for image generation and StableFlow for editing could maybe work. But as others have mentioned, it's not really the way I would use ComfyUI

- 
- 
- 
- 
- 
- 

# discuss-comfy-local-llama
- ## 

- ## 

- ## 

- ## [what is the strongest image describer in comfyui? (what you use?) : r/comfyui _202502](https://www.reddit.com/r/comfyui/comments/1iu4izz/what_is_the_strongest_image_describer_in_comfyui/)
  - many of cool workflows use a node to describe the photo first, so im wondering whats is the best option for it with SUPER DETAIL? strong enough to even mention clothes details
  - joy caption? QWenImage2Prompt? florence 2?
- I've said it before here, but Gemini on AI Studio is the best at this, hands down, point blank, period. If you prompt it right it will give you everything you ever need.

- Florence 2 good enough for me

- I tried them all. I usually go with JoyCaption. Perfect spot. ChatGPT playground is also quite good. Florence is disappointing.
- Joycaption 2, llama 3.2 vision

- I do it locally using OllamaVision node that comes with comfyui-ollama. Run local instance of ollama with a vision llm, I get amazing and detailed results with llama3.2-vision but it takes some time to generate the caption. My process is this: 
  - Load Image
  - Resize it maintaining the aspect ration to around 512px width
  - Pass the resized image to OllamaVision
  - In OllamaVision, set keep_alive to 0 and in textarea write something like "Describe the image in great detail with subject, background, clothes, colors and tint explained as a senior photographer. Reply in a single line"
  - You can join output of ollama vision with another text node that has prefixes like "good quality, masterpiece, 90s vibe, studio lightning, " etc using Text Combine node.

- I use Janus-Pro. It's pretty accurate most of the time.

- In my opinion every Model is lacking in details, so most of the times i manually correct generated Prompts

- Qwen 2, and Janus-Pro-7B for me. Florence 2 tends to get things wrong at lot of times. Qwen 2 has honestly been the best for me. Janus-Pro is good but it doesn't follow the prompts well (it needs a really detailed prompt)
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Why aren’t LoRA’s a big thing i the LLM realm? : r/LocalLLaMA _202312](https://www.reddit.com/r/LocalLLaMA/comments/18oj983/why_arent_loras_a_big_thing_i_the_llm_realm/)
- Loras work for stable diffusion because the models share an architecture
  - With language models there's a lot of variety so there's not a standard base

- The use cases aren't obvious; with Stable Diffusion it's clear how you can add a character or pose or whatever, with text the styles are more subtle.
  - An image model just needs a few pictures, text usually needs a lot more for what people want it to do.

- in some contexts, for an LLM it makes more sense to share the dataset rather than the LoRA. A LoRA will be stuck on whatever prompt format it was trained on, a dataset can (if set up correctly) easily switch to whatever prompt format you want. Plus, it makes it easier to extend the model by editing the dataset a little bit, and it avoids the problem of overwriting the existing instructions/examples by including them in the new fine-tune training.
  - There are far too many secret datasets.

- They are but people keep frigging releasing the merged model only.
  - Basically all finetunes are already trained as loras, and many backends/frontends support loras at runtime, but uploaders just dont post them.

- We need a Civitai for LLMs (no huggingface is not it)

- A big problem is that the Loras are trained on base transformers models while people want to run quantized models, as far as I know you can't use those loras then.
- qLoRAs specifically for some, it's a lot cheaper to train them, compared to a full fine tune, with similar performances.

- People release the merged model instead, as it's easier to quantize that, than just release the peft/adapter. Almost no one downloads the full fp16 model, it's easier to download a 4 bit gguf or gptq.

- ## [LoRA for LLM : r/LocalLLM _202502](https://www.reddit.com/r/LocalLLM/comments/1ii7q1y/lora_for_llm/)
  - Like can i download deepseek on a server. Use a LoRA trained on forums for IT problems and then cut it off from the internet. Feed it our customer database so like a LoRA for each customer or something.

- Look into RAG and vector database.
  - LLM provides the comprehension and logic skills, the knowledge itself is built on your stored dataset.
  - I keep playing with the concept of a data lake (tickets, network info, etc...) with AI playing the role of switchboard operator...
- lora is used to fine tune LLMs. But it isn't great for teaching an LLM new facts. It's more about teaching it input and output patterns. For example, if you train it in a dataset to take articles and output the authors name in a json object, it will learn how to do that, but it will not learn the contents of the articles or the author's names from the training dataset.

- Check out Llama. CPP server as it has support for Lora adapters.

- ## 🧩 [What is the Local LLM equivalent of a LORA? : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1axig7m/what_is_the_local_llm_equivalent_of_a_lora/)
- LoRAs were technically invented for language models first, before being applied to image models.
  - There's several tools for training them, including oobabooga/text-generation-webui, PeFT, and Axotol.
  - They're not as popular for text models because people usually merge them with their base model before distributing them on huggingface, but there are some plain LoRAs listed on huggingface. 

- Funny thing is basically all finetunes are trained as loras and merged with the weights after. It would be like all loras on CivitAI being distributed as 8GB+ checkpoints.
  - Basically the llm community never got in the habit of applying loras, so there isnt much pressure on UIs/backends for good support.
  - That is changing though. We have Lorax now, PEFT and VLLM just got lora support, ooba has had it for awhile...

- ## [Why lora isn't as famous in LLM as opposed to stable diffusion? Or am I missing out ? : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1dwohbd/why_lora_isnt_as_famous_in_llm_as_opposed_to/)
- LoRA work only on the base model it was trained on. For Stable Diffusion we had basically only SD 1.5 and its fine-tunes for a while, so no matter what LoRA you decided to train, you could be sure it would match 99% of all models out there.
  - For LLMs almost every model out there is a different base model.
- LLM space is arguably still waiting for its "Stable Diffusion moment" that would outline any LLM that stays on top of the pile for longer than a couple of months
- Base models in the world of LLM are replaced literally every month to a new better ones.

- Stable Diffusion (SD) models are essentially refined versions of the original weights—they all share the same parent model. This means that parameter 1 in model 1 will reference the same data as parameter 1 in model 2. Because of this, LoRAs for SD all essentially share the same internal "map" of their parameters. The only real difference is the magnitude by which they change the values.
  - most "base" versions of LLMs have different internal mappings. 
  - In order for LoRAs to take off for LLMs in the same fashion as SD, we would have to map out the parameters in both the LLM and the LoRA file, so we can apply the proper parameter adjustments to the correct relationships. 
  - A Stable Diffusion LoRA is cross-compatible because they all share the same internal structure.
  - LLM LoRAs are not cross-compatible because they all have different internal structures based on the model and training data.

- Merging lora into quantized models is a bigger problem. It's only possible for llama.cpp (that unfortunately still doesn't support runtime lora). Stuff like GPTQ/EXL requires running it over top and eating extra memory. Otherwise you have to get the full model, merge and then quantize again.
  - tldr: lora are inconvenient.

- most of the good ones are closed source

- Making a dataset a lora for SD is cheap in time and compute, you could make a lora for sd 1.5, 2.1 and SDXL and still finish it in a week.
  - Doing the same thing for llm is far more time and compute consuming, a bit more hazardous as you need far more data point than you could read in 10 years.. and training it on many models is inconceivable as each model reacts differently

- literally all fine tunes are loras. we just merge them down to the base model in LLMs because running inference with a lora is (or at least was) buggy and not really viable.

- Most of the fine-tuned models, especially for models >7B are LoRA or QLoRAs merged with the base model.

- ## [embarassing question: diffusers vs checkpoint : r/StableDiffusion _202404](https://www.reddit.com/r/StableDiffusion/comments/1cgv77m/embarassing_question_diffusers_vs_checkpoint/)
- To oversimplify, Diffusers is each part of the model (unet, text encoder etc.) split into separate files/folders. 
  - A safetensor/ckpt has this all bundled up together as one single file. 
  - Diffusers have a faster load time due to this.

- There are many different libraries (used from command line scripts) and UI: [List of SDK/Library for using Stable Diffusion via Python Code : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1askr5f/list_of_sdklibrary_for_using_stable_diffusion_via/)
  - Diffuser is one of the earliest and most popular such libraries, and in the beginning, it does not support safetensor or chkpt and has it own format. 
  - AFAIK, the latest version of the diffuser library now support them.

- ## [Should I use ComfyUI? : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1invics/should_i_use_comfyui/)
  - I have an extensive background in software development mostly developing frontend and backend using javascript and python. I want to start my journey with stable diffusion to generate something interesting. Should I learn how to use ComfyUI or would that be a waste of time considering I am already familiar with programming? 

- It will be easier for you to develop your own nodes with Comfy, but all third-party code is poorly written, seemingly made by inexperienced developers. (I examined how all Comfy front-end and back-end node interactions were implemented, and it's truly a developer's nightmare, with coding done in the worst way possible. Nevertheless, it mostly works.)
  - You can also implement your own inference backend using Diffusers as a low-level wrapper, which will take more time. The final output with Diffusers will be of the same quality as any other web UI.

- ComfyUI gets native support for a lot of the big releases on day 1, so if running new models on day 1 is of importance to you, then learn ComfyUI.

- Depends on what you want to do. If you're trying to automate image generation (e.g. for an IRC bot), then it's easy to use the diffusers python library
  - ComfyUI works as an JSON-over-HTTP API, and makes the best backend you can probably hope for in this space. You can export workflows as 'API' workflows once you're happy with them
- 🌹 The largest benefit is memory management. ComfyUI lets you swap between two dozen different models without leaking memory, which is not a feature I've noticed with Diffusers or Forge.

- ## [What's up with diffusers and ComfyUI? : r/comfyui _202310](https://www.reddit.com/r/comfyui/comments/17fvb49/whats_up_with_diffusers_and_comfyui/)
- Everything that has to do with diffusers is pretty much deprecated in comfy rn.. There has been a loader for diffusers models but its no longer in development, that's why people are having trouble using lcm in comfy now and also the new 60% faster sdxl (both only support diffusers)
  - Basically the diffusers library stores models in a completely different format like you mentioned, making it harder for users to create a local library of models. There can also be overhead from the storage aspect if the same model is duplicated inside the huggingface repo just to match the folder layout (happens too often imo). 
- ComfyUI does support some models in diffusers format (advanced->loaders->UNETLoader) but how it works is that it converts them to stability (ldm or sgm) format internally. 
- Diffusers format isn't widely used by most SD users, a1111 has zero out of the box support for those models and very few people use them with comfyui. You can create a custom node that loads a model with the diffusers unet code but it's not something I would add to the main repo.
