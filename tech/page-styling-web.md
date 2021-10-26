---
title: page-styling-web
tags: [css, styling, web]
created: '2020-12-30T11:52:13.417Z'
modified: '2021-01-19T11:00:41.227Z'
---

# page-styling-web

# css

## [Why use Classes or IDs on the HTML element?](https://css-tricks.com/why-use-classes-or-ids-on-the-html-element/)

- tips
  - 添加到`<body>`上，因为第3方工具库经常添加到`<html>`
  - 用class，不用id，因为一个元素不能有多个id，而测试和发布时常需要不同id

- I’m frequently seeing ID and class specifications to `<body>` and `<html>` elements. 
  - I’m curious as to why one would do this? If it is unique to either element, then why not specify body or html in the CSS?

``` HTML
<html class="html-happyNewYear">
```

``` CSS
.html-happyNewYear {
  background: url(/images/fireworks.jpg);
}

html {
  background: url(/images/fireworks.jpg);
}
```

- If you view source and look at a page in isolation, I can see how any class or ID on the `<html>` element seems superfluous. 
  - The fact is, these top-level classes can be extremely useful. 

- The idea of CSS is to abstract design away from markup. 
  - Pages on a site may all use the same exact CSS file. 
- A top-level class can serve to identify which page is currently being viewed and thus apply styling to that a different page may not get.
  - `<html class="page-2">`
  - Different pages, same CSS file, different designs

- A WordPress powered site uses themes to display pages.
  - `<body <?php body_class(); ?>>`
  - `body_class()` outputs a whole bunch of classes that are specific to the type of page being loaded
  - Just as an FYI, you can absolutely just move the function up to the `HTML` element.

- Modernizr is a JS library that also adds top level classes. 
  - It adds them dynamically to the `html` element when it loads and runs. 
  - The classes are symbolic(标志的，象征的) of what the current browsers capabilities are. 
  - So whereas WordPress applies classes you can use to make different pages look different, 
    - Modernizer applies classes you can use to make the same page look different, depending on browser capabilities.

- [ID Your Body For Greater CSS Control and Specificity](https://css-tricks.com/id-your-body-for-greater-css-control-and-specificity/)
  - using `id` to do current navigation highlighting. 
  - Let’s say you want to change the color of your links on just your contact page to red. They are blue on every other page
    - You could declare a separate stylesheet for your contact page. 
      - it’s redundant
    - You could give all those links a unique class on that page. 
      - it isn’t very semantic and it’s also redundant
    - The best solution is to give your the body a unique ID. 
      - You can use the same stylesheet and target just the links you want to with a single CSS selector.

- discussion

- It makes sense to take into account that `HTML` element cannot have `class` attribute (at least in XHTML 1.0). 
  - It’s better to apply class to `BODY` element instead.
  - In HTML 5 it’s valid to have classes and ID’s on the `<html>` element.
    - In xHTML, you are correct, the code won’t validate with classes on the `<html>` element 
    - but all browsers will interpret the code as expected so it’s practical to do so.
    - I usually put page backgrounds on the `<html>` element as the background will fill the viewport regardless of content length. 
    - Pages working correctly cross-browser is more important than validation.
  - I was wondering if there were more pros/cons regarding this issue and so far I figured out the following pros of using a class or ID on the html element versus using it on the body element:
    - viewport-filling property (as Peter Wilson said);
    - multiple backgrounds with no additional markup (i.e. one for the html element, one for the body element);
  - while the cons might only be that it doesn’t validate in XHTML.

- I’m a fan of `body.isloading { cursor: progress; }`
- remember, that’s a body element you’re looking at, no wrapper! 
  - `<body>` is already a wrapper and can be hacked to achieve some pretty remarkable layout and clean code!
  - So no more excuses. Stop using wrappers, and especially don’t try and hide a wrapper behind HTML5 bling by using a section, that’s wrong.
- I like to specify what version of IE, if any, is being used in the `<html>` tags, so I can specify workarounds for those people.
- I’m curious whether or not using that many classes on an element is decreasing site performance or is in any way ‘bad’.
  - The MODERNIZR example you gave has loads of classes
  - I see if often on websites and I always wondered if that has an impact on site speed or anything really regarding the website.
  - I tried out adding 10, 000 unique classes to the HTML element to see if it affected performance. 
    - It doesn’t. Even in IE6. Fast fast fast.
    - However if all those classes were added one-by-one (as they were in the early days of HeadJS) you were be in reflow city. And that’d be bad.
- I use classes to work with html tags. 
  - Because when developing dynamic pages, IDs sucks.
  - Actually, when I have to pass different IDs to Divs in the development phase, the names of ID’s conflicts with the development end. 
    - And definitely, **we can’t use multiple IDs on same Div**. That’s why classes are better.
- Using this trick is great for setting ‘active’ state on main navigation items (when an active class is not pinned to a nav-item): `body#about li#nav_about {font-weight:bold /*etc*/}`
  - This trick is also good for re-purposed pages, such as a page needing to fit within a modal dialog would need slimmer content, headers, footers, etc.
  - `body.modal div#content {width:800px /*etc*/}`
- the best part is that in the past loading different stylesheets one after the other meant that all the stylesheets would not load in parallel (there are ways around that) 
  - but this method of using one stylesheet for all CSS not only proves to be faster but more ‘semantic’.
- Here’s a clever (yet slightly messy) use of classes on the HTML element from Paul Irish. 
  - Target versions of IE with conditional comments and a single stylesheet
- I’d use IDs on html/body elements mostly for attaching a unique CMS item identifier to the final markup, which in turn would make it rather simple to provide content specific styling.
  - Another use-case (at least for me) for classes in the same element is whether or not the rendered page should leave space for a sidebar.
- I’m using different body classes to distinguish between background formats on my personal site
  - If you look through the pages, I change the space available in the heading area based on 3 different body classes.
- I’ve found body class tags especially helpful in letting sitewide jQuery code know what methods are needed for that page.

# more-styling
