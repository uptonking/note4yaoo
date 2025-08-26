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

- ## [Best way to share models between ComfyUI, Forge, and Automatic1111 : r/StableDiffusion _202403](https://www.reddit.com/r/StableDiffusion/comments/1b8gc4o/best_way_to_share_models_between_comfyui_forge/)
- You could change the config files for each package to all point to the same directories (or use symlinks).

problem is when software like InvokeAI or some else are using the diffusers format and is also converting the .safetensors to a directory

- problem is when software like InvokeAI or some else are using the diffusers format and is also converting the .safetensors to a directory

- ## [What projects and plugins have implemented the separation of the frontend and backend in ComfyUI? · Issue · comfyanonymous/ComfyUI _202407](https://github.com/comfyanonymous/ComfyUI/issues/3973)
  - Frontend: Extracting the ComfyUI frontend into a separate project.
  - Backend: A GPU cluster receives tasks and runs them in ComfyUI worker, with multiple frontends sharing these GPU clusters.
  - The number of frontend users is much greater than the number of backend GPU nodes, and user tasks are queued for execution.

- Swarm does this, allowing both many-users and many-backends relatively cleanly.
  - There are also various webservices that do things like dynamic backends, such as ComfyDeploy

- ## [Execution Model Inversion · comfyanonymous/ComfyUI _202408](https://github.com/comfyanonymous/ComfyUI/pull/2666)
  - This PR inverts the execution model -- from recursively calling nodes to using a topological sort of the nodes. 
  - This change allows for modification of the node graph during execution. 
- This allows for two major advantages:
  - 1. The implementation of lazy evaluation in nodes. or skip evaluation
  - 2. Dynamic expansion of nodes. This allows for the creation of dynamic "node groups". Specifically, custom nodes can return subgraphs that replace the original node in the graph. This is an incredibly powerful concept.

# discuss-diffusers
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
  - With Diffusers i can run in one pass: txt2img, img2img (another checkpoint), Face fix, Upscale - it does work on 4Gb VRam. 
  - With Comfy UI it is literally impossible. 
  - Only when I saw what is possible with custom implementation, I realized how sh1tty all those "Web UIs".

