---
title: toc-data-api
tags: [api, data, datasource]
created: 2020-07-12T13:13:27.939Z
modified: 2020-11-11T13:16:24.994Z
---

# toc-data-api

# metadata

- https://github.com/open-metadata/OpenMetadata
  - https://open-metadata.org/
  - Open Standard for Metadata. A Single place to Discover, Collaborate and Get your data right.
  - OpenMetadata is an all-in-one platform for data discovery, data lineage, data quality, observability, governance, and team collaboration. 

- https://github.com/GeoNode/geonode
  - GeoNode is an open source platform that facilitates the creation, sharing, and collaborative use of geospatial data.
  - 
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
# api-toy
- hacker news api
  - https://github.com/HackerNews/API
  - https://hacker-news.firebaseio.com/v0/item/8863.json?print=pretty

- imdb-movie

- [前端需要的免费在线api接口](https://juejin.cn/post/7041461420818432030)
  - 返回100条数据，每条内容都有帖子 ID、发贴人 ID、标题、以及简介。
    - http://jsonplaceholder.typicode.com/posts
  - 每次请求都会随机返回一张猫的图片。
    - https://api.thecatapi.com/v1/images/search?limit=1
# cn-no-auth
- [天气JSON API，不限次数获取十五天的天气预报](https://www.sojson.com/blog/305.html)
- http://t.weather.itboy.net/api/weather/city/101030100
  - 不能使用ajax，必须后端语言，比如 Java、PHP、C#，PY等。 注：Android，iOS 之类直接调用，我发现后会封掉，建议后端调用。

- ## [中国天气网-气象大数据平台-test-key](http://www.weatherdt.com/help.html)
- 预报接口调试
  - http://api.weatherdt.com/common/?area=101160901|101160801&type=forecast&key=fd034bf8fe70289698ec4ea79876feaa
  - 响应结果全是编码，难以理解

- ## [V2EX API 接口](https://www.v2ex.com/p/7v9TEc53)
  - 默认情况下，每个IP每小时可以发起的 API 请求数被限制在 120 次
- 最热主题，相当于首页右侧的10条热点内容。
  - https://www.v2ex.com/api/topics/hot.json
- 最新主题，相当于首页的“全部”下的最新内容。
  - https://www.v2ex.com/api/topics/latest.json

- ## [干货集中营API v2文档](https://gank.io/api)
- 获取文章所有子分类
  - https://gank.io/api/v2/categories/Article
- 获取干货分类下Android子分类的10个随机文章列表
  - https://gank.io/api/v2/random/category/GanHuo/type/Android/count/10

- ## more
- https://github.com/yuyang2016/Chinese-Free-API
  - 已停更
- https://github.com/fangzesheng/free-api
  - 统计了网上诸多的免费API，有些接口来自第三方，在第三方注册就可以成为他们的会员，免费使用他们的部分接口。

- ## toy-api

- [kieng api 视频、音乐、IP、其他类型的API接口](https://api.kieng.cn/)
- 随机一句话
  - https://api.kieng.cn/inaword

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
# ww
- https://github.com/public-apis/public-apis

- the widely known Hacker News API 
  - https://hn.algolia.com/api
  - This API is built on top of Algolia Search's API. 
  - It enables developers to access HN data programmatically using a REST API. 
  - This documentation describes how to request data from the API and how to interpret the response.

- https://github.com/mdn/data
  - There's a top-level directory for each broad area covered: for example, "api", "css", "svg". 
  - Inside each of these directories is one or more JSON files containing the data.
