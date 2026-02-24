---
title: toc-data-api
tags: [api, data, datasource]
created: 2020-07-12T13:13:27.939Z
modified: 2020-11-11T13:16:24.994Z
---

# toc-data-api

# guide

- tips
  - 相比较免费，api的稳定更重要

- free-api-faq
  - [有哪些好玩的免费的API接口? - 知乎](https://www.zhihu.com/question/32225726/answers/updated)
  - [国内有哪些类似如百度apistore 的平台？ - 知乎](https://www.zhihu.com/question/47541137/answers/updated)
  - [前端常用免费API接口汇总 - 掘金](https://juejin.cn/post/6844903982276542478)

- https://github.com/fangzesheng/free-api /markdown 
  - 统计了网上诸多的免费API，为您收集免费的接口服务，做一个API的搬运工

- 聚合api平台
  - https://www.apifox.cn/web/main
  - [免费API调用-免费数据块下载-聚合数据](https://www.juhe.cn/vip)
  - [天行数据TianAPI](https://www.tianapi.com/vip.html)
  - [百度API商城，只能购买一次](https://apis.baidu.com/)
  - [阿里云API市场](https://market.aliyun.com/data)
  - [果创云 YesApi.cn](http://www.yesapi.cn/)
  - [接口大全-免费API, 收集所有免费的API](https://www.free-api.com/)
  - [免费API - 免费接口调用平台](https://api.iwyu.com/)
  - [星辰API - 提供免费接口调用平台](https://collect.xmwxxc.com/)
# api-toy
- hacker news api
  - https://github.com/HackerNews/API
  - https://hacker-news.firebaseio.com/v0/item/8863.json?print=pretty

- imdb-movie

- [JSONPlaceholder - Free Fake REST API](http://jsonplaceholder.typicode.com/)
  - 返回100条数据，每条内容都有帖子 ID、发贴人 ID、标题、以及简介。
    - http://jsonplaceholder.typicode.com/posts
  - 每次请求都会随机返回一张猫的图片。
    - https://api.thecatapi.com/v1/images/search?limit=1
  - [前端需要的免费在线api接口](https://juejin.cn/post/7041461420818432030)
# cn-no-auth
- [kieng api 视频、音乐、IP、其他类型的API接口](https://api.kieng.cn/)
- 随机一句话
  - https://api.kieng.cn/inaword

- [V2EX API 接口](https://www.v2ex.com/p/7v9TEc53)
  - 默认情况下，每个IP每小时可以发起的 API 请求数被限制在 120 次
- 最热主题，相当于首页右侧的10条热点内容。
  - https://www.v2ex.com/api/topics/hot.json
- 最新主题，相当于首页的“全部”下的最新内容。
  - https://www.v2ex.com/api/topics/latest.json

- [干货集中营API v2文档，invalid](https://gank.io/api)
- 获取文章所有子分类
  - https://gank.io/api/v2/categories/Article
- 获取干货分类下Android子分类的10个随机文章列表
  - https://gank.io/api/v2/random/category/GanHuo/type/Android/count/10

## 天气类

- [天气JSON API，不限次数获取十五天的天气预报](https://www.sojson.com/blog/305.html)
- http://t.weather.itboy.net/api/weather/city/101030100
  - 不能使用ajax，必须后端语言，比如 Java、PHP、C#，PY等。 注：Android，iOS 之类直接调用，我发现后会封掉，建议后端调用。

- [免费天气API接口|天气预报接口|全球天气API接口|气象预警|空气质量](https://www.tianqiapi.com/)

### [中国天气网-气象大数据平台-test-key](http://www.weatherdt.com/help.html)

- [【手把手教你】如何获取中国天气网，获取想要城市的天气-图文并茂-分析代码 - 掘金](https://juejin.cn/post/7140859507730546695)

- 预报接口调试
  - http://api.weatherdt.com/common/?area=101160901|101160801&type=forecast&key=fd034bf8fe70289698ec4ea79876feaa
  - 响应结果全是编码，难以理解

- [气象大数据平台](http://www.weatherdt.com/)
  - 平台为注册用户提供免费数据产品集试用，为期一个月，小于1万次调用，每个注册账号可购买一次。

## 快递物流类

- [快递鸟api】](https://www.kdniao.com/membership)

## more

- 百度OCR的API是免费的

- https://github.com/yuyang2016/Chinese-Free-API
  - 已停更

- [味分享数据](https://www.liangmlk.cn/)

- [自己实现的免费开放接口API](https://blog.csdn.net/c__chao/article/details/78573737)
- 新实时段子
  - https://api.apiopen.top/getJoke?page=1&count=2&type=video

- [WHOIS信息查询](https://swho.cn/api/document)

- 非官方 api
  - https://github.com/search?o=desc&q=%E9%9D%9E%E5%AE%98%E6%96%B9+api&s=updated&type=Repositories

- ## deprecated-api
- 豆瓣非官方api
  - https://github.com/zce/douban-api-docs
  - https://douban-api-docs.zce.me/
  - 全部需要apikey，已经无法使用
# cn-auth
- [美团餐饮开放平台openAPI文档](https://open.waimai.meituan.com/openapi_docs/)
# covid-19
- https://github.com/BlankerL/DXY-COVID-19-Crawler
  - https://lab.isaaclin.cn/nCoV/
  - 上次更新于202004
  - 由于接口压力较大，自2020年3月19日起，本接口以停止返回时间序列数据，可以直接通过数据仓库获取时间序列数据。
- 全国疫情概览
  - https://lab.isaaclin.cn/nCoV/api/overall
- 返回湖北省疫情最新数据
  - https://lab.isaaclin.cn/nCoV/api/area?latest=1&province=湖北省
- 返回中国全部城市及世界其他国家疫情最新数据
  - /nCoV/api/area?latest=1
- 返回与疫情有关的谣言以及丁香园的辟谣。
  - /nCoV/api/rumors?page=1&num=10&rumorType=1(返回第2页可信信息，每页10条)
- https://github.com/ExpDev07/coronavirus-tracker-api
  - https://coronavirus-tracker-api.herokuapp.com/
  - Currently 3 different data-sources are available to retrieve the data:
  - JHU
  - nyt
  - csbs

- https://github.com/disease-sh/API
  - https://disease.sh/docs/#/
  - https://disease.sh/v3/covid-19/all
  - API for Current cases and more stuff about COVID-19 and Influenza
- https://github.com/mathdroid/covid-19-api
  - https://covid19.mathdro.id/api
  - Serving data from John Hopkins University CSSE as a JSON API
- https://github.com/covid19india/api
  - https://api.covid19india.org/v4/min/data.min.json
  - Aggregated sheets provide aggregated data at the ~~district~~/state levels in csv format.
- https://github.com/amodm/api-covid19-in
  - COVID Rest API for India data, using Cloudflare Workers

## open-data-not-api

- https://github.com/CSSEGISandData/COVID-19
  - https://systems.jhu.edu/research/public-health/ncov/
  - This is the data repository for the 2019 Novel Coronavirus Visual Dashboard operated by JHU CSSE
- https://github.com/pomber/covid19
  - https://pomber.github.io/covid19/timeseries.json
  - Transforms the data from CSSEGISandData/COVID-19 into a json file

- https://github.com/nytimes/covid-19-data
  - An ongoing repository of data on coronavirus cases and deaths in the US.
  - 数据全为csv

- https://github.com/owid/covid-19-data
  - Data on COVID-19 (coronavirus) cases, deaths, hospitalizations, tests • All countries
  - Updated daily by Our World in Data
  - 数据大多数是csv，少部分是json
# ww
- https://github.com/public-apis/public-apis
  - [Public APIs — A directory of free and public apis](https://publicapis.io/)
  - [A Collaborative List Of 1400+ Public APIs For Developers](https://publicapis.dev/)

- https://github.com/algolia/hn-search /MIT/202403/ruby/ts
  - https://hn.algolia.com/api
  - the widely known Hacker News API 
  - This API is built on top of Algolia Search's API. 
  - It enables developers to access HN data programmatically using a REST API. 
  - This documentation describes how to request data from the API and how to interpret the response.
  - https://github.com/HackerNews/API
    - Documentation and Samples for the Official HN API
    - In partnership with Firebase, we're making the public Hacker News data available in near real time
- https://github.com/DOSAYGO-STUDIO/HackerBook /MIT/202602/js
  - The unkillable, offline Hacker News archive, updated Weekly.
  - [I fit 22GB of Hacker News into SQLite : r/sqlite _202602](https://www.reddit.com/r/sqlite/comments/1rcmny9/i_fit_22gb_of_hacker_news_into_sqlite/)

- https://github.com/mdn/data
  - There's a top-level directory for each broad area covered: for example, "api", "css", "svg". 
  - Inside each of these directories is one or more JSON files containing the data.
