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
