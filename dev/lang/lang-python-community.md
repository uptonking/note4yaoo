---
title: lang-python-community
tags: [community, python]
created: 2023-08-28T06:14:04.458Z
modified: 2023-08-28T06:14:28.873Z
---

# lang-python-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-django-stars
- ## 

- ## 

- ## 
# discuss-django-drf
- ## 

- ## 

- ## 

- ## [Sync Vs Async Views in DRF : r/django _202511](https://www.reddit.com/r/django/comments/1onfnyo/sync_vs_async_views_in_drf/)
  - I was recently doing a poc on whether we should or shouldn't try using the Async Views in our api. There is a flow where we have to call 3-4 internal APIs, one is called twice with different params, then that called another api which calls another api.
  - I tried doing a benchmarking test today. Made a view with time.sleep(15) for synchronous and asyncio.sleep(15) for Async view.
  - Used JMeter with users = 100, ramp up time = 1 and loop count = 50. Interesting result was that throughput of sync view and Async view were same, 6.6 per second.
  - Like even with python manage.py runserver, the sync apiview was behaving like Async.
  - To sate my curiosity, I wrote the same thing for a FastApi, and results were same.

- Did you use only manage.py runserver? Or you also tried to use daphine with asgi or uvicorn? If you only used manage.py runserver so definitely you'll get the same results because you still use the traditional way of how Django handles the requests which is dedication of a worker per request
  - I did three things -
  - Normal runserver for sync view
  - Another project, with unicorn for Async view
  - Same logic in fastApi.
  - I got same results for all 3.
  - I think I should maybe look into the memory usage by all and also the number requests to be more per second.
- I did a similar tests for my graphql api recently ust to compare sync and async calls. Adding some results for the same api query and mutations. Test is run with locust 100 users with 10 spawn rate:
  - Even tough the tests are not exactly identical, I decided to go with async for my needs. Hope this helps.

- You will need to use an async development server: https://docs.djangoproject.com/en/5.2/howto/deployment/asgi/daphne/
# discuss-django
- ## 

- ## 

- ## 🤼 [Seriously underrated Django feature: database fixtures : r/django](https://www.reddit.com/r/django/comments/1plqyjr/seriously_underrated_django_feature_fixtures/)
  - The reason for this is: it's exceptionally fast to populate the sqlite database with fixtures. It bypasses much of the ORM, resulting in much quicker database configuration. Also, you can create suites of fixtures that truly do model real-world information, and it makes testing a breeze. In particular, it makes test setup simple, because you simply affix the fixtures to the TestCase and you're off.
  - One (strong) recommendation: use natural keys. They make writing the fixtures a lot easier, because you don't have to contend with manually setting primary/foreign keys (ultimately, you'll have collisions and it sucks, and it's terribly unclear what foreign key "12" means).

- Have you tried the same test suite using factories instead? I suspect the end results won't be different and they avoid a lot of headaches when models change.
  - I'm referring to https://factoryboy.readthedocs.io/en/stable/ - there are other libraries but Factory Boy is the de facto standard.

- This is good and all but once your application grows it becomes a headache. Integration and mocking (although requiring more thought) is the way to go.

- ## [Forcing clients to use latest static assets served from S3 storage what are your strategies? : r/django](https://www.reddit.com/r/django/comments/1pggodf/forcing_clients_to_use_latest_static_assets/)
  - What techniques/strategies do you use to force clients to use the latest css and other changing static assets from S3 compatible storage?
  - I already separate assets with a development bucket and production bucket, but what is a good way to force clients to use the latest version in the production bucket instead of their cached version?

- The asset files should have their content hash in the name ie project.{xyz}.css Webpack has things like [contenthash] etc to automatically do it, look into documentation of your bundler.

- `<script source=my file.js?version=1> ` Pass it a random parameter instead. I use v for version.
  - Whenever you change this it will force a client to download new assets. So if I know file is updated I increment the version clients use

- ## [In which cases you use custom middlewares : r/djangolearning _202511](https://www.reddit.com/r/djangolearning/comments/1onq17b/in_which_cases_you_use_custom_middlewares/)
- You can add custom code in your middleware so you can add a condition to whether to do something or not do anything.

- Check the django-htmx package to see a real practical use case for custom middleware.

