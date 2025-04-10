---
title: lang-python-toolchain-devtools
tags: [devtools, python, toolchain]
created: 2025-04-09T02:50:13.470Z
modified: 2025-04-09T02:50:35.187Z
---

# lang-python-toolchain-devtools

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-pkg/pip/uv
- ## 

- ## 

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
# discuss
- ## 

- ## 

- ## 
