---
title: web-layout-table-blog
tags: [layout, table, web]
created: '2020-07-28T16:02:49.375Z'
modified: '2020-12-21T07:46:26.570Z'
---

# web-layout-table-blog

## Responsive CSS Table

- ### [Responsive Data Tables_2011](https://css-tricks.com/responsive-data-tables/)
- Responsive design is all about adjusting designs to accommodate screens of different sizes. 
- So what happens when a screen is narrower than the minimum width of a data table? 
  - zoom out and see the whole table, but text may be too small
  - zoom in to read, but scrolling by touch sucks
- The biggest change is that we are going to force the table to not behave like a table by **setting every table-related element to be block-level**. 
- Then by keeping the zebra striping we originally added, it’s kind of like each table row becomes a table in itself, but only as wide as the screen. No more horizontal scrolling! 
- Then for each “cell”, we’ll use CSS generated content ( `:before` ) to apply the label, so we know what each bit of data means.
- two alternative ideas that are both very cool
  - One of them makes a pie graph from the data in the chart. On narrower screens, the pie graph shows and the table hides, otherwise only the more information-rich table shows
  - The next idea is to turn the table into a mini graphic(like a thumbnail or placeholder image) of a table on narrow screens, rather than show the whole thing. This shows the user there is a data table here to be seen, but doesn’t interfere with the content much. Click the table, get taken to a special screen for viewing the table only, and click to get back.

- ### [Responsive Data Table Roundup_2012](https://css-tricks.com/responsive-data-table-roundup/)
- The idea of the original was to abandon the grid layout of the table and **make each cell its own line**. 
  - Each of those lines is labeled with a pseudo element. 
  - This creates a much taller table, requiring more vertical scrolling, but does not require horizontal scrolling. 
  - It’s easier to browse the data without losing the context of what’s what. 
  - The downside is that you might lose the context of data comparison since you no longer see cells of data right next to other cells of that type.
- Mobifreaks published a very similar idea, which uses the same layout change and pseudo element labeling. 
  - They used HTML5 `data-*` attributes for the labeling, which removes the need to have custom CSS for different tables. 
- Stewart Curry had the idea of just hiding less important columns for smaller screens. 
- Brad Czerniak has an idea he calls Rainbow Tables where on smaller screens the grid structure of the table is abandoned and the data cells are squished into each other as tight as they will go, while still being a “row”. 
  - Then instead of the data be identified by which column it is in, the data is color-coded to match a key.
- Zurb has a new technique they’ve published. 
  - It is focused on having the left-most column be sort of the “key” column. 
  - On wide screens, it’s just a normal column. 
  - On small screens, it becomes fixed/sticky to the left and the rest of the columns can scroll. 
  - This allows for row-to-row comparison.
  - it utilizes JavaScript for a bit of DOM manipulation and screen size measurement. 

- ### [Accessible, Simple, Responsive Tables with flexbox_2017](https://css-tricks.com/accessible-simple-responsive-tables/)
- The tables I find most frustrating are comparison tables or normal content layout tables, there are really no comprehensive CSS based solutions for making these types of tables responsive.
- Standard table markup seems to make semantic sense and does a pretty decent job of aligning cells. 
  - One of my main concerns was accessibility. 
  - Surely native table markup helps a user with a screen reader understand the order content should be read in and navigated through？
    - Neither CromeVox or VoiceOver tells you when you are on a table heading. 
    - The reader steps through the table via rows no matter how your content is arranged. 
- In essence, nothing in the markup tells the screen reader user if the content should be read via rows or columns.
  - The most meaningful markup still comes from non-tabular semantic content.
- Approaches for Responsive Tables 
  - Squash(挤压、挤扁): 
    - If columns have little content they might squash horizontally with no issues on a mobile screen, so not changing the layout needs to be a valid option.
  - Scroll(水平滚动): 
    - If the layout and content is exact and critical, a user could scroll to the left or right. 
    - This is trivial(不重要的；琐碎的) in CSS with an `overflow: auto` wrapper.
  - Collapse by rows(每个单元格一行，先行后列): 
    - Split each row into its own single column mini-table on small screens. 
    - Switching `display:table` into `display:block` will cause this with normal table markup.
  - Collapse by columns(每个单元格一行，先列后行): 
    - You can’t do this with normal table markup in pure CSS because the code order is by rows and the `<tr>` wrappers lock it in. 
    - We either have to change the markup or start manipulating with JavaScript.

