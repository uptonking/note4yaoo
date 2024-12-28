---
title: lib-saas-zulip-docs
tags: [docs, zulip]
created: 2024-06-23T02:09:54.316Z
modified: 2024-06-23T02:10:01.601Z
---

# lib-saas-zulip-docs

# guide
- resources
  - [Zulip overview](https://zulip.readthedocs.io/en/latest/overview/readme.html)
  - [Zulip help center](https://zulip.com/help/)
  - [History of the Zulip project](https://zulip.com/history/)
# docs

## overview

## [Zulip architectural overview ](https://zulip.readthedocs.io/en/latest/overview/architecture-overview.html)

- codebase
  - backend (written in Python 3.x and Django), 
  - web app (written in JavaScript and TypeScript)
  - webhook integrations with other services and applications 
- Zulip is primarily implemented in the Django Python web framework. 
  - We also make use of Tornado for the real-time push system.
  - Tornado runs the server-to-client real-time push system. The app servers are configured by the Supervisor configuration
- Zulip’s HTML is primarily implemented using two types of HTML templates: 
  - backend templates (powered by the Jinja2 template engine used for logged-out (“portico”) pages and the web app’s base content) 
  - and frontend templates (powered by Handlebars) used for live-rendering HTML from JavaScript for things like the main message feed

- clients
  - Zulip Mobile is the official mobile Zulip client supporting both iOS and Android, written in JavaScript with React Native, 
  - and Zulip Desktop is the official Zulip desktop client for macOS, Linux, and Windows. 
  - Zulip Terminal is our official terminal-based client.

- integrations and other glue code: 
  - Python API bindings; JavaScript API bindings; 
  - a Hubot adapter; 
  - integrations with Phabricator, Jenkins, Puppet, Redmine, and Trello; and many more.

- A server can host multiple Zulip realms (organizations), each on its own (sub)domain.

- We use supervisord to start server processes, restart them automatically if they crash, and direct logging.

- memcached is used to cache database model objects.

- Redis is used for a few very short-term data stores, primarily our rate-limiting system.

- We use RabbitMQ for queuing expensive work (e.g. sending emails triggered by a message, push notifications, some analytics, etc.) that require reliable delivery but which we don’t want to do on the main thread. 
  - It’s also used for communication between the application server and the Tornado push system.
  - Most of the processes started by Supervisor are queue processors that continually pull things out of a RabbitMQ queue and handle them; they are defined in zerver/worker/.

- PostgreSQL is the database that stores all persistent data

## 🧩 [Realms in Zulip](https://zulip.readthedocs.io/en/latest/subsystems/realms.html)

- Realms are the Zulip codebase’s internal name for what we refer to in user-facing documentation as an organization (the name “realm” comes from Kerberos).
- Wherever possible, we avoid using the term realm in any user-facing string or documentation; “Organization” is the equivalent term used in those contexts

## 🔌🎨 [Widgets ](https://zulip.readthedocs.io/en/latest/subsystems/widgets.html)

- Widgets are special kinds of messages: polls, TODO lists, /me messages, Trivia bot
- Some widgets are used with a leading / (like /poll Tea or coffee?), similar to slash commands
  - but these two concepts are very different. Slash commands have nothing to do with message sending.

- It may be useful to think of widgets in terms of a bunch of clients exchanging peer-to-peer messages. 
  - The server’s only real role is to decide who gets delivered which submessages. It’s a lot like a “subchat” system.

- Right now we don’t have a plugin model for the above widgets; they are served up by the core Zulip server implementation. 
  - Of course, anybody who wishes to build their own widget has the option of forking the server code and self-hosting, but we want to encourage folks to submit widget code to our codebase in PRs
  - If we get to a critical mass of contributed widgets, we will want to explore a more dynamic mechanism for “plugging in” code from outside sources, but that is not in our immediate roadmap.

- This is sort of a segue to the next section of this document. Suppose you want to write your own custom bot, and you want to allow users to click buttons to respond to options, but you don’t want to have to modify the Zulip server codebase to turn on those features. This is where our “zform” architecture comes to the rescue.

- zform (trivia quiz bot)
  - Zulip’s trivia bot sends the Zulip server a JSON representation of a form it wants rendered, and then the client renders a generic “zform” with buttons corresponding to short_name fields inside a choices list inside of the JSON payload.
  - The beautiful thing is that any third party developer can enhance bots that are similar to the trivia_quiz bot without touching any Zulip code, because zforms are completely generic.

## 🔌 [Slash commands](https://zulip.readthedocs.io/en/latest/subsystems/slash-commands.html)

- Slash commands are commands to quickly do some stuff from the compose box
  - The codebase refers to these as “zcommand”s, and both these terms are often user interchangeably.
- Currently supported slash commands are:
  - /light and /dark to change the UI theme
  - /fluid-width and /fixed-width to toggle that setting
  - /ping to ping to server and get back the time for the round trip. Mainly for testing.
- It is important to distinguish slash commands from the widget system. Slash commands essentially do not send messages, while widgets are special kinds of messages.

- Typeahead for both slash commands (and widgets) is implemented via the `slash_commands` object 

## ⚡️ [Performance and scalability ](https://zulip.readthedocs.io/en/latest/subsystems/performance.html)

- First, a few notes on philosophy.
  - We consider it an important technical goal for Zulip to be fast, because that’s an important part of user experience for a real-time collaboration tool like Zulip. 
    - Many UI features in the Zulip web app are designed to load instantly, because all the data required for them is present in the initial HTTP response, and both the Zulip API and web app are architected around that strategy.
  - The Zulip database model and server implementation are carefully designed to ensure that every common operation is efficient, with automated tests designed to prevent the accidental introductions of inefficient or excessive database queries. 
    - We much prefer doing design/implementation work to make requests fast over the operational work of running 2-5x as much hardware to handle the same load.

- Zulip has many important optimizations, including soft deactivation to ensure idle users have minimal impact on both server-side scalability and request latency.

- 🏠 Zulip’s Tornado-based real-time push system, and in particular GET `/events`, accounts for something like 50% of all HTTP requests to a production Zulip server. 
  - Despite GET `/events` being extremely high-volume, the typical request takes 1-3ms to process, and doesn’t use the database at all (though it will access `memcached` and `redis`), so they aren’t a huge contributor to the overall CPU usage of the server.
- Because these requests are so efficient from a total CPU usage perspective, Tornado is significantly less important than other services like Presence and fetching message history for overall CPU usage of a Zulip installation.
- It’s worth noting that most (~80%) Tornado requests end the longpolling via a heartbeat event, which are issued to idle connections after about a minute. 
  - These heartbeat events are useless aside from avoiding problems with networks/proxies/NATs that are configured poorly and might kill HTTP connections that have been idle for a minute.
- Currently, Tornado is sharded by realm, which is sufficient for arbitrary scaling of the number of organizations on a multi-tenant system like zulip.com. 

- `POST /users/me/presence` requests, which submit the current user’s presence information and return the information for all other active users in the organization, account for about 36% of all HTTP requests on production Zulip servers. 
  - For this article, it’s important to know that presence is one of the most important scalability concerns for any chat system, because it cannot be cached long, and is structurally a quadratic(二次方的) problem.
- Because typical presence requests consume 10-50ms of server-side processing time (to fetch and send back live data on all other active users in the organization), and are such a high volume, presence is the single most important source of steady-state load for a Zulip server. 
  - This is true for most other chat server implementations as well.
- There is an ongoing effort(202304已合并) to rewrite the data model for presence that we expect to result in a substantial improvement in the per-request and thus total load resulting from presence requests.

- Zulip is somewhat unusual among web apps in sending essentially all of the data required for the entire Zulip web app in this single request, which is part of why the Zulip web app loads very quickly – one only needs a single round trip aside from cacheable assets (avatars, images, JS, CSS). 
  - Data on other users in the organization, channels, supported emoji, custom profile fields, etc., is all included. 
  - The nice thing about this model is that essentially every UI element in the Zulip client can be rendered immediately without paying latency to the server; this is critical to Zulip feeling performant even for users who have a lot of latency to the server.

- There are only a few exceptions where we fetch data in a separate AJAX request after page load:
  - Message history is managed separately; this is why the Zulip web app will first render the entire site except for the middle panel, and then a moment later render the middle panel (showing the message history).
  - A few very rarely accessed data sets like message edit history are only fetched on demand.
  - A few data sets that are only required for administrative settings pages are fetched only when loading those parts of the UI.

- The above doesn’t cover all of the work that a production Zulip server does; various tasks like sending outgoing emails or recording the data that powers` /stats` are run by queue processors and cron jobs, not in response to incoming HTTP requests.
  - For all of our queue processors, any serialization requirements are at most per-user, and thus it would be straightforward to shard by user_id or realm_id if required

- In addition to the above, which just focuses on the total amount of CPU work, it’s also relevant to think about load on infrastructure services (memcached, redis, rabbitmq, and most importantly postgres), as well as queue processors (which might get backlogged).
- it is worth considering that database time is a more precious resource than Python/CPU time (being harder to scale horizontally).
- Most optimizations to make an endpoint cheaper will start with optimizing the database queries and/or employing caching, and then continue as needed with profiling of the Python code and any memcached queries

- For a handful of the critical code paths listed above, we further optimize by skipping the Django ORM (which has substantial overhead) for narrow sections

## import/export

### 🧐👣 [Import from Mattermost | Zulip help center](https://zulip.com/help/import-from-mattermost)

- To import your Mattermost organization into Zulip, 
  - Export your Mattermost data
  - Import your Mattermost data into Zulip
  - Get your organization started with Zulip
- Mattermost's bulk export tool allows you to export all public and private channel messages.

## 3rd-party libs

# more
