---
title: thread-blog-pm-products
tags: [blog, pm, products, thread]
created: 2021-06-29T07:04:44.912Z
modified: 2021-06-29T07:05:13.621Z
---

# thread-blog-pm-products

# office-doc

# bi-data-tooling

## [New in Kibana: How we made it easier to manage visualizations and build dashboards_202106](https://www.elastic.co/blog/new-in-kibana-how-we-made-it-easier-manage-visualizations-and-build-dashboards?utm_content=&utm_medium=social&utm_source=twitter)

  - My hope for this post is that it helps inform the mental models of our curious power users while they attempt to learn these new dashboard creation flows.
  - By-ref vs By-value
  - A dashboard is populated with panels. 
  - Each panel has what’s known as an embeddable. 
  - Embeddables are responsible for displaying your visualization, whether it’s a chart, map, or tag cloud. 
  - In 7.11 and earlier, all visualization panels that you added to a dashboard were **by-reference** embeddables. 
  - Kibana stores by-reference embeddables as saved objects, which contain a saved object ID that is used to render the visualization in the panel.
  - Kibana stores by-reference embeddables as saved objects, which contain a saved object ID that is used to render the visualization in the panel.
  - In 7.12, you can now also add **by-value** embeddables to your dashboards.
  - By-value embeddables are NOT saved in the Visualize Library. 
  - Instead, everything that the dashboard needs to render the visualization is packaged in the by-value embeddable that is stored in the dashboard data structure. 
  - Visualizations contained within by-value embeddables only exist within the dashboard. 
  - If you compare the JSON of a dashboard with only by-value embeddables to a dashboard with only by-reference embeddables, you’d see that the dashboard with by-value embeddables contains much more information than the by-reference embeddable dashboard. 
  - In 7.12, the new flow is streamlined so you can spin up dashboards as quickly as possible. 
  - The new visualization is a by-value embeddable and only exists within your dashboard. 
  - This means you can freely edit or delete the visualization without affecting other dashboards or visualizations. 
  - This is the dashboard-first flow: if you create a visualization directly from a dashboard, you are returned directly to the dashboard with your new visualization when you select Save and return. 
# more-products
- ## 

- ## 

- ## 

- ## 

- ## [linktree: 六小时开发的工具，竟然值13亿美元？全球网红都爱 - 知乎](https://zhuanlan.zhihu.com/p/534781260)
- 2016年，一个名为Linktree的工具诞生，而它的代码，是在6个小时内完成的。
- 在Linktree上，创作者可以将Instagram、TikTok、Twitch、Facebook、YouTube、Twitter等社交平台上的内容聚合在一个链接中。
- 成立不到7年，Linktree已经累积拿到了接近6000万美元的融资，估值达到13亿美元。它的火爆也逐渐催生出了一个新赛道。
- Link in Bio的出现，源于社交媒体的局限性。Instagram等社交平台中，只有个人主页处的链接可以直接点击，而其他地方的外链只能手动复制在浏览器中打开。为了弥补社交平台中有效链接的缺失，市场上逐渐衍生出了Link in Bio功能。
- Link in Bio赛道不仅在国外打得火热，国内部分出海创业者也推出了自己的产品。结合中国用户习惯，中国版Link in Bio更多以二维码的形式出现。比如，二维彩虹推出了社交媒体二维码，可以将超过16款主流社交媒体渠道汇集在一个用户界面，点击页面按钮就可以直接跳转到对应的APP、页面或内容。
- “Link in Bio”是一种创作者数字身份管理工具，它可以帮助创作者在个人主页上添加一个有效链接。其使命在于解决单一社交媒体中自我表述空间的有限，打破平台间的隔阂。
- 除了专注于Link in Bio的创作者数字身份管理平台外，还有一些拥有多种核心产品的创作者公司也推出了类似工具。
- Link in Bio的出现打破了逐渐割裂、封闭的互联网环境。这些链接好比一个自由传送门，只要通过简单的点击，就可以实现在不同平台之间的切换。
- 但究其本质，从社交媒体中诞生的Link in Bio，它的基因先天性不足，需要依附在社交网络中生存。
- 此前，自定义裁剪照片和拼贴画应用风靡一时，后来Instagram添加了这些功能，这些APP便逐渐消失了。Link in Bio功能也面临着同样的问题。
- Instagram曾因为不允许在帖子中添加链接而备受诟病，但这也正是它成功的原因之一。但对创作者们来说，赚钱才是第一位，他们需要在这片净土中获得商机。从这个角度来看，Link in Bio并不会因为社交媒体功能的增加而失去生存空间，二者并没有本质上的冲突。
