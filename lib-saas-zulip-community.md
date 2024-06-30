---
title: lib-saas-zulip-community
tags: [community, zulip]
created: 2024-06-23T02:09:40.203Z
modified: 2024-06-23T02:09:51.024Z
---

# lib-saas-zulip-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [Zulip Server 1.9: HipChat import and much more | Hacker News _201811](https://news.ycombinator.com/item?id=18400988)
- How do you handle high availability for Zulip? Last I looked that was a problem for it.
  - If you're self-hosting, our commercial support offerings will help you setup your servers in a way that achieves your uptime goals; because Zulip is so stable, usually folks just go with a hot spare (our enterprise customers generally only report downtime related to server upgrades, which is usually avoidable).

- ## [Document story regarding horizontally scalability  _201509](https://github.com/zulip/zulip/issues/54)
- Anyway to horizontally scale for both high availability and high performance purposes?
- Yeah, we haven't written up documentation on scalability stuff. The short story is:
  - If you're hosting multiple realms on the same server like we do with zulip.com, you can scale horizontally without any real code changes by adding additional frontends -- two frontends only need to talk to each other if they have users that exchange messages.

- ## [how does zulip scale _202104](https://github.com/zulip/zulip/issues/18291)
  - I am looking for solutions to handle multiple concurrent connections, but django does not natively support websocket - the way it is built cannot support it anyway. 
  - As zulip is built with django, I am curious how you're handling multiple websocket connections per organization.

