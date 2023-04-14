---
title: lib-notebook-jupyter-dev
tags: [jupyter, lib, notebook]
created: 2021-05-17T11:52:36.756Z
modified: 2021-05-17T11:53:13.568Z
---

# lib-notebook-jupyter-dev

# guide

# faq
- ## vote: if you do exploratory data analysis or build machine learning models, what tool do you reach for first?
  - local, Jupyter notebook
  - local, data science ide(spyder, rstudio, jupyterlab, matlab)
  - hosted, colab
  - pycharm, vscode
- JupyterLab has made some really nice improvements lately – would definitely feel comfortable calling it an IDE, and certainly feel that it is differentiated compared to Jupyter notebooks.
- I think Jupyter Lab is in the same category as RStudio etc, though i don't think I'd call it an IDE, maybe an IDSE (integrated data science environment). I think it's worth emphasizing the order of priorities to be DS first, developing second
- why do so many people still use notebooks and not Jupyter Lab?
  - [Benefits of the classic UI and use cases for classic over JupyterLab](https://discourse.jupyter.org/t/benefits-of-the-classic-ui-and-use-cases-for-classic-over-jupyterlab-was-why-is-tim-not-moving-to-lab/2419)
  - The goal of the jupyterlab-classic project is to look as close to the classic notebook UI as possible, while leveraging the efforts put in the development of JupyterLab itself and its extension system
# pieces

# jupyter-js-notebook

# jupyter-extensions
- https://github.com/yunabe/tslab
  - tslab is an interactive programming environment and REPL with Jupyter for JavaScript and TypeScript users. 
  - You can write and execute JavaScript and TypeScript interactively on browsers and save results as Jupyter notebooks.

- https://github.com/twosigma/beakerx
  - BeakerX is a collection of JVM kernels and interactive widgets for plotting, tables, autotranslation, and other extensions to Jupyter Notebook and JupyterLab version 1.2.x and 2.x.
  - Version 2.x of BeakerX improves on the original solution architecture by providing independent modules that end-users can install to better tune the platform.
  - The kernel is originally derived from lappsgrid, but has been rewritten in Java and refactored and expanded.

- https://github.com/bloomberg/ipydatagrid
  - Fast Datagrid widget for the Jupyter Notebook and JupyterLab
  - [I see some cons using Web Workers like it is done in ipysheet](https://github.com/bloomberg/ipydatagrid/issues/3)
# docs
- [Project Jupyter](https://jupyter.org/)
  - Project Jupyter exists to develop open-source software, open-standards, and services for interactive computing across dozens of programming languages.

- https://github.com/jupyter/jupyterlab
  - JupyterLab: The next generation user interface for Project Jupyter
  - notebook、editor、console、terminal

- [The Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html)

## [Jupyter Notebook](https://jupyter.org/)

- The notebook extends the console-based approach to interactive computing in a qualitatively new direction, 
  - providing a web-based application suitable for capturing the whole computation process: developing, documenting, and executing code, as well as communicating the results.
- The Jupyter notebook combines two components:
- A web application: 
  - In-browser editing for code, with automatic syntax highlighting
  - In-browser editing for rich text using the Markdown markup language
  - The ability to execute code from the browser
  - Displaying the result of computation using rich media representations, such as HTML, LaTeX, PNG, SVG, etc
  - The ability to easily include mathematical notation within markdown cells using LaTeX, and rendered natively by MathJax.
- Notebook documents: 
  - contains the inputs and outputs of a interactive session as well as additional text that accompanies the code but is not meant for execution.
  - These documents are internally JSON files and are saved with the `.ipynb` extension. 
  - Notebooks may be exported to a range of static formats

## [The Jupyter Notebook File Format](https://nbformat.readthedocs.io/en/latest/format_description.html)

- The official Jupyter Notebook format is defined with this JSON schema, which is used by Jupyter tools to validate notebooks.
- All metadata fields are __optional__.
  - While the types and values of some metadata fields are defined, no metadata fields are required to be defined. 
  - Any metadata field may also be ignored.

- At the highest level, a Jupyter notebook is a dictionary with a few keys:
  - metadata (dict)
  - nbformat (int)
  - nbformat_minor (int)
  - cells (list)
- Some fields, such as code input and text output, are characteristically multi-line strings. 
  - If you intend to work with notebook files directly, you must allow multi-line string fields to be either a string or list of strings.
  - On disk, multi-line strings MAY be split into lists of strings.
  - When read with the nbformat Python API, these multi-line strings will always be a single string.

- Cell ids
  - Since the 4.5 schema release, all cells have an `id` field which must be a string of length 1-64 with alphanumeric(含有字母和数字的), -, and _ as legal characters to use.

- There are a few basic cell types for encapsulating code and text. 
- All cells have the following basic structure:

```JSON
{
  "cell_type" : "type",
  "metadata" : {},
  "source" : "single string or [list, of, strings]",
}
```

### Markdown cells

- Markdown cells are used for body-text, and contain markdown, as defined in GitHub-flavored markdown, and implemented in [marked](https://github.com/markedjs/marked).

```JSON

{
  "cell_type" : "markdown",
  "metadata" : {},
  "source" : "[multi-line *markdown*]",
}
```

- Heading cells have been removed in favor of simple headings in markdown.

### Code cells

- Code cells are the primary content of Jupyter notebooks. 
  - They contain source code in the language of the document’s associated kernel, and a list of outputs associated with executing that code. 
  - They also have an execution_count, which must be an integer or null.

```JSON
{
  "cell_type" : "code",
  "execution_count": 1, # integer or null
  "metadata" : {
      "collapsed" : True, # whether the output of the cell is collapsed
      "scrolled": False, # any of true, false or auto
  },
  "source" : "[some multi-line code]",
  "outputs": [{
      # list of output dicts (described below)
      "output_type": "stream",
      ...
  }],
}
```

### Code cell outputs

- A code cell can have a variety of outputs (stream data or rich mime-type output). 
- These correspond to messages produced as a result of executing the cell.

```JS
{
  "output_type": "stream",
  "name": "stdout",
  # or stderr "text": "[multiline stream text]",
}
```

- Rich display outputs, as created by `display_data` messages, contain data keyed by mime-type. 
  - This is often called a mime-bundle, and shows up in various locations in the notebook format and message spec.
  - mime-types are used for keys, instead of a combination of short names (text) and mime-types, and are stored in a data key, rather than the top-level. i.e. output.data['image/png'] instead of output.png.

```JSON

{
  "output_type" : "display_data",
  "data" : {
    "text/plain" : "[multiline text data]",
    "image/png": "[base64-encoded-multiline-png-data]",
    "application/json": {
      # JSON data is included as-is
      "key1": "data",
      "key2": ["some", "values"],
      "key3": {"more": "data"}
    },
    "application/vnd.exampleorg.type+json": {
      # JSON data, included as-is, when the mime-type key ends in +json
      "key1": "data",
      "key2": ["some", "values"],
      "key3": {"more": "data"}
    }
  },
  "metadata" : {
    "image/png": {
      "width": 640,
      "height": 480,
    },
  },
}
```

- Results of executing a cell (as created by `displayhook` in Python) are stored in `execute_result` outputs. 
  - `execute_result` outputs are identical to `display_data`, adding only a `execution_count` field, which must be an integer.

```JSON

{
  "output_type" : "execute_result",
  "execution_count": 42,
  "data" : {
    "text/plain" : "[multiline text data]",
    "image/png": "[base64-encoded-multiline-png-data]",
    "application/json": {
      # JSON data is included as-is
      "json": "data",
    },
  },
  "metadata" : {
    "image/png": {
      "width": 640,
      "height": 480,
    },
  },
}
```

- Failed execution may show a traceback

```JSON
{
  "output_type": "error",
  "ename": "str",  # Exception name
  "evalue": "str",  # Exception value

  # The traceback will contain a list of frames, represented each as a string.
  "traceback": ["list"],
}
```

### Raw NBConvert cells

- A raw cell is defined as content that should be included unmodified in nbconvert output. 
  - For example, this cell could include raw LaTeX for nbconvert to pdf via latex, or restructured text for use in Sphinx documentation.
- The notebook authoring environment does not render raw cells.
- The only logic in a raw cell is the `format` metadata field. 
  - If defined, it specifies which nbconvert output format is the intended target for the raw cell. 
  - When outputting to any other format, the raw cell’s contents will be excluded. 
  - In the default case when this value is `undefined`, a raw cell’s contents will be included in any nbconvert output, regardless of format.

```JSON
{
  "cell_type" : "raw",
  "metadata" : {
    # the mime-type of the target nbconvert format.
    # nbconvert to formats other than this will exclude this cell.
    "format" : "mime/type"
  },
  "source" : "[some nbformat output text]"
}
```

### Cell attachments

- Markdown and raw cells can have a number of attachments, typically inline images that can be referenced in the markdown content of a cell.

```JSON

{
  "cell_type" : "markdown",
  "metadata" : {},
  "source" : ["Here is an *inline* image 

![inline image](attachment:test.png)

 "],
  "attachments" : {
    "test.png": {
        "image/png" : "base64-encoded-png-data"
    }
  }
}
```

### Metadata

- Metadata is a place that you can put arbitrary JSONable information about your notebook, cell, or output. 
  - Because it is a shared namespace, any custom metadata should use a sufficiently unique namespace
- Metadata fields officially defined for Jupyter notebooks are listed here:
- #### Notebook metadata
- kernelspec
- authors

- #### Cell metadata
- collapsed
- scrolled
- deletable
- editable
- format
- name
- tags
- jupyter
  - source_hidden
  - outputs_hidden
- execution
  - iopub.status.busy
  - iopub.status.idle
  - shell.execute_reply
  - iopub.execute_input

- #### Output metadata
- isolated
  - Whether the output should be isolated into an iframe

### Backward-compatible changes

- As of nbformat 4.x, backward-compatible changes include:
  - new fields in any dictionary (notebook, cell, output, metadata, etc.)
  - new cell types
  - new output types
- New cell or output types will not be rendered in versions that do not recognize them, but they will be preserved.

- [Changes in nbformat](https://nbformat.readthedocs.io/en/latest/changelog.html)

## [Supported markup formats](https://nbformat.readthedocs.io/en/latest/markup.html)

- The Jupyter Notebook format supports Markdown in text cells.
- Most Jupyter Notebook interfaces use the [marked.js](https://marked.js.org/) JavaScript library for rendering markdown.
- This supports markdown in the following markdown flavors:
  - CommonMark
  - GitHub Flavored Markdown
  - as the Marked.js specification changes, so to will the behavior of Markdown in many notebook interfaces.
- There are a few extra modifications that Jupyter interfaces tend to use for rendering markdown. 
  - Specifically, they automatically render mathematical equations using MathJax.

## [JupyterLab](https://jupyterlab.readthedocs.io/en/latest/getting_started/overview.html)

- JupyterLab is the next-generation web-based user interface for Project Jupyter. 
- JupyterLab enables you to work with documents and activities such as Jupyter notebooks, text editors, terminals, and custom components in a flexible, integrated, and extensible manner.
- You can arrange multiple documents and activities side by side in the work area using tabs and splitters
- JupyterLab also offers a unified model for viewing and handling data formats. 
  - JupyterLab understands many file formats (images, CSV, JSON, Markdown, PDF, Vega, Vega-Lite, etc.) 
  - and can also display rich kernel output in these formats
- JupyterLab is served from the same server and uses the same notebook document format as the classic Jupyter Notebook.

- JupyterLab provides flexible building blocks for interactive, exploratory computing. 
- While JupyterLab has many features found in traditional integrated development environments (IDEs), it remains __focused on interactive, exploratory computing__.
- The JupyterLab interface consists of a main work area containing tabs of documents and activities, a collapsible left sidebar, and a menu bar.
- JupyterLab sessions always reside in a workspace. 
  - Workspaces contain the state of JupyterLab: the files that are currently open, the layout of the application areas and tabs, etc. 
  - Workspaces can be saved on the server with named workspace URLs.
