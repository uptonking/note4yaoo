---
title: thread-pm-pieces
tags: [pm, thread]
created: '2021-04-19T14:52:23.297Z'
modified: '2021-04-19T14:52:58.244Z'
---

# thread-pm-pieces

> new features for pm

# pieces
- ## 

- ## 

- ## 

- ## 

- ## The word2vec service cost $10 to upload 2.7M 1kb files to GCS. 
- https://twitter.com/tomlarkworthy/status/1422945919419523073
  - But then it's about $0.03 a month to run. 
  - If you can avoid the complexity of a database, do so. 
  - Cloud storage services like S3 and GCS are rock solid scalable Key-Value stores, (ab)use them.
- So easy to geo-replicate, scale out (CDN), and cache (HTTP cache), migrate (rsync) etc. 
  - I love a services built on keyed files. 
  - So much tooling can be applied, and the reliability is so much higher than regional DBs. 
  - Of course, big minus, they only have prefix querying.

- ## How do you test your startup ideas before you commit to them?
- https://twitter.com/panphora/status/1422210617369268232
  • A twitter thread?
  • An email to friends and family?
  • Cold calling potential customers?
- I’d assume someone within my network could be a potential customer. I’ll treat them like a fresh customers and ask corresponding questions. Test if the idea is valid based on a good amount of conversation, maybe 25, maybe 50.
- Website with a waitlist and paid advertising. We'll use the click through metrics to determine interest. It's the most reliable way to understand if what you're building actually resonates with customers via action not words.
- Make a MVP using nocode within a week

- ## Notion has a solid ecosystem, it’s not an overnight success.
- https://twitter.com/felix12777/status/1421300363999682563
- They’re empowering makers to:
  1️⃣ Make money from templates
  2️⃣ Fully customize their workspace
  3️⃣ Be proud of being a user
  4️⃣ Leverage user-generated-content 
- Total agreed. When Notion lauched @NotionAPI . They have been truely done their slogan: "Notion for Everything". Everyday when I open Notion, I always feel so lucky when humans got a product like this.

- ## What the most difficult aspects of building a JAMStack app today?
- https://twitter.com/flybayer/status/1421121549315280902
- Not being able to use (a reasonably priced) Postgres DB w/ NextJS-on-vercel
- Blog list page.
  - I want to collect the list of mdx posts along with their metadata export that I have in one folder. 
  - But Nextjs doesn't provide a route list so I need to write a separate script to do that.
  - You still need a server side function to grab the metadata and the list of slugs, but it is doable.
  - Even I have one working implementation in my site which I stole from Radix docs. I needed this because I export meta objects from mdx files instead of frontmatter but it has some caching issues.
- Probably auth
  - Can't really do sessions unless you've got a real backend so you're gonna be managing JWT's or some kind of token
  - Lack of many good libraries
  - Lack of frameworks with auth opinions
  - Of course Redwood handles all three of these problems but not everyone's using Redwood

- ## 2010s - New Javascript framework every week; 2020s - New Kubernetes PaaS every week
- https://twitter.com/flybayer/status/1421210855295889410
- Currently using Render. I don't want to touch Kubernetes
  - Im hearing it’s really good for static hosting. If your solution does not require the features of Kubernetes it’s best to use something simpler.

- ## A change I don't know if all developers are ready for is that over time, most/all code will be purely "boring" business logic at most companies, with the non business logic increasingly factored out into pure SaaS companies
- https://twitter.com/fulhack/status/1418588422990614535
- This has become so clear to me after joining Wikimedia, where we (except with rare exceptions) don’t use SaaS products or third party vendors. 
  - For privacy and transparency reasons, we are open source all the way down to our own servers in data center.
  - We don’t buy our way out of problems, we engineer our way out. 
  - It comes with its own costs and benefits.
- I think that is part of the reason Google has not created any new breakthrough product since Chrome (everything big since then has been acquired). Their moat was hardcore CS skills and that has been commoditized to a large degree.
  - My conspiracy theory is they mostly try to create a talent monopoly and employ them on fake projects to prevent anyone from creating a competitor
- With low-code apps like @getLogicLoop even business logic will be in the hands of operators and analysts in SaaS tools
  - I am very skeptical of this. Once you get past a certain amount of "logic", code is the best way to express that logic
- IMO, All the "boring" business logic will be converted from a rule-based logic to ML-driven in all the SaaS companies. If a company keeps writing "boring" business logic, it's a high signal to leave the company.
  - Correction: I should've used all the business rules will be automated instead of ML-driven.

