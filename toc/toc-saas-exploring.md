---
title: toc-saas-exploring
tags: [exploring, pm, toc]
created: 2020-05-03T08:34:20.399Z
modified: 2021-05-14T14:30:22.685Z
---

# toc-saas-exploring

# guide

- [翻译服务商价格](https://doc.tern.1c7.me/zh/folder/pricing/#%E7%BF%BB%E8%AF%91%E6%9C%8D%E5%8A%A1%E5%95%86%E4%BB%B7%E6%A0%BC)
# exploring
- https://github.com/opentestimonials/opentestimonials
  - https://opentestimonials.typedream.app/
  - Collect and showcase testimonials using Airtable
  - 类似"大家都说好"的marketing

- https://github.com/soxoj/maigret
  - https://maigret.readthedocs.io/
  - Maigret collects a dossier(卷宗；档案) on a person by username only, checking for accounts on a huge number of sites and gathering all the available information from web pages. 
  - No API keys required. 
  - Maigret is an easy-to-use and powerful fork of Sherlock.
  - https://github.com/sherlock-project/sherlock
    - Sherlock, a powerful command line tool, can be used to find usernames across many social networks. 
    - It requires Python 3.6 or higher and works on MacOS, Linux and Windows.

- https://github.com/infinitered/nsfwjs /MIT/202402/ts
  - https://nsfwjs.com/
  - NSFW detection on the client-side via TensorFlow.js
  - A simple JavaScript library to help you quickly identify unseemly images; all in the client's browser. 
  - NSFWJS isn't perfect, but it's pretty accurate (~90% with small and ~93% with midsized model).
  - The library categorizes image probabilities in the following 5 classes: Drawing, Hentai, Neutral, Porn, Sexy

- https://github.com/jason5ng32/MyIP /MIT/202502/js/vue
  - https://ipcheck.ing/
  - 轻松检查你的 IP，IP 地理位置，检查DNS泄漏，检查 WebRTC 连接，速度测试，ping 测试，MTR测试，检查网站可用性，查询 Whois 信息等等
# self-hosted-appstore
- https://gitlab.opencode.de/bmi/opendesk/deployment/opendesk /apache2/202512/python
  - openDesk is a Kubernetes-based, open-source and cloud-native digital workplace suite provided by the Zentrum für Digitale Souveränität der Öffentlichen Verwaltung (ZenDiS) GmbH.
  - 集成了 Collabora, CryptPad, XWiki, Element-chat, OpenProject, Jitsi

- https://github.com/tracim/tracim /MIT+GPL/202512/python/js
  - https://tracim.fr/
  - Collaborate with your team from anywhere, intuitively and efficiently, and leverage your knowledge and files.
  - MIT for the backend, functionnal tests, docker recipes, documentation, etc.
  - 集成了 Collabora
# news/marketing
- https://github.com/liangdabiao/XHS_Business_Idea_Validator /202601/python
  - 小红书收集和分析数据来解析市场需求用户痛点及竞争格局
  - [上线了怎样使用XHS_Business_Idea_Validator-小红书解析市场机会智能体 ](https://linux.do/t/topic/1409279)
  - https://github.com/liangdabiao/Business_Idea_Validator /MIT/202506/python/inactive
    - https://liangdabiao.com/
    - 一种 AI 驱动的工具，可通过自动 Web 抓取和智能分析来验证业务概念。该系统通过分析在线讨论和生成评分验证报告来评估市场需求、竞争水平和可行性
    - 这是一款专业的商业调研应用程序，为用户提供友好的界面来：1. 验证商业创意 ， 2. 分析用户评论。 
    - [【开源】新版本：Business_Idea_Validator 小红书收集和分析数据来解析市场需求用户痛点及竞争格局 ](https://linux.do/t/topic/1407486

- https://github.com/liangdabiao/Reddit_Business_Idea_Validator /202601/python
  - Reddit 收集和分析数据来解析市场需求、用户痛点及竞争格局 深度！评论分析！用户画像！找商机！
  - Reddit 数据抓取: 自动抓取相关帖子和评论数据（使用用户输入作为搜索关键词）
  - [【开源】Reddit 生意调研Agent: 收集和分析数据来解析市场需求 ](https://linux.do/t/topic/1417660)

- https://github.com/sansan0/TrendRadar /42.7kStar/GPL/202601/python
  - 告别信息过载，你的 AI 舆情监控助手与热点筛选工具！聚合多平台热点 + RSS 订阅，支持关键词精准筛选
  - 全网热点聚合 知乎 抖音 bilibili 热搜 华尔街见闻 贴吧 财联社热门 今日头条
    - 默认监控 11 个主流平台，也可自行增加额外的平台
  - 个性化热点算法: 不再被各个平台的算法牵着走，TrendRadar 会重新整理全网热搜
  - 多存储后端支持：
    - 远程云存储：GitHub Actions 环境默认，支持 S3 兼容协议（R2/OSS/COS 等），数据存储在云端，不污染仓库
    - 本地 SQLite 数据库：Docker/本地环境默认，数据完全可控
    - 自动后端选择：根据运行环境智能切换存储方式

- https://github.com/666ghj/BettaFish /34.1kStar/GPL/202601/python
  - https://deepwiki.com/666ghj/BettaFish
  - 微舆：人人可用的多Agent舆情分析助手，打破信息茧房，还原舆情原貌
  - 构建了从 BettaFish（数据收集与分析）到 MiroFish（全景预测）的完整链路

- https://github.com/ZhuLinsen/daily_stock_analysis /MIT/202601/python
  - [[开源自荐] 基于AI的股票分析系统 _202601](https://linux.do/t/topic/1427263)
  - 起初只是自己做一个帮忙分析自选股和大盘的工具，减少盯盘、盯股票分析的精力，后面本着开源精神开源出来了，能够每天定时推送到企业微信上。
  - 用的都是免费的方案，github action + Gemini的API + Serpapi和TAVILY的检索功能，免费额度足够日常使用
  - 每日自动生成大盘复盘
