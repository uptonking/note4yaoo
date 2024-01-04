---
title: thread-domain-chat-im
tags: [chat, im, instant-messaging, thread]
created: 2024-01-04T01:28:02.550Z
modified: 2024-01-04T01:28:58.097Z
---

# thread-domain-chat-im

# guide

# discuss-stars
- ## 

- ## [Support ActivityPub for GitLab (&11247) · Epics · GitLab_202308](https://gitlab.com/groups/gitlab-org/-/epics/11247)
  - The goal of those documents is to provide an implementation path for adding fediverse capabilities to Gitlab.
  - Among the push for decentralization of the web, several projects tried different protocols with different ideals behind their reasoning (some examples : Secure Scuttlebutt or ssb for short, Dat, IPFS, Solid). 
  - But one gained traction recently : what is known as ActivityPu

- ## [FAQ | AT Protocol - Why not use ActivityPub?](https://atproto.com/guides/faq)
- 🐛 Account portability is the major reason why we chose to build a separate protocol. 
  - We consider portability to be crucial because it protects users from sudden bans, server shutdowns, and policy disagreements. 
  - Our solution for portability requires both signed data repositories and DIDs, neither of which are easy to retrofit into ActivityPub. 
  - The migration tools for ActivityPub are comparatively limited; they require the original server to provide a redirect and cannot migrate the user's previous data.
- 🐛 Other smaller differences include: a different viewpoint about how schemas should be handled, a preference for domain usernames over AP’s double-@ email usernames, and the goal of having large scale search and discovery (rather than the hashtag style of discovery that ActivityPub favors).

# discuss
- ## 

- ## 

- ## 
# discuss-mastodon
- ## 

- ## [Why Bluesky and not something like Mastodon? : KnowledgeFight_202307](https://www.reddit.com/r/KnowledgeFight/comments/14tawvg/why_bluesky_and_not_something_like_mastodon/)
- Mastodon's cool but it seems to confuse a lot of people, so the choice of Twitter replacement platform to reach a large audience is likely Threads vs BlueSky
- Bluesky is easier to setup (provided you get an invite) and will eventually be part of the fediverse.

- ## [What are your thoughts on those who use Mastodon alongside Bluesky : Mastodon_202308](https://www.reddit.com/r/Mastodon/comments/160vzob/what_are_your_thoughts_on_those_who_use_mastodon/)
- Mastodon's decentralization, including Activity Pub which has approval of the W3 consortium, is what can help make sure there isn't another Elon in the future.
  - The developers at Damus (the NOSTR client) regularly post about the problems they have with ActivityPub as a protocol, and yet they still fairly quickly implemented Mastodon relays.

- ## 🆚️ [Everything happening on Bluesky | Hacker News_202305](https://news.ycombinator.com/item?id=35830612)
- > Although Bluesky is currently hosted on only one server under the control of the Bluesky team, its intention is to eventually become a decentralized protocol for a multiplicity of federated servers with a variety of different moderation practices

- Bluesky made some key decisions that are different from Mastodon:
  - Profiles and posts are portable across hosted instances. If you have a problem with your admins, etc, you'll be able to hop away without much fuss.
  - Moderation is decoupled from hosting. They're still working out the details, but the overall vision is that the global firehose is public, and you'll be able to opt in and out of different moderators which operate on that stream. If you don't like what a moderator is doing, you'll be able to just turn them off for yourself. Moderation doesn't prevent people from posting, it allows people to prevent themselves from seeing.
- As far as I can tell, this is only with cooperation of the server owner; since their "DID Placeholder" relies on a server to provide a string of identity updates. ActivityPub can do the same thing with HTTP redirects; and Mastodon supports cooperative profile redirection, which is morally equivalent. Polycentric is a tad more decentralized than this, AFAIK it's specifically designed to make cryptographic keys first-class identities (so called "sovereign identity"). No clue if they've managed to solve the obvious pitfalls of cryptoidentity.

- Journalists are flocking to Bluesky, and not Mastodon because Bluesky allows retweets—which Mastodon doesn’t allow. Oh, and about hashtags, direct messages, and post edits not being available on Bluesky? Journalists don’t need them.

- ## 🆚️ [Blue Sky Server? : BlueskySocial_202304](https://www.reddit.com/r/BlueskySocial/comments/12nqfgz/blue_sky_server/)
- There is actually a lot of documentation for the ATP. It doesn’t cover the recent changes they’ve implemented, but there’s more than enough there to develop against the protocol and to understand the differences between it and AP.
- The major differentiators are also documented:
  - Data portability. Your data is stored in a self signed structure similar to a git repository. You own your data and you can move it around seamlessly without needing a 3rd party to verify it.
  - Algorithmic choice. It’s built around the idea that algorithms are useful and we need them, but users should be able to choose them.
  - Moderation. Moderation selection is also built into the protocol, although it’s still under development. Uses will be able to subscribe to different moderation providers separately from their host.
  - Performance. The performance cost of the protocol is a top priority and it’s something that was ignored with AP. They are designing it around the idea that low power hardware should be able to run an implementation of the protocol. AP is very… chatty, and it costs a lot to keep servers in sync with the federation.

# discuss-bluesky/threads
- ## 

- ## 

- ## [Threads or BlueSky, which is next? : cybersecurity_202307](https://www.reddit.com/r/cybersecurity/comments/14srryy/threads_or_bluesky_which_is_next/)
- Meta can’t launch Threads in the EU yet, that’s all I need to know about that.
  - 最初，Threads暂未在欧盟推出，是因为欧盟极为严苛的数字服务监管系统。

- Bluesky is like a merging of Twitter and Reddit. It's amazing, and the conversations there are very organic.

