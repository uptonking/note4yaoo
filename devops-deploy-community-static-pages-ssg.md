---
title: devops-deploy-community-static-pages-ssg
tags: [deploy, static-site-generator]
created: 2026-06-17T05:41:18.985Z
modified: 2026-06-17T05:57:03.299Z
---

# devops-deploy-community-static-pages-ssg

# guide

# cloudflare-pages
- pros
  - free
  - built-in ddos protection
  - unlimited number of preview deployments active on your project
  - Pages site can be managed by an unlimited number of users via the Cloudflare dashboard

- cons
  - ?

- notes
  - 100 deploys per day limit and a 25 MB per file limit

- [Limits · Cloudflare Pages docs ](https://developers.cloudflare.com/pages/platform/limits/)
  - 1 concurrent build
  - 500 Builds per month, 16.7 builds/day
  - 100 custom domains
  - Pages sites can contain up to 20, 000 files
  - maximum file size for a single Cloudflare Pages site asset is 25 MiB
  - A _redirects file can have a maximum of 2, 000 static redirects and 100 dynamic redirects
  - a soft limit of 100 projects within your account in order to prevent abuse

- [Especially when Cloudflare Pages is free with unlimited bandwidth, if you don't ... | Hacker News _202511](https://news.ycombinator.com/item?id=45931329)
  - Cloudflare Pages is free with unlimited bandwidth, if you don't need any other backend. The only limit is 100 custom domains and 500 builds per month in their CI/CD, the latter of which you can bypass by just building everything in Github Actions and pushing it to Pages.
# github-pages
- pros
  - free

- cons
  - ?

- notes
  - bandwidth limit of 100 GB/mon

- [GitHub Pages limits - GitHub Docs ](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits)
  - GitHub Pages is not intended for or allowed to be used as a free web-hosting service to run your online business, e-commerce site, or any other website that is primarily directed at either facilitating commercial transactions or providing commercial software as a service (SaaS). 
  - only create one user or organization site for each account
  - Pages source repositories have a recommended limit of **1 GB** . 
  - Pages sites have a soft bandwidth limit of **100 GB** per month.
  - Pages sites have a soft limit of **10 builds per hour** . This limit does not apply if you build and publish your site with a custom GitHub Actions workflow.
  - Pages deployments will timeout if they take longer than 10 minutes.
  - In order to provide consistent quality of service for all GitHub Pages sites, rate limits may apply. you might receive an appropriate response with an HTTP status code of 429, along with an informative HTML body.
# vercel-deploy
- pros
  - ?

- cons
  - ?

- notes
  - ?
# pages-free
- netlify
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-free/awesome
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [How much traffic can Cloudflare's free plan handle? : r/CloudFlare _202410](https://www.reddit.com/r/CloudFlare/comments/1g17a6y/how_much_traffic_can_cloudflares_free_plan_handle/)
- One of my websites on Cloudflare’s free plan got DDoS’d and received over 1.4 billion requests without any issues so you should be fine with pretty much any amount of traffic!
  - Zero downtime and 99.9% of the requests were blocked/cached too!

- Cloudflare does not have bandwidth limits (aka caps) on self-service plans (Free, Pro, and Business). The only limitation they set is on the type of content (video and large files)
  - Cloudflare’s content delivery network (the “CDN”) Service can be used to cache and serve web pages and websites. Unless you are an Enterprise customer, Cloudflare offers specific Paid Services (e.g., the Developer Platform, Images, and Stream) that you must use in order to serve video and other large files via the CDN. Cloudflare reserves the right to disable or limit your access to or use of the CDN, or to limit your End Users’ access to certain of your resources through the CDN, if you use or are suspected of using the CDN without such Paid Services to serve video or a disproportionate percentage of pictures, audio files, or other large files. 

- You can have a lot more traffic as a free plan, personally my website have 22k daily visitors, and I know people that have a lot more (all on the free tier). So you dont have to worry about anything.
- Cloudflare recently defended against a 3.8Tbps DDOS attack, and let me tell you, that's a lot of traffic.

- 250k daily visits on my static site and never had a downtime.
  - I use netlify + Cloudflare DNS with Cache everything rule and never had to pay for anything. 8 terabytes bandwidth a month for free.

- There are limits in other areas (don't quote me on specifics - I'm going based on memory):
  - DNS - free accounts can not have more than 3000 records
  - File Upload Size (Max): 100 MB  
  - Cloudflare Pages: 500 builds per month

- ## [Where should I host my Blog — Cloudflare Pages, Vercel, Netlify? : r/webdev _202602](https://www.reddit.com/r/webdev/comments/1r5a89w/where_should_i_host_my_blog_cloudflare_pages/)
- You’re fine on Cloudflare. Pages isn’t just static anymore, you can pair it with Workers and Nitro actually has a Cloudflare preset so SSR works too.
  - If it’s mostly a blog, you can even prerender most routes and keep only API stuff on Workers. That keeps it cheap and fast.
  - Ads monetization won’t care where you host as long as you’re serving over HTTPS and not blocking their scripts. Vercel and Netlify are solid too, but for a Nuxt.js blog Cloudflare Pages + Workers is a pretty good.
- Cloudflare Pages supports SSR with Nuxt (via Nitro), so your backend will work. Just make sure you're using Cloudflare's edge runtime for serverless functions. For ads monetization, there shouldn't be issues, but test your ad scripts after deploying since edge environments can sometimes be picky with third-party code.
- For ads monetization, no issues. Cloudflare does not interfere with ad scripts. One thing worth knowing early: Pages has a 100 deploys per day limit and a 25 MB per file limit. For a blog neither should matter.

- One of the plus sides is if everything is pre-rendered, it'll be WAY faster. People seem to forget connecting to db, pulling data, converting it to html in a high-level language, and sending it down the wire is way more expensive and an order of magnitude slower than loading pre-built html from disk (or disk cache!!) and sending it down the wire.
  - Cached dynamic pages are not that slower, if they are cacheable, as they would be if it is a blog.
# discuss-paid
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
