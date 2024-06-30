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
# discuss-web-fwk
- ## 

- ## 

- ## 

- ## [Which Python Web Framework to Choose for 2023: Django, Flask, FastAPI or Tornado? | by PrimerPy | Medium _202302](https://primerpy.medium.com/which-python-web-framework-to-choose-for-2023-django-flask-fastapi-or-tornado-9d05860adfe3)
- If you’re building a traditional, monolithic web application with a relational database, Django might be the best choice.
- If you’re building a small, simple API, Flask might be a good option.
- FastAPI is a relatively new framework that’s designed for building high-performance APIs. It’s based on Starlette for the web parts, and Pydantic for the data parts. It is a great option if you want to build fast and modern APIs.
- Tornado is a mature, non-blocking web framework that’s well suited to building real-time applications, such as chat applications and online games.

# discuss
- ## 

- ## 

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
