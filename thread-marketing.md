---
title: thread-marketing
tags: [marketing, thread]
created: '2020-12-07T06:07:44.432Z'
modified: '2021-01-06T14:40:06.842Z'
---

# thread-marketing

# guide

# pieces
- ## 

- ## 

- ## 

- ## 苹果今天公布的财报说，它有7亿的付费订阅用户。这太惊人了，应该是全球最大的在线服务提供商了。
- https://twitter.com/ruanyf/status/1420221512456359936
  - iCloud、苹果音乐、苹果电视、苹果健身、苹果新闻、Apple Arcade

- ## Make money without: Capital or Skills. Do this:
- https://twitter.com/sean0to10k/status/1420021674859192321
  1.  Pick a service you want to sell
  2.  Find someone offering that on Fiverr + agree a price
  3.  Land clients using email, LinkedIn + cold calls
  4.  Charge 2-3x the price you pay the freelancer

- ## I'm taking the rest of the year off to work on @tldraw full time. 
- https://twitter.com/steveruizok/status/1419048412431933441
  - Turns out there's a lot of enthusiasm for an open source hackable SVG-rendered drawing tool. 
  - My goal is to get it the entire architecture open and toot tooting by the end of the year.
- What do I mean by architecture? 
  - I'm starting off with a slice-and-dice, separating the current Next.js app into a layered architecture that allows other folks to build on either the app or the renderer.
- What about hackable? 
  - The renderer (a React component) is "shape agnostic", meaning that it relies on the implementation to provide it with both the document and the tools to interpret the document. 
  - This makes it *very* easy to modify existing shapes or add new ones.
- The app layer is also going to be a NPM module: essentially the current @tldraw app published as a React component that you'll be able to embed it in any React project. 
  - Control the document either through props or through an imperative API, respond to events—even theme it!
  - The app layer will include a basic set of shapes and tools, just like @tldraw does now. 
  - Want to experiment with a custom shape, or change the way things work? Smash that fork button and have a play.