- It's much more useful to learn one comfyui api or forge api. Forge has a much cleaner api, but it's less flexible. There's just a lot of vram optimization that forge and comfyui do that are tedious to replicate.

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
# discuss-InvokeAI
- resources-InvokeAI
  - 🎯 [v4.2.6 _202407](https://github.com/invoke-ai/InvokeAI/releases/tag/v4.2.6)
    - Checkpoint models work without conversion to diffusers
    - The `diffusers` library now supports loading single-file (checkpoint) models directly, and we have removed the mandatory checkpoint-to-diffusers conversion step.
    - The main user-facing change is that there is no longer a conversion cache directory.

- ## 

- ## 

- ## 🆚🤔 With invoke AI when I scan a folder for models from stable diffusion is it copying them??? somewhere? Id like to use the models as is
- https://discord.com/channels/1020123559063990373/1020123559831539744/1409616188539142254
- there's an 'in-place' checkbox, if it's checked, they'll stay where they are and it'll use those
  - otherwise it copies them, and uses those copies instead

- yes I checked the inplace, however it is hash checking them?
  - that's normal

- for latest invoke v6, when i set Scan Folder to ~/Documents/ComfyUI/models  and mark in-inplace as checked, will invoke auto convert all my checkpoint/lora safetensors to internal diffusers format, so duplicated?
  - thats are old info about invoke. 
  - since version 4.2.6 "Checkpoint models work without conversion to diffusers"
  - i still convert model that i use most of the time for faster loading time.

- ## [Invoke.ai in Stability Matrix - way to share models? : r/StableDiffusion _202411](https://www.reddit.com/r/StableDiffusion/comments/1h0h5b3/invokeai_in_stability_matrix_way_to_share_models/)
  - since Invoke in S. M. doesn't offer the normal model sharing option that all other GUI have, I wonder how other users of multiple AI GUI are dealing with the fact that you already have possibly two dozen great model files, each with 6 GB, on your hard-drive, that Invoke. AI simply doesn't 'see'. Duplicating them is obviously no option.

- The reason why InvokeAI doesn't the share thing through the symlink is because there is simply no folder where the model could be shared to. That's why you have to add the whole Models folder through the Models tab in InvokeAI.
  - Otherwise everything that InvokeAI downloads is in diffusers format.

- That may be an explanation - but to me this is still no sufficient reason why they departed from the common way. I've got 7 different image generator GUI in 'Stability Matrix' - but only Invoke.ai is not playing by the rules here. 
  - InvokeAI uses diffusers library, other UIs have their own implementations. It seems that they prefer if you use diffusers files that you can directly download just by inputting HF repository, while pointing to folders for everything else.

- ## 🤔 [What is stopping InvokeAI from getting popular in this community? : r/StableDiffusion _202403](https://www.reddit.com/r/StableDiffusion/comments/1b4jbhq/what_is_stopping_invokeai_from_getting_popular_in/)
- One of my biggest issues was my inability to re-use my models.
- For me the main reason to nuke it and never reinstall is that it is based on the diffusers file format and needs duplicates of all models. 
  - On top of that it doesn't even consider the huggingface_cache. More dupes. 
  - Fast disk space is always tight so this is a weak link.
  - Also diffusers samplers/schedulers are usually missing the latest, somewhat unmaintained and often are of lower quality. 
- This is the same reason I've also stopped using it. I want to be able to just point it at the same folders with models, loras, etc that I use in all other programs.

- InvokeAI was way behind in compatibility for ages - couldn't do LoRAs and it couldn't process past the 77th token in a prompt which put a lot of people off.

- 👷: I’m one of the early folks on the project and now-CEO of our business. 
  - It’s important to recognize that our teams focus is serving the professionals looking to use this for work. 
  - They need something that is commercially licensed (a lot of research/frontier code and models in this space are not usable, or built for stable deployments) and useful for the day to day workflow.
  - We’re building for the long term, making sure new features “just work” with everything else, and consolidating the core pro feature set into a single integrated deployment.
  - The non-commercial stuff can be easily extended with custom nodes and workflows.
  - AMD on Windows is still very much an issue - We've heard some folks report success w/ Docker installs, or running on WSL - But it requires a bit of fiddling.

- Invoke's power lies in giving users the ability to control and guide the output in an interface that is easy and nice to use. 
  - Invoke is not the only creative interface. Krita and Photoshop plugins do the same thing, and OpenOutpaint has even more features even if it is clunky to use. 

- As an advanced user I couldn't use Invoke for a long time because it didn't even support embeddings
  - Embeddings were definitely messy at one point. For some time they only supported single-vector TI, so effects would not match between Invoke and A1111. I think that was about a year ago now.
  - One of the main problems is that there were core issues that didn't get fixed for a long time while they worked on refactoring their backend to run on Diffusers and Nodes. It was a good plan for the future, but it took so long that Invoke garnered a reputation for being behind the curve.

- Infinite Canvas has some lovely features that are extremely polished, but Open Outpaint has better features (at time of testing summer of 2023) that makes me put up with its jank over InvokeAI:
  - Composition layers
  - A proper history list for the composition like Photoshop/Affinity/GiMP
  - A history of prompts used in the composition
  - Soft edge masking
  - Eraser tool for masks
  - Ability to export prompts and canvas and canvas resources and canvas history as an external file that you can later import. Like a .psd file for Stable Diffusion workflow
- The lack of those sorts of things made me bounce hard off Invoke. Which is a pity, because Invoke does have a nice interface.

- InvokeAI had a lot of things done right. Like, how embedding work. You write < and start writing and it searches from available embeddings. It seems a lot slicker and compact. While unified canvas offers very simple way of outpainting, cropping, changing composition fast. I have not tried inpainting models, because there is no need.

- I did not like that they forced me to use diffusers format. I do not want to save all of my models twice on my hard drive and wait for all the conversion
- Forced? It reads safetensor and ckpt just fine.
  - Yeah, but it is just converting them to diffusers format and keeping the ckpt/safetensor on your drive also.

- ## [Invoke AI saved me! My struggles with ComfyUI : r/StableDiffusion _202508](https://www.reddit.com/r/StableDiffusion/comments/1mxolbn/invoke_ai_saved_me_my_struggles_with_comfyui/)
- I've got both Invoke and Comfy installed, but then I realised Comfy doesn't have a canvas or any easy way to add masks and guidances really, and the learning curve to get plugins for all that and installing everything properly is way too steep for someone who doesn't even know how to generate properly yet.
  - I'm glad you understand: the canvas, layers etc... are the real thing that separates this as a usable tool compared to the ramshackle nonsense that ComfyUI demands
- Comfy has a canvas. It's in the drop-down menu in the load image node. There's a hotkey shortcut too but I can't remember what it is. You just load the image, open the canvas, and draw on the mask. Simple.
  - https://github.com/Azornes/Comfyui-LayerForge

- That's the main idea behind InvokeAI: to have an interface for those who have worked with image editors in the past. The canvas is excellent; you can do whatever you want as an artist, quickly and easily.
  - The only problem is that it updates very slowly and doesn't implement the latest advancements. For example, you can't use Flan-T5-XXL-FP16 like in Forge, and they still haven't implemented support for Chroma or Nunchaku.

- If Comfy can solve its dependency and node issues, it will become a far more accessible and widely used tool. 
  - Unlike Invoke, there's no easy canvas, layering system, or asset gallery to make working efficient. Having to scrub about in output folders is maddening.

- I like Invoke and the people working on it seems decent, but they are to far behind with adding support for anything new. (Local support)
  - They need to add svdquant/nunchaku support, though I doubt they will. And their upscale works but it’s far from perfect and slow.

- I feel that comfy is a good tool for working with workflows, but a bad tool for working with images.
- You get it. Professionals don't have time to be a node/workflow hobbyist and traverse the nightmare that is the UI. I think people misunderstand what these tools are. ComfyUI is a great developer playground for testing things out, but it's absolutely not an efficient and professional way to work.

- ## [What do you think about invoke? : r/comfyui _202411](https://www.reddit.com/r/comfyui/comments/1h0hjha/what_do_you_think_about_invoke/)
- I love it, but it uses more VRAM than Comfy.
  - I honestly just like the simple UI and how it uses boards to organize images.

- I personally think that integrating diffusion tools in existing drawing software like krita for example is a better idea than trying to do a whole photoshop interface from scratch like they are doing.
  - The only thing they have over ComfyUI is better UX in some specific areas but I think we will surpass them soon if we have not already.

- I couldn’t get invoke to perform in a ROCm setup. So it was super slow and buggy for me. 

- ## [InvokeAi vs ComfyUi overall outputs quality : r/StableDiffusion _202507](https://www.reddit.com/r/StableDiffusion/comments/1m9pkg7/invokeai_vs_comfyui_overall_outputs_quality/)

- Invoke was made and tuned for inpainting, Comfyui was made to run all open source ai model available.
  - Invoke lean more into heavy inpainting so it's tools refined to make inpainting more easy. In comfy same can be done but probably will require a lot fiddling with workflows and custom nodes.

- Considering that InvokeAI still doesn't support CN inpaint, I hardly use it for inpainting specifically.
- Are you sure it doesn't support that? I'm inpainting at 1.0 denoise with a control layer that's using the controlnet union promax in invoke. The results are great. Is that not controlnet inpainting?
  - Union may automatically do something that is beside the inpainting but other type of CN. Besides, you can do 1.0 denoising strength generation even without any CN model, so it doesn't even play a role here. My issue is that I want to use CN models and not whatever they are using instead.
  - It also lacks specific preprocessors for inpaint

- It can't be CN because it lacks preprocessors for inpainting, which uses both a mask and an image - control layers don't do that
  - Denoising strength at 1.0 also isn't specific to CNs (Fooocus inpaint is a patch and not a CN). It just that CNs generally do it better.

- some general tips:
  - Inpainting works much better when the underlying pixels kinda-sorta match the color you're going for.
  - Zoom in by shrinking the bounding box, and make sure autoscaling is turned on (default setting so if you haven't messed with it you should be good). Invoke renders small bounding box areas at full resolution and then scales down, which can help details come through better.
  - But don't zoom in too much. Zooming in will give you better detail, but Invoke will lose the context of the surrounding area.
  - If necessary, do two passes. The first "main" pass, and then a second low-denoise pass along the border to help things blend better.

- Bonus part is that invoke also supports tablets with pen pressure sensitivity so it makes it a lot easier.

- I like invoke but they don't support Chroma yet.
  - Chroma has flash and quantitative models now too, so it's way improved.
  - There is technically a node for Chroma in InvokeAI: https://gitlab.com/keturn/chroma_invoke But at this point it is easier to deal with it in ComfyUI

- ## [ComfyUI or InvokeAI? : r/StableDiffusion _202505](https://www.reddit.com/r/StableDiffusion/comments/1koj2br/comfyui_or_invokeai/)
- Invoke is better: 
  - If you want direct control over the composition and output - the control layers and regional prompting are smooth and easy to work with
  - If you do lots of inpainting and refinement
  - If you want an easier, more polished experience

- Comfy is better:
  - If you have some specific piece of tech you want to use that isn't supported elsewhere
  - If you want direct control over the render pipeline (ie: what happens during each step)
  - You want to create automated workflows

- Invoke has a much better UI, but is limited by what is implemented (models, etc.). Comfy does everything, but much more awkwardly.

- I like InvokeAI for it's UI and canvas, but it's options limited. Want more options - use node builder. If I need node builder after all, why I needed InvokeAI, I go to more powerful and flexible ComfyUI.

- ## [[bug]: Flux Extremely Slow in Invoke Compared to ComfyUI and Forge · Issue · invoke-ai/InvokeAI _202502](https://github.com/invoke-ai/InvokeAI/issues/7612)
- I think the developers are not interested in optimizing and popularizing InvokeAI. There are a couple of similar issues here, and after months, there’s still no response from anyone.
  - While I’ve always been pleasantly impressed by their frontend, their backend is unbelievably sluggish and outdated. 
  - Invoke consistently runs slower while consuming more resources, and its features pale in comparison to even the basic ComfyUI (I'm not talking about the huge number of third-party nodes from enthusiasts).

- ## [InvokeAI's alternatives? : r/StableDiffusion _202405](https://www.reddit.com/r/StableDiffusion/comments/1d4jbsp/invokeais_alternatives/)
  - It lacks a lot of important features for composition: such as layers, color filters and even integration with other AI image processors for segmentation-based selection/masking.

- Invoke was really good for a while, but their refusal to add models like SC because they don't like the license is a bummer. The infinite canvas was such a game changer for me, but going to ditch it in the near future and learn the damn comfy one because it supports like every model type ever. I can train them all in one trainer, so I need a UI that can use them all to match it.

- Anyone who uses SD for work, or as a very serious hobby, should just bite the bullet and learn to use ComfyUI. It is not the easiest thing to use and has a learning curve, but it can do anything you want if it is doable with SD at all.
  - ComfyUI is the "official" (along with StableSwarmUI, which uses ComfyUI as the underlying engine) UI for SAI products. comfyanonymous works at SAI.
  - Almost without exception, all new techs appear first on ComfyUI. 
  - So if you like to play with shiny new toys, it is better to use ComfyUI (or StableSwarmUI if you want a friendly UI).
  - For example, support for new models such as Cascade, SD3, PixArt, CosXL all appear first there (and some are still not supported with A1111). Same with fancy options such as AYS, PAG, IPAdapter, Faceid, etc.

- Not as comprehensive but I use NMKD Stable Diffusion GUI locally. Its ok but it hasn't gotten an update in months. It doesn't have any of those newer features but it is fast
# discuss-comfyui-like
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

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

- ## 🚀 [ComflowySpace: An open-source version of better ComfyUI | Hacker News _202403](https://news.ycombinator.com/item?id=39639418)
- The non standard licensing puts me off in contributing or using this
  - This is not Open Source. It is Source Available with usage restrictions. 
  - But the license not only restricts commercial use, it fails to even allow modification or redistribution.

- I look at the readme and I think it's just a minimal effort layer on top of ComfyUI. It's main point seems to be "easier installation" but it's not ComfyUI that's difficult to install. It's the GPU libraries. CPU based ComfyUI is a `git clone` and a `pip install -r requirements`.
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

# discuss-comfyui
- ## 

- ## 

- ## 

- ## 

- ## [Proposal: Replacing aiohttp with FastAPI in ComfyUI Backend · comfyanonymous/ComfyUI _202412](https://github.com/comfyanonymous/ComfyUI/discussions/5931)
- our team at Nextcloud—where we were considering offering ComfyUI to the community—has currently put that plan on hold until the situation improves.

- ## [ComfyUI backend questions · Issue · comfyanonymous/ComfyUI _202307](https://github.com/comfyanonymous/ComfyUI/issues/930)
- On the latest you can "enable dev mode options" in the settings (gear beside the "Queue Size: ") this will enable a button on the UI to save workflows in api format.

# discuss-comfy-local-llama
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
