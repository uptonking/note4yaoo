---
title: lib-net-api-openapi-swagger
tags: [api, network, openapi, swagger]
created: 2023-02-06T09:11:08.598Z
modified: 2023-02-06T09:14:21.143Z
---

# lib-net-api-openapi-swagger

# openapi
- OpenAPI 规范（OAS）是一种通用的、和编程语言无关的 API 描述规范，使人类和计算机都可以发现和理解服务的功能，而无需访问源代码、文档或针对接口进行嗅探。正确定义后，使用者可以使用最少的实现逻辑来理解远程服务并与之交互。
  - OpenAPI 始于 Swagger 规范，Swagger 规范已于 2015 年捐赠给 Linux 基金会后改名为 OpenAPI，并定义最新的规范为 OpenAPI 3.0。
# swagger

## [swagger跟openAPI不同](https://blog.csdn.net/fanzhongcang/article/details/102695534)

- OpenAPI 3.0是该规范的第一个正式版本，因为它是由SmartBear Software捐赠给OpenAPI Initiative，并在2015年从Swagger规范重命名为OpenAPI规范。
- OpenAPI =规范
- Swagger =实现规范的工具
- Swagger工具集包括开源工具，免费工具和商业工具的组合，可在API生命周期的不同阶段使用。
  - Swagger编辑器：使用 Swagger编辑器，您可以在浏览器内的YAML中编辑OpenAPI规范，并实时预览文档。
  - Swagger UI： Swagger UI是HTML，Javascript和CSS资产的集合，这些资产从符合OAS的API动态生成精美的文档。
  - Swagger Codegen：允许在给定OpenAPI规范的情况下自动生成API客户端库（SDK生成），服务器存根和文档。
  - Swagger Parser：用于从Java解析OpenAPI定义的独立库
  - Swagger Core： Java相关的库，用于创建，使用和使用OpenAPI定义
  - Swagger Inspector（免费）： API测试工具，可让您验证API并从现有API生成OpenAPI定义
  - SwaggerHub（免费和商业）： API设计和文档，为使用OpenAPI的团队而构建。
# jsonapi
- [JSON: API — A specification for building APIs in JSON](https://jsonapi.org/)

## 🆚️🧩 [JSON API, OpenAPI and JSON Schema Working in Harmony _201809](https://medium.com/apis-you-wont-hate/json-api-openapi-and-json-schema-working-in-harmony-ad4175f4ff84)

- 🧩 JSON API
- JSON API is a specification written with the goal of being an anti-bikeshedding tool for writing JSON APIs.
  - JSON API is one of many data formats that is often applied to REST (or RESTish) APIs, as an alternative to Siren, HAL, Uber, etc.
- The goal of JSON API is to standardize some of the specifics of API design that the REST paradigm leaves to the implementer. 
  - REST has no opinions on how you implement resources vs collections, or where meta data should go, how to include related resources, how pagination should work, or anything else, so JSON API tries to fill in a lot of those gaps for you.
  - Firstly, JSON API explains what shape the body of the HTTP request and response should take. Specifically, where primary data goes, where meta data goes, where should links to other resources be placed, and how exactly should related data be included.
  - Sparse Fieldsets, compound documents, pagination, filter
- All of this is basically very structural, but none of it tells you anything about what the data is, or anything about the data. 
  - There is no “schema” functionality (or types, as some folks call them). 
  - For that, you need to look at something like OpenAPI, or JSON Schema.

- 🧩 OpenAPI
- OpenAPI aims to describe both the service model (the API in general), endpoints, request metadata like headers, authentication strategies, response metadata, etc., 
  - and it also covers the HTTP request/response body using a bunch of keywords based on JSON Schema

- 🧩 JSON Schema
- JSON Schema aims to describe an instance of JSON data, like the ones found in a HTTP request or response, but is in no way limited to a HTTP API.
- In describing the data, you can say which fields are required, mention common formats like email, UUID, etc., add more complex validation rules to those fields like maximum length, or regex patterns

## 🆚️ [OpenAPI vs JSON: API - Stack Overflow](https://stackoverflow.com/questions/64828587/openapi-vs-jsonapi)

- OpenAPI's goal is really to provide a full description on how your API can be called, and what operations are available. 
  - JSON: API gives you a strong opinion on how to structure it.
  - You can use OpenAPI to describe API's, and JSON: API is a standard to structure your apis. 
  - If you use JSON: API, you can still use OpenAPI to describe it.

- Think about it as OpenAPI is a “Data Format” and JSON API is a “Data Contract”.
# webhook vs api

## [APIs vs. Webhooks: What’s the difference?](https://www.mparticle.com/blog/apis-vs-webhooks/)

- An API (Application Programming Interface) enables two-way communication between software applications driven by requests. 
- A webhook is a lightweight API that powers one-way data sharing triggered by events. 

- An API is like a portal through which information and functionality can be shared between two software services. 

- A webhook can be thought of as a type of API that is driven by events rather than requests. 
  - Instead of one application making a request to another to receive a response, a webhook is a service that allows one program to send data to another as soon as a particular event takes place.
  - Say for instance you want to receive Slack notifications when tweets that mention a certain account and contain a specific hashtag are published. 
  - Instead of Slack continuously asking Twitter for new posts meeting these criteria, it makes much more sense for Twitter to send a notification to Slack only when this event takes place. 
  - This is the purpose of a webhook––instead of having to repeatedly request the data, the receiving application can sit back and get what it needs without having to send repeated requests to another system.

## [Webhook vs. API: differences + when to use each | Zapier](https://zapier.com/blog/webhook-vs-api/)

- APIs open the door to back-and-forth communication between software applications via requests
  - App A requests information from App B, and App B decides whether to send the information.
- A webhook is a type of event-driven API. 
  - Rather than sending information in response to another app's request, a webhook sends information or performs a specific function in response to a trigger—like the time of day, clicking a button, or receiving a form submission. 
  - Since the application sending the data initiates the transfer, webhooks are often referred to as "reverse APIs." 
