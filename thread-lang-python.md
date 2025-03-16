---
title: thread-lang-python
tags: [python, thread]
created: 2024-02-14T12:34:29.423Z
modified: 2024-02-14T12:35:31.547Z
---

# thread-lang-python

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## Python 3.13 is out and you can now disable the infamous GIL 
- https://x.com/arpit_bhayani/status/1845816870458339499
  - It is a free-threaded execution which means Python can now fully utilize all available CPU cores. 
  - By the way, Python 3.13 also has a pretty awesome JIT compiler, which may speed up some programs.

- I first came across GIL when I was trying multithreaded matrix multiplication and I noticed that there wasn't any improvement from single-threaded one. Will try this again in python 3.13 so see the changes

- Parallelism comes with its own caveats, so we need to be careful while using it.
# discuss-web-fwk
- ## 

- ## 

- ## 经我考虑后，决定在新项目上采用Django和PostgreSQL技术栈。
- https://x.com/1oogle/status/1844008735838257644
  - 虽然最开始我也想继续沿用FastAPI，但是考虑到和同事之间协作顺利、ORM与DTO的转换、第三方生态库以及分包开发的问题，最后还是用敲定用Django这最为成熟的方案

- 只开发rest api吗还是前后端不分离的（比如要后端通过template engine渲染页面）？如果只是前者，感觉Django有点重，如果是后者或者后者+rest api，我觉得Django非常适合。个人觉得Django的orm用的不是很顺手，比如laravel的eloquent好用

- Django的用户权限代码生成做得不错，很适合CMS，不过关键在于app做好部署怎么保证large scale吧

- 要写视图的话用 jinja2 别用 django 那自带的残废模板

- 还需要加上redis做缓存。注意要优化所有的全表搜索，否则很容易就把服务器搞死了

- Django + DRF，现在已经全面支持async了，建议直接上asgi，做一套boilerplate到处都能用
  - 其实说法不对，Django也没完全支持，ORM都还是通过 sync_to_async这种魔改的方式来强行支持……至于DRF, 作者现在心思都放在 httpx 以及 Starlette 上了, 所以DRF仍不支持Async，只能用第三方包adrf来支持，但这个包能否在生产上稳定使用仍未知

- ## [Which Python Web Framework to Choose for 2023: Django, Flask, FastAPI or Tornado? | by PrimerPy | Medium _202302](https://primerpy.medium.com/which-python-web-framework-to-choose-for-2023-django-flask-fastapi-or-tornado-9d05860adfe3)
- If you’re building a traditional, monolithic web application with a relational database, Django might be the best choice.
- If you’re building a small, simple API, Flask might be a good option.
- FastAPI is a relatively new framework that’s designed for building high-performance APIs. It’s based on Starlette for the web parts, and Pydantic for the data parts. It is a great option if you want to build fast and modern APIs.
- Tornado is a mature, non-blocking web framework that’s well suited to building real-time applications, such as chat applications and online games.

# discuss-toolchain-python
- ## 

- ## 

- ## uv still has a bunch of issues.
- https://x.com/HanchungLee/status/1900942356377202762
  - it’s not pip
  - lack of ide and coding agent support
  - venv created by uv cant be used without uv
  - poor documentation. there’s no playbook on how to migrate to it. information scattered around like a changelog.
- If you’re dealing with complex dependencies, like stuff in requirements.txt that comes directly from GitHub, or certain things involving CUDA libraries, then uv has some rough edges. But for many projects it “just works” at this point and it’s wildly faster and very nice to use.
- The third one is not true, you can do uv pip install pip and then pip install whatever didn't work before. I'm doing this basically every other day
- can't you just run `source ./venv/bin/activate` like normal?
  - you can. but that venv does not have pip and will use global. so a pip install will mess up your global python environment.

# discuss
- ## 

- ## 

- ## 

- ## 说一说将 MarkItDown 运行在浏览器中只有中国大陆程序员会遇到的一个问题
- https://x.com/miantiao_me/status/1869366259818885429
  - Pyodide 是一个在 WebAssembly 中运行 Python 的工具库，使用 Micropip 通过 PyPI 来安装包。
  - PyPI 在中国大陆是无法正常访问的，但是有许多的 Mirror。清华、阿里云、腾讯云、华为云等不少网站都提供了镜像。这些镜像除了清华的 tuna，其他都不支持 JSON-based Simple API for Python (PEP 691)。
  - 由于 WebAssembly 在浏览器内运行需要跨域和 PEP 691，但是清华的 tuna 又不支持 CORS 跨域。所以在中国大陆可能没有 Micropip 可用的 PyPI 镜像。
  - 基于这个背景，使用 Cloudflare 搭建了一个支持 PEP691 和 CORS 的 Mirror。

- 这种算是通过workers进行反向代理吧…新政策禁止用户通过CF的服务创建代理…存在违反使用政策被封禁的担忧

- ## Python 届的三大 Web Frameworks：Flask、Django 和 FastAPI，居然是三足鼎立之势。
- https://x.com/tualatrix/status/1869364341935591858
  - 现在只需要写 API 的场景越来越多了

- 多年 aiohttp 用户飘过
- 没想到 FastAPI 涨这么快

- ## Python这个基于路径导入就是一坨XXX，只能搞黑魔法。 因为根本不可能同时让Jupyter notebook/vscode-python/命令行工具三个都满意，
- https://twitter.com/JXQNHZr1yUAj5Be/status/1786997922120204397
  - 如果你用复杂的项目配置(pyproject/src-layout)，那jupyter和命令行死给你看。 
  - 如果你用简单的项目结构，那就很难打包成一个可复用的项目。
- 自己写个environment management脚本把，每次使用时候，执行脚本设置相关的环境变量
  - 这样vscode-python没法检查你的python脚本（因为import有问题），这就是为啥我很反对去搞这个环境变量。。。当然一个简单的办法其实是把脚本搞进代码目录里，而不是另外开一个script文件夹。
- 有哪个语言不是基于路径的吗？
  - c，c++，c#，java
- 包也是路径，动态库也是路径

- python 没有make cmake 之类的东西

- ## Is Jinja2 still the king of the hill for Python templating engines?
- https://twitter.com/willmcgugan/status/1757724990160441764
- I love that jinja2 templates can contain basic logic and  be composed of subtemplates. And it certainly feels fast. What else do you need? I think it was one of your projects that made me realize that jinja is not just for web generation. Very powerful.
- It's certainly the one that I would consider. The only exception is that for Django projects I still use the Django templates.
