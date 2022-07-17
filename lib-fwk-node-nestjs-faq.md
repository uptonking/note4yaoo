---
title: lib-fwk-node-nestjs-faq
tags: [faq, nestjs]
created: 2020-12-17T18:04:47.102Z
modified: 2021-04-23T18:12:22.607Z
---

# lib-fwk-node-nestjs-faq

# faq-not-yet

# faq-repeat

# faq

 

- "Circular dependency" error
  - Circular dependencies can arise from both providers depending on each other, or typescript files depending on each other for constants, such as exporting constants from a module file and importing them in a service file.
  - In the latter case, it is advised to create a separate file for your constants. 
  - In the former case, please follow the guide on circular dependencies and make sure that both the modules and the providers are marked with forwardRef.
