---
title: toc-repos-lang-python
tags: [lang, python, toc]
created: 2025-02-26T15:03:52.334Z
modified: 2025-02-26T15:04:15.883Z
---

# toc-repos-lang-python

# guide

# popular
- https://github.com/pallets/flask
  - /52.2kStar/BSD/202009
  - Python micro framework for building web applications.
- https://github.com/dpgaspar/Flask-AppBuilder
  - /3kStar/BSD/202009
  - rapid application development framework, built on top of Flask

- https://github.com/django/django
  - The Web framework for perfectionists with deadlines.
  - [Modern JavaScript for Django developers | Hacker News _202501](https://news.ycombinator.com/item?id=42711387)

- https://github.com/langgenius/dify /82.5kStar/apache2/202503/python
  - https://dify.ai/
  - Dify is an open-source LLM app development platform
  - combines AI workflow, RAG pipeline, agent capabilities, model management, observability features and more

- https://github.com/keras-team/keras
  - /49.9kStar/MIT/202009
  - Deep Learning for humans

- https://github.com/scrapy/scrapy
  - a fast high-level web crawling & scraping framework for Python.

- https://github.com/ansible/ansible
  - IT automation platform that makes your applications and systems easier to deploy
# starter/template
- https://github.com/roboflow/template-python /202210/python
  - A template repo holding our common setup for a python project.
  - make `check_code_quality` to check code quality (PEP8 basically)
# fastapi
- https://github.com/fastapi/full-stack-fastapi-template /37.1kStar/MIT/202508/python/ts
  - Full stack, modern web application template. 
  - fastapi, SQLModel, pydantic
  - react, chakra-ui
  - Tests with Pytest.
  - [How to use Sqlite instead Postgresql _202403](https://github.com/fastapi/full-stack-fastapi-template/discussions/1132)

- https://github.com/adr1enbe4udou1n/fastapi-realworld-example-app /202504/PostgreSQL
  - https://fastapirealworld.okami101.io/api
  - built with FastAPI including CRUD operations, authentication, routing, pagination, and more. Using the very last SQL Alchemy 2.0
  - Validate API with Newman
  - fastapi, alembic, pydantic, requests, httpx, sqlalchemy2, psycopg

- https://github.com/borys25ol/fastapi-realworld-backend /202412/python
  - A real-world backend application (API) using Python, FastAPI and SQLAlchemy
  - PostgreSQL, Pytest

- https://github.com/nightriddler/fastapi_realworld /202201/python/postgresql
  - Implementation for RealWorld project using FastAPI and SQLAlchemy.
  - fastapi, pydantic, sqlalchemy, alembic, asyncpg, asyncio, aioredis, pytest, httpx

- https://github.com/nsidnev/fastapi-realworld-example-app /MIT/202202/python/archived
  - Backend logic implementation for realworld with FastAPI
  - NOTE: This repository is not actively maintained because this example is quite complete and does its primary goal - passing Conduit testsuite.
  - PostgreSQL, sqlalchemy, poetry
  - All routes are available on /docs or /redoc paths with Swagger or ReDoc.
  - [Can you talk more about how you split queries between aiosql and pypika?](https://github.com/nsidnev/fastapi-realworld-example-app/issues/98)
    - At first I only used raw SQL strings in this project and it worked
    - But reading such code in github was not easy, and also some of these SQL string simply could not be read 
    - So, to fix the first issue, I used `aiosql`, which helped me move all static queries into separate files
    - But dynamic queries were still a problem, so I wanted to use `pypika` for that
  - Could you tell why you chose to work without an ORM?
    - At the time of this project writing, there was no good async ORM for python. The Tortoise-ORM was very young (and remains so), SQLAlchemy did not have support for async, orm from encode also had limitations (for example, m2m fields). 
    - I used to work with SQLAlchemy, and on this project I just wanted to try the other side of working with the database
  - Do you plan to refactor this repository with SQLAlchemy 1.4?
    - Sorry, but no. I'd like to keep current implementation for DB part.
  - 🍴 forks
  - https://github.com/DataDog/fastapi-realworld-example-app /202409
  - https://github.com/Mathieu2016/fastapi-realworld-example-app /202411/updateDeps
  - https://github.com/markqiu/fastapi-mongodb-realworld-example-app /202210
    - fastapi+mongodb
  - https://github.com/liamcoatman/fastapi-realworld-example-app /202401
    - 被改造用来sklearn
  - https://github.com/SourceryAI/fastapi-realworld-example-app /202207/simplify
# django

## django-fwk

- https://github.com/vitalik/django-ninja /8.7kstar/MIT/202511/python
  - https://django-ninja.dev/
  - a web framework for building APIs with Django and Python 3.6+ type hints.
  - Very high performance thanks to Pydantic and async support.
  - Standards-based: Based on the open standards for APIs: OpenAPI (previously known as Swagger) and JSON Schema.
  - Django friendly: (obviously) has good integration with the Django core and ORM.
  - https://github.com/c4ffein/realworld-django-ninja /MIT/202408

## django-apps

- https://github.com/yoonge/conduit-drf /MIT/202406/python
  - Exemplary back-end realworld application (called Conduit) in Python, built with Django + DRF + MySQL + MySQLClient + SimpleJWT, managed by PDM.
  - https://github.com/yoonge/conduit-react
    - Exemplary front-end realworld application (called Conduit) in TypeScript, built with Axios + Hox + React + react-bootstrap + react-router-dom + Vditor, managed by pnpm.

- https://github.com/Sean-Miningah/realWorld-DjangoRestFramework /MIT/202412/python/js
  - uses django rest framework to create a backend service for the blog.
# flask
- https://github.com/gothinkster/flask-realworld-example-app /MIT/201909/archived
  - real world JSON API built with Flask 
  - 🍴 forks
  - https://github.com/DataDog/flask-realworld-example-app /MIT/202412
  - https://github.com/deepak010789/realworld-be-app /202210
    - Added healthcheck api
  - https://github.com/authzed/flask-realworld-example-app /202104
    - forked from the RealWorld sample apps and includes modifications that demonstrate adding permissions using Authzed.
  - https://github.com/peterclemenko/flask-realworld-example-app-dockerized /202212
  - https://github.com/ilona-simonnet/flask-realworld-example-app /202107/updateDeps
  - https://github.com/SimonCao1207/flask-realworld-example-app /202501/updateDeps
  - https://github.com/MetaCringer/flask-realworld-example-app /202402/ci
  - https://github.com/ericyame/flask-realworld-example-app /202011

- https://github.com/Willis0826/flask-realworld-example-app-ci-cd /MIT/202302/inactive
  - 介紹如何透過 GitLab CI，可以建置一個具有 Test、Pack、Cluster、Deploy 四個階段的 Pipeline 來進行持續整合與部屬(CI/CD)
# more
