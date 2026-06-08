---
title: lib-office-community-format
tags: [format, office]
created: 2024-12-29T18:09:06.783Z
modified: 2024-12-29T18:09:21.233Z
---

# lib-office-community-format

# discuss-stars
- ## 

- ## 

- ## [Why are the Microsoft Office file formats so complicated? (2008) | Hacker News _201609](https://news.ycombinator.com/item?id=12471604)
- Regardless of XML-ness, you still have to check that the values are valid. With XML, you also have to check whether they're of the right type, because the format is so much more flexible.
  - It is far easier to repair and recover an xml file than a binary format.

# discuss-ooxml
- ## 

- ## 

- ## [The cost of ODF and OOXML | Hacker News _201205](https://news.ycombinator.com/item?id=4032429)
- I have always wondered why Open Document standard would not be based around HTML instead of inventing new XML schema? Can someone who has more insight on ODF/OOXML tell me why HTML is not suitable for office document format?
  - HTML made for continuous display and re-flowing for different sizes.
  - ODF is for publishing, i.e. where you can have separate pages, with footers, margins, absolute position inside page (versus whole document), corrections tracking, authorship, figures.
- Open Office has a far richer format than HTML allows 

- That seems like a bad idea. TeX doesn't allow separation between markup and presentation very well. Something like DocBook with a presentation engine like XSLT might be better, if it wasn't for the verbosity of the XML source.

- ## [European Commission's use of Microsoft 365 infringes data protection law for EU | Hacker News _202403](https://news.ycombinator.com/item?id=39666561)
- How would ODF be better? Office Open XML standards are also publicly available if you need them.
  - 👷🏻 co-author of the ODF spec (2006 ISO) here, I also got involved via NLNet to work with my local standards office to improve OOXML.
  - The OOXML spec was offered to the ISO standard along an unusual path, a fast standardization lane. Where there was no option for any of the people reviewing it to actually change anything. It was rubber-stamped(不加思考便机械式地批准〔含贬义〕) in other words.
  - That fact alone doesn't mean it is a bad, but it is a bit of a red flag. The fact is, it is a really bad specification. It is a full 7000 pages long with lots of conflicting details.
  - Compare it to ODF which is 1/10th of the size. Has a lot of reuse of concepts and was written under OASIS, a standards organization, unlike the OOXML spec which was written by Microsoft and the full 7000 pages dropped on the world.
- I could imagine that some of the points you mentioned might be related to Microsofts focus on backward compatibility. Some of the points certainly might also have less noble reasons.
- ODF deferred some important things to be done in later revisions of the spec. For example spreadsheet formulas. OOXML on the other hand had hundreds of pages covering spreadsheet formulas, including detailed mathematical definitions and explanations for functions.

- My current favourite is OnlyOffice – pretty concise interface and good compatibility. Unfortunately, there's no build for Linux on Arm yet, so I'm stuck with LibreOffice (not too bad either).
  - Their browser-based self-hosted solution has optional closed-source components, but the desktop app is pretty much open source
- Isn't OnlyOffice browser-based? Or is that something else?
  - It is, but they also package it as a desktop app using CEF. (It is one of maybe two Chromium-based desktop apps that I like, the other one being VSCodium.)
# discuss-office-suite
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [An open letter to office suite users, just before the Euro-Office announcement : r/libreoffice _202606](https://www.reddit.com/r/libreoffice/comments/1u00lie/an_open_letter_to_office_suite_users_just_before/?sort=top)
  - In recent days you will have read various articles announcing the arrival of Euro-Office, which is being “marketed” as the first open-source office suite developed in Europe. We feel compelled — reluctantly, since open source should rest on transparency, not deception — to correct this claim. The first open-source office suite developed in Europe was OpenOffice.org in 2001, based on StarOffice’s source code, followed by LibreOffice from 2010.
  - These are two genuine open-source office suites, built from source code that originated in Europe. They are not a freeware clone of MS Office whose code provenance is undisclosed
  - It is worth remembering that many of those who champion Digital Sovereignty today were silent back in 2006, when the open ISO/IEC ODF standard — the pillar of Digital Sovereignty — was announced: not only did they not listen to us during all these years, but in some cases they greeted us with a condescending smile.
  - Document formats are a subject still rife with misinformation. This is understandable on the part of Microsoft, which developed and controls the horrible proprietary OOXML format, designed precisely to prevent Digital Sovereignty by maintaining content lock-in. It is far less understandable on the part of companies that claim to advocate open source, such as those promoting Euro-Office.
  - Euro-Office defaults to the fully proprietary OOXML document format, developed and controlled solely by Microsoft. This makes it a de facto ally of Microsoft in its content lock-in strategy, with control remaining firmly in Redmond and far from Europe.

- ## [The biggest blocker to LibreOffice adoption? LibreOffice (2023) | Hacker News _202411](https://news.ycombinator.com/item?id=42225260)
- Microsoft really doesn't want anyone to reliably copy their formats. Their standard is purposefully complicated and convoluted, it was almost rejected by ISO for this reason and it took heavy lobbying before it passed (I know of this personally as the ISO vote went through national ISO bodies).

- The biggest blocker to LibreOffice adoption is that the general purpose office suite is dying a slow death.
  - If you’re writing up some documentation for a business process, that should live in a system designed for that purpose where documents can be linked together and integrate with other systems. Examples include Confluence or Notion.
  - The second biggest blocker is that LibreOffice isn’t in your browser. It’s a slow-installing slow-loading clunky old desktop application.
  - The third biggest blocker to LibreOffice adoption is the dogshit ancient-looking UI. It looks nothing like a native application on any platform which constantly reminds you you’re using the knockoff of the Real McCoy.
# discuss
- ## 

- ## 

- ## 

- ## 
