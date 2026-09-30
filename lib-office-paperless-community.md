---
title: lib-office-paperless-community
tags: [community, ocr, paperless, pdf, rag]
created: 2026-09-27T10:51:07.159Z
modified: 2026-09-27T10:51:40.218Z
---

# lib-office-paperless-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## 

- ## 

- ## 

- ## ✅ [[Feature Request] Alternative OCR engines (Azure AI Vision, Google Cloud Vision etc.) _202312](https://github.com/paperless-ngx/paperless-ngx/discussions/5128)
  - Tesseract OCR is pretty bad. 
  - consider allowing supporting external APIs, such as Azure OCR API, and one from Google.

- Allow openai compatible vision api to an ocr llm would be nice. There are so many of them now.

- ## [Plugin architecture - create an ecosystem around Paperless-ngx _202410](https://github.com/paperless-ngx/paperless-ngx/discussions/8084)
  - Personally, there are 2 features that I would like to see one day: using an S3-compatible service as storage backend and importing documents directly from Google Drive

- 👷 202411: I think I'm going to attempt to attempt to refactor the storage code into a plugin architecture, so that in the future S3 support could be added.

- ## [S3 as document backend _202204](https://github.com/paperless-ngx/paperless-ngx/discussions/762)
- it could be achieved easily through external tools, like s3-fuse - s3fs-fuse/s3fs-fuse but with limitations. Native support from the application would be great

- I guess one could use `django-storages` to implement S3 storage.
  - From what I can see, paperless uses `shutil` for interacting with files. Unfortunately, this does not appear to be the django default way to implement file storage. Adding an S3 backend is therefore probably not straightforward.
- There are wrappers around S3 that mimic the `shutil` API surface, like `s3shutils`, which is reasonably up to date.

- Personally I'm not a big fan of a `S3-fuse` since S3 is blob storage not block storage. It is not POSIX compliant and just waiting for a disaster to happen. First class support via `boto3` or `s3shutils` (uses boto) would be awsome.

- Implementing S3 is super easy and tying it to the meta data in the database is very easy. Many projects that do not choose to implement S3 or similar storage option and instead defer to fuse or similar shows the inexperience of the developer. PHP is another sign. I may from this and put the S3 option in place. Again s3 has been around a long time and super easy to implement and tie to the meta data.
  - there are many reasons to not use fuse or similar solutions. Most important, doing so means the application is not aware it's using S3 storage instead of a file system. File systems have locking, fast scanning, and incremental updates. S3 doesn't.
  - The right way to use S3 is to use it to store data the application never has to refer in detail again. I

- we have started using paperless and use S3 Storage as descriped by mounting via rclone. DB is running locally (due to performance in the future), but we back it up to s3 as well... 
  - For us, seems like a good working solution, 
  - except this issue: upload a doc assign another storage path => this should be refelected, but instead, the org file gets deleted !
  - after digging around a bit, it seems that S3 storage in gerneal does not support moving files, but instead we need a cp / delete operation.
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
