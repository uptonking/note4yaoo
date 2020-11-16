---
title: pm-list-vs-grid
tags: [comparison, grid, list]
created: '2020-09-25T16:41:20.596Z'
modified: '2020-11-16T12:43:51.117Z'
---

# pm-list-vs-grid

## summary

- 使用场景
  - 要显示的内容中图片、图表多吗，grid更适合显示图片
  - 用户对编辑功能需求的多少，grid更常用于编辑，list更常用于阅读
  - 搜索的场景更适合用list，展示给用户更详细的信息进行比较，但只包含简单数据的表格也方便比较
  - 设备与ui设计的因素
    - 桌面端常用grid，移动端更常用list

- ui布局参考因素
  - 是否要提供切换列表视图和表格视图的选项，将更多的精力花在优质内容上
  - 实现排序和过滤操作的需求和难度，grid更适合排序
  - 比较项目时，grid用于比较更直观
  - 考虑文字和图片的重要程度，若图片更重要则考虑使用grid布局，参考图片类网站
  - 若图片都相似，则考虑使用list显示文字详情
  - 考虑待展示内容中包含文字的多少、数据的大小，list更适合显示更多文字
  - 内容的结构是否是主次分明的，可以包含层次，可以突出最重要或最有吸引力的部分，list适合突出部分内容
  - search的结果更适合用list
  - 要滚动的距离长短
  - 一行或一个单元格自定义显示组件的可扩展性
  - 用户在每个项目内容上的思考时间、认知时间、停留时间
  - 具体业务常识，如地图上的格网划分和poi标记列表

- 实现细节
  - 若采用flexbox和css grid这类布局功能，浏览器执行了换行、对齐等任务，优点是减少了开发者的工作，缺点是对于实现复杂内容的显示和布局，不够灵活，但大多数的需求都是不那么复杂的，要根据具体情况权衡得失

- Tables are good when:
  - Horizontal space is not a limitation.
  - All data columns are of equal or unknown importance.
  - sorting and filtering are much more native to a grid structure than to tiles. 

- Lists are appropriate when:
  - There is a useful hierarchy to the data that will be displayed.
  - Opinionated data arrangement (that’s what I call your lists) establishes a hierarchy of data and makes more flexible use of space. What we now widely refer to as “cards”
    - In this case, users are looking for a known structure and priority of information and the presentation can aid their evaluation.

## list vs grid (Card vs Tabular)

- ### [UI cheat sheet: list vs grids](https://uxdesign.cc/ui-cheat-sheet-list-vs-grids-48151a7262a7)
- Grid is usually (but not always) better for desktop, while list is better for mobile.
- If your user is in browse mode, they are there for entertainment so will probably be focused on images (Instagram, Pinterest or meme sites), on headlines/statuses (Twitter, news sites) or perhaps a combination of both (Facebook). 
  - If this is the case, bring what they are looking at to the forefront.
- If your user is in search mode, you should also support some browsing behaviour, but focus on how they will be skimming or comparing different items. 
  - You will need to identify what it is that users are using to compare items, it could be: star rating, price, amount of community engagement, images, certifications, etc. or a combination.
- Cognitive load refers to how long it takes for the brain to compute information, e.g. a single image = low cognitive load, 10 images = high cognitive load. 
  - As a general rule, when browsing, display more items at once. 
  - When searching, display fewer items at once. 
  - But this rule is broken again and again (see: Instagram and online stores) so don’t take it to heart.

- Grid views work well when you are trying to show off the image, 
  - but it also allows you to have multiple products displayed next to each other at the same time. 
  - This also helps the user to compare different items visually. 
  - The downside here is that there isn’t much space for text.
- When to use a grid view:
  - If the image of the result item is most important to the user.
  - If a user needs to be able to compare items visually (e.g. to compare shoes).
  - If your search results don’t need a description.
- Standard grid 等宽等高
  - While there are many different types of grids, the most common is a standard grid where the containers are the same height and width. 
  - A standard grid is when all the items are the same size. 
  - This grid allows all their products to be kept neat and tidy, making it easier for users to compare items.
  - Who should consider using it: Online retail stores for physical products, possibly portfolio sites (artists, illustrators, etc).
  - Why is it good: It allows users to compare product images and prices easily.
  - Who uses it: Walmart, Amazon (sometimes), Esty, most online retail stores.
- Masonry grid(瀑布流网格) 等宽不等高
  - in a masonry grid, the heights are different. 
  - This allows images to be displayed to their original proportions without being cropped to a set size.
  - However, the longer the image is in height, the more space it gets. 
  - A lot of Pinterest marketers use this to their benefit and make really long images so that they get more ‘screen time’ while the user is scrolling.
  - Who should consider this pattern: Interest and portfolio sites.
  - Pros: It encourages users to carry on scrolling.
  - Cons: It is difficult to compare items.
  - Who uses it: Unsplash, tumblr., Pinterest, and some artist/designer portfolio sites.
- Justified grid 等高不等宽
  - Unlike masonry grids, justified grids resize the images so that they fit in justified rows rather than columns.
  - This by default makes the grid look very neat, nevertheless, it lacks the scroll-more-iness of masonry grids. 
  - Who should consider this pattern: Image sites.
  - Pros: You may be able to display more images which encourages bulk comparing.
  - Who uses it: Shutterstock, Google Images, Flickr.
