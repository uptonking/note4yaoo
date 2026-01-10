---
title: spec-format-xml
tags: [format, xml]
created: 2019-12-24T12:58:13.163Z
modified: 2020-12-08T13:52:49.103Z
---

# spec-format-xml

# spec

- 

# faq

- 

# summary

- 

# dev

- 

# discuss-html
- ## 

- ## 

- ## [Html to Pdf library suggestions : r/Python _202601](https://www.reddit.com/r/Python/comments/1q74ivt/html_to_pdf_library_suggestions/)
- playwright is probably the best one even though it's heavier since it needs to run a browser in headless mode
  - for css and images you are gonna have the same problem independently on the library you are using
  - if these styles and images are just static files that don't require authentication you can just use the full url in the template

- Personally, I've given up trying to tame these HTML->PDF beasts. I rather create a Word-file which the user later can print/convert to PDF if they so require. It's so much easier (imho).

- I actually usually write a tiny wrapper around a statically compiled wkhtml2pdf binary. Works great, gives some control, and is VERY simple and easy. 

- If your html is not too complicated, wkhtmltopdf.
  - I think that if you want reliable rendering your best option is always going to be a headless browser. In which case you should look at pyppeteer.

- [Html to Pdf library suggestions : r/django](https://www.reddit.com/r/django/comments/1q74j4u/html_to_pdf_library_suggestions/)
  - I think that if you want reliable rendering your best option is always going to be a headless browser. In which case you should look at pyppeteer.
# discuss
- ## 

- ## 

- ## 

- ## [XML is the future | Hacker News_202306](https://news.ycombinator.com/item?id=36466248)
- XML the data format is pretty great in its basic form. Not space-efficient, but unless you're dealing with bulk data, the inefficiencies don't matter unless you're googlescale or can't spare a millisecond. The format itself doesn't absolve you from the design work of your model; your ssn example is typical of the "CEO said we have to use XML now" rush-jobs at the peak of the SOA hypecycle.
  - XML data validation through XSD is a dream. The insistence of the JSON-people to sabotage any kind of data validation is absurd to me.
  - XML Webservices are easy and consuming them from a WSDL is easy.
  - SOA on an enterprise level was a stupid idea creating a giant expensive communication middleware with the ESB without delivering on the promises.
- Every other thing in the XML space is brainfuck-level overcomplicated bullshit dreamt up by bored enterprise architects. 
  - WS-* is a cacophony of overcomplicated solutions to problems that only exist because enterprise architects dreamt of having a single data model that's inter-operable between companies.

- Having written a bunch of XML schemas and a bunch of JSON schemas at the same time while integrating multiple third party APIs, I can unreservedly say that JSON schema is awful.
  - It just about works, but it's horrible to write and horrible to maintain. What you can actually do with the validation is surprisingly limited in some forms and the fact that you have to write JSON to write the schema shows just how non-user-friendly JSON is.
  - A friend told me that she writes JSON schemas in YAML and then uses a build step to downgrade that to JSON for the actual validator. I wish I'd thought of that.

- 
- 
- 