- ## The worst part of open source
- https://twitter.com/devongovett/status/1417867860605497347
  - is when you spend months researching and developing something, release it, 
  - and other projects simply copy it rather than using and collaborating on your work. 
  - I know that’s kinda the point in some ways, but it doesn’t feel great either.
- you know what’s even worse? When they raise money for their competing product.
- Didn't you do the same with the webpack?
  - Didn't webpack do the same with browserify?
  - Parcel didn't copy stuff from Webpack, and the Webpack codebase was very very very hard to contribute to.
- Is this about react-aria and tailwind's headlessui?
  - I don't think so? I'm the Tailwind CSS community manager yet I still use react-aria and intend to contribute to the react-aria project in the future
- This is exactly what GPL and copyleft is for! Now they are required to contribute back.

- ## If you’re building a social app, you should assume by default that your idea is wrong and map out the possible pivots.
- https://twitter.com/nikitabier/status/1413392823630680071
  - Then use this pivot map to create reusable building blocks (such as the friendfinder, invites, onboarding system). 
  - It will save you months, if not years.
- Ok loser. Best is to build one app that just works and then acquired by fb (the “fast sellout, no morals” way)

- ## I think there is something in the water with document creation.
- https://twitter.com/chriscoyier/status/1412881853959266304
  - Notion & Coda & Cover & Slite & Craft & Nuclino
  - See also: Confluence, Slack
- is Gutenberg the OG of the slash approach?
- we call it "cards" and it's going to change everything
- For science, here’s Quip
- I’m building a note editor and I cannot wait to build this UI too

- ## do you know any interesting examples of people making money from "tools for developers"?
- https://twitter.com/Wattenberger/status/1412408988319236108
  - https://trianglify.io/
  - I'm thinking of, eg. a generative art tool that lets you export svg patterns for a small fee. 
  - Really anything infinitely scalable that isn't ads and keeps the tool partly free
  - another one that comes to mind is tinypng, which has a freemium api for compressing images. although it's not exactly infinitely scalable, with hosting costs. I know @JoshWComeau experimented in this space with Tinkersynth (which I loved!) it didn’t really work for me in terms of being profitable, but I also didn’t really put in the work / give it a solid test.
