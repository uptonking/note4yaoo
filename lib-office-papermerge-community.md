---
title: lib-office-papermerge-community
tags: [community, docs, papermerge, pdf]
created: 2025-12-09T13:51:06.475Z
modified: 2025-12-09T13:51:18.940Z
---

# lib-office-papermerge-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-paperless-ngx-issues
- ## 

- ## 

- ## [[Feature Request] Alternative OCR engines (Azure AI Vision, Google Cloud Vision etc.) _202312](https://github.com/paperless-ngx/paperless-ngx/discussions/5128)
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
# discuss-paperless-ngx
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [How I would like to use papermerge as a paperless user · Issue · ciur/papermerge _202007](https://github.com/ciur/papermerge/issues/34)

# discuss-issues
- ## 

- ## 

- ## [Please ignore dot files from macOS _202104](https://github.com/ciur/papermerge/issues/363)

- ## [Deleting nodes does not get rid of underlying filesystem folders · Issue · ciur/papermerge _202403](https://github.com/ciur/papermerge/issues/607)
  - When deleting nodes/files in papermerge I noticed that the folders created for the nodes are still present.
  - Also I'm curious as to the reasoning of the folder structures. I can understand the need to provide the GUID folder for uniqueness of uploaded files, file versioning, merging etc, but the extra folder structures on top of the GUID folder seems weird to me. 
  - It seems to me applying only the GUID folder should be sufficient, and would allow for easier manual decorruption in the event something catastrophic happened and you needed to piece an instance back together.

- Regarding your question about extra folder on top of GUID folder.
  - The reason is to reduce number of file system nodes (files or folders) in a specific folder.
  - Example: let's say you have 120, 000 pages; then with just GUID folder, the pages folder will contain 120, 000 entries! The problem is that usually there is a limit of number of subfolders on fiven file system. By adding one extra folder, with two digits of the UUID, the limitation is reduced by factor of 256. Thus if you have 120, 000 pages, on the file system there will be max 120, 000 / 256 ~ 468 folders.

- ## 🐛 [When user is deleted - delete all its storage data as well · Issue · ciur/papermerge _202209](https://github.com/ciur/papermerge/issues/485)
  - Storage data - is (are?) document files and document OCR data stored under media root.
  - Expected: when user is deleted, both its folders should be deleted as well
  - Actual: both folders are still there and contain documents!

- 似乎修复的pr实现逻辑存在问题
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