- The site (http://tldraw.com) is going to be just one example of how the component can be used. 
  - Features such as file management, multiplayer collaboration, and cloud-backed documents can all be managed at this level.

- ## Cloudflare 官网罕见发文，抨击亚马逊云服务出口带宽太贵。
- https://twitter.com/ruanyf/status/1418792375405613056
  - 它给了一张详细表格，列出它拿到的带宽批发价与亚马逊的零售价之间的对比。
  - 结论就是，在美国，亚马逊的带宽价格是批发价的80倍。
- 还好吧，微软的更贵，一个IP每月都好几刀呢
- 亚马逊太黑, 贵不说, 还很鸡贼, 很多扣费项目藏的很深, 就算不用了, 也还在偷偷的扣着你的钱.
- cf自己搞个云吧，已经白嫖它的proxy很久了，如果不是它的proxy，我的翻墙服务器需要经常更换。所以很想补偿一下这样的良心厂家。
- 真得贵得离谱，比do/linode贵太多了，和我用的cc家小鸡$3有5000G就更夸张了
- 服务器资源卖的便宜，赚你流量钱
- 大陆的流量价格是AWS的3倍以上。

- ## One thing I've consistently had to relearn in developer marketing:"Talk benefits, not features" doesn't work!
- https://twitter.com/swyx/status/1361279902889086980
- Developers are sick of vague promises and wary of black boxes.
- Instead:
  - Demo - reach Wow! in <10 mins
  - Explain how it works
  - Show how real companies use in prod

- ## webpack sponsored: In November 2020, 28 backers joined ( @EasyAgile , +27) - you are the best! Raising hands We received $13, 996 from 281 backers and we spent $15, 651 on . Our current balance is $10, 116.
- https://twitter.com/webpack/status/1333751566004838401
- In May 2021, 20 backers joined ( @mayhemBCN , @lucamezzalira , @tu4mo , +17) - you are the best! 🙌 We received $26, 056 from 273 backers and we spent $17, 044. Our current balance is $60, 138.

- ## What are some good examples of sponsorware done right? 
- https://twitter.com/mattgperry/status/1410122128037486594
  - I'm looking closely at @steveruizok (glob) but it feels like a tricky thing to get right.
- @tiptap_editor v2 by @_ueberdosis is a great example imo, launched early to backers, after 5k/mo released publicly
  - Thanks for the mention! Let me know if you have any questions, we’re on our way to double down on Sponsorware.
- Lots of thoughts here! I think sponsorware works great with dev log content where that sponsorware covers the secondary/“try it yourself” content. As long as the open content is good, you can build that audience/support without shilling
  - For tldraw the sponsored content is an app, but I could imagine a blog where interactive examples or additional code samples are all gated like that.
  - If everything is aligned, it’s a great motivator: make new stuff, write about it, get new supporters. I’m 100% okay with being lured by good free content into supporting individual devs.

- ## The rationale there is that traffic tends to continue strong until a weekend is hit, 
- https://twitter.com/JoshWComeau/status/1409624431715098627
  - so by publishing early in the week, the weekend hit happens later. 
  - But often I’ll publish on Tuesday because I get busy or forget on Monday
- Same here. Try to publish before usa wakes up but often a bit late 

- ## I love @github 's approach to marketing pages and a pattern that I think Next.js and React can help democratize(民主化)
- https://twitter.com/rauchg/status/1407769747954049036
  - 分析了github运营页的布局
- Best DX I’ve seen on a documentation page is from @stripe where they inject your own key on code snippets. We need more pages like that.
- meta-search is here to stay!!!

- ## We @vercel just raised a $102M Series C @ 1.1B on our mission to help build a faster Web, made for everyone. 
- https://twitter.com/rauchg/status/1407716317507948549
- Our goals: 
  - 1️⃣ Build the SDK for Web 
  - 2️⃣ Lower the barrier of entry 
  - 3️⃣ Focus on the end-user

- ## 苦读十多年，进入顶尖名校，熟悉前沿技术，进入互联网大厂，拿着 996 的高薪，最重要的工作是：骗人多点一下「继续抽奖」。
- https://twitter.com/shrugged_hi/status/1407037885325484034
- 跟谷歌的那帮人，世界上最聪明的头脑都在绞尽脑汁儿的卖广告 一个意思嘛
- 确实如此～还有咨询公司进入大厂做战略的也都是类似的活儿
- 我觉得应该是【帮忙砍一刀】
- 高级人才的定义：分析什么样的优惠券有更多人点击。
- 日常功课工作：在朋友圈发领导诗歌的赏析
- 有个笑话：推荐算法发展到最后都会给你推服装搭配。所以不如一开始就推送服装搭配
- 哈哈，计算广告。

- ## Apple has now paid over $230 billion to developers since the app store has launched. (Weird I thought customers paid them)
- https://twitter.com/tominniss/status/1401972522325774341
- Or put another way, they've creamed off nearly $100 Billion!
- Same shit for YouTubers. YouTube gets ad Money and pays the creators. At least Apple talks about the Money, they keep for all of this. YouTube Money is still mysterious because its based on multiple things How much you can own
  - I can bet that hosting YouTube is significantly more expressive than the Appstore. So maybe it doesn't make sense for YouTube to provide such data and have people fight them into bringing the rate down, i.e., destroy their core business model.
- Here is why Netflix is not supported in shareplay, and this is also how Apple is preparing for the removal of the anti-steering(操纵，控制) provisions(条款，规定；供应品、粮食)

- ## The whole open source model of relying on donations from individuals, and to a much lesser extent, companies, is really problematic. 
- https://twitter.com/devongovett/status/1392201493596446722
  - The pandemic has shown us that it's not sustainable
  - even the most successful projects like webpack and Babel have seen huge declines in funding.
- Building companies around open source can also be problematic though. 
  - It's hard to say when the VC money will run out, 
  - or the company will need to pivot to become profitable in a way that hurts open source users.
- An alternative model is for companies looking to improve a project to hire contributors and pay them to work on it together with members of the project from other companies. 
  - The project can't be owned by any individual company for this to work – all parties need to be equal.

- ## 一直需要一个很好用的财税 SaaS 服务，强付费需求，要不是我不懂行我早下场自己做了。
- https://twitter.com/waylybaye/status/1385921039989755906
- 财税的基础逻辑还是简单的，也都比较死，没啥技术难度。
  - 但是第一，企业要合理避税甚至操控报表（部分操控报表的行为也是合法的），财税软件很难做到
  - 第二，各种税法很繁琐，甚至有些标准年年在变，因此将其转化位代码也很繁琐
- 澳新有两个公司做得比较好，MyOB和Xero。业务也很成功。
- 财税太专业了，投下去无底洞。而且它的核心竞争力也不在好不好用。
- 阿里云貌似有相关产品，按照要求记账，自动报税
  - 阿里是抄袭的自记账。太不要脸了。

- ## As a designer & indie maker, I must tell you this: Visual design (read: aesthetic) is the least important thing to focus on. 
- https://twitter.com/philipyoungg/status/1378658135456448513
  - Make it work and focus on UX (onboarding(onboarding是新用户引导流程, 是刺激用户激活的增长手段之一), reduce friction(分歧，争执；摩擦), good contrast). 
  - Visual is the deciding factor when your competitor has equally good product.
- Similar app as Session has similar pricing but make more revenue each month despite having uglier visual design. Why?
  - They have integrations (Todoist, JIRA etc), 
  - available on web (don't need to install app), 
  - they have simple to do list
  - ...essentially reduce friction
- So, stop focusing on logo design, brand name, aesthetic, etc
  - It doesn't matter if your product doesn't solve the problem and have many frictions. 
  - I regret spent a lot of time (even days) designing linear and radial gradient for Session. Twice even (for light and dark mode).

- ## Why is JavaScript hardly taught in any major universities? Based on the current market, it should be 80% of the entire curriculum!
- https://twitter.com/SimonHoiberg/status/1376569844993232902
- JavaScript is a bad programming language for first time learners. Preparing students for a single job makes them unprepared to jump from one task to the other and how to teach themselves. CS is not JavaScript, the other way round.
- JS is bad for teaching theory. Theory doesn't go out of style, so the language used is almost an after thought. Also JS changes WAY to fast and too often. If you know the theory, picking up JS is more a matter of time to learn the syntax. (and the gotchas)

- ## I'm in the market for a ticketing system (eg Zendesk). Ideally one developer-friendly, with a solid API.
- https://twitter.com/JoshWComeau/status/1370831667749863428
- Helpscout is really great. It’s email based from the customer side, whereas Zendesk it feels like you’re talking to help desk with their ticketed emails and I hated it.
- I use Freescout which is free and open source, has extra modules that you can buy, and presumably you can make your own as well, but I haven't tried (uses Laravel)
- Intercom is the best and easiest for both you and the customer. But it's paid and costly with limited API.

- ## SaaS is not passive income. When I stop shipping new features and/or stop marketing, I feel sales slowing. SaaS is something you have to keep working on.
- https://twitter.com/yongfook/status/1369276581567365123
  - The only people who talk about SaaS as passive income are folks trying to sell you their passive income SaaS course!
- It’s definitely not passive income but it also depends on where your top of the funnel(漏斗；漏斗状物) traffic is coming from.
  - I just recently saw a SaaS that invested heavily in content marketing for a few years and now gets traffic on autopilot(自动驾驶).
  - High domain authority = barrier to entry. It would take years for a new competitor to outrank them.
- It can become passive if you hire good people to do those things for you as well as run the day to day things. I think this is really hard for many bootstrapping founders to do.

- ## Startup idea: A social network (let's call it "the web") where people can post digital art, *but* they first need permission ("a licence") from the artist.
- https://twitter.com/AmeliasBrain/status/1368598410673025025
  - Artists can sell permission in various ways:
  - exclusive to one owner or not
  - transferable or not
  - No chained blocks required
- I'm seeing so many cool digital artists post links to their NFT offerings & as much as I hate the blockchain absurdity of it, I've felt like I couldn't blame people for grabbing some of the cash flying around.

- ## Has anybody built a social network for rich people yet?
- https://twitter.com/sebastienlorber/status/1357606986066653185
  - It would only work on the very latest, most expensive iPhone.
  - You'd have to buy new hardware every 6 months to prove you are wealthy
- [I Am Rich](https://en.wikipedia.org/wiki/I_Am_Rich) is an iOS application developed by Armin Heinrich and which was distributed using the App Store.
  - I Am Rich was sold on the App Store for US$999.99 
  - The application was removed from the App Store without explanation by Apple Inc. the day after its release, August 6, 2008

- ## Singapore is pretty great¹ for indie hackers
- https://twitter.com/swyx/status/1355099275252785153
  - No corporate tax up to $100k/yr
  - No sales tax on Int'l Services (incl digital goods)
  - No auditor needed <$1m
  - Took 30 mins and $300 to register co and open bank account!
- Estonia is pretty damn good too and no local residency requirement (I think you can get around it in Singapore, but they're obviously not as keen as Estonia)
- i dont think CXO title is meaningful for companies under 50 people
- Singapore corporate tax exemption is for new companies. Your first 3 years of business only. Still, it’s a nice perk.

- ## Today I'm open sourcing the code that I've made $500K off of
  - https://twitter.com/_rchase_/status/1334619345935355905
  - I want everyone to see how bad it is, 

    - and I hope it inspires someone out there who is worried that they're not a good enough programmer to be able to start a SaaS business.
    - Unfortunately, I don't have time to individually mentor everyone in my DMs
    - Good news is no one individually mentored me either

  - Hint: The next HostiFi won't be built by someone forking this and starting another UniFi cloud hosting service.

    - Start something new. Put your ideas through the meat grinder
    - I think we do well at this in our market. Unlike our competition, we don't just do IT support. 
    - We innovate new solutions and new products for our customers that even our competitors occasionally end up using (or their clients do at least)
    - you’ll be competing with dozens of others (maybe hundreds after this tweet), all racing to the bottom to be “the cheaper HostiFi”

  - I almost gave up and didn't launch HostiFi because I felt I wasn't a good enough programmer. 

    - I was trying to write it with Django and couldn't get it working, 
    - but I kept trying different things until I finally made it work with WordPress and these 2 files.

  - While I know there isn't likely a single answer here, how'd you get your initial couple dozen customers?

    - TLDR; tried lots of stuff, still doing lots of stuff. 
    - First 6 months I didn't get any organic search traffic, after that started to rank 1st page Google for relevant terms like "UniFi cloud hosting"

  - how you come up with this idea ? Have you ever been in networking field already, or faced problem with ubiquiti devices? And what your idea bring as benefits to the users ? 

    - Yes it was “scratch my own itch” 
    - I had discovered the problem because it was something I wanted to do. 
    - I was installing UniFi networks as an IT consultant and wanted to manage them all from one cloud server, but it took a while to figure out how to do it.
    - I had an IT service business on the side and was installing UniFi lots of places, 
    - it didn't make sense to me to buy a Cloud Key every time or manage multiple installs when I could centralize it to one cloud server.
