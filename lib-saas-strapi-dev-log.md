---
title: lib-saas-strapi-dev-log
tags: [dev-log, strapi]
created: 2024-03-21T13:27:55.928Z
modified: 2024-03-21T13:28:16.872Z
---

# lib-saas-strapi-dev-log

# guide

# draft

# not-yet
- ❓ Cannot destructure property 'uid' of 'U' as it is undefined.
  - 在访问content item时会抛出异常
  - 经排查是strapi-plugin-reactions导致，移除就正常了
# done
- strapi useDocumentLayout 出现了多次执行，一直没找到触发的逻辑
  - 触发原因是自定义插件的文件名version.js/history.js，没分析出来是自定义文件
  - console.trace比console.log提供更详细的调用栈
# more


- ## Is there any v5 engineer to help  me migrate entityService decorator logic to documentService?
- https://discord.com/channels/811989166782021633/1095091586452426824/1222904152032546856
  - In v5 decorators no longer exist they will be replaced by documentService Middlewares that are currently not yet fully stable 
  - Still there is a version of the new docuemtService Middlewares in strapi 
- what's the v5 way to transform response?
  - Document middleware or route middleware.
- from the doc, route middlewares require me to enumerate the model uid.but I need to modify the response for several routes by a rule.
  - You can dynamically inject route middlewares in register.(js/ts)
  - And I assume the same thing is posible for document service middleware but I would have to test that out.

- 
- 
- 
