---
title: pm-community-ugc-content-sensitive
tags: [community, pm, sensitive, ugc]
created: 2022-09-27T00:14:13.302Z
modified: 2022-09-27T00:15:28.972Z
---

# pm-community-ugc-content-sensitive

> 关于内容审核

# guide
- 按敏感类型
  - 涉黄
  - 涉政
  - 涉恐
  - 版权

- 按内容类型
  - 文字
  - 图片
  - 视频
  - 音频
  - 直播流
  - 嵌入资源/外链
# discuss

## 

## 

## [国内大部分平台并没有明令禁止接入GPT，但对最终输出结果做内容监管。](https://twitter.com/easychen/status/1640537601785597958)

- 我升级了之前开源的openai proxy，加上了文本安全审核，支持「按句子流式审核」，效果见视频。
  - 应该是目前效率和体验最好的方案了，做国内业务的同学可以收藏一下
- 一提到内容审核一些人就又高潮了，问题是OpenAI自己也做内容审核啊，也把接口拿出来卖呢，区别只是中国美国的敏感词不同而已。快去联合AI推翻人类啊 👋
  - [Moderation API Reference - OpenAI API](https://platform.openai.com/docs/api-reference/moderations/create)
- 敏感词过滤用的哪个仓库呢
  - 直接对接的腾讯云的服务，自己搞词库维护更新很麻烦…

## [UGC网站的内容审核管理是怎么做的？](https://www.zhihu.com/question/20661252)

- 内容的重点程度，决定了审核的侧重点如何分配。
  - 一个新闻发布系统，则新文章需要经过相对严格的人审
  - 淘宝也可以假拟为一个UGC网站，商品上架偏重于机审、人审为辅
- 审核不是目的，只是手段。
  - 需要通过额外的体系，刺激用户发布不违规的内容，以体现其在站内的价值最大化。如网站的ranking、首页曝光、用户社区虚拟价值等

- 一是用户分级，把工作重心放在风险更高的用户群上；
- 二是内容过滤系统与时俱进，能搞定文本、图片、视频、音频等；
- 三是分级处理，比如视严重程度决定禁言还是封号，既达到惩戒的效果，又不影响 UGC 内容生产积极性。
- 四是积累数据，用来训练机器，让算法更加准确。不管用户特征的准确分析，还是内容性质的精准识别，数据的积累都是非常重要的，比如网易云反垃圾系统，基于20年反垃圾特征数据沉淀及云计算资源，海量垃圾特征实时更新，才能为网易云音乐、网易新闻等业务快速过滤各种有害信息。

## [B站有没有可能采取豆瓣模式？（以规避审查）？](https://www.zhihu.com/question/550440738)

- b站近年来因番剧延迟播出、内容删减而广受诟病，如果认为b站相对于其他播放源的优势在于弹幕和评论环境，是否可以像豆瓣只提供弹幕而没有播放源？
  - 具体而言可以搭建一个在线实时互动的外挂弹幕，用户自行寻找在线播放源（各种网站）。技术问题应该不难解决，版权和政策问题参照豆瓣，那是否有这种可能？

- 问题在于你愿意为这套模式付费吗？延迟播出也好，内容删减也好。有多少人愿意为了一个外挂插件消费大会员呢？

- 既然资本选择了陈睿，且可以选择陈睿，说明b站坚定的导向了商业最大化
  - 那么b站的未来只会是更多的用户（海外），更垄断的地位（长短视频延伸），更高的收益（广告，游戏，电商，会员，直播，投资）
  - 没有平台可以规避审查，豆瓣被关了多少小组了，只是时间问题。就算你服务器在海外，也能屏蔽或者直接定为违法，和几个浏览器公司安全公司合作屏蔽或报毒，方法有的是。
