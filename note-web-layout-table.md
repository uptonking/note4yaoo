---
title: note-web-layout-table
tags: [layout, table, web]
created: '2020-07-10T02:40:36.658Z'
modified: '2020-07-23T05:59:56.279Z'
---

# note-web-layout-table

## guide

- ref
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table
  - https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Legacy_Layout_Methods
  - [**mdn Table Reflow Internals**](https://developer.mozilla.org/en-US/docs/Archive/Table_Reflow_Internals)
  - [HTML Living Standard - table element](https://html.spec.whatwg.org/multipage/tables.html)
  - [CSS vs Tables: The Debate That Won’t Die_2009](http://vanseodesign.com/css/css-divs-vs-tables/)
  - [Why CSS should not be used for layout_2009](http://www.flownet.com/ron/css-rant.html)
  - [Why CSS Should Be Used for Layout_2009](https://www.newmediacampaigns.com/blog/why-css-should-be-used-for-layout)
  - [Slow response when the HTML table is big](https://stackoverflow.com/questions/8640692/slow-response-when-the-html-table-is-big)
  - [Are large html tables slow?](https://stackoverflow.com/questions/1364213/are-large-html-tables-slow)
  - [A Complete Guide to the Table Element](https://css-tricks.com/complete-guide-table-element/)

## faq

- table使用 `white-space: nowrap` 会增加列的宽度，如何隐藏超出列宽部分

``` CSS
td {
  border: 1px solid black;
  width: 100px;
  max-width: 100px;
  white-space: nowrap;
  overflow: hidden;
}
```

- When should you NOT use HTML tables?
  - HTML tables should be used for tabular data — this is what they are designed for. 
    - Unfortunately, a lot of people used to use HTML tables to lay out web pages, 
    - e.g. one row to contain the header, one row to contain the content columns, one row to contain the footer, etc.
  - Layout tables **reduce accessibility** for visually impaired users 
    - Screenreaders, used by blind people, interpret the tags that exist in an HTML page and read out the contents to the user. 
    - Because tables are not the right tool for layout, and the markup is more complex than with CSS layout techniques, the screenreaders' output will be confusing to their users.
  - Tables produce tag soup
    - table layouts generally involve more complex markup structures than proper layout techniques. 
    - This can result in the code being harder to write, maintain, and debug.
  - Tables are **not automatically responsive**
    - When you use proper layout containers (such as `<header>, <section>, <article>, or <div>` ), their width defaults to 100% of their parent element. 
    - Tables on the other hand are sized according to their content by default, so extra measures are needed to get table layout styling to effectively work across a variety of devices.

- Why should I use `display:table` instead of `<table>` ?
  - Pros of Table Element: 
    - Most designers use table for a consistent look. 
    - Tables are also easy to maintain. 
    - Another advantage of table is that it is compatible with the most browsers.
  - Cons of Table Element: 
    - All this comes with a cost: Too many nested tables increase complexity, page size and download time. 
    - More table elements push important content down so search spiders are less likely to add content to search engines.
  - Pros of DIV Element: 
    - div with CSS we can achieve the same table based page structure and reduce the number of elements on the page, which allows the page to load faster. 
    - It also makes page more compatible with search engine spiders.
  - Cons of DIV Element: 
    - The major drawback of this is not all CSS elements are not browser compatible. 
    - Because of this we have to write some custom CSS to resolve issues. 
  - html5 have better alternatives for layout
  - ref
    - [Why should I use display:table instead of table](https://stackoverflow.com/questions/2867476/why-should-i-use-displaytable-instead-of-table)
    - [Actual table Vs. Div display-table](https://stackoverflow.com/questions/2617895/actual-table-vs-div-table)
    - [Why are people making tables with divs?](https://softwareengineering.stackexchange.com/questions/277778/why-are-people-making-tables-with-divs)

## summary 

- Table reflows row groups in multiple passes
  - Pass 1 - unconstrained width, height and requests max elem width.
    - The table figures out the column widths (balances) given the style width constraints on the table, col groups, cols, cells the preferred and max element sizes of the cells (from the pass 1 reflow), and considers colspans
  - Pass 2 - cell widths are constrained by the column widths (heights are only constrained in paginated mode).
  - In each pass, row groups reflow rows which reflow cells which reflow cell blocks.
  - The row group figures out the row heights given its style height constraints, its rows and cells, and the actual heights of its rows and cells from the pass 2 reflow.
- Table incremental reflow
  - In the style change cases where a target is between the table and the cell, the table is told to rebalance.
  - When a target is the cell or below and the cell changes size, the row tells the table so it can decide if it needs to rebalance
  - When a target is inside the cell's block, the cell requests max element, preferred sizes of its block in case they change
  - After the table reflows the row group(s) containing the targets, if it rebalances, it then does a pass 2 reflow.
- When there is a `%` height frame inside a cell without a computed height
  - the frame will never get a chance to size based on the final cell height
  - in paginated mode when there is a height on the table, the table doesn't allocate extra height to rows until after it does a pass 2 reflow and then it is too late
  - This can be fixed by doing a special **3rd pass reflow**

## pieces

- Tables have to be downloaded and render in full before they are displayed, appearing to take a longer to display. This lapse all depends on processing power. You can 
  - remove gradient backgrounds (as they are rendered by the browser)
  - paginate form data
  - output form rows in chunks (say, 200 rows at a time)
  - does removing all css help?
  - specify a exact width + height on table rows, cells
  - Set the table-layout CSS attribute to fixed on the table.
  - Explicitly define col objects for each column.
  - Set the WIDTH attribute on each col.

- A table is a structured set of data made up of rows and columns (tabular data). 
- A table allows you to quickly and easily look up values that indicate some kind of connection between different types of data
- HTML has a method of defining styling information for an entire column of data all in one place — the `<col>` and `<colgroup>` elements.
  - These exist because it can be a bit annoying and inefficient having to specify styling on columns
  - you generally have to specify your styling information on every `<td>` or `<th>` in the column, or use a complex selector such as `:nth-child()` .
  - Styling columns like this is limited to a few properties: `border` , `background` , `width` , and `visibility` . 
  - To set other properties, you'll have to either style every `<td>` or `<th>` in the column, or use a complex selector such as `:nth-child()` .
- Floated grid limitations
  - The biggest limitation of this system is that it is essentially one dimensional. 
    - We are dealing with columns, and spanning elements across columns, but not rows. 
    - It is very difficult with these older layout methods to control the height of elements without explicitly setting a height, 
    - and this is a very inflexible approach too — it only works if you can guarantee that your content will be a certain height.
  - When using a system like this you do need to take care that your total widths add up correctly, 
    - and that you don’t include elements in a row that span more columns than the row can contain. 
    - Due to the way floats work, if the number of grid columns becomes too wide for the grid, the elements on the end will drop down to the next line, breaking the grid.
    - Also bear in mind that if the content of the elements gets wider than the rows they occupy, it will overflow and look a mess.
- Flexbox was never designed as a grid system and poses a new set of challenges when used as one.
  - Flexbox is one-dimensional by design. 
    - It deals with a single dimension, that of a row or a column.
    - We can’t create a strict grid for columns and rows, meaning that if we are to use flexbox for our grid, we still need to calculate percentages as for the floated layout.
- In your project you might still choose to use a flexbox ‘grid’ due to the additional alignment and space distribution capabilities flexbox provides over floats. 
- You should, however, be aware that you are still using a tool for something other than what it was designed for. So you may feel like it is making you jump through additional hoops to get the end result you want.
- All Skeleton (or any other grid framework) is doing is setting up predefined classes that you can use by adding them to your markup. It’s exactly the same as if you did the work of calculating these percentages yourself.
- Assistive technology such as screen readers may have difficulty parsing tables that are so complex that header cells can’t be associated in a strictly horizontal or vertical way. 
  - This is typically indicated by the presence of the `colspan` and `rowspan` attributes.
  - Ideally, consider alternate ways to present the table's content, including breaking it apart into a collection of smaller, related tables that don't have to rely on using the `colspan` and `rowspan` attributes.
  - If the table cannot be broken apart, use a combination of the `id` and `headers` attributes to programmatically associate each table cell with the header(s) the cell is associated with.

## Are CSS Tables Better Than HTML Tables

- [Are CSS Tables Better Than HTML Tables? _2011](https://vanseodesign.com/css/tables/)

- The css table model is based on the html4 table model and has pretty good browser support. 
- In both table models, the table structure parallels the visual display of the table itself.
- Rows are primary. The row is specified explicitly and columns are derived from how the rows and cells are set up.
- Each html table element has an equivalent css display value. The only real difference is that there’s no distinction between td and th with the css variety.
- Below are the html table elements and their corresponding css display value.

``` scss
table     { display: table }
tr        { display: table-row }
thead     { display: table-header-group }
tbody     { display: table-row-group }
tfoot     { display: table-footer-group }
col       { display: table-column }
colgroup  { display: table-column-group }
td, th    { display: table-cell }
caption   { display: table-caption }
```

- Looking at the above it shouldn’t be too hard to figure out how to set up a css table.

``` html
<div id="table">
  <div class="row">
    <span class="cell"></span>
    <span class="cell"></span>
    <span class="cell"></span>
  </div>
  <div class="row">
    <span class="cell"></span>
    <span class="cell"></span>
    <span class="cell"></span>
  </div>
  <div class="row">
    <span class="cell"></span>
    <span class="cell"></span>
    <span class="cell"></span>
  </div>
</div>
```

``` scss
#table {display: table;}
.row {display: table-row;}
.cell {display: table-cell;}

```

- If you look only at the html above, you can easily see the basic table structure except that I’ve used `div and span` with ids and classes instead of `table, tr, and td` .
- Different table elements have different stacking contexts for the purpose of adding backgrounds to these different layers.
  01. table – lowest layer
  02. column group
  03. columns
  04. row group
  05. rows
  06. cells – highest layer
- The background of any layer will only be seen if all the layers above it have backgrounds set to transparent.
- The width of css tables can be calculated using one of two algorithms. 

- The `table-layout` CSS property sets the algorithm used to lay out `<table>` cells, rows, and columns.
  - `auto`
    - By default, most browsers use an automatic table layout algorithm. 
    - The widths of the table and its cells are adjusted to fit the content.
    - The width of table is set by width of columns and borders
  - `fixed`
    - Table and column widths are set by the widths of table and col elements or by the width of the first row of cells. 
    - Cells in subsequent rows do not affect column widths.
    - Under the `fixed` layout method, the entire table can be rendered once the first table row has been downloaded and analyzed. 
      - This can speed up rendering time over the "automatic" layout method, but subsequent cell content might not fit in the column widths provided. 
      - Cells use the overflow property to determine whether to clip any overflowing content, but only if the table has a known width; otherwise, they won't overflow the cells.
    - The width of the layout is not determined by its content, but rather by the widths set on the table, cells, borders, and/or cell spacing

- The important thing to consider is that a `fixed` table-layout is a one-pass calculation and very quick. 
- On the other hand `auto` requires the same multiple passes of html tables. It’s also the default value.
- If you explicitly set a `width` on the table, then the fixed table layout algorithm will be used.
- By default the cell `height` will be the minimum necessary to display the contents of the cell, 
  - but you can also explicitly set heights. 
  - All cells in a row will be the height of the cell with the maximum minimum necessary height.
- The `vertical-align` property of each table cell determines the cell’s alignment within the row
- css table borders
- `border-collapse` — values can be collapse, separate, or inherit
- `border-spacing` — values can be horizontal length  vertical length, or inherit. 
  - border-spacing is the distance between cell borders.
- `empty-cells` — values can be show, hide, or inherit. 
  - If cells are empty or set to `visibility: hidden` content doesn’t show by default. 
  - Setting `empty-cells: show` on the table will cause backgrounds and borders to display for the empty cell.
- Cons for using html tables for layout over a combination of divs and css.
  - Extra code
    - html tables require more structural code than divs, but css tables use just as much. 
    - If anything css tables use more since ids and classes will likely be added. 
    - If html tables use too much code then css tables do too.
  - Rigid structure
    - html tables are source dependent. 
    - The order you structure the cells is the same order in which they’ll display. 
    - The same is essentially true of css tables as well.
  - Browser rendering
    - browsers require multiple passes at the structure of html tables. 
    - They should only require one pass to display a css table if the table-layout is set to fixed. 
    - They’ll require the same multiple passes if set to auto.
- Considering the above, css tables aren’t offering enough benefit over html tables to use them for layout.
- CSS tables do have the advantage of being more semantically correct, as we can choose html elements that better describe our content.
- Overall it’s hard for me to see much improvement in css tables over html tables, some perhaps, but not enough to justify to myself using them.
- There are two arguments for CSS tables that haven’t been made (or I missed them):
  - You can enclose (CSS-) table rows in their own form, which is helpful if you want to make a CRUD-like table with editable rows.
    - If you have one form per row, only the input in the selected row will be submitted; 
    - with HTML tables you can only enclose the entire table in a form and you’ll then have to figure out on the server side what row has been edited (not to mention an unnecessary large POST if you have a large table).
  - You can create a responsive layout without needing Javascript and e.g. resize or hide columns depending on the device size.
    - Or you can split rows: for example, for very narrow devices you might want to switch the table to a single column layout simply by removing or replacing the “display: table*” style without generating different HTML for that case.

## CSS vs Tables: The Debate That Won’t Die

- One of the debates that never seems to go away in the web development community is that of css vs tables and which is better to use for the layout of your site.
- I do think css is the better option, but feel free to develop sites any way you want.
- What the css vs tables debate is really about is whether or not to structure a web page with tables or divs. In its simplest form we’re comparing:

``` html
<table>
  <tr>
    <td>Some content here</td>
  </tr>
</table>

<!-- vs -->

<div>Some content here</div>
```

- tables are a more complex structure than divs. 
  - As we add more to the page’s design, the table complexity continues to increase compared to divs.
  - Every table cell is dependent on the other table cells in its row to maintain the structure. Divs can work independently from each other. Using table makes it not easy to move dom elements
  - The third problem with tables is in how browsers render them. 
    - In order for a browser to render a page built with tables, it needs to read the code on the page twice. 
    - Once to understand the structure and another time to present it. 
    - That extra pass at the code makes table-based layouts take longer to display. 
    - With a simple table structure, the extra time might not be noticeable, 
    - but as the structure becomes more complex with more and more tables nested inside each other it is noticeable.
- A div-based layout is:
  - easier to maintain
    - less code and less complexity to the structure makes things easier to find and change.
  - more flexible
    - since one div is not dependent on the other divs on the page it allows for more freedom in your design
  - quicker to load 
    - blocks of code can be presented right away instead of the browser requiring an extra pass
- CSS (divs) are better for SEO?
  - Search engines don’t care one bit if the code behind your page uses tables or divs. 
  - Search engines are interested in your content, not your code. 
  - It’s true that less code means less potential for show stopping errors, but those show stoppers can exist regardless of your site’s structure.

## CSS performance test: Flexbox v CSS Table

- [CSS performance test: Flexbox v CSS Table](https://benfrain.com/css-performance-test-flexbox-v-css-table-fight/)

- You can see that in this incredibly limited test layout, Flex layout is slower than Table Layout on every browser tested. 

## The Anti-hero of CSS Layout - "display:table"

- [The Anti-hero of CSS Layout - "display:table"](https://colintoh.com/blog/display-table-anti-hero)

- There are two ways that you can use table in layout - HTML Table and CSS Table.
- HTML Table refers to the usage of table with the native `<table>` tag while CSS Table mimics the same table model as HTML Table but with CSS properties.

``` scss
table    { display: table }
tr       { display: table-row }
thead    { display: table-header-group }
tbody    { display: table-row-group }
tfoot    { display: table-footer-group }
col      { display: table-column }
colgroup { display: table-column-group }
td, th   { display: table-cell }
caption  { display: table-caption }
```

- CSS Table has a key differentiation over HTML Table. It can choose not to be a table by just adjusting its CSS properties. Something that HTML Table is incapable of.
- A common use-case for `display:table` . With it, you can achieve a true vertical alignment (right in the middle) for elements with dynamic height
- A new way to horizontally center-align a dynamic element with no side effects. Apply `display:table` and `margin: auto` to the dynamic element
- CSS Table can choose not to behave like a table when it want to. By switching the element's `display` property from `table-cell` to `block` , we are able to stack the element.
- With `display:table` , you are able to create a sticky footer with dynamic height.

## Why Tables Are Bad For Layout

- Tables are usually more bytes of markup.
  - (Longer to download, and more bytes of traffic for the host.)
- Tables usually prevent incremental rendering.
  - (Takes longer for the user to see anything on the page.)
- Tables may require you to chop single, logical images into multiple ones.
  - (This makes redesigns total hell, and also increases page load time [more http requests and more total bytes].)
- Tables break text copying on some browsers.
  - (That's annoying to the user.)
- Tables prevent certain layouts from working within them (like `height:100%` for child elements of `<td>` ).
  - (They limit what you can actually do in terms of layout.)
- Once you know CSS, table-based layouts usually take more time to implement.
  - (A little effort up-front learning CSS pays off heavily in the end.)
- Tables are semantically incorrect markup for layout.
  - (They describe the presentation, not the content.)
- Tables make life hell for those using screen readers.
  - (Not only do you get the other benefits of CSS, you're also helping out the blind/partially-sighted. This is a Good Thing.)
- Tables lock you into the current design and make redesigns MUCH harder than semantic HTML+CSS.
  - (Have you seen CSS Zen Garden?)
- Tables are 100% acceptable, appropriate, and correct for use with tabular data

## A Complete Guide to the Table Element

- [A Complete Guide to the Table Element](https://css-tricks.com/complete-guide-table-element/)

- The `<table>` element in HTML is used for displaying tabular data. 
- row: description of an obj
- column: get a sense of the variety or pattern of data
- header: thead > tr > th
- tbody: rows of data： tr > td
- footer: tfoot > tr > th 
- The individual cells of a table are always one of two elements: `<td>` or `<th>`
- `<th>` elements are not necessarily limited to being within the `<thead>` . They simply indicate header information. So they could be used, for instance, at the start of a row in the `<tbody>`
- By default, all table cells are spacing out from one another by 2px (via the user-agent stylesheet)
- Notice the slight extra gap between the first row and the rest. That is caused by the default border-spacing being applied to the `<thead> ` and `<tbody>` pushing them apart a bit extra. This isn’t margins, they don’t collapse. 
- `border-collapse: collapse;` remove the space among borders
- There are two important attributes that can go on any table cell element ( `<th>` or `<td>` ): `colspan` and `rowspan` . 
  - They accept any positive integer 2 or larger. 
  - If a `td` has a `colspan` of 2 (i.e. `<td colspan="2">` ) it will still be a single cell, but it will take up the space of two cells in a row horizontally. 
  - Likewise with rowspan, but vertically.
- `colspan` is fairly easy. 

   - Any table cell is “worth” one, unless it has a colspan attribute and then it’s worth that many. 
   - Add up the values for each table cell in that table row to get the final value. 
   - Each row should have exactly that value, or else you’ll get an awkward table layout that doesn’t make a rectangle (the longest row will stick out).

- If a table element has a `rowspan` attribute, it spans across two rows vertically. 
  - That means the row below it gets +1 to it’s table cell count, and needs one less table cell to complete the row.
- The table element itself is unusual in how wide it is. 
  - It behaves like a block-level element (e.g. `<div>` ) in that if you put one table after another, each will break down onto its own line. 
  - But the actual width of the table is only as wide as it needs to be
  - If the amount of text in the tables widest row only happens to be 100px wide, the table will be 100px wide. 
  - If the amount of text (if put on one line) would be wider than the container, it will wrap.
  - However if text is told to not wrap (i.e. `white-space: nowrap;` ), the table is happy to bust out of the container and go wider
- Two Axis Tables 首行和首列都是表头

``` HTML
<table>
  <tr>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
  </tr>
  <tr>
    <th>2</th>
    <td>4</td>
    <td>6</td>
    <td>8</td>
  </tr>
  <tr>
    <th>3</th>
    <td>6</td>
    <td>9</td>
    <td>12</td>
  </tr>
  <tr>
    <th>4</th>
    <td>8</td>
    <td>12</td>
    <td>16</td>
  </tr>
</table>
```

- When To Use Tables
  - a plan/pricing/features comparison, bowling scores, an internal grid of employee data, financial data, a calendar, the nutrition facts information panel, a logic puzzle solver, etc
- When Not To Use Tables
  - An inappropriate use for tables is for layout 
    - bad for accessibility
    - source order dependency
- CSS has properties to make any element you wish behave as if it was a table element. 
  - You’ll need to structure them essentially as you would a table
- A handy trick here is that you don’t even need the `table-row` element in there if you don’t want. 
  - A bunch of `display: table-cell;` elements that are children of a `display: table;` element will behave like they are all in one row.
- You always alter the display property of the element to get the table-style behavior.
  - Notice there is no `<th>` alternative. That is for semantic value only. 
  - It otherwise behaves just like a `<td>` , so, no need to replicate it in CSS.

``` 
display: table                /* <table>     */
display: table-cell           /* <td>        */
display: table-row            /* <tr>        */
display: table-column         /* <col>       */
display: table-column-group   /* <colgroup>  */
display: table-footer-group   /* <tfoot>     */
display: table-header-group   /* <thead>     */
```

- webkit user agent stylesheet for table 
  - The UA stylesheet for tables differs from browser to browser. 
  - That’s what CSS resets (and related projects) are all about: removing the differences.

``` CSS
table {
  display: table;
  border-collapse: separate;
  border-spacing: 2px;
  border-color: gray
}

thead {
  display: table-header-group;
  vertical-align: middle;
  border-color: inherit
}

tbody {
  display: table-row-group;
  vertical-align: middle;
  border-color: inherit
}

tfoot {
  display: table-footer-group;
  vertical-align: middle;
  border-color: inherit
}

table>tr {
  vertical-align: middle;
}

col {
  display: table-column
}

colgroup {
  display: table-column-group
}

tr {
  display: table-row;
  vertical-align: inherit;
  border-color: inherit
}

td,
th {
  display: table-cell;
  vertical-align: inherit
}

th {
  font-weight: bold
}

caption {
  display: table-caption;
  text-align: -webkit-center
}
```

- use `th,td {display: inline;}` to untable a table
- Zebra Striping Tables
  - `tbody tr:nth-child(odd) { background: #eee; }`
- Hightlighting a particluar row is fairly easy.
  -  You could add a class name to a row specifically for that
- Highlighting a column is a bit trickier. 
  - One possibility is to use the `<col>` element. However this is rarely useful. If you set the background of a row element or table cell element, that will always beat a background of a column element. Regardless of specificity.
  - You’re probably better off setting a class name on each individual table cell element that happens to match that column position in the row.

- highlight row, column, cell on hover
- Tables Can Be Difficult in Fluid/Responsive Designs
  - Turn Rows into Blocks
- The most modern way of handling fixed headers is `position: sticky;`
- custom implementation
  - search
  - sort

## Responsive CSS Table

- ### [Responsive Data Tables_2011](https://css-tricks.com/responsive-data-tables/)
- Responsive design is all about adjusting designs to accommodate screens of different sizes. 
- So what happens when a screen is narrower than the minimum width of a data table? 
  - zoom out and see the whole table, but text may be too small
  - zoom in to read, but scrolling by touch sucks
- The biggest change is that we are going to force the table to not behave like a table by **setting every table-related element to be block-level**. 
- Then by keeping the zebra striping we originally added, it’s kind of like each table row becomes a table in itself, but only as wide as the screen. No more horizontal scrolling! 
- Then for each “cell”, we’ll use CSS generated content (:before) to apply the label, so we know what each bit of data means.
- two alternative ideas that are both very cool
  - One of them makes a pie graph from the data in the chart. On narrower screens, the pie graph shows and the table hides, otherwise only the more information-rich table shows
  - The next idea is to turn the table into a mini graphic(like a thumbnail or placeholder image) of a table on narrow screens, rather than show the whole thing. This shows the user there is a data table here to be seen, but doesn’t interfere with the content much. Click the table, get taken to a special screen for viewing the table only, and click to get back.

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
01. Horizontal Minimalist
02. Vertical Minimalist
03. Box
04. Horizontal Zebra
05. Vertical Zebra Style
06. One Column Emphasis
07. Newspaper
08. Rounded Corner
09. Table Background
10. Cell Background

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

- Another approach doing the narrow viewport layout is using a combination of Grid and `display: contents` . 
  - Please note that display: contents in supporting browsers has issues with accessibility at the moment
  - Each `<tr>` element is set to ` display: grid` , and each `<td>` element is set to `display: contents` .
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

## collection of well-designed tables

- [Beautiful HTML Tables](https://www.hongkiat.com/blog/html-table-building-30-beautiful-examples-and-useful-javascripts/)

## ref

- [HTML Table Styler - CSS Generator](https://divtable.com/table-styler/)