- We use it to active timezone to the users in order to return datetime correctly from the database, other uses case i found: authn, authz, audit logs, error handling, etc.

- ## 🆚 django-admin flush vs migrate
- flush
  - Deletes all data from the database but preserves the database schema (tables, columns, etc.).
  - Does NOT alter the database schema.
  - 修改过的schema不会回滚

- migrate
  - Synchronizes the database state with the current set of models and migrations.
# discuss-fwk-python
- ## 

- ## 

- ## 

- ## 

- ## [Fast API better option than Django? : r/Python _202509](https://www.reddit.com/r/Python/comments/1npercr/fast_api_better_option_than_django/)
  - because I come from Django, but as apps grow, especially with CRUDs, it's easier to use viewsets than to create each of the endpoints in FastAPI with their functions.

- So as someone who’ve worked on django apps before and then pushed for FastAPI. There are some cons and pros to both.
  - Django is like “apple”, a nice as all-in-one opinionated solution, whereas long as you stick within the wall garden most things just work. But at times it’s slow to adopt or makes counterintuitive design decisions you have to live it (I hate the Django orm, I had to untangle so many bad queries generated by it).
  - FastAPI is sort of more like “Linux”, where its bare bones and anytime you need something on top you have to evaluate different options, your choices are more open-ended. It really just does one thing, and one thing only which is provide a simple abstraction to handle http requests. The rest is up to you: orm choice, auth choice, design patterns etc
  - FastAPI does have some clear winners for a few things, like FastAPI+sqlalchemy+alembic+jinja2+Authlib+pydantic-settings (and maybe celery) gets you what most people use Django for (so around 60% of the core features we care about in Django).
- Most Django users will still want an admin/back of house (sqladmin or starlette-admin would be the advice here) and they might be a little annoyed they have to roll their own RBAC. 

- If you're expecting your product to be large and long-lived, I would use FastAPI. It will give you the modularity you need to adapt to any unforeseen requirement. Django will continuously fight you every step of the way. Rewriting is not a huge pain, but getting painted in a corner or using workarounds for framework limitations is horrible.

- The main advantage of FastAPI over Django is not async support, but its flexibility and intuitive design. It is much easier to pick up, whereas Django comes with a steep learning curve.

- remember that you can deal with application speed in more ways than just “django vs fastapi”. tuning your app server (gunicorn, unicorn), using caching (with redis or pure python), tuning your nginx, and scaling deployments
# discuss
- ## 

- ## 

- ## 

- ## Did you know that #Python supports chained comparison? 
- https://twitter.com/driscollis/status/1719731090750071245
  - It's only valuable for niche circumstances, but it's super handy!
  - if 60 < num_variable < 100

- ## Flask today is a different framework than the one I have created. 
- https://twitter.com/mitsuhiko/status/1719716779532931466
  - But that is in many ways what it should be. 
  - It took me many years to realize that projects are not just code and I did not know how to onboard people.

- ## What is wrong with “is” in Python
- https://twitter.com/clcoding/status/1718350871610708374
- “is” operator compares address of both variable and return True if they are pointing at same address, otherwise False
  - If number is between 0 to 256, then that variable will point at fixed address only irrespective of shallow copy, deep copy or separate variable.
  - If number is >256 then it’ll create new address if they are deep copied or created separately.
  - But for larger numbers like 257, "a is b" is False because they are stored in different places in memory.

- The behavior we are observing is due to a memory optimization in Python, which is specific to small integer objects. 
  - In Python, small integer objects (typically in the range -5 to 256) are cached and reused for memory efficiency. 
  - When you assign the same integer value to multiple variables within this range, they will refer to the same memory location, which is why `is` returns `True` in such cases. 
  - 👉🏻 This is an optimization mechanism known as "interning."

- ## 🧐 TIL python does not recreate default function params each function call
- https://twitter.com/ethanniser/status/1716612454568861903
- Yep if the param is mutable this issue happens sadly
- Yea that’s known and not fixed
- One of the most annoying known quirks of Python

- ## 你们现在是用什么来管理Python版本和库依赖的？_202310
- https://twitter.com/river_leaves/status/1710489478924783778
- docker+pip
- 对于单机运行环境，例如科研、个人开发环境来说，conda固然是不错的，我也会用。但是如果需要CI/CD，conda太重了，大，慢，并且配套的生态也不是为CI/CD准备的。
