---
title: lang-python
tags: [lang, python]
created: 2019-06-09T05:36:34.221Z
modified: 2020-07-14T09:27:30.503Z
---

# lang-python

# guide 🐍

- classic-examples-python
  - tips: 数据与ai计算的主力语言，也能快速开发业务
  - editor: lasuite-docs, jupyter(framework)
  - ai: 🌹 langgraph, comfyui, mlx
  - data: superset
  - devops: airflow, posthog
  - crdt
  - git-like
  - apps: docling
  - more: json-parser, tree

- tutorials 🧑‍🏫
  - [Python Cheatsheet](https://www.pythoncheatsheet.org/cheatsheet/basics)
  - https://github.com/gto76/python-cheatsheet

- who is using #python
  - 国内: 
  - .

- python-versions
  - [Status of Python versions](https://devguide.python.org/versions/)
  - [Download Python | Python.org](https://www.python.org/downloads/)
  - https://github.com/pyenv/pyenv

- resources-python
  - [Built-in Functions — Python documentation](https://docs.python.org/3/library/functions.html)
# python3

# python2

# python并发
- Python是通过一个全局解释器锁GIL（Global Interpreter Lock）来实现线程同步的。当Python程序只有单线程时，并不会启用GIL，而当用户创建了一个thread时，表示要使用多线程，Python解释器就会自动激活GIL，并创建所需要的上下文环境和数据结构
- 线程调度机制将会为线程分配GIL，获取到GIL的线程就能开始执行，而其他线程则必须等待。由于GIL的存在，Python的多线程性能十分低下，无法发挥多核CPU的优势，性能甚至不如单线程。因此如果你想用到多核CPU，一个建议是使用多进程
- 操作系统里面最重要的两个概念是进程和线程，Python中使用的是PyInterpreterState和PyThreadState来表示的
# python解释器
- Python程序运行的原理
  - 执行 `python demo.py` 后，将会启动Python解释器
  - python.exe解释器会将源码中的demo.py编译成一个字节码对象PyCodeObject
    - 将编译结果保存到了pyc文件中，这样下次就不用编译，直接加载到内存
    - .pyc文件是字节码对象(PyCodeObject)在本地磁盘上的表现形式
    - PyCodeObject对象包含了源码中的字符串、常量值以及通过语法解析后编译生成的字节码指令
  - demo.py被编译后，接下来就由Python解释器来执行字节码指令了
  - Python解释器会从编译得到的PyCodeObject对象中依次读入每一条字节码指令，并在当前的上下文环境中执行这条字节码指令

- 解释器
- gc
  - python虚拟机的垃圾回收使用的是引用计数法
    - 频繁更新引用计数会降低运行效率
    - 引用计数无法解决循环引用问题
# django
- who is using #django
  - zulip
  - lasuite-docs/drive/meet
  - authentik
  - openedx
  - baserow
  - plane
  - MrDoc, MaxKB, fiduswriter
  - apps: librephotos, django-helpdesk
  - fwk: django-eav2, wagtail-cms

- resources
  - [django-admin and manage.py commands](https://docs.djangoproject.com/en/5.2/ref/django-admin/)

## docs-django

- [Quick install guide | Django documentation](https://docs.djangoproject.com/en/5.2/intro/install/)
  - Django is a high-level Python web framework that encourages rapid development
  - [Django topics](https://docs.djangoproject.com/en/5.2/topics/)
- 🌰 [Django documentation contents | tutorial](https://docs.djangoproject.com/en/5.2/contents/)
  - tutorial: app-structure, db-crud, view-template, view-generic

### QuerySet

- To represent database-table data in Python objects, Django uses an intuitive system: A model class represents a database table, and an instance of that class represents a particular record in the database table.

- A `QuerySet` represents a collection of objects from your database. 
  - It can have zero, one or many filters. Filters narrow down the query results based on the given parameters. 
  - In SQL terms, a QuerySet equates to a `SELECT` statement, and a filter is a limiting clause such as `WHERE` or `LIMIT`.
- You get a QuerySet by using your model’s Manager. Each model has at least one Manager, and it’s called `objects` by default.
  - A Manager is accessible only via model classes, rather than from model instances, to enforce a separation between “table-level” operations and “record-level” operations.

- Each time you refine a QuerySet, you get a brand-new QuerySet that is in no way bound to the previous QuerySet. 
  - Each refinement creates a separate and distinct QuerySet that can be stored, used and reused.
  - The initial QuerySet (q1) is unaffected by the refinement process.

- QuerySet objects are lazy – the act of creating a QuerySet doesn’t involve any database activity. You can stack filters together all day long, and Django won’t actually run the query until the QuerySet is evaluated. 

- If you know there is only one object that matches your query, you can use the `get()` method on a Manager which returns the object directly
  - Note that there is a difference between using get(), and using filter() with a slice of [0]. If there are no results that match the query,  `get()` will raise a `DoesNotExist` exception. 
  - Similarly, Django will complain if more than one item matches the get() query

- Some methods on managers and querysets - like get() and first() - force execution of the queryset and are blocking. 
  - Methods that return new querysets: These are the non-blocking ones, and don’t have asynchronous versions. You’re free to use these in any situation, though read the notes on defer() and only() before you use them.
  - Methods that do not return querysets: These are the blocking ones, and have asynchronous versions - the asynchronous name for each is noted in its documentation, though our standard pattern is to add an a prefix.

- You can evaluate a QuerySet in the following ways:
  - Iteration. (for-in)
    - A QuerySet is iterable, and it executes its database query the first time you iterate over it. 
  - Slicing an unevaluated QuerySet usually returns another unevaluated QuerySet, but Django will execute the database query if you use the “step” parameter of slice syntax, and will return a list.
  - Pickling/Caching.
  - repr(). A QuerySet is evaluated when you call repr() on it. 
  - len(). A QuerySet is evaluated when you call len() on it.
  - list(). Force evaluation of a QuerySet by calling list() on it.
  - bool(). Testing a QuerySet in a boolean context, such as using bool(), or, and or an if statement, will cause the query to be executed
- If you pickle a QuerySet, this will force all the results to be loaded into memory prior to pickling.

- Transactions are not currently supported with asynchronous queries and updates. 
  - If you wish to use a transaction, we suggest you write your ORM code inside a separate, synchronous function and then call that using `sync_to_async`

- To compare two model instances, use the standard Python comparison operator, the double equals sign: ==. Behind the scenes, that compares the primary key values of two models.
  - If a model’s primary key isn’t called id, no problem. Comparisons will always use the primary key, whatever it’s called.

- When Django deletes an object, by default it emulates the behavior of the SQL constraint `ON DELETE CASCADE` – in other words, any objects which had foreign keys pointing at the object to be deleted will be deleted along with it.

- Instances of F() act as a reference to a model field within a query. These references can then be used in query filters to compare the values of two different fields on the same model instance.

- Keyword argument queries – in filter(), etc. – are “AND”ed together. If you need to execute more complex queries (for example, queries with OR statements), you can use Q objects.
  - Q objects can be combined using the &, |, and ^ operators. When an operator is used on two Q objects, it yields a new Q object.

- If you find yourself needing to write an SQL query that is too complex for Django’s database-mapper to handle, you can fall back on writing SQL by hand. 

- 
- 

### storage

- [Managing files | Django documentation | Django](https://docs.djangoproject.com/en/5.2/topics/files/)
  - [File storage API | Django documentation | Django](https://docs.djangoproject.com/en/5.2/ref/files/storage/)
- By default, Django stores files locally, using the `MEDIA_ROOT` and `MEDIA_URL` settings. 
- Internally, Django uses a django.core.files. File instance any time it needs to represent a file.
- Django delegates decisions about how and where to store files to a file storage system. 
  - Django’s default file storage is `django.core.files.storage.FileSystemStorage`.

- [Amazon S3 - django-storages 1.14.6 documentation](https://django-storages.readthedocs.io/en/latest/backends/amazon-S3.html)
  - The backend is based on the `boto3` library which must be installed
- [S3 - Boto3 1.39.14 documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html)
  - use the AWS SDK for Python (Boto3) to create, configure, and manage AWS services, such as Amazon Elastic Compute Cloud (Amazon EC2) and Amazon Simple Storage Service (Amazon S3).

- 
- 
- 
- 

## docs-drf

- [Django REST framework](https://www.django-rest-framework.org/)
  - optional pkgs: PyYAML, uritemplate, markdown, Pygments, django-filter, django-guardian
  - Authentication policies including packages for OAuth1a and OAuth2.
  - Serialization that supports both ORM and non-ORM data sources.
  - just use regular function-based views if you don't need the more powerful features

- A serializer class is very similar to a Django `Form` class, and includes similar validation flags on the various fields, such as required, max_length and default.
  - We can also serialize querysets instead of model instances.

- REST framework introduces a `Request` object that extends the regular `HttpRequest`, and provides more flexible request parsing. The core functionality of the Request object is the `request.data` attribute, which is similar to request. POST, but more useful for working with Web APIs.

- One of the big wins of using class-based views is that it allows us to easily compose reusable bits of behavior.

- IsAuthenticatedOrReadOnly, which will ensure that authenticated requests get read-write access, and unauthenticated requests get read-only access.

- `ViewSet` classes are almost the same thing as `View` classes, except that they provide operations such as `retrieve, or update`, and not method handlers such as `get or put`.

- Because we're using ViewSet classes rather than View classes, we actually don't need to design the URL conf ourselves. The conventions for wiring up resources into views and urls can be handled automatically, using a Router class. All we need to do is register the appropriate view sets with a router, and let it do the rest.

- 

## more-django