- Best practices for grids
  - To encourage potential buyers, consider how you can make it easier for them to compare products.
    - Using the same or similar background colours. white/plain background
    - make sure your models are in familiar poses.
  - Title length as a general rule — shorter is better for grids. 
    - 限制最大字符数
    - avoid having descriptions or anything else that will be deemed as distracting from the main focus (the image)
  - If you expect to have lots of results per screen (e.g. a big retailer) you should have more columns. 
    - If you expect to only have a few results per screen (e.g. a boutique retailer) you can have fewer columns with bigger images. 
  - Most of the sites I reviewed keep their grid on mobile, and move over to two columns, 
    - the exception was Amazon who moved over to a list view. 
    - Having smaller images in two columns allows your users to see more items at once and makes comparing easier. 

- The list view is used when the content or description is the most important thing for the user. 
  - There may or may not be an image, and if there is, it is supplementary or used to give more information.
  - Because a list item takes up all the vertical space, it means that fewer results appear on the screen at the same time. 
  - This could seem like a bad thing, but if the user is skimming the results — the fewer results on a page may help with reducing cognitive load and make for easier comparisons.
- When to use a list:
  - If your results need descriptions or supporting text.
  - If you can’t rely on your results having (decent) images.
  - If your images are all similar and need a description to differentiate.
  - If there are certain text variables that need to be highlighted.
  - If you expect some of your users to be in ‘search mode’.
  - If you want to encourage your users to compare items.
- Simple lists
  - Simple lists have very few variables displayed in them — usually just a headline and a description
  - With such a simple layout, it allows users to easily skim and compare headlines and descriptions.
  - Who should consider this pattern: Search engines and news sites
  - Pros: You don’t need to rely on specific variables
  - Cons: Because they are so simple, they can look under-designed without the proper consideration.
  - Who uses it: Google search, most news sites
- Horizontally stacked items
  - The standard layout for horizontally stacked items from left to right seems to be:
    - Image
    - Left-aligned title and description
    - Right-aligned star rating and price
  - I would only recommend this layout for non-physical products (online courses, home rentals, etc), 
  - because with physical products, users tend to only visually compare items and not their information (think of when you are buying shoes or clothes) in which case a grid is better.
  - Who should consider this pattern: online retailers selling digital products, real estate companies, tourism, and other non-physical services or products.
  - Pros: Good for skimming and comparing information.
  - Who uses it: Airbnb (desktop), Udemy, Bookings.com, Amazon (sometimes), some news sites.
- Vertically stacked items
  - Products that were designed to be ‘mobile-first’ generally have vertically stacked items 
  - Depending on the context, some sites may switch between vertically and horizontally stacked items. 
    - For example, on desktop, Airbnb is horizontally stacked, while on mobile it is vertically stacked.
  - Who should consider this pattern: Social networks
  - Pros: Works if some of the results don’t have images.
  - Cons: Can view fewer items on a screen (desktop).
  - Who uses it: Airbnb (mobile), Instagram, Twitter, Facebook
- Best practices for lists
  - Ideal line length on horizontally stacked items
    - According to Web Typography: 45–75 characters per line
  - The list with vertically stacked elements works really well on mobile. 
    - If you have a grid that is horizontally stacked, see if you can reshuffle it on mobile to stack vertically.
  - The fact that you have gone with a list and not a grid, tells me that either, 
    - a) you are relying on your users to upload images, 
    - b) images aren’t as important as the text content. 
    - So, when setting up your design rules — make sure to have a fallback/default image if it is missing

- common stylings for search results or items.
  - Skeuomorphic/elevated cards
    - Google’s standard search uses this pattern on mobile and not on desktop
    - Pros: Looks like a single unit.
    - Cons: Not great if you need to have multiple links on a single card.
    - Designer notes: Make sure your background and card colours are different as the dropshadow alone isn’t clear enough to elevate it.
    - Who uses it: Google Search (mobile), Sky News (Checked in May 2020)
  - Outlined cards
    - These guys are the nerdy cousin of the elevated cards. They work the same way — but they load a bit quicker.
    - Pros: Because it isn’t as skeuomorphic as elevated cards, users don’t expect them to act as a single unit as much and you can get away with more links in a result. Just look at Bookings.com.
    - Cons: I personally don’t find it as attractive as some of the other designs, but hey, one of the world’s biggest social network’s uses it so it must be effective, right?
    - Designer notes: Consider making your background a bit different from the card’s colour.
    - Who uses it: Facebook (desktop), Bookings.com (Checked in May 2020)
  - Flat
    - Because it is clean, simple, quick to load and puts the emphasis on the content and not the design, this style of flat list has become very popular.
    -  use white space and consistent design elements or faint lines to show separation. 
    - Pros: Clean, simple, and puts emphasis on the content.
    - Cons: Flat designs can look ‘under-designed’ without the proper graphic consideration. Just compare AirBnb and Amazon (list view) to see what I mean. Both have graphics, line separators, star reviews, etc. but AirBnb just looks more polished.
    - Designer notes: Be very considerate when choosing your background and font colours. Avoid defaulting to #000 and #fff as this can be very strenuous on the eyes. (Reference)
    - Who uses it: Google Search (desktop), Amazon, Pinterest, Airbnb, Twitter, Udemy, CNN, (Checked in May 2020)

- Closing thoughts
  - The reason I first got interested in this subject was because a team I was working with wanted to use a grid design for our online learning platform’s search page.
    - Because grids are pretty. Because images are pretty. Because text is ugly.
    - And then I walked in, guns blazing, saying that for online courses, a description is more important than having a big image (unless it is like, art classes or something) hence we needed to use a list layout. 

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