![types of responsive tables](https://css-tricks.com/wp-content/uploads/2016/03/types-of-responsive-tables.gif)

- Not recommended ways to build a responsive table
  - Generating a second narrower table via JavaScript and hide/show alternately by breakpoint.
    - Why? Content duplication, no better than an ‘.m’ site. 
    - Will break any unique IDs inside a table. 
    - Poor idea for Styleguide driven components.
  - Using normal table markup and JavaScript at a breakpoint to rearrange the table into a responsive version.
    - Why? Requires different markup for vertical and horizontal tables. 
    - Will break any JS initialisation of table content. 
    - Requires lots of JS event listeners and DOM manipulation.
  - Keeping table markup but switch to `display:flex` for vertically aligned table content.
    - Why? Not possible to align cells across rows with `<tr>` type wrappers and `display: table-cell` overrides the flex-item.

- Responsive tables with flexbox
  - **For row-oriented tables**
    - Order markup exactly how a mobile or screen reader should read it, use semantic headers and content.
    - Abandon all concept of ‘row’ wrappers.
      - 利用的是flex-wrap和百分比宽度
      - 如果删除一个cell的数据，下面的cell会提升，最后一行cell会变宽
    - Set the width of each cell as a percentage based on number of columns or rows.
    - Auto sizing column widths is not possible.
  - **For column-oriented tables**
    - Set the flex `order` by row to instantly create a vertical table. 
      - This must be inline otherwise we would need a unique class for every row.  必须使用行内样式设置order，较繁琐
      - Fairly easy to do manually, or very easy for a CMS or JavaScript to apply.
  - Style to help make connections
    - Style cells individually in any pattern you require.
    - Fix cell border duplication with negative margins.
  - Collapse to blocks on small screens
    - In a small-screen media query, set everything to `display: block` . That gives us responsive tables!
  - Collapsing to Tabs or Accordions
    - Tab and accordion markup is inside the table in a logical position
    - Toggle either row or column depending on the cell `order`
    - Use `display: none` to toggle for both visual users and screen readers
  - Other enhancements
    - Align cell content
    - column margins
    - zebra striping
    - column spans
      - There is no way to do rowspans on a flex table. ???!!!

- You can use the same cell styling for other types of markup
  - even standard table markup
  - for list, box, etc.
- For older browsers, you can detect flexbox (with Modernizer) and show the mobile version, which is a good example of graceful degradation as fallback ui.

- ### [CSS only Responsive Tables_2012](https://dbushell.com/2016/03/04/css-only-responsive-tables/)
  - [Responsive Tables (and a calendar demo)](https://dbushell.com/2012/01/04/responsive-calendar-demo/)
  - [Responsive Tables (2)_2012](https://dbushell.com/2012/01/05/responsive-tables-2/)

- Chris Coyier presented a good idea in August 2011. His solution requires hard-coded content inside CSS, not good at all for many reasons. 
- Chris Garret has evolved the idea very recently using `data-*` attributes in HTML and the `content: attr(data-*)` technique in CSS
- Filament Group blogged a different idea in December 2011 that maintains the table appearance by reducing the columns visible. 
  - It relies on JavaScript for the interactive choice of visible columns (making it an acceptable use of standards), but again, only suitable for certain data.

- implemented the idea that I was alluding to with horizontal scrolling
- once you go block, you can’t go back! Changing the display of a table and its rows & cells to block level is a lot easier than re-implementing the table model with CSS. 
- it’s commonly advised to build responsive websites from small to large 
- I’ve found with tables it may be better to firstly have the larger traditional table version as default and use max-width media queries to scale down

- When it comes to responsive tables there is no one size fits all solution. Tables are good for housing a lot of data but on small screens data comparison is difficult because the visible real estate is very limited. There will never be a single plugin that solves this problem.
- My solution simply makes `<table>` elements scrollable and offers an optional axis flip if appropriate to the content. It doesn’t magically solve the user experience.
- Maybe a table isn’t the answer!
- The scrolling shadows act as a visual indicator for content overflow and invite scrolling. Nicer than a hard cut-off in my opinion.

- ### [Top 10 CSS Table Designs_2008](https://www.smashingmagazine.com/2008/08/top-10-css-table-designs/)
- This article will show you ten most easily implemented CSS table designs
- the general rule of thumb for styling of tables
  - Tables love space. 
    - Set the width of tables carefully, according to the content. 
    - If you don’t know the perfect width, simply set the width of the table to 100%. 
    - Tables look nicer when they have “overwidth”, and when it comes to tables too much width is definitely better than too little width.
  - Cells need some padding. 
    - Define some space between the cells, crammed up table cells are so much harder to read.
  - Treat tables the way you treat content. 
    - Tables are read similarly to the way we read text — except it’s harder and it takes more time to read a table. 
    - So be careful with the amount of contrast you are giving to your table. 
    - Use soft colors — it’s easier for the eyes.
    - Don’t treat your table like it’s a graphical decoration. 
    - Make sure that the style you apply to it makes the content more readable, not the other way around.

- Horizontal Minimalist
- Vertical Minimalist
- Box
- Horizontal Zebra
- Vertical Zebra Style
- One Column Emphasis(强调表头列，汇总列，特殊列)
- Newspaper(底边边框变浅色，其他边框用突出色或特殊样式如虚线强调阅读重点)
- Rounded Corner
- Table Background(使用图片)
- Cell Background

- ### [Table Design Patterns On The Web_2019](https://www.smashingmagazine.com/2019/01/table-design-patterns-web/)
- Tables are a design pattern for displaying large amounts of data in rows and columns, making them efficient for doing comparative analysis on categorical objects.

- If your dataset isn’t that large, and features like pagination and sorting are not necessary, then consider a css-only(JavaScript-free) option. 
  - You can get some pretty nice results that work well on a whole gamut of screen sizes without the added weight of a large library.

- do nothing
  - If your data fits in a table with only a few columns and lots of rows, then such a table is pretty much mobile-ready to begin with.
  - The issue you’d have is probably having too much room on wider screens, so it might be advisable to “cap” the maximum width of the table with a `max-width` while letting it shrink as necessary on a narrow screen.
  - This sort of a pattern works best if your data itself isn’t lines and lines of text. If they are numeric, or short phrases, you can probably get away with not doing much.

- David Bushell wrote up his technique for responsive tables back in 2012, which involved invoking overflow and allowing users to scroll to see more data. 
  - One could argue that this isn’t exactly a responsive solution, but technically, the container is responding to the width of the viewport.
  - 在出现滚动条的左右两侧添加scroll shadows，指示可滚动查看数据
    - for browsers that don’t support scrolling shadows, you can still scroll the table as per normal. 
    - It doesn’t break the layout at all.
    - 对于不支持scroll shadows的浏览器，就不显示阴影，仍可滚动
  - Another scrolling option would be to flip the table headers from a row configuration to a column configuration, while applying a horizontal scroll onto the `<tbody>` element’s contents. 
    - This technique leverages Flexbox behavior to transform the table’s rows into columns.
    - headers are always in view, like a fixed header effect
    - this technique results in a discrepancy(不一致，差异) of the visual and source order

- layout options that involving morphing the table by modifying `display` values sometimes have negative implications for accessibility, which require some minor DOM manipulation to rectify.
- If you’re working with a relatively simpler dataset, perhaps you would like to write your own functions for some of these features.

- make use of **media query** to switch the `display` property of the table element and its children to `block` on a narrow viewport.
  - On a narrow screen, the table headers are visually hidden, but still exist in the accessibility tree. 
  - By applying `data-` attributes to the table cells, we can then display labels for the data via CSS, while keeping the content of the label in the HTML
  - The original method applies a width on the pseudo-element displaying the label text, but that means you’d need to know the amount of space your label needed to begin with. 
  - The above example uses a slightly different approach, whereby the label and data are each on opposite sides of their containing block.
  - We can achieve such an effect via auto-margins in a flex formatting context.  
    - If we set the `display` property for each `<td>` element to `flex` , because pseudo-elements generate boxes as if they were immediate children of their originating element, they become flex children of the `<td>` .
    - After that, it’s a matter of setting `margin-right: auto` on the pseudo-element to push the cell’s content to the far end edge of the cell.

- Another approach doing the narrow viewport layout is using a combination of Grid and `display: contents` . 
  - Please note that display: contents in supporting browsers has issues with accessibility at the moment
  - Each `<tr>` element is set to `display: grid` , and each `<td>` element is set to `display: contents` .
  - When `display: contents` is applied to the `<td>` , td gets “replaced” by its contents, in this case, the pseudo-element and the `<span>` within the `<td>` become the grid children instead.
  - What I like about this approach is the ability to use `max-content` to size the column of pseudo-elements, ensuring that the column will always be the width of the longest label, without us having to manually assign a width value for it.
  - The downside to this approach is you do need that additional `<span>` or `<p>` around the content in your table cell if it didn’t have one already, otherwise, there’d be no way to apply styles to it.

- sprinkle on some javascript
  - paginate on table rows 
  - have some sort of indicator of which column is currently being sorted and in what order. 
  - have each input field as part of the table in their respective columns for search

- Let A Library Handle It
  - With large datasets, it might make sense to use an existing library to manage your large tables
  - The column toggle pattern is one whereby non-essential columns are hidden on smaller screens.
    - provide a drop-down menu which allows users to toggle the hidden columns back into view.
  - https://github.com/filamentgroup/tablesaw /MIT/5.4kStar/201903
    - A group of plugins for responsive tables
    - Stack Mode, Column Toggle Mode, Swipe Mode,Mode Switcher
    - no dependencies, or with tablesaw.jquery.js plugin

- which approach you pick depends heavily on the type of data you have and the target audience for that data.

- ### [Picking a Responsive Tables Solution](https://cloudfour.com/thinks/picking-responsive-tables-solution/)
- Do people use the tables to compare rows? Compare columns?
- What information is essential?
- What information do people care about the most?
- What is necessary to be able to differentiate one piece of information from another?
- Is it necessary for everything to be on the same screen or can you conditionally load additional detail as needed?

- But regardless of how many responsive tables solutions we have to choose from in the future, the way to select the right one for your project will remain the same.
- Your content will dictate the best responsive table solution. 
- You just have to ask the right questions of it.

- ### [An Idea for a Simple Responsive Spreadsheet](https://css-tricks.com/idea-simple-responsive-spreadsheet/)
- How do you make a spreadsheet-like interface responsive without the use of any JavaScript?
- First we need to add our markup for the table
  - We just have a regular ol’ table with a `<thead>` and a `<tbody>` , but we do wrap the whole table in the `table-wrapper` div
- Next, we’ll add basic styling to that wrapper element to move it into the center of the page and also give it a `max-width`
  - make sure that the `.table-wrapper` has `overflow` set to `scroll`
- Now we can add styles for the first column of our table and the thead element as well as basic styling for each of the table cells
- The problem here is that we’ve now made a pretty inaccessible table; although we can scroll around in the spreadsheet we can’t read which column or row is associated to which bit of data.
- `position: sticky` lets you stick child elements to their parent containers so that as you scroll around the child element is always visible. 
- And this is exactly what we need here for the first column and the heading of our table element.
- This `z-index` values are important here because we want the header to overlap the first left hand column that will also be sticky
- A simple responsive spreadsheet where you can view both the heading and the first column no matter where you are in the table. 
- `position: sticky` has relatively patchy support right now and so it’s worth thoroughly testing before you start using it

## collection-blog-table

- [accessible responsive table](https://www.accessibility-developer-guide.com/examples/tables/responsive/)
- [Responsive HTML Table Techniques & Examples](https://speckyboy.com/responsive-html-table-techniques/)
  - Horizontal Scrolling
  - Collapsible Cells with Repositioned Table Headers
  - Static Left Table Headers with Horizontal Scrolling
  - Element Queries
