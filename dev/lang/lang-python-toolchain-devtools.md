---
title: lang-python-toolchain-devtools
tags: [devtools, python, toolchain]
created: 2025-04-09T02:50:13.470Z
modified: 2025-04-09T02:50:35.187Z
---

# lang-python-toolchain-devtools

# guide

# cli-xp

```sh
# Use as the default Python version, python3, and python executables are also installed.
uv python install --default 3.13 
```

# discuss-stars
- ## 

- ## 

- ## 
# discuss-pkg/pip/uv
- ## 

- ## 

- ## 

- ## 💡 [uv-managed python installed into .local/bin can't be used with venv module · Issue · astral-sh/uv _202411](https://github.com/astral-sh/uv/issues/8821)
  - `python3.12 -m venv` fails to create a virtual environment.
  - ModuleNotFoundError: No module named 'encodings'

- this works for me
  - might be better than using ls -1 which may not work if you have multiple python interpreter

```sh
export PATH=$(dirname $(realpath $(which python))):$PATH
```

- ## what's uv's equivalent to `pip install diff_cover`

- uv tool install diff-cover
  - This will fetch diff-cover, put its executable on your PATH, and isolate it from your project’s venv 

- ## [How to add requirements.txt to uv environment - Stack Overflow](https://stackoverflow.com/questions/79344035/how-to-add-requirements-txt-to-uv-environment)

```sh

uv pip install -r requirements.txt

# also add the requirements to the project's pyproject.toml
uv add -r requirements.txt

# install into the system Python environment.
uv pip install --system
```

- ## 🆚 [What's the difference between `uv pip install` and `uv add` · Issue #9219 · astral-sh/uv _202411](https://github.com/astral-sh/uv/issues/9219)
- The `uv pip` APIs are meant to resemble the pip CLI. 
  - uv add, uv run, uv sync, and uv lock are what we call the "project APIs". These are "higher-level"
- `pip install` will only install into its own environment, `uv pip install` can target other environments.
  - `uv run script.py` will activate a virtual environment if necessary, and read PEP 723 inline metadata or sync your project if necessary, then call `python script.py` — the latter just uses your current environment as-is.

- ## [The creators of ruff and uv are building a new static type checker for Python : r/Python _202501](https://www.reddit.com/r/Python/comments/1idk4ko/the_creators_of_ruff_and_uv_are_building_a_new/)
- Free me from pylance please
  - pyright or based-pyright

- Hopefully, this will lead to a language server. A good one.

- Am I the only one who thinks it should be part of Python itself, not a 3rd party lib?
  - I prefer that Astral's type checker be maintained OUTside the processes for Python core. Rough summary: the costs of coordination of the two pieces look to me larger than the benefit of a more inclusive core.

- Like mypy but fast? Sign me up!
  - Mypy will never be in-sync with your IDE so it’s a pain.

- poetry can't do python version management.
- uv can't replace poetry. What do you feel is missing?
  - Dependabot

- ## [My take on UV and Ruff _202501](https://www.jujens.eu/posts/en/2025/Jan/25/uv-and-ruff/)
  - these tools are under very active development and thus change quickly. The drawbacks listed here may not be a think any more when you’ll read it.
- Ruff
  - ruff the linting tool to unite them all, especially formatter.
  - It’s main selling point is: it’s blazing fast.
  - it will also replace type checkers one day with a much faster alternative.
  - The only issue I see is: ruff doesn’t yet support plugins. 
- uv
  - uv is a new package manager. It can replace pip and tools like poetry
  - It supports dependencies groups and lock files. Everything will be into your pyproject.toml file following the latest PEP. 
  - It can also replace pipx to install and run Python commands. 
  - Even better, you can add dependencies to your script and let uv create a venv and run the script in it with all its dependencies automatically
  - Once again, with uv you don’t need anything else to run Python scripts and projects!

# discuss-compiler
- ## 

- ## 

- ## 

- ## 

- ## 🧩 What if you could get 37x faster Python with one line of code?
- https://x.com/KhuyenTran16/status/2002031397330923845
  - Slow Python functions in large codebases are painful to optimize. You might try Numba or Cython, 
  - but Numba only works for numerical code with NumPy arrays.
  - You might try Cython, but it needs .pyx files, variable type annotations, and build setup. That's hours of refactoring before you see any speedup.
  - Codon solves this with a single @codon .jit decorator that compiles your Python to machine code.
  - https://github.com/exaloop/codon /apache2/python/cpp

- Yeah Codon has been my goto tool when I need to quickly speedup python, most of the time it's good enough..gets you 80% the performance. But to really squeeze every drop of performance, i always revert to C/Zig ~ the last 20%.

- Just build a C++ Python module using pybind11.
- Or could just do rust. If you squint, it can be pythonic.

- Maybe just don't use Python?
# discuss-lsp
- ## 

- ## 

- ## Announcing the Beta release of ty: an extremely fast type checker and language server for Python, written in Rust. _202512
- https://x.com/charliermarsh/status/2001038023434047623
  - We now use ty exclusively in our own projects and are ready to recommend it to motivated users.
  - 10x, 50x, even 100x faster than existing type checkers and LSPs.
  - ty was designed from the ground up to power a language server. The entire ty architecture is built around "incrementality".
  - ty also includes a best-in-class diagnostic system, inspired by the Rust compiler's own world-class error messages.
  - we're targeting a Stable release next year, with the gap between Beta and Stable largely focusing on: stability and bug fixes
  - On a longer time horizon, though, ty will power semantic capabilities across the Astral toolchain: dead code elimination, unused dependency detection, SemVer-compatible upgrade enforcement, CVE reachability analysis, type-aware linting, and more.

- I previously tried ty, but it gave me a lot of false positives, so I temporarily used Pyrefly. I then started using Zuban, which I find to be a reasonable library. Could you please include this type checker in your benchmarks?

- next up python runtime in rust
  - Rustpython exist but the performance is not better and still have bugs

- It looks interesting but I wasn't able to use it with Django. Has that changed recently? The idea of a near-instant type checking sounds wonderful

- it's great, but on Zed it doesn't seem to be showing any completions/suggestions.

- need pyright alternative in rust
# discuss
- ## 

- ## 

- ## 

- ## I really wish Python imports were lazy and would pull bindings in like ES6 does. 
- https://x.com/mitsuhiko/status/1928436437621293392
  - It would also solve so many issues with typing now which greatly encourage circular imports.
  - When you "from foo import bar" you look up "bar" in that module's scope at import time and place it in the current module's global scope. The improved approach is to pull in a binding and to only resolve that binding when someone looks it up for the first time.

- ES imports not being lazy by default was a huge oversight(失察; 忽略). I expect import defer will become the default soon enough.

- in langchain, We had to do stuff like this all over the place
