---
title: lib-notb-jupyter-docs
tags: [docs, jupyter]
created: 2024-06-30T03:27:11.916Z
modified: 2024-06-30T03:27:25.387Z
---

# lib-notb-jupyter-docs

# guide

- [Project Jupyter](https://jupyter.org/)
  - Project Jupyter exists to develop open-source software, open-standards, and services for interactive computing across dozens of programming languages.

- [The Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html)
# docs-jupyterlab
- [Jupyter and the future of IPython — IPython](https://ipython.org/)
  - IPython 3.x was the last monolithic release of IPython, containing the notebook server, qtconsole, etc. 
  - As of IPython 4.0, the language-agnostic parts of the project: the notebook format, message protocol, qtconsole, notebook web application, etc. have moved to new projects under the name Jupyter. 
  - IPython itself is focused on interactive Python, part of which is providing a Python kernel for Jupyter.

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

## extensions

- [Unofficial Jupyter Notebook Extensions](https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/)
  - https://github.com/ipython-contrib/jupyter_contrib_nbextensions
    - [jupyter_contrib_nbextenions appears to be incompatible with Jupyter Notebook v7](https://github.com/ipython-contrib/jupyter_contrib_nbextensions/issues/1647)
- [Extending the Notebook — Jupyter Notebook 7.1.0](https://jupyter-notebook.readthedocs.io/en/stable/extending/index.html)
  - ⚠️ Please note that the extension system for Notebook 7 is radically different from the one used in Notebook 6.5.x and earlier.
  - With Notebook 7 being developed on top of JupyterLab and Jupyter Server, the frontend extension system is now based on the same extension system used by JupyterLab.
# docs-jupyterhub

- 
- 
- 
- 

## [Institutional FAQ — JupyterHub documentation](https://jupyterhub.readthedocs.io/en/stable/faq/institutional-faq.html)

- the core JupyterHub application recently reached 1.0 status, and is considered stable and performant for most institutions
- JupyterHub has been used at-scale for large pools of users, as well as complex and high-performance computing

- For interactive computing sessions, JupyterHub controls computational resources via a spawner. 
  - Spawners define how a new user session is created, and are customized for particular kinds of infrastructure.

- JupyterHub works well at both a small scale (e.g., a single VM or machine) as well as a high scale (e.g., a scalable Kubernetes cluster).
  - The scalability of JupyterHub largely depends on the infrastructure on which it is deployed.

- For JupyterHubs that are deployed in a containerized environment (e.g., Kubernetes), it is possible to configure the JupyterHub to be fairly resistant to failures in the system.

- Jupyter is a polyglot project, and there are over 40 community-provided kernels for a variety of languages (the most common being Python, Julia, and R).

## 🐳 [Zero to JupyterHub with Kubernetes ](https://z2jh.jupyter.org/en/stable/)

- 
- 
- 
- 

- JupyterHub services (not to be confused with Kubernetes Service objects) are processes that interact with the JupyterHub API. nbgrader and culling idle Notebooks are examples of production services
  - Services can be run externally from the Hub, meaning they are started and stopped independently of the Hub and must know about things like their Hub authentication token on their own. 
  - Alternatively, a service can be Hub-managed, where the Hub starts and stops the process and passes key information to the service via environment variables.

- [The JupyterHub Architecture ](https://z2jh.jupyter.org/en/stable/administrator/architecture.html)
  - Major releases of Z2JH may include a major release of JupyterHub that requires an upgrade of the database schema. 
  - If you are using the default database provider (SQLite), then the required db upgrades will be performed automatically when you do a helm upgrade. 
  - A backup of the old database is automatically created on the hub volume.

- [FAQ ](https://z2jh.jupyter.org/en/stable/administrator/troubleshooting.html)
- I thought I had deleted my cloud resources, but they still show up. Why?
  - You probably deleted the specific nodes, but not the Kubernetes cluster that was controlling those nodes. 
  - Kubernetes is designed to make sure that a specific set of resources is available at all times. 
  - This means that if you only delete the nodes, but not the Kubernetes instance, then it will detect the loss of computers and will create two new nodes to compensate

- 
- 
- 

# more