- [Performance and scalability — Zulip 9.0-dev+git documentation](https://zulip.readthedocs.io/en/latest/subsystems/performance.html)
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 💰 [New plans for self-hosted Zulip customers | Hacker News _202312](https://news.ycombinator.com/item?id=38659529)
- It's always annoying to have something that was free taken away from you, but this seems pretty fair. There's no way to handle push notifications without a centralized server.
  - all of the code is open source, so if someone else thinks they can offer Zulip hosting for cheaper, they are free to do so.
- You can send notifications from your own server. But you have to patch the mobile apps
- It sounds like if you want to use the official mobile apps they can only receive notifications from Zulip's service so you can't run your own.

- This is quite disappointing - having the same pricing as a fully managed Zulip Cloud for simply getting push notifications (at $8/user/mo!) is really steep and feels like a clear way to push people to Zulip Cloud and discourage self-hosting.

- I lead the Zulip project. I agree the existing React Native mobile apps have been the biggest pain point for Zulip. Our mobile team's main focus for the last year been rewriting our mobile apps in Flutter, which will result in apps that are faster, dramatically more correct in terms of how faithfully they implement Zulip's API and business logic, and with a cleaner design. Here's the section of the Zulip 8.0 blog post about it

- While I imagine it's no priority, nor a solution for everyone, I wish more apps would support UnifiedPush. The notification limitation is purely an Apple/Google one, and there's no "hub" setup you can easily configure with either.

- Conversations (the XMPP client) has also figured out a way to receive notifications without using centralized servers by keeping an TCP open thus avoiding any centralized servers for push notifications. Modern XMPP servers can be instructed to only use the TCP connection when a notifying message arrives to avoid radio and battery consumption. Conversations also can act as a UnifiedPush distributor for other apps which don't want to maintain their own TCP connection.

- Wasn't Zulip grandstanding about remaining free when Mattermost removed their free plan?
- It seems like Mattermost is basically the same deal unless you use their “Test Push Notifications Service”, which they discourage using in production, no?
  - “Same deal” in that you can either pay a per-user fee, or host the push server yourself and ship patched mobile apps to receive them.
- There's no Zulip Test Notifications Service. And after a few years of running on the Mattermost Test PNS it is generally pretty stable, you just don't get any support if things do go wrong.

- Zulip is 100% open source. In open core products, those specific features just don't exist at all in the open source version. For example, Mattermost requires the proprietary Mattermost Professional at $10/user/month if you want to use SSO, LDAP sync, user groups, read receipts, etc.
  - If you compare Zulip's pricing options to Mattermost's, our offering is substantially more generous. It would be even if we went open core and moved a few dozen features of Zulip to a proprietary version. But we're not going to do that: we really do care about being an 100% open source project.

- Maintaining an open TCP/IP or even UDP/IP network socket to receive incoming notification messages requires sending a packet back and forth every so often to confirm the socket is live and keep it open, even while the socket is idle and there are no notifications.
  - You can technically open a socket without doing this, and this does work on parts of the internet. It often works between devices on your LAN. But many modern networks have unreliable connectivity, handovers between base stations (i.e. mobile or wifi), often one or more layers of NAT and/or firewalls, and more. 
  - 👀 The only generally reliable solution to get real-time inbound notifications to a device, is for the device to open an outbound socket and the protocol to send a packet occasioally in each direction. The packets confirm liveness to the receiving endpoint, as well as telling other parts of the network the socket is still live.
  - When your device hasn't received a confirmation after a configurable timeout, it's time to open a new socket from the device, because the original socket may have stopped working.
  - That's three technical reasons to have a single, centrally managed notification service per device.

- 
- 
- 

- ## [Why Zulip will not get on the blockchain bandwagon | Hacker News _202111](https://news.ycombinator.com/item?id=29205346)
- the ONE and ONLY thing a public blockchain is useful for is censorship-resistant payments.
  - Which might include good things (donation to your favorite whistleblower or buying weed or whatever) but definitely WILL include bad things — for example it is uniquely well-suited for paying ransoms(赎金), hence the ransomware explosion!
  - Again, this is the ONLY thing. It is horrendously bad in every way, there's just no other choice for this kind of usage.

- Today’s reality is that cryptocurrencies are enabling massive amounts of criminal behavior. ... The lack of effective regulation of crypto assets puts people at high risk of being manipulated by scammers.

- I'm surprised to see a lot of people here skipping over why Zulip needs to write this article. Building a chat app brings you pretty quickly into the digital identity and presence space. Regardless of getting involved with NFTs and ICOs and such, a wallet is a pretty adjacent concept to this domain. There's a reason a ton of chat apps currently offer some form of payments or payments integration. Venmo shows how hard it is to build "social" from payments, while the other direction is much easier to do because of network effects.

- ## [Zulip – Threaded real-time chat for distributed teams | Hacker News _202205](https://news.ycombinator.com/item?id=31572278)
- I hope at some point to see a federated implementation of the Zulip communication model over Matrix. https://github.com/zulip/zulip/issues/356

- Zulip is great. One thing that I don't see mentioned that is a huge deal that you don't realize at first. The topic for a message can be changed after the fact and by anyone.

- Threading feels bolted on in Mattermost, but is the primary feature of zulip.
  - Think of Zulip as a realtime version of NNTP, and Mattermost as a more modern IRC with a "reply" feature. 
  - The "right" way to use Zulip and Mattermost is quite different, though each one can be easily used as an inferior version of the other.
- Disclaimer: PM at Mattermost
  - when I first joined the company in 2019 I also found that threading felt "bolted on". Primarily because channels rendered everything in the same linear feed regardless if it was a message or comment so there wasn't much point in taking the time to first hit reply.
  - However, Collapsed Reply Thread has been a game changer for me and not only do I no longer feel that way about threading, my productivity would plunge without it. That feature has been in public beta since last summer and will go into general availability in two weeks to officially become the "right" way to use Mattermost.

- Big fan of Zulip. Only problem is that you don't get email notifications unless you're directly @ mentioned in a response, even if you're participating in a discussion, and even if they're replying directly to you. Otherwise I find the threading approach to be a big win.

- Discord added threads this year and it’s lovely.

- 🎞️ How are the video call options on Zulip?
  - Zulip doesn't do video calls itself, but we have handy "Start a call" button and you can configure which video call provider that uses

- ## 🤔 [Why Zulip will stand the test of time | Hacker News _202112](https://news.ycombinator.com/item?id=29595926)
- Love Zulip! Simple architecture, amazing packaging release/upgrade process and very developer friendly at all levels
  - Login-with-Google was trivial to setup. Some users prefer to email the server and the gateway was so easy to setup. Search Just Worked(tm). It's fast. It's easy to admin.
- I have only one complaint... but it's a biggie: the UI/UX.
  - UI is inconsistent: layouts/fonts/icons vary by screen and surface
  - UX buries common features (e.g. reply, reaction) and promotes uncommon features (e.g. invite new user). UX is rough, e.g. click-targets are tiny and not always obvious, and features are hidden behind mouseover.
  - promotes the name "Zulip" all over, which is a problem for users who don't know what a Zulip is or why they'd want one, e.g. emails from "Zulip" and not the name of the community.
  - needs a way to "nudge" conversations into a smaller set of topics/threads, e.g. suggestions.
  - conversation UI still suffers from scaling issues and needs some reddit-like way to display larger conversations...
  - no way to control which previews are shown/hidden
- Very much agree: Zulip is fantastic, except for the UI (mostly the look & feel) which makes difficult to convince non-tech users to adopt Zulip instead of Slack.

- Maybe a better title would be "Why your Zulip data will stand the test of time".

- Slack’s threads suck compared to Zulip’s. In Slack, threads only notify thread participants unless you choose to send it to the channel too, which defeats the purpose of threads by interrupting other conversations. In Zulip, everything in the channel/stream must be a thread, kinda like email.

- Zulip is implementing the same bad architecture as google/ms/apple/fb's messengers (custom protocol, no federation), but at least it does it well (open source, usable, do-one-thing-well, no dark patterns, powerful and stable API).
- How is it "bad" if it's the standard used by the most successful messenger platforms
  - Because there isn't a standard. The point is each one implements their own protocol instead of adapting a standard such as Matrix or XMPP. (Whether any suitable standard exists (much less existed in 2012!) is another issue, but regardless it's fair to say that the current state of things is not ideal.)
- I don't think "whether any suitable standard exists" is another issue, it's the exact one. If you're building a product and there is no standard to cover core technology, you roll your own because it's faster than waiting for someone else to invent one.

- They told that they are working om Matrix integration. I have no idea whether that work is still on track or already abandoned.

- Discord forces to use one account everywhere, Slack sucks for search and threads and causes too much noise and clutter, Teams , well we are still recovering from the emotional and productivity damaged it caused. What else is there?

- Where is Matrix support for zulip-style threads? It's been a while.
  - My understanding is that it exists already in the spec (and I think Synapse might even support it??). It is just that no clients have implemented it yet...
  - IIRC, the Element team has been working on it, but they seem very hesitant to release anything around threads that is half-baked. They really want to get them right the first time!

- ## 🎯 [Zulip 7.0: Threaded open-source team chat | Hacker News _202305](https://news.ycombinator.com/item?id=36141107)
- With their (somewhat new) public server feature, the chat is available for browsing without needing an account first.

- the thing that Slack does so much better than everything else I've tried, is search. For context, I'm not talking just about the ease and speed of searches, but also about the support for basic filters, exact phrase searching (Discord doesn't have this) or bypassing fuzzy search (Discord always fuzzy searches on the individual words of your search words)
  - very nice workaround with zulip — it has official exporter (zulip-archive) that creates static html of all accessible streams (and with a trivial change all PMs too). Which makes reading/searching a local operation.
- You can do search engine indexing via https://github.com/zulip/zulip-archive; it defaults to archiving your public access streams. We will eventually support search engine indexing without the extra overhead of running a separate archive tool (likely as an organization-level settings checkbox, since not everyone who wants public access wants search engine indexing).

- 🧩 threaded conversations (called "instances" in Zephyr https://sipb.mit.edu/doc/zephyr/, which Zulip's model is inspired by) are infinitely better than anything Discord/Slack/IRC have to offer and greatly contribute to discussion culture: it is considered a faux pas to not switch an instance when conversation topic changes, so you can easily narrow in on the entirety of a conversation even if a number different conversations are happening at the same time.

- 🆚️ What is the difference between using Zulip threads for topic discussions vs. using Discourse, with its categories?
  - The big Zulip feature, IMO, is that you can easily reorganize topics afterwards.
  - It’s not like in a forum where you create a topic and then get answers (although you can).
  - It’s more like a chat conversation that you can group and label once you detect it have its own topic.
- Yes; if you've ever wanted to go back in time and create a new thread for an e-mail topic, you will understand what I like so much about Zulip.

- ## 🎯 [Zulip 5.0: Threaded open-source team chat | Hacker News _202203](https://news.ycombinator.com/item?id=30846659)
- I kinda like the idea of 'resolving threads'. You could create a temporary war room for a particular issue then close it as needed. Although I doubt our company is big enough where it makes sense to segregate beyond job divisions.

- I think the "thread-only" feature is the biggest selling point, it's niche-y by default. Zulip is the meeting point of a hackernews/reddit-like board, real time chats and mailing lists. UX and UI needs work, but the base concept is its main feature.

- what does this accomplish that a self-hosted matrix/synapse setup doesn't?
  - The main differentiator of Zulip IMO is the threading model. Instead of chat rooms with multiple un-separated concurrent conversations taking place, every message* must start a topic or be placed in one (topics are like the subject line in an email). You can still look at the room and see all of the topics at once, but you can also focus in on a single topic. And it remembers your read progress at a per-topic level, so it's quite feasible to catch up on chats asynchronously. Basically Zulip brings the best things about mailing lists to chat.
  - you can now turn off the topic requirement, in which case messages go into a "no topic" topic. But not using topics kind of defeats the purpose of using Zulip IMO.

- ## 🎯 [Zulip 4.0: Threaded open source team chat | Hacker News _202105](https://news.ycombinator.com/item?id=27149123)
- Apart from the threading model, I love Zulip for its openness. It's quite sad Slack and Discord are often the first choice for open communities. They are siloed and unless you are deliberately searching in a specific workspace, you'll never run into the information in a search engine.
- In comparison, Zulip:
  - provides HTML export functionality
  - URLs are nice and encode meaning, compare with Slack/Discord meaningless character sequences
  - allow viewing workspaces in 'guest' mode, without registering at all

- Zulip can give you the best of both worlds. It's a regular chat. But the threading model also encourages long-form, more forum or email like discussions.
  - The only downside is the very subpar UX when compared to Discord or even Slack.

- Slack threads are useless compared to Zulip. In Zulip you can create threads on the fly from existing messages, so if discussion starts diverging you can turn it into a new thread. It's just a fundamentally superior model.

- We gave Zulip (and Mattermost, Element/Matrix, Rocket Chat etc) a try when our company was looking for self hosted alternatives to Slack.
  - The fact that Zulip is threaded (and this threading is enforced) is what makes it so valuable, at least to me. Your proposals would get rid of its main feature and go completely against one of its core ideas.
- I liked the ideas of topics and such, but other people weren't so enthusiastic to learn about a whole new chat paradigm.

- Mattermost doesn't seem to be improving at all for years. I just don't get how it's difficult to reply or quote someone's message when it's such a basic chat feature. Instead they invent weird code like "shrug" thinking it's funny during business chat. Also I often get logged out of mobile app and notifications stop reaching which makes it very unreliable as a business tool.

- 🔡 The Zulip Django source code (the "zerver" subdirectory) is a great read too. It's Python 3 with a lot of typing hinting (has no mypy errors).
  - Unlike a lot of Django code bases it heavily uses function-based views. It also uses relatively few third-party django apps.

- The Rust project uses Zulip and I love it.

- how does it compare to matrix/element?
  - Zulip has a far more advanced threading model than Matrix. Currently, Matrix only has basic replies in the spec. In practice, everything in a Matrix room is in a single thread. It definitely makes it hard to follow conversations that are long-lived or in busy rooms or both.
  - Matrix is federated and Zulip isn't. You can run your own Matrix server and communicate with all the other Matrix servers that already exist. Rooms live on multiple servers and are resilient to the failure of any participating servers as long as one remains.
  - Matrix is far more general than Zulip. It acts as a store for arbitrary, eventually-consistent, ordered JSON data. Most of the time this is used to create an instant messaging service, but it can be used for much more.
  - Zulip subjectively has a nicer default client than Matrix (Element). Zulip's is special-built to handle its unique threading model.
  - It's also worth noting that Matrix is adding support for arbitrary threading 

- Is there a chat app that is native anymore? I know Hipchat was back in the day, but the 2 I've used in recent years (Slack and Cliq) are both Electron as well. (As is Mattermost, but I haven't used it)

- With Zulip, why do you need two namespaces for every chat content? I find it hard to understand it
  - One namespace (Stream) is a long-lived, durable category. 
  - The second namespace (Topic) is the specific conversation you're in and is more like an email subject line.
  - Topics are lightweight and can be split, merged and moved around as needed.

- 🛢️ Zulip has a notoriously bad db schema. For example, a single write in a 5000 member public group would result in 5000 writes to the user table.
  - This hasn't been true since we implemented soft deactivation in 2017. You can read about the feature in our documentation here; 
  - It is true that Zulip writes a tiny UserMessage table row with (user_id, message_id, flags) for every active recipient of a message, we need to do so in order to track the unread state for all of those recipients (as well as related details, like mobile push notifications state). We need to write to that row a second time when the user reads the message.
  - With modern postgres and SSDs, writing 1000 rows is really cheap, and so part this is extremely fast when sending messages with 1000 online recipients, which isn't a thing real users do constantly anyway (since that's effectively an announcement, not a chat message).
  - You could have a bad experience if you use remote storage that rate-limits "IOPS", though, because AWS at least used to count each row as an IOP and would use your full quota for 20s if you marked 20K messages as read with a 1000 UOP/s plan
- No software architect here so I might be completely off the target but, is not read/unread count something that squares perfectly with the "eventually consistent" model? You don't need to write it down to the persistent storage right now as long as the client UI has it, then some kind of cache has it (so mobile can be in sync when refreshed) and then you persist it to the DB.
  - We could certainly do something in that direction, but it'd be a lot of complexity (and risk of synchronization bugs) to avoid a few ~10ms of latency when sending messages to very large audiences.
  - Especially since that latency is mostly invisible, thanks to local echo
  - It's also not very high-value to optimize; that database write is 10-20% of the total time to process sending a message to everyone in a large open community like chat.zulip.org (with 18K total users).

- Zulip uses standard HTTPS encryption for traffic and Argon2 for passwords.

- I was skeptical about Zulip when I first tried it. What is it supposed to be? A chat? A forum? Why is the UI so ugly?
  - But after using it a while I now really dislike Slack et al, both in professional teams and for open source communities.
  - Zulip can give you the best of both worlds. It's a regular chat. But the threading model also encourages long-form, more forum or email like discussions.
  - Threads are easily discoverable and it's trivial to catch up on all the relevant discussions that you missed, while skipping everything that doesn't concern you.
  - The only downside is the very subpar UX when compared to Discord or even Slack.

- ## 🚀 [Dropbox has open-sourced Zulip | Hacker News _201509](https://news.ycombinator.com/item?id=10279961)
- We've used IRC and Jabber, looked at Slack and Hipchat and Skype and Lync, and somehow keep coming back to Zulip. It lets us have real, ongoing, and substantive conversations, with a large number of participants, without being overwhelmed.
  - Zulip's threading model exists somewhere between Slack's rigid "rooms" model and Twitter's everything-is-public model, so it's much lighter-weight to participate in multiple places at once than on Slack but it's also easier than on Twitter to have the right conversation with the right people without bothering others with something irrelevant to them. 
  - And Zulip's threading model makes it much easier to have multiple conversations within the same space without stepping on each others' toes or getting distracted.
- Zulip was acquired in March 2014

- I haven't yet tried Zulip's threading model, but I can certainly say I'm not pleased with Slack's. It can be very frustrating to try and trace a conversation backwards in a crowded Slack channel. I haven't used IRC in a while, but at least my client had a feature to toggle highlighting on a back-and-forth conversation, but that wasn't perfect.

- Zulip use RabbitMQ for passing messages where persistence is desired; last I checked Redis didn't support persistent on-disk queues.
  - Zulip's use of redis right now is basically just for the API rate-limiting; it could be easily removed.
- Redis does have persistence options... I was just thinking Redis is often used as a more advanced memcached, while also supporting pub/sub channels and acting as a mq broker with a frontend... was just thinking in terms of reducing the requisite services, since rabbitmq requires erlang and it's own services as well as memcached.
  - Two things you often want are at-least-once delivery and the ability to queue messages without requiring the consumer to be connected. It requires a fair amount of work to get this to work in Redis. It's not simple configuration.
