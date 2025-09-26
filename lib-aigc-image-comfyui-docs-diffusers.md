---
title: lib-aigc-image-comfyui-docs-diffusers
tags: [comfyui, diffusers, docs, image]
created: 2025-08-23T06:42:00.128Z
modified: 2025-08-23T11:42:50.170Z
---

# lib-aigc-image-comfyui-docs-diffusers

# guide

# docs-concepts
- [IPAdapter · vladmandic/sdnext Wiki](https://github.com/vladmandic/sdnext/wiki/IPAdapter)
  - IP-Adapter is a tool designed for style transfer with minimal resource usage. It provides an efficient way to clone faces or apply image transformations.
  - Low Resource Usage: The IP-Adapter is lightweight, with memory requirements under 100MB for SD 1.5 and 700MB for SD-XL, making it an efficient choice for style transfer tasks.
  - Style Transfer: It offers powerful style transfer capabilities, allowing you to clone faces or apply various image styles.
  - Integration with ControlNet: IP-Adapter can be combined with ControlNet for more stable results, especially useful for batch processing or video tasks.

- 
- 
- 
- 
- 
- 
- 

# docs-sd-webui

- 
- 
- 
- 

## api-webui

- [API · AUTOMATIC1111/stable-diffusion-webui Wiki](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/API)
  - [Stable Diffusion web UI txt2img img2img api example python script](https://gist.github.com/w-e-w/0f37c04c18e14e4ee1482df5c4eb9f53)
- /sdapi/v1/txt2img
  - 

- request POST
  - `override_settings`: The purpose of this parameter is to override the webui settings such as model or CLIP skip for a single request.
  - `sdapi/v1/options`: different from override_settings because this change will persist

```JSON
{
  "prompt": "",
  "negative_prompt": "",
  "styles": [
    "string"
  ],
  "seed": -1,
  "subseed": -1,
  "subseed_strength": 0,
  "seed_resize_from_h": -1,
  "seed_resize_from_w": -1,
  "sampler_name": "string",
  "scheduler": "string",
  "batch_size": 1,
  "n_iter": 1,
  "steps": 50,
  "cfg_scale": 7,
  "width": 512,
  "height": 512,
  "restore_faces": true,
  "tiling": true,
  "do_not_save_samples": false,
  "do_not_save_grid": false,
  "eta": 0,
  "denoising_strength": 0,
  "s_min_uncond": 0,
  "s_churn": 0,
  "s_tmax": 0,
  "s_tmin": 0,
  "s_noise": 0,
  "override_settings": {},
  "override_settings_restore_afterwards": true,
  "refiner_checkpoint": "string",
  "refiner_switch_at": 0,
  "disable_extra_networks": false,
  "firstpass_image": "string",
  "comments": {},
  "enable_hr": false,
  "firstphase_width": 0,
  "firstphase_height": 0,
  "hr_scale": 2,
  "hr_upscaler": "string",
  "hr_second_pass_steps": 0,
  "hr_resize_x": 0,
  "hr_resize_y": 0,
  "hr_checkpoint_name": "string",
  "hr_sampler_name": "string",
  "hr_scheduler": "string",
  "hr_prompt": "",
  "hr_negative_prompt": "",
  "hr_cfg": 1,
  "force_task_id": "string",
  "sampler_index": "Euler",
  "script_name": "string",
  "script_args": [],
  "send_images": true,
  "save_images": false,
  "alwayson_scripts": {},
  "infotext": "string"
}
```

- response-200-Successful
  - `images` is a list of base64-encoded generated images.

```JSON
{
  "images": [
    "string"
  ],
  "parameters": {},
  "info": "string"
}
```

- response-422-Validation Error

```JSON
{
  "detail": [
    {
      "loc": [
        "string",
        0
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}
```

- 
- 
- 
- 

# docs-diffusers
- A diffusion model combines multiple components to generate outputs in any modality based on an input, such as a text description, image or both.
- For a standard text-to-image model:
  - A text encoder turns a prompt into embeddings that guide the denoising process. Some models have more than one text encoder.
  - A scheduler contains the algorithmic specifics for gradually denoising initial random noise into clean outputs. Different schedulers affect generation speed and quality.
  - A UNet or diffusion transformer (DiT) is the workhorse of a diffusion model. At each step, it performs the denoising predictions, such as how much noise to remove or the general direction in which to steer the noise to generate better quality outputs. The UNet or DiT repeats this loop for a set amount of steps to generate the final output.
  - A variational autoencoder (VAE) encodes and decodes pixels to a spatially compressed latent-space. Latents are compressed representations of an image and are more efficient to work with. The UNet or DiT operates on latents, and the clean latents at the end are decoded back into images.
- The `DiffusionPipeline` packages all these components into a single class for inference.
- Adapters insert a small number of trainable parameters to the original base model. 
  - Only the inserted parameters are fine-tuned while the rest of the model weights remain frozen. This makes it fast and cheap to fine-tune a model on a new style. 
  - Among adapters, LoRA’s are the most popular.
- Quantization stores data in fewer bits to reduce memory usage. It may also speed up inference because it takes less time to perform calculations with fewer bits.
- 
- 
- 
- 
- 
- 

# docs-InvokeAI
- When you start working on a blank Canvas, your first image generation will be added as a Raster Layer
- Layers are a powerful set of tools enabling you to control and guide the image generation process to produce a desired outcome.
- Regional Reference Image layers use Image Prompt (IP) Adapters to inspire a new image with the content of an input image. You can use add Regional Reference Images as layers on the ‘Layers’ tab.
- Inpaint Mask layer allows you to specify a region that will be modified for generation, while preserving the rest of your raster layer data.
  - The Denoising Strength that you select will dictate how much change you want the AI model to generate in the selected region. At very high denoising strengths, the newly generated content will be very different from your original image, and at low denoising strengths, it will only make minor changes.
- Regional Guidance layers allow you more fine-tuned control over the prompt information used to guide the generation process. 
- Control Layers can provide structural control over the output of your image generations, with a number of different ways to instruct the system using visual representations like sketches, edge maps, and depth renderings.
- A Raster Layer is the image content of your canvas, similar to other Image Editing solutions. 
  - When included in your bounding box, these images serve as the base image content to start your creative process
  - This layer allows you to inspire the generation process with an initial drawing or image, which preserves the original image's rough structure, colors, and layout, while using AI to reimagine new content with your input prompt based on your denoising strength.
- Inpainting, in the context of image generation, is a process where we try to fill in parts of an image with new or modified content.
  - inpainting methods use the available information in an image (such as edges, textures, colors) to predict what the incomplete areas should look like, and then uses the selected model to regenerate that portion of the image
- 
- 
- 
- 
- 

# more
- [Hosting a ComfyUI Workflow via API - 9elements _202402](https://9elements.com/blog/hosting-a-comfyui-workflow-via-api/)
