---
title: lib-fwk-nextjs-faq
tags: [faq, nextjs]
created: 2020-12-20T08:19:13.475Z
modified: 2020-12-20T08:20:38.440Z
---

# lib-fwk-nextjs-faq

# faq-not-yet

# faq-repeat

## nextjs vs react

- 主要区别
  - 最大的区别在于普通纯react应用渲染在client side客户端浏览器，而nextjs的ssr需要在服务端将数据和组件渲染出html字符串
    - nextjs的ssr渲染计算需要占用服务器资源
    - ssr的主要目的是为了seo
  - nextjs可结合使用多种开箱即用的策略，如首屏用ssr，之后用client side render
  - nextjs可配置性更强，定制更灵活

- [What is the difference between NextJs and Create React App](https://stackoverflow.com/questions/62967958/what-is-the-difference-between-nextjs-and-create-react-app)
  - Next.js on the other hand is a framework based on React to build Node.js server-side apps. 
    - This means you will use the same component-oriented logic to build pages and leverage the Next.js routing engine for page to page navigation. 
    - Server-side rendering will allow loading time to be more spread over time, so perceived performance will be probably better. 
    - Redux can be used as well but there will be some additional steps(next-redux-wrapper) to make it work properly
  - scalability depends on your choice: 
    - if you choose Next.js you will host the app on a server infrastructure which should be sized according to your audience 
    - whereas React bundle created with CRA just need to be statically hosted somewhere.
  - SSR
    - CRA doesn't support SSR out of the box.
      - However, you can still configure it.
      - It just takes more effort to setup SSR with your preferred server and configuration.
    - NextJs supports different types for SSR out of the box
      - Static generation: fetch data at build time.This works best for use cases like blogs or static websites
      - Server side rendering: fetch data and render for each requests.You have to do this when you need to serve different view for different users.
  - Configurability
    - CRA doesn't leave you a lot of room to configure it.
      - Configurations like webpack config cannot be changed unless you stray away from normal CRA way (eject, rescripts, rewired).
      - Basically, you have to use what's configured in react-scripts which is the core of CRA.
    - Almost everything is configurable.

- [What’s The Difference Between NextJS and Create-React-App?_202010](https://medium.com/frontend-digest/whats-the-difference-between-nextjs-and-create-react-app-11b55650a612)
  - While CRA is a tool for scaffolding React applications, NextJS is a framework for building React applications with features out of the box
  - Advantages of using Create-React-App
    - It's unopinionated
      - use whichever libraries you like
    - It's rendered client-side
      - Since we render Create-React-Apps on the client-side, deployment is easy.
      - You can host your application on any file host, like S3. 
      - Client rendered apps are easier to work with and easier to reason about.
  - Disadvantages of Create-React-App
    - It's hard to customize.
      - no built-in way to customize your application
      - once ejected, you have lost most of the benefits of using Create-React-App in the first place
    - It abstracts complexity.
      - Create-React-App works great until you have to do something that it doesn’t support. Then it gets hairy. 
    - It’s bad for SEO
      - should not be used for e-commerce or marketing efforts.
  - Advantages of using NextJS
    - It blazing fast.
      - Thanks to server-side rendering and static-site generation
    - It’s easy to deploy.
      - Vercel (the company behind NextJS) makes it easy to deploy
      - This includes preview deployments and production deployments.
    - It gives us API Routes.
      - If your application works with third-party APIs, you often need your own API to proxy requests and keep your tokens secret. 
      - NextJS’s API routes are perfect for this use case.
    - It’s easy to customize.
      - NextJS lets us customize our babel or webpack configuration. 
      - It’s easy to add webpack loaders or babel plugins.
  - Advantages of using NextJS
    - It’s opinionated.
      - here’s only one way of dealing with routes in NextJS, and you can’t customize it. 
      - NextJS is limited to its file-based router, and dynamic routes are only possible when used with a NodeJS server.
  - When to use NextJS
    - When SEO matters.
      - Thanks to server-side rendering, NextJS shines in this department.
    - When building a landing page.
    - When building websites.
      - Rendering our application on the server lifts the burden of rendering off of our clients. 
      - For users on slower devices, this can lead to much faster load times.
      - Web applications in general benefit less from server-side rendering. 
        - They are generally used by reoccurring users, 
        - and we can use caching to give them lightning-fast load times without the cost or hassle of SSR.

# faq
