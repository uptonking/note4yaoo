---
title: tech-testing-mock
tags: [mock-api, testing]
created: 2021-08-12T20:21:02.816Z
modified: 2021-08-12T20:21:51.264Z
---

# tech-testing-mock

# guide

- mock示例：react-jwt-authentication-example/react_base_auth
  - 采用的思路都是在应用入口执行configureFakeBackend(), 拦截window.fetch

- mock
  - mock的主要使用场景是测试，而不是切换app的测试环境
  - 应用自身常常存在很多请求处理的其他逻辑和中间件，所以不一定要在全局实现mock和test，将更多的精力放在测试重要的场景
# blogs

## [Choosing a JavaScript testing framework: Jest vs. Jasmine vs. Mocha_202205](https://mattermost.com/blog/comparing-javascript-testing-frameworks/)

- Jest’s primary use is strong front-end testing. 
  - Its main goal is to be a zero-config framework, which it achieves by being built on top of one of the other frameworks we’re looking at today: Jasmine.
  - Jest also pairs well with React apps. It’s the main in-house framework for JS testing with React at Facebook. 
- Jasmine, is great for both front-end and back-end testing. 
  - Jasmine’s front-end suite works better with Angular than it does with React. 
  - Jasmine is one of the oldest frameworks in the JavaScript community and has been a stable anchor for JS testing.
- Mocha is probably the most flexible of the three. 
  - The main problem with Mocha is that it has more dependencies than the other two frameworks. 

- Final Thoughts: Selecting Your Javascript Testing Framework

- Jest, optimally paired with React, is best for front-end development, 
  - but it isn’t ideal when paired with convoluted backend systems that require lots of dependencies.
- Jasmine is optimally paired with Angular. 
  - It’s best used on complex backend systems that require a stable testing suite but might not be suitable for tough front-end frameworks that require lots of UI testing. 
- Mocha, the most flexible of the three, is best when paired with simple projects and simple tests, 
  - but isn’t as strong in more technically complex projects where Jest or Jasmine would be a better fit. 

- [Mocha vs Jest Comparison of Testing Tools in 2022](https://www.blog.duomly.com/mocha-vs-jest/)

- Jest is designed to be simple and straightforward, while Mocha has more options and can be more difficult to learn.
- Jest is also faster than Mocha. It has built-in support for snapshot testing, which means tests are run automatically on each change to the code. This makes it easy to keep your tests up to date as you work.
# discuss
- ## fetch-mock mocking all requests
- https://stackoverflow.com/questions/41868698
- I'm using fetch-mock in order to mock some requests to the server.
  - But not only this endpoint is being mock, but all the requests made with isomorphic-fetch
- The problem is caused because fetch-mock's main goal is to help with testing. 
  - In a test environment, it's better if you get an exception for any non-mocked calls being dispatched.
- The library used to have an option for that but it was removed in V5. 
  - This has now been replaced by a .catch() method which accepts the same types of response as a normal call to .mock(matcher, response). 
  - It can also take an arbitrary function to completely customise behaviour of unmatched calls. 
  - It is chainable and can be called before or after other calls to .mock(). 
  - The api to check for unmatched calls remains unchanged.
- Since fetch-mock v.6.5 there is a new config property called fallbackToNetwork that allows you to control how unhandled (unmatched) calls shall be handled by fetch-mock
# examples-fake-fetch-mock
- https://github.com/wheresrhys/fetch-mock
  - http://www.wheresrhys.co.uk/fetch-mock/
  - 依赖 lodash、querystring、whatwg-url、node-fetch
  - Mock the fetch() global to return a fake response obj
  - v7(2018), v8(2019) & v9(2020) are practically identical, only differing in their treatment of a few edge cases, or in compatibility with other libraries and environments.
- https://github.com/grug/data-mocks
  - 依赖 fetch-mock、xhr-mock
  - Library to mock local data requests using Fetch or XHR
  - Library (written in TypeScript) to mock REST and GraphQL requests
- https://github.com/marmelab/FakeRest
  - Intercept AJAX calls to fake a REST server based on JSON data.  
  - Use it on top of Sinon.js (for XMLHTTPRequest) or fetch-mock (for fetch) to test JavaScript REST clients on the browser side (e.g. single page apps) without a server.
- https://github.com/typicode/json-server
  - Get a full fake REST API with zero coding in less than 30 seconds (seriously)
- https://github.com/mswjs/msw
  - Seamless REST/GraphQL API mocking library for browser and Node.js.
  - https://github.com/stordco/msw-toolbar
    - a little utility package that helps toggle between your mocks + a real API. 

- https://github.com/Matsuuu/Bulle /202011/ts
  - Bulle is a modern solution for mocking HTTP API's.
  - Bulle will start a fastify HTTP server to serve the endpoints, and provide a CLI interface for monitoring requests.

- https://github.com/fiverr/react-fetch-mock-provider
  - wrapper around fetch-mock, that provides a more React-friendly interface.
- https://github.com/mbugerald/react-requests-fetch
  - 只依赖fetch-mock; 
  - 实现了 const [response, setRequest] = useRequestFetch(url)
  - a ReactJS target library for handling http fetch requests considering bia-directional stateless and stateful data extraction. 
  - The same logic and parameters used when performing http requests using the fetch api are kept, with the difference in flexibility as to how data is retrieved. 

- https://github.com/skidding/react-mock /201903/inactive
  - 无依赖
  - Declarative mocks for React state and global APIs.
  - Now I don't think mock state is a good testing method.
  - We should follow the testing-library principles.

- https://github.com/nock/nock
  - HTTP server mocking and expectations library for Node.js

- https://github.com/tusharjo/mockme
  - MockME is an app where you can mock and store your own API calls and use those calls wherever possible while development phase.
# examples-mock-react
- https://github.com/HarveyD/mock-api-react
  - 结构非常标准，基于express模拟api
# ref
- [Stop mocking fetch](https://kentcdodds.com/blog/stop-mocking-fetch)
  - 更多的是作为msw的宣传