- Tools are a harder straight sell than educational resources: most companies will have budgets for education that devs can spend on books or subs, but not as easy to spend on tools.
- I’ve recently had some success with http://tldraw.com, which is sponsorware; but that’s more about supporting the content I make around the app (as entertainment?). Access to the app is a pretty sweet perk tho!
- I love the sponsorware model, but I think it's hard to scale up, and I have a tendency to procrastinate if there's any pressure on me 
- not quite an answer, but back when we were making a WebAssembly data science notebook env, we deliberated (反复思考，深思熟虑) about how to commoditize(商品化) the complement. I've found it to be a good mental model for the monetizing-devtool pattern (which is a tough space to be in)
  - [Laws of Tech: Commoditize Your Complement](https://www.gwern.net/Complement)
- Usually, things like SVG pattern and color palette generators, code explainers (https://domevents.dev), etc. are free. 
  - Seems like a tough market to charge money in. 
  - However, I've seen them used as funnels into a product that is for sale (includes a link to a book, course, etc.)
- Not entirely pattern-driven or generative, but @blushdesignapp offers highly modular, randomizable illustrations for free.
  - 2x, 3x PNGs and SVGs are (paid) pro features.

- ## 不同频道在相同的时间可以有不同的广告 
- https://twitter.com/vixvix/status/1411762345957863425
- 长知识了，怪不得我看到欧洲杯都是支付宝和抖音
- 现在不都是虚拟广告牌了吗？赚钱最大化
- Real time live rendering
- Sportsvision, 根据场上相机焦距/角度等参数计算出来的实时AR效果, 现在已经应用非常广泛了, 似乎最开始是NFL显示虚拟首攻线先使用的
- 由于广告牌是固定的，转播方在不同地区使用不同的滤镜，类似于在照片上增加呢一个图层。但这仅限于画面中固定不动的目标，像球员衣服上的广告在直播的时候就做不到这一点。另外，所谓的直播会比实际的比赛延迟几秒钟，这几秒钟用于计算滤镜处理的缓存时间。
- 这个技术开始超出认知了，本届欧洲杯转播已经全面实现了么？这个比东京奥运会研究什么16K可牛X多了

- ## Does any static site generator have a market for themes and/or people that sell themes for it?
- https://twitter.com/rauschma/status/1410627179772354565
- https://themeforest.net/search/gatsby

- ## 宇树科技推出了面向普通消费者的机器狗，售价1.6万~2万人民币，天猫现在就能预订，10月之前发货。
- https://twitter.com/ruanyf/status/1410769253972647939
  - 这个机器狗能够自主跟随和避障，有强大的保持平衡能力，跌倒可以爬起来。价格只有波士顿动力公司同类产品的十分之一

- ## What are some visual application builders for the web where you only have a limited range of built-in components but they’re all high-level (e.g. grid/list that can bind to data)? Like Access+VBA but for today
- https://twitter.com/dan_abramov/status/1410342969786486786
- Some listed here - Airtable is the closest match to Access
- Retool, they basically advertise themselves as VBA but in the context of the cloud + browser + JS
- @builderio is! Specifically our "components-only mode"
- http://openchakra.app
  - Components are limited to those available in the source library, and styling options are limited to those tokens found in the theme
- I wanna say https://editorx.com. You get collection components (grid, list, repeater) which you can bind to data. You can even add buttons, select events, and it will create and bind empty fns - just like VB of yore.
- I used to use @xojo for software development. It has it's own flavor of VB, has a good community, and is pretty good!

- ## kind of want to start a consultancy where someone describes their data in detail and i recommend which visualization techniques are appropriate, 
- https://twitter.com/tmcw/status/1409317416665026563
  - this should exist, at least someone should do this. 
  - just narrowing down the appropriate types would do so much good in the world.
- Unfortunately it’s usually the other way round… “hey, we really want this cool data visualization to communicate the data”. Plot twist: there is no data. 
- You should get paid just to find every time someone tries to put a 3D pie-chart into a PowerPoint and tell them no

- ## 家具定制怎么没有低端定制的，
- https://twitter.com/waylybaye/status/1409321600663441415
  - 比如我只需要用 iPhone 的 LiDAR 扫一扫房间，App 自动生成房间 CAD 图，AI 自动生成装修方案，用户选一个后，下单到工厂，工厂用最便宜的合成板加工出家具，寄给用户。年轻人租房也能拥有品质不低的生活。
  - 大家需要吗，需要的话我回老家菏泽搞一个，菏泽到处都是家具厂，500块，不，200块就能搞一个定制大柜子
- iPhone测量不精确，留条缝或者塞不下都很尴尬
  - 低端定制要求什么严丝合缝
  - 然后就会发现iphone扫出来的尺寸差了2厘米，柜子放不进去白做了。
- 最大的问题在用户身上，这个测量设计的误差因为用户原因可能会很大。不可靠因素太多了。
- 家具定制都是派人上门用手持激光测距仪测量各种尺寸的。。别的不准。。
- 年轻人根本不需要订制，买预制就好了，反正是租房说不定还能搬下一个房子，何苦要订制？
- 淘宝上的标化成品家具，闲鱼的二手家具，宜家这种环保性好一些的一次性家具，都是面向租房市场的解决方案。
- 库克看了你这条推文马上就整个Apple Furniture
- 定制的生产成本比规模化生产更高，哪怕用最便宜材料定制，也不见得比普通材料的量产成本低，所以订制只能走高端的
- 目前你在淘宝能买到的家具，就有很多菏泽货，这就是零售能做到的最低价。而且不含定制成本。
  - 如果你能做到比什么维莎、原始原素等大型低端品牌价格更低，那必然是超过马斯克的商业奇才。
- 室内装修一般都是这样的，都是上门去丈量定做。我觉得没你想的这么简单，虽然实现的方案是可行的，我觉得。

- ## “自动合影机”，可以挑选自己喜欢的体育明星合影。
- https://twitter.com/ruanyf/status/1408412534474874883

- ## This riderless bike took about four months to be made and it's almost totally open source[hardware and structure on github]
- https://twitter.com/Rainmaker1973/status/1406207562924630016
  - 自动行驶的自行车
  - http://www.pengzhihui.xyz/
- Clearly it's the wow factor. I actually found riding adult sized tricycles less stable than bicycles. 
- Good for people with no arms or the blind.

- ## Unpopular opinion: reproducible presentations (e.g., R Markdown Xaringan, Jupyter Rise, etc) are easier than WSWYG ones (e.g., Powerpoint, Keynote)
- https://twitter.com/TiffanyTimbers/status/1404823614596128768
  - I don't stand by this 100% of the time, but I do most of the time. When do I choose a WSWYG presentation tool? When there is no analysis involved, & for short, one-off presentations. 
- I have never used WYSWYG because I learn LaTeX before I needed to write my first presentation. Always LaTeX (reports, presentations, posters, journal articles, ...), with knitr if data analysis is involved 
- IMHO best is very background dependent. In general, only a small fraction of my presentations relate to actual results, while most is background and implications. I do like Rmarkdown for automatic analysis updates or standard analysis templates.

- ## Automatically fill your Notion database from events on your website.
- https://twitter.com/splitbee/status/1401872538393796612
- [Splitbee Automations: Write to Notion](https://splitbee.io/blog/notion-support-in-automations)

- ## Life as a developer in 2021
- https://twitter.com/dabit3/status/1400804133158989825
  - Current tech company: you’ve done an excellent job this year, here’s a 4% raise.
  - Developer’s email inbox: here are 700 offers for 200% of what you’re making in your current role.
  - Amazon: you’re in the top 5% of the entire company, nice work comrade.
- I'm not a developer yet, but I work in IT and this is exactly what happened. I'm getting a 20k a year raise with the new job I'm about to start, and my current company refuses to even give raises. I'm also in an area where the talent is extremely hard to find lol. Oops
- Someone I know was recently promoted to Principal Engineer and it came with a whopping 4% raise. The company's also really stingy with their equity, so I wouldn't be surprised if the 4% was itself 100% of the increase.

- ## we kind of had webmail before 2004, but webmail didn't become A Thing until gmail. 
- https://twitter.com/Rich_Harris/status/1395548128087003146
  - browser-based IDEs are about to become A Thing, with all that entails (security, live collab, zero install, etc)
- I don't think StackBlitz is the final word here — 
  - they've basically just invented a new market (previous browser IDEs were more tech demo than useful product, IMHO, at least once you get beyond building toys)
- Cloud9, Github Codespaces, etc. all seem like full-featured products that have been used by people who preferred browser-based development, but apparently they remained niche(市场定位；生态位). The only difference I see here is better offline support, and... idk if it's enough.
  - I mean, it's definitely cool, and I like this idea as well as all the IDEs before it, but don't see what changed drastically market-wise.
- biggest difference i see is that the browser run everything, instead of being a thick client for a proprietary backend. (but yeah, not sure what node brings here other than npm ecosystem compat).
- The drastic change is in the performance you can expect from a local runtime vs a server you're sharing with a bunch of other people in who-knows-what region. I've generally found cloud IDEs unusable, latency/perf wise

- ## I've been thinking a lot in the last few days, how a code editor/IDE focused on React could looks like. So it brings me to this
- https://twitter.com/danilowoz/status/1393212141122031621
  - 在行号左边有一列操作拦，可以拖拽移动一行代码
  - https://codesandbox.io/s/ide-concept-ke6vz

- ## Just use @splitbee and make your analytics dashboard public
- https://twitter.com/peduarte/status/1390930597942636544
- https://app.splitbee.io/public/mxstbr.com
- Sorry to hijack this convo, but are there any docs or examples for A/B testing with @splitbee ? 
  - I'm struggling to find some I'm happy with Plausible but willing to give Splitbee a go for A/B testing!
- I think Splitbee looks great, but in case you missed you can make your Fathom analytics public too

- ## Product GIFs are your best friend.
- https://twitter.com/heyblake/status/1389725794063331333
  - If you have a SaaS or DTC product, show don't tell. Give us action shots.
- Don't really use GIF, though. 
  - Video formats tend to be more efficient at playing video, and you can achieve the same look and feel with the right HTML markup (most GIFs platforms use mp4 videos under the hood).

- ## What are your thoughts on-sponsors-only (Sponsorware) open source and npm packages?
- https://twitter.com/giuseppegurgone/status/1389833727564451845
- How would that be different than non-oss paid products?
  - I think you'd be better off talking about it as a product people can buy (including the source) than calling it sponsorware. 

- ## Unpopular opinion but true: Google Docs blows chunks for user experience.
- https://twitter.com/gruber/status/1386764214874824706
- Word: "90% of users use 10% of the features"
  - Docs: "here's 10%"
- Try Google Sheets on an iPad. It’s a whole different level of WTF.
- Sometimes worse is better. Google Docs does low-friction collaboration better than anyone -- just send them a URL. 
  - iWork can run it 60fps and be fluid AF, but if you need to pick a random stranger to collab with, good luck.
  - I use Keynote 4 my own prezos, but Docs for collab.
- The entire G-suite is terrible. I've replaced everything with standalone apps where I can -- sadly no good solution for GDocs.
- Try using Microsoft Sharepoint and you'll come crawling back
- Funny, we experienced completely the opposite at work.
