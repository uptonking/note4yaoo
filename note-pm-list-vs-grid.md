---
title: note-pm-list-vs-grid
tags: [comparison, list-grid]
created: '2020-09-25T16:41:20.596Z'
modified: '2020-09-25T16:46:17.782Z'
---

# note-pm-list-vs-grid

## summary

- 参考因素
  - 需要展示的内容中文字的多少，数据大小
  - 用户在每个项目的思考时间、停留时间
  - 滚动距离长短
  - 实现排序和过滤操作的难度
  - 多选
  - 列或单元格自定义显示的可扩展性
  - 具体业务常识，如地图上的poi标记
- Tables are good when:
  - Horizontal space is not a limitation.
  - All data columns are of equal or unknown importance.
  - sorting and filtering are much more native to a grid structure than to tiles. 
- Lists are appropriate when:
  - There is a useful hierarchy to the data that will be displayed.
  - Opinionated data arrangement (that’s what I call your lists) establishes a hierarchy of data and makes more flexible use of space. What we now widely refer to as “cards”
  - In this case, users are looking for a known structure and priority of information and the presentation can aid their evaluation.

## list vs grid (Card vs Tabular)

- ### [Tabular vs Card-based presentation, which is better for lots of data?](https://ux.stackexchange.com/questions/98167/tabular-vs-card-based-presentation-which-is-better-for-lots-of-data)
- Comparison is very easy in the tabular format because it enables vertical scanning (i.e. find the lowest price). 
  - In the card format comparison requires more effort, because data are mixed.
- Long free text is very difficult to read in the tabular format and also increases the row width. 
  - Card format enables you to display text in a much more readable format.
- Too many columns in the tabular format creates long horizontal scrolling, which is very confusing and in-efficient. 
  - Card format may eliminate horizontal scrolling completely.
- Images are very difficult to display in tabular format, you have to create very small thumbnails. 
  - For e-commerce sites product image size is very important, small images can reduce sales. 
  - The card format does not have this limitation.
- Labels in the card format are repeated for every row, which creates more clutter(杂乱).
- Amount of data for each record: If the data includes text, images, actions then a card layout will help the user to read more easily.
- Time spent on each record: It basically correlated with the data you are showing. If user spends time thinking about each record a card might be more valuable. But an overview of many items is what table is for.
- Sorting & Filtering: Since data is neatly kept in columns for grid layout, column level filtering is easier for grid layout. So if user wants to quickly rummage through a huge dataset a grid is more suitable.
- Multiple selection: Does the user work on multiple records at the same time? Like selecting many to copy, move, delete etc. In such scenario grid is more helpful than cards.
- Flexibility: If user want to change the column options or want to tweak the way the data is displayed it is much easier to do so in grid layout, where the change is data parameters are less likely to disturb the view.
- Domain: Users mental model is suited for what kind of data. Users know Amazon and expect cards or thumbnail view in E-commerce, whereas the same user might expect long grid while visiting Gmail.
- Real Estate Availability: Business consideration to show X number of records in one screen will also impact the choice of metaphor
- Impact: A direct visual impact for each record can be achieved in cards with thumbnails or specific formatting to certain parameters of the record. That is harder to do in grid.

- ### [List vs grid: which one is right for your mobile design](https://www.justinmind.com/blog/how-to-prototype-mobile-ui-patterns-for-real-users-part-2/)
- The grid. It’s characterized by a set of cells. 
  - Those cells are divided by columns and gutters. 
  - Typically, the grid is used to divide the screen space into equally-sized cells which makes navigation easier to understand. 
- The beauty of the grid is how customizable it is and how much order it can give to your designs. 
- Other benefits of the grid include:
  - Makes efficient use of space and structure
  - Grids can offer visual harmony
- The list is unlike the grid in that this navigation pattern simply consists of one element following another whether alphabetically, numerically or even randomly.
  - They’re great for letting the user flow from the top to bottom when using a vertical scrollable menu. 
  - The list can come in many different disguises like the product list above or even drop down menus. 
- Lists take up less space than a grid so are a good option if your content is text-heavy.
- Other benefits to lists include:
  - Great for efficient scanning
  - Perform better when there’s less screen space
