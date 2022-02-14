---
title: thread-pm-kickstarter-devops-xp
tags: [kickstarter, marketing, pm, thread, xp]
created: '2021-08-16T06:54:23.073Z'
modified: '2021-10-29T15:05:56.151Z'
---

# thread-pm-kickstarter-devops-xp

# discuss

- ## 

- ## 

- ## SaaS 公司的价值: 说实话，即便是我们做了一套很牛的软件产品，也就是“一把不错的铁锹”，卖铁锹给别人，别人挖出来金矿和我们没有任何关系。 我们还是一个卖铁锹的。
- https://twitter.com/ThaddeusJiang/status/1492133196087308289
  - 卖铁锹的，怎么能跟客户的营收有关系呢？我们可以考虑加入到行业的业务层面，帮助客户一起找金矿。给客户挖金矿的方法或者一起运营金矿的业务，这样才能和客户一起分享挖出来的金矿。
  - 等挖金矿的人多了，卖铁锹也赚钱啊。这就相当于做基础设施建设，Figma 还有国内的 Moka 就属于这一类，也赚得钵满盆溢啊。不过你得根据挖金矿的人的需求升级，得做自动挖矿铁锹， 不能一直做铁锹。

- ## I'm going to keep working on @tldraw . I'll be raising money in the new year to build a team and build an open-core platform for spatial canvas apps.
- https://twitter.com/steveruizok/status/1468630460305747977
- Turns out everyone like an infinite canvas. 
  - I'm convinced that many of the next great products will be built on "design tool" paradigms—zoomable canvas, direct manipulation, and real-time multiplayer collaboration.
- Bad news: these types of applications are incredibly hard to develop! 
  - Especially for the web, where there are vanishingly few resources and trade-offs everywhere. 
  - It takes a team of experts—and there just aren't enough experts.
- Good news: spatial UI apps are 90% identical, with hundreds of "table stakes" features and services that can be abstracted away, so that a team focus on their domain problems instead of getting stuck on selection logic, arrow binding, or alignment snapping.
- What do you mean by spacial UI? 
  - This one is also sometimes called a "zoom ui", or "infinite canvas". Think miro / mural / figma, etc.

- ## Startup idea. Get really good at state machines. Use them to solve a difficult problem. Sell the solution
- https://twitter.com/mpocock1/status/1469329372691808263

- ## Let’s talk about funding for open source projects, specifically my thoughts for @tldraw .
- https://twitter.com/steveruizok/status/1469978436257169410
  - I get about $2, 000 a month from GitHub sponsors. 
- First off, I like open source for lots of reasons, some more ☭ than others, but the value game is all wrong. 
  - Companies are making millions off of passion projects or casual labor—that’s neither fair nor sustainable.
- For me, open source has been a way of sharing what I like to do, raising my profile as a developer while also sorta paying down some privilege. 
  - It’s great to connect with other “prosumers”, collectively producing the product that we want to use.
- tldraw is my first major open source project, insofar as I’m really building it to be used by other teams; 
  - but, like anything serious, it’s too big to do “on the side” without sacrificing the project’s quality or my own happiness.
- And while GitHub Sponsors has been a great way to help fund it’s early development (thank you) that money doesn’t remotely compare to the salaries I’ve turned down to work on it.
- I see a few options:
- 👉🏻️ 1. Sell time as a consultant for teams using the library. 
  - For me, that would mean taking contacts with teams who need help integrating tldraw or building certain features which I would solve via the open source project.
- 👉🏻️ 2. Build a product around the core library and monetize that product. 
  - For me, this would be the tldraw engine (open) and the tldraw whiteboarding app (open core with new paid services for teams, etc).
- 👉🏻️ 3. Raise VC money and hire a team to work on the project and related products of services, with the goal of gaining wide adoption. 
  - For me, that would mean making tldraw the react/firebase of spatial uis, ie the default dev option, selling things like multiplayer.
- 👉🏻️ 4. Find a corporate sponsor that will hire me to work on the project. 
  - Ideally keep ownership of the project, in case things don’t work out and I decide to pivot to other options.
- 👉🏻️ 6. Get acquihired by a company that does not want to maintain the project, but where I could work on similar problems within the company’s own products. 
  - Not the worst ending for me, but death for the open source project.
- 👉🏻️ 5. Double down on individual contributions. 
  - Focus on content, start putting out YouTube videos, Twitch streams and farm sponsorships. Go very wide.
- They’d all have trade offs, either in my own time, my freedom to set priorities myself, the value I’m able to extract for myself, or the possible scale of the project.
  - Of all, the most comfortable would be acquisition by a company who wants to build on the project, or where it’s success would align with its other business goals.
  - The least comfortable would be relying on sponsorships (content is hard!). Contracting isn’t too far ahead, though I think I could make it work.
- Raising money would mean more pressure to build the product into a business though ideally with a longer runway than doing so myself, and a more ambitious goal with more people involved, and more likelihood of success.
  - It’s pretty hard to strategize! And many conflicting priorities.

- Have you considered selling the product? Replicache uses the bsl license, is developed in the open, like open source and becomes true open source after two years. We don’t have concrete data on how well this works but early signals are good and it directly reflects your goals.
  - I think this is compatible with raising money. The difference I’m getting at is compared to (2): instead of giving away the core and selling something else (a service), just sell the core directly.
- 
- 

