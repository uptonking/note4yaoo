---
title: toc-lib-fwk-baas
tags: [baas, firebase, framework, toc]
created: 2021-05-25T09:40:21.484Z
modified: 2021-05-25T09:40:55.797Z
---

# toc-lib-fwk-baas

# guide

- 比较了parse、firebase、couchdb、kuzzle、remoteStorage、Hoodie
  - [How does Kinto compare to other solutions?](https://docs.kinto-storage.org/en/stable/faq.html)
# firebase-like
- supabase /41.1kStar/apache2/202211/ts
  - https://github.com/supabase/supabase
  - https://supabase.com/
  - an open source Firebase alternative.
  - Hosted Postgres Database
    - PostgREST is a web server that turns your PostgreSQL database directly into a RESTful API
  - Realtime subscriptions
    - Realtime is an Elixir server that allows you to listen to PostgreSQL inserts, updates, and deletes using websockets. 
  - Authentication and authorization
  - Auto-generated APIs
  - Dashboard

- appwrite /27.4kStar/BSD/202211/ts/php
  - https://github.com/appwrite/appwrite
  - https://appwrite.io/
  - Appwrite is an end-to-end backend server for Web, Mobile, Native, or Backend apps packaged as a set of Docker microservices. 

- https://github.com/javascriptdb/jsdb-server /js
  - https://javascriptdb.com/
  - The open source firebase alternative that uses SQLite.
  - Arrays and Objects operations read and write into your database. Magic.
  - JSDB is very much a work in progress, expect things to fail here and there, up and down.
    - When you use .filter to search over an array, we are not using indexes. 
  - https://github.com/javascriptdb/jsdb-sdk
  - https://github.com/javascriptdb/jsdb-react

- https://github.com/parse-community/parse-server
  - Parse Server works with the Express web application framework.

- https://github.com/eugeneware/firedup /201306/js/inactive
  - A node.js implementation of firebase based on leveldb/levelup.

- kuzzle /1.3kStar/apache2/202211/js
  - https://github.com/kuzzleio/kuzzle
  - https://kuzzle.io/
  - Kuzzle is a generic backend offering the basic building blocks common to every application.
  - API First: use a standardised multi-protocol API.
  - Realtime Notifications: use the pub/sub system or subscribe to database notifications.
  - User Management: login, logout and security rules are no more a burden.

- https://github.com/asheghi/NeoBase /202209/ts/inactive
  - The open source Firebase alternative
  - NeoBase is a hosted platform. You can sign up and start using NeoBase without installing anything. You can also self-host and develop locally.
  - 依赖 express、mongoose、vue

- https://github.com/asheghi/waterbase /202104/js
  - an attempt to create an alternative for CloudFlare realtime database, Cloud FireStore
  - add `Subscription` to Keystone.js CMS GraphQL api

- https://github.com/TheHadiAhmadi/minibase /202211/js
  - minimal (and slow) firebase alternative
 

- CoCreateJS /19Star/MIT/202212/js
  - https://github.com/CoCreate-app/CoCreateJS
  - https://cocreate.app/
  - A collaborative low code headless CMS and Javascript framework for building collaborative no code platforms, apps and UI
  - https://github.com/CoCreate-app/CoCreate-crud-client /202212/js
  - An useful CRUD api operate Create, read, update, delete with built in database. 
  - Can be used as a firebase alternative
 - https://github.com/CoCreate-app/CoCreateWS
    - Server Side for CoCreateJS. Containing websocket, crud, auth, server side rendering, and permission components.
  - https://github.com/CoCreate-app/CoCreate-admin
    - A No Code Admin, CRM, CMS, Website Builder platform. 
    - Powered by CoCreateJS to provide Realtime and Collaborative CRUD functionality.

- kinto /4.2kStar/apache2/202210/python
  - https://github.com/Kinto/kinto
  - http://docs.kinto-storage.org/
  - A generic JSON document store with sharing and synchronisation capabilities.
  - Backends: In-memory (development), PostgreSQL 9.5+ (production)

- https://github.com/pocketbase/pocketbase /go/svelte
  - PocketBase is an open source Go backend
  - embedded database (SQLite) with realtime subscriptions
  - built-in files and users management

- https://github.com/easycrud/easycrud
  - https://easycrud.org/
  - This project is aimed at providing a series of handy packages for the development of a typical CRUD web application.
  - The packages are work around a kind of schema written in JSON for database table.
# baas/backend-as-a-service
- https://github.com/lagonapp/lagon /rust/ts
  - Lagon is an open-source runtime and platform that allows developers to run TypeScript and JavaScript Serverless Functions close to users.
  - I've been building this fully open-source edge runtime and platform as an alternative to CF Workers & Deno Deploy for the past 10 months
# python-framework
- https://github.com/jam-py/jam-py /BSD/python/js
  - https://jam-py.com/
  - Jam.py is an object oriented, event driven framework with hierarchical structure, modular design and very tight DB/GUI coupling. 
  - The server side of Jam.py is written in Python, 
  - the client utilizes JavaScript, jQuery and Bootstrap.
  - 依赖werkzeug、sqlalchemy
  - https://jampyapplicationbuilder.com/
    - https://jampyapp.pythonanywhere.com/
    - https://northwind.pythonanywhere.com/
# more
- https://github.com/nils-simons/spackoDB /202206/js/starter
  - Firestore Alternative