- ## 🪶 [Bluesky migrates to single-tenant SQLite | Hacker News_202311](https://news.ycombinator.com/item?id=38171322)
- I'm not opposed to this setup at all and it does have its place. But we are running away from schema-per-tenant setup at warp speed at work. There are so many issues if you don't invest in it properly and I don't think many are prepared when they initially have the idea.
  - The funny thing is that about a decade ago, the app was born on a SQLite per tenant setup, then it moved to schema per tenant on Postgres, now it's finally moving to a single schema with RLS. So, the exact opposite progression.

- Interesting... I like the strategy of having each user be 1:1 with a DB. What would be done for data that needs to be aggregated across users though?
  - To summarise the relevant details, the "AppView" service is responsible for the sorts of queries that aggregate across users, and that has its own database setup - I think postgres but I'm not 100% sure on that.
- You're right, as usual. AppView is on a Postgres cluster with read replicas doing timeline generation (and other things) on-demand. We're in the process of moving it toward a beefy ScyllaDB cluster designed around a fanout-on-write system.
  - The v1 backend system was optimized for rapid development and served us well. 
  - The v2 backend will be somewhat less flexible (no joins!) but is designed for much higher scale.

- Can someone that knows more about bluesky explain what data is stored in sqlite and not? Because i assume it isnt messages etc between users.
  - It's all your posts and replies as a user. While they currently host the only* PDS themselves, the end goal is for every end user to have their own PDS. Inrupt/SOLID calls this concept a "pod".

- This seems like a very misleading title, the Bluesky PDS is the meant-for-selfhosting thing they distribute, not the bluesky service as experienced and used by most of its users.
- AFAIK there's only one version of the software so "the service" runs the same thing that you self-host. SQLite seems like it will simplify the single-user case though.
  - That's right. This is the same code Bluesky is running on our new PDS hosts. It's all open source.
  - The main motivation in moving from a big central Postgres cluster to single tenant SQLite databases is to make hosting users much more efficient, inexpensive, and operationally simpler.
  - But it's also part of the plan to run regional PDS hosts near users, increasing performance by decreasing end-to-end latency.
  - The most experimental part of this setup is using Litestream to replicate these many SQLite databases (there are almost 2 million user repositories) to cloud storage. But we're not relying on this alone, we're also going to maintain standard SQLite ".backup" snapshots as well.

- I am curious, does the HN folks know if bluesky is more active than nostr or the mastodon network?
  - Less active than Mastodon, I'd assume more active than Nostr.
  - But the interesting thing for me isn't activity — it's the people on there.
  - Of the cohort who had >100k followers on Twitter, I think more of them post regularly on Bluesky than post on Mastodon. Bluesky definitely has a more cohesive feel, especially because there's currently just one instance & mod team.
- My bet is regardless of any initial good intentions, since BlueSky is a company, market pressures will inevitably force them into dark patterns like we see on every other commercial social network (going back to the early days of the companies, Facebook, Twitter, and even Google looked really good early on until all were corrupted by profit motive). My belief is that the profit motive is necessarily at odds with free communication.
  - To me, the ActivityPub network (Mastodon and friends) is relatively unique in the social media space in having no direct commercial pressures (the protocol is developed by W3C) and therefore being inoculated against the causes for these dark patterns.

- Why not use Postgres with RBAC (Row Based Access Control).
  - simpler db client
  - simpler cloud architecture
  - simpler resource management
  - simpler partial backups/restore
  - simpler compliance with law enforcement
  - partitioning might be easier
  - maybe simpler billing for storage ("just" size of DB)

- ## [Can you bookmark posts in BlueSky app?_202305](https://mrhack.io/can-you-bookmark-posts-in-bluesky-app/)
- as of now, bookmarking posts on BlueSky is not possible.
  - The only option available for users is to like a post.
  - After liking a post, it will be added to your list of liked posts. But, unfortunately, you cannot see your own likes as well.
- here are some tips to keep your favorite posts organized:
  - Use the "save post" feature on your device. This will save the link of the post, and you can easily access it again.
  - Use a third-party app to manage your bookmarks. Many apps are available on app stores that allow you to save and organize your favorite links.

- ## ✨ The official Bluesky app for Web, iOS, and Android is now open-source_202305
- https://twitter.com/addyosmani/status/1658228255328190464
  - Powered by @reactjs & @expo w/thanks to @pfrazee

- ## [First Impressions of Bluesky's Brand New iOS App | Hacker News_202303](https://news.ycombinator.com/item?id=35009723)
- Why would they expect anyone to build on top of their new social networking protocol? It is owned and will be driven by a private company and it’s desire for profitability, ⚖️ ActivityPub is an open standard that has been around for ~5 years and battle tested and already in use across different platforms.
- Maybe their efforts will be co-opted, but judging by the team's background -- André Staltz with Secure Scuttlebutt, Paul Frazee with dat/Beaker/Hypercore Protocol -- I think it's pretty clear the driving motivation for much of the team behind Bluesky is not profit.
- Bluesky's answer is this
  > Account portability is the major reason why we chose to build a separate protocol. We consider portability to be crucial because it protects users from sudden bans, server shutdowns, and policy disagreements. Our solution for portability requires both signed data repositories and DIDs, neither of which are easy to retrofit into ActivityPub. The migration tools for ActivityPub are comparatively limited; they require the original server to provide a redirect and cannot migrate the user's previous data.
  - > Other smaller differences include: a different viewpoint about how schemas should be handled, a preference for domain usernames over AP’s double-@ email usernames, and the goal of having large scale search and discovery (rather than the hashtag style of discovery that ActivityPub favors).
