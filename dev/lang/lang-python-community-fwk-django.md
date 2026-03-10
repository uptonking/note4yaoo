---
title: lang-python-community-fwk-django
tags: [community, django, python]
created: 2026-03-05T19:31:46.524Z
modified: 2026-03-05T19:32:00.353Z
---

# lang-python-community-fwk-django

# guide

- pros
  - ?

- cons
  - ?

- features
  - ?

- tips
  - ?

- resources
  - ?
# discuss-stars
- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## 
# discuss-news
- ## 

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
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-examples/extensions 🌰
- ## 

- ## 

- ## [I built django-lumen — a Django app for visualizing Django models : r/django](https://www.reddit.com/r/django/comments/1roikva/i_built_djangolumen_a_django_app_for_visualizing/)
  - It renders an interactive ERD of all your project's models directly in the browser - no external diagram libraries, just vanilla JS + SVG generated on the fly from the live model registry.
  - https://codeberg.org/Lupus/django-lumen /NoDeps
- Have you looked at Graph models from Django extensions? https://django-extensions.readthedocs.io/en/latest/graph_models.html
  - I’ve used it for years, but building the Graphviz module is a pain on certain platforms. Plus, it ends up being just a static image anyway. My goal is to let anyone with admin access browse models more quickly while finally ditching that Graphviz dependency.

- How well does it work with larger systems? We have about 425 tables across many apps. One app has like 65 tables
- I have 700+ tables in a few dozen apps in my Django project. It's a project that manages the operations, billing, scheduling, maintenence, and more for utilities districts. Several of those are pghistory models for audit purposes.
- I just tried it on a project with ~300 tables. It was a bit of a visual mess, but I had no issues with performance.

- ## [Made My Django Admin Look 10x Better in One Step : r/django](https://www.reddit.com/r/django/comments/1rklfiz/made_my_django_admin_look_10x_better_in_one_step/)
  - https://github.com/unfoldadmin/django-unfold /MIT
  - I tried django-unfold while back and it took few minutes to get it running. No model changes, no weird hacks. Just install and use `ModelAdmin` from unfold instead of django. The admin instantly looked modern, and building a small dashboard on top was way easier than I expected.

- Well, no model changes….true, but yes, you’ll need to adapt Admin classes adding a mixin and if the project is mature enough, you’ll probably need to deal with some widgets, css classes and filters.
  - Anyway, I do agree, django-unfold is great and the look feels really modern. I had installed in several projects so far and I couldn’t be happier with it.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Thoughts on using django admin (with a good looking theme and restricted enough) as MVP ? : r/django](https://www.reddit.com/r/django/comments/1qtd4j6/thoughts_on_using_django_admin_with_a_good/)
- Just MVP? im using django admin with unfold as the main interface it looks good and has a lot of customization and if you know how to override things you are set for life

- Check https://github.com/SmartBase-SK/django-smartbase-admin it aims exactly at this simplifying object access permission setup. Has a bit of learning curve because of that but you will be able to run standard admin too for real admins.

- I've built many projects over the years that have handled hundreds of millions in revenue all managed through django admin.. i haven't had a project yet that needed more.. sure I guess it would be "nice" to spend all this time making some pretty admin dashboard.. but eh

- Django admin is more like graphical SQL Viewer/editor than real admin. You can use it that way, but still it is too low-level to be useful in many cases. For simple, mvp-like things you can use it, but in 99% cases this is a place to low-level fix things broken by admins by super admin too lazy to edit db directly 

- ## [Why doesn’t Django serve static files by default in production? : r/django](https://www.reddit.com/r/django/comments/1q3rn2y/why_doesnt_django_serve_static_files_by_default/)
- It's performance. Webservers like Nginx are dramatically faster than Django is at serving static files and they have lots of configuration options and other features for working with static files, all of which Django lacks. But they're also better at scalability and separation of concerns.
  - This. Most "real" webserver's will handle static files by using the kernel's sendfile system call. The kernel then reads the data from the file system and pipes it to the network device without the data ever touching the server process which saves a lot of (expensive) coping around of data.

- serving static files via a dynamic server is kinda a waste of resource. ngnix, apache, caddy, ... are too good at this task.

- first perfomance reason, second because in production, if your site has a lot of trafic, you are going to use a CDN anyway

- Lots of good comments saying why you should use nginx in production, but not one mentioned security and SSL.
  - You need a webserver like nginx to handle domains routing and certificates for https.
  - This can be done with Cloudflare and CF tunnels though. It's still good to have nginx behind it with fail2ban. 

- When deployig, django is used with a web server and a reverse proxy. This setup ha the benefeits of speed, scalibilty, security and much more. Your core django app should be mainly about logic, authentication and authorization (the last 2 can even be outsourced). Overall, its a really bad decision to even serve django in production with runserver.

- ## [Confused About Django Project Structure: Traditional vs Service–Repository — Which One Should I Use? : r/django _202512](https://www.reddit.com/r/django/comments/1prgz0j/confused_about_django_project_structure/)
  - I’m working on a Django project and I’m confused about which project structure is best to follow. I see multiple approaches: Traditional Django structure (models, views, urls, etc.) Service + Repository pattern Controller-based or layered structure I want to understand: When should I stick with the traditional Django approach? At what point does using services and repositories make sense? Is it over-engineering for small or medium projects? 

- Start with traditional Django structure. Enhance as needed.
  - You can add in repository pattern type stuff with managers. https://docs.djangoproject.com/en/6.0/topics/db/managers/ And if you need something outside that, nothing stopping you adding it later.
  - You can also add in services later as needed on a per module basis. I'd start with methods on the model until it gets unweildy.

- Follow the approach recommended by Django, focusing domain logic in the models. Logic that depends on the instance should reside in the model itself. When the logic does not involve a specific instance, it can be placed in the Manager. For more specific, reusable, and chainable queries, it is ideal to create custom QuerySets. In practice, Managers and QuerySets already fulfill the role of repository in Django, so there is no need for extra abstractions.

- Django or at least DRF already follows somewhat a very opinionated controller service repository pattern, the components are just named a bit differently. If you just have a general "service" file, it can grow extremely large so Django tries to break it down for you and ask you to just inject your classes in. 

- ## [Strategies for removing django-polymorphic from codebase : r/django](https://www.reddit.com/r/django/comments/1pmow0e/strategies_for_removing_djangopolymorphic_from/)
  - The codebase grew with polymorphic in place, but it is causing more headaches and testing nightmares than the little abstraction help it provides. Going about removing it from some rather central models, while keeping all data and transferring to inheriting from abstract base classes instead, has been veeeery painful to say the least.
  - The biggest issue is not being able to get database fixtures for tests to work because of content type mismatches.

- We've used factory-boy for creating test data. Works perfectly fine with polymorphic models. Also, the factory library can be used to created related data automatically. Also, tests can have just the data they need without everything else.
  - Anyways, if you need to use fixtures, use natural foreign keys
  - See natural keys and `dump data --natural-foreign` for more information.
  - While the polymorphic library isn't exactly using generic foreign keys, the tip about using natural foreign keys still applies.

- I've migrated some models to `django-model-utils` `InheritanceManager`. Mostly because I need to profetch relations that are not supported by django-polymorphic

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