- Grids are a useful tool for bringing logical structure to your design. 
  - with the prevalence of responsive web design and prototyping, grids are now taking up the entire screen. 
  - When it comes to displaying cards or designing a task-based mobile app, a grid can really help you here.
- When it comes to consuming content, however, the grid is less useful because the large structure doesn’t afford the designer much space to use additional content.
  - The list, on the other hand, is in its element when it comes to browsing and consuming content
  - If you take a minimalist approach to displaying your content, then a grid is going to do wonders. 
  - However, if you have a lot of content to show then a list is going to help you present comparatively more content and, surprisingly, more visual elements in the overall UI design.
  - List is best for presenting homogeneous(同类的) data type

- When scrolling, Grid takes up the entirety of the screen. 
  - This is a great way to emphasize the navigation because it’s clear and obvious and the bold use of imagery adds to the ease of use. 
  - And each block of the grid has a good amount of content for the user to digest
  - grid isolates blocks of related content in a condensed way.
- List allows for easier scanning with multiple links traveling down the page. 
  - In our list, it’s easier to read all of the important information including navigational links because the list presents the information in a coherent way – one link after another. 
  - When it comes to using a list, it’s good practice to have ample spacing between links so as to avoid unwanted clicks. 
  - You want to create menu links which are big enough to be easily tapped or clicked.

- In the grid above, the view is more appealing to the eye and helps users when examining visual distinctions between items with images.
  - Although, it should be noted that this style of grid view can create longer pages forcing the user to scroll more than they might want to.
- Everything in our list above is ordered well and is easy to understand.  
  - There is more detail involved – price, rating, distance, location, date and name. 
  - The list is great when you need to be more comprehensive because your users have to make decisions and need relevant information.
- In essence, the grid is useful when you don’t need to give the user much information (for example, on Asos.com where users only want to look at the clothes and see how it looks on a model). 
  - When you don’t need to give out more crucial information, then a list is your best bet because the user is making a decision based on more intricate factors than solely appearance alone.

- ### [Grid View vs List View for products](https://ux.stackexchange.com/questions/60412/grid-view-vs-list-view-for-products)
- In conclusion, Grid view for similar products (where you make your decision by the appearance of the product). 
- List view for products with different (and important) information and/or specifications.

- Ultimately the decision to use list view versus grid view should be aligned with your overall mobile strategy and what is most valuable to your users.
  - If they value seeing additional information about products like discounts and ratings, you should consider using a list view.
  - If your customers prefer to quickly swipe and see as many options at a glance as possible, you should go with the grid view.
  - The key is providing optimized mobile experiences that meet your mobile customers’ unique needs.

- ### [List or Grid, It Is Not Important](https://uxplanet.org/listview-or-gridview-it-is-not-important-b767d20ec05e)
- List view has space for many textual elements such as title, description and reviews. It helps users make a decision based on detailed information.
  - Put the most important element on the left and vice versa.
- Grid view is about images. Try to limit the textual elements along with the images.
  - Making some space around the grid can help users receive information easily.
- Most of the time, users prefer list view when they are searching with specific requirements while they love grid view for exploring.
- To sum up, when a relatively serious decision needs to be made, people prefer to know some details about an item before they click/tap on it.
- List view has more space. Does that mean we can add textual information as much as possible? The answer is no. Users can easily get overwhelmed by all kinds of information
- These days, allowing users to switch between list view and grid view seems old-fashioned. However, it is still nice to do. 
  - Depending on the purpose of every page, you pick a default view. 
  - For example, on the search result page where users are looking for a specific item, display list view as the default view.
- Make the best of list view and grid view, and do not put an equal amount of information on them. 
  - Otherwise the grid view will end up too long and you lose the value of having both views available. 
  - Users will find themselves which view is better for their needs and learn about the advantages of each view.
- Regardless of which view you are using, display items that attract users most on the top.

- List view provides users a format that follows their natural reading patterns like the F-shaped pattern, 
  - while grid view is a little more interruptive, making it best suited for visual content. 
  - You can jump from one image to the next without worrying about order or continuity. 
  - It's all about discovery and just seeing everything.
- As usual, it all comes down to "content is king."