- ## Unpopular opinion: an SQLite SaaS would be my pick for anything slow/write fast/read scenario (blogs to name one). Not sure why nothing exists already out there
- https://twitter.com/WebReflection/status/1476586199251058689
- Can you tell me how important SQL part is, or do you technically need Firebase infra with option to send SQL? Or maybe SQL is not important?
  - any NoSQL library out there looks like knex but is not standard ... which is why I believe SQL is extremely important but, on top of that, I have mentioned SQLite, not any SQL, strictly, truly, SQLite as a remote service that any static page *could* access: no Server needed.
- But if you are using it as SaaS you'd just be using SQL to it, so from your POV there'd be no difference to using some other db like postgresql at the back? (modulo the dialects etc). Same local dev + prod is Hundred points symbol tho. SQLite at lambda/cloudflare workers would be 

- ## I repeat, this is a 100% true story that isn’t about open source but gives a good idea about what it’s like to maintain an open source project. 
- https://twitter.com/slicknet/status/1430334633611202562
  - A lot of people suggest a lot of changes to open source projects not understanding that there is a maintenance cost to every new line of code added.
  - The person coming up with the idea thinks that it’s great because they aren’t the ones that have to maintain it.
- But I think maintainers should teach those who are willing to contribute to the project cause it's easy to suggest but hard to implement so maybe having the right guideline on how the project works and all that can help.

- ## This summer marked four years of working full-time on my own business(Tailwind UI)
- https://twitter.com/adamwathan/status/1296447318074568704
  - Here are some of the things I believe the most strongly about making a living as an independent maker
- The best way to build an audience is to simply be helpful on the internet. 
  - Give people a reason to pay attention to you, and keep your signal to noise ratio high. 
  - Better to tweet 4 good ideas per week than 10 useful ideas + a bunch of BS about how Starbucks screwed up your order.
- Giving away your work for free is like compressing a spring that releases when you finally put something up for sale. 
  - The longer you do it, the more energy is released. 
  - Steve and I compressed the Refactoring UI spring for over two years. 
  - It made $1, 000, 000 in the first month.
- Marketing doesn’t have to feel gross. 
  - Sharing what you’re working on, writing about the behind-the-scenes process, and documenting hard problems you’ve solved is all marketing, 
  - and people are *excited* to see that sort of stuff, not put off by it.
- Marketing a product after it’s released is way harder than marketing it before you launch. 
  - You need to start marketing at the very beginning, when all of the exciting development is happening and you have lots of interesting things to share.
- Ignoring people who are critical of your work is not “creating an echo chamber”, it’s building a community. 
  - You wouldn’t tell Slayer to write songs for the people who don’t like Slayer. 
  - Find the people who love what you’re doing and spend your attention on them, ignore the rest.
- **Analytics are overrated**. 
  - I’ve never once made a decision that was informed by open rates or traffic sources. 
  - In fact Tailwind UI has no website analytics at all. 
  - Doing great work has always been a more efficient lever for me.
- Build real friendships, not a “network”. 
  - People who want to help you > people you ask to help you. 
  - I’ve never had to ask anyone to help promote my work.
- Work in public. 
  - Tailwind only exists because a bunch of people seemed excited about some boring CSS files I was using when I was live-streaming some work on a completely different project. 
  - I never would have seen the potential on my own.
- Always think long-term. 
  - Early in my entrepreneurial career, I made a lot of short-sighted decisions about time-limited deals, and other urgency/scarcity based marketing strategies. 
  - It made me look like a scummy internet marketer and I will never do that again.
- Pick a “business hero” and ask yourself “would they do this?” whenever you’re trying to make a tough decision about a marketing tactic. 
  - For me it’s Basecamp. 
  - Lots of decisions feel hard for me to make for myself, but are obvious when I ask myself “what would Basecamp do?”
- “Early access” doesn’t have to be cheaper, in fact you can easily make the argument for making it more expensive. 
  - If I wanted to early access to the unmastered recordings of a new album I was looking forward to would that be cheaper?
- A landing page is the last step in validating an idea, not the first. 
  - Put your ideas out there as tweets, articles, videos, conference talks, etc. first and see what people are excited about. 
  - A landing page takes you from 90% confidence in an idea to 95%, not 0% to 100%.
- Compete on quality. 
  - There are tons of people writing blog posts, making screencasts, open sourcing libraries, etc., but very few people making stuff that’s really *great* from end-to-end. 
  - Forget the 80/20 rule when it comes to putting out projects. Go the full 100.
- Stand out by doing the hard work that everyone else is too lazy to do. 
  - For example, @reinink was the 1000th person to write a tutorial on the Eloquent ORM, 
  - but he was the first person to bite off the really *hard* problems and do the grueling work to come up with good answers.
- Learning is more important than your ego. 
  - I ask for help about dumb shit on Twitter all the time, no one thinks I’m stupid and I have grown 100x as a result. 
  - I literally started a podcast just to get people to explain things to me that I didn’t fully understand.

- discussion

- Making money as the first goal was the worst mistake I made in life. Just like you said, people need to be given the result of real work and polished. Thank you, man!
- Here's an honest question: How did you not break financially while developing your own products? Freelancing?
  - I wrote my first book over a three month period just evenings and weekends, and was fortunate enough that the launch made enough money for me to quit and start working on the next thing 
- Could you share the process and tools you used to write your first book please?
  - I wrote it all as one giant markdown file in Sublime Text, then compiled the markdown to HTML with a few custom scripts and turned the markdown into PDF with PrinceXML and a custom stylesheet.
- In case it’s helpful Matthew, I’ve started using ASCIIDoc for my ebooks as it has converters to PDF in most languages. 
