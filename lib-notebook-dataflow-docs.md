---
title: lib-notebook-dataflow-docs
tags: [dataflow, docs]
created: '2021-05-14T17:35:43.079Z'
modified: '2021-05-14T17:35:56.576Z'
---

# lib-notebook-dataflow-docs

# guide

## [ObservableHQ vs. Dataflow](https://alexgarcia.xyz/dataflow/docs/#using-dataflow)

- 相互import，暂不支持

# blogging

## overview

- https://github.com/asg017/dataflow
  - https://alexgarcia.xyz/dataflow/docs/
  - A self-hosted Observable notebook editor, with support for FileAttachments, Secrets, custom standard libraries, and more!

- Observable notebooks are reactive, JavaScript-based computational notebooks that run inside your browser.
- Dataflow is one of the first fully open-sourced and fully featured Observable notebook editors
- Dataflow notebooks are files on your computer, in the form of `.ojs` files. 
- A single `.ojs` file is analog to a single Observable notebook, and `.ojs` files can import from other .ojs files.
  - dataflow run my-notebook.ojs will start a dev server at localhost:8080 that shows a live rendered look at a notebook defined in my-notebook.ojs
  - Any update you make to the my-notebook.ojs file from any text editor will instantly update.
  - Dataflow can also compile these notebooks with dataflow compile to plain JavaScript ES modules, and generate HTML files that run a notebook locally.
- Since Dataflow notebooks aren't ran in a sandboxed iframe, that means you can control every aspect to how a notebook looks.
  - Dataflow also offers easy access to your filesystem with file attachments. 
  - Instead manually uploading files, you can simple include a configuration comment in a notebook to the path of your FileAttachment, and Dataflow will be instantly available 
- Finally, since Dataflow is just another service that runs on localhost:8080, you can build your own APIs and webservices

## [Introducing Dataflow, a self-hosted Observable Notebook Editor](https://observablehq.com/@asg017/introducing-dataflow)

- Dataflow is a new tool that lets you run, edit, and compile Observable notebooks locally on your own computer, with any text editor you want!
- In Dataflow, Observable notebooks are files on your computer, with a `.ojs` extension by convention (to distinguish Observable JavaScript from other JavaScript files). 
  - `.ojs` files cam import other .ojs files, and from notebooks hosted on observablehq.com.

- **features**
- Import from other local .ojs files!
- Import from ObservableHQ notebooks!
- FileAttachments!
  - FileAttachments in Dataflow are just files on your computer. 
  - A configuration comment at the very top defines the names and path of a FileAttachment, 
  - and they can be referenced in code with the FileAttachment builtin!
- Live File Attachments!
  - LiveFileAttachments are a Dataflow specific feature that allows you to reference a FileAttachment, and have it update whenever the underlying file updates! 
  - This is fantastic when you're working with other CLI tools or programs
- Secrets
  - Pass in secrets from the `dataflow run` command to avoid putting secrets in source code! 
- Custom Standard Libraries!
- Compile to ES Modules and html!
  - using the `dataflow compile` command to compile your notebook into ES modules and an example index.html file! 

- Dataflow, or ObservableHQ?
  - Dataflow uses the same underlying open source technologies as the notebooks on observablehq.com, such as the Observable notebook runtime, parser, standard library, and inspector. 
  - The sole exception is the compiler, which the observablehq.com compiler is closed-sourced, but Dataflow uses the unofficial-observablehq-compiler project.
  - ObservableHQ is a fantastic SaaS product with an in-browser editor and collaboration features, while Dataflow is a CLI tool that works with local files that you must selfhost. 

# [docs](https://alexgarcia.xyz/dataflow/docs/)

## Quickstart

- Dataflow is a program that you install on your computer and use on the command line.
  - `dataflow run` will start a dev sever that enable a live editing experience for your `.ojs` notebook files, a
  - nd `dataflow compile` will compile those files into re-usable JavaScript ES modules for use in other projects.
- In Dataflow, you work with .ojs files, which has a similar vibe as JavaScript, but with key differences. 
  - If you copy+paste the cells found in Observable notebooks at observablehq.com into a new file by itself, then that would be an `.ojs` file!
  - you can use whatever text editor you want: VS Code, vim, nano, whatever can edit a file!
- Just like observablehq.com, Dataflow uses the Observable notebook Standard Library, so cells like Promises, html, md, require, and more all are builtin by default. 
  - `viewof` and `mutable` cells are also supported.
- One key difference with observablehq.com: The builtin cells for `html` and `svg` use `@observablehq/htl` instead. 
  - This means that not all notebooks found on observablehq.com will work when importing from Dataflow, 
  - but the API is similar enough to make upgrades only take a few minutes.
  - Also, since v3.5.0 of the Observable standard library, the builtin cells `Plot`, `Inputs`, `vl`, `d3`,  `htl` have been included, and are available in Dataflow.

## File Attachments

- FileAttachments paths are defined in a configuration comment at the very top of a `.ojs` file. 
- Live File Attachments are a Dataflow-specific feature that is only available in the `dataflow run` command (ie, not in compiled notebooks). 
  - Live File Attachments "watch" for live updates to a file attachment.

## [Compiling Notebooks](https://alexgarcia.xyz/dataflow/docs/#compiling-notebooks)

- Your `.ojs` files can be compiled to ES modules for easier integrations with other tools, similar to the Advanced Embedding and Downloading on observablehq.com.
  - These compiled files could be included in other projects like React apps, SPAs, or any other place the web can reach
- Compiling does not bundle everything needed to run an Observable notebook. 
  - You will still need to include the Observable runtime when embeding your notebooks elsewhere, 
  - and any dynamically fetched dependencies (like require() or import()) inside your code will not be included in the compiled bundle. 
- FileAttachments are included inside the compiled bundle.
