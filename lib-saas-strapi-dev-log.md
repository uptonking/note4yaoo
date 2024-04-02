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
- version number should update when content changed and hit save
  - 可以在useEffect里面检测内容变化，若变化了就refetch，甚至reload-page

- strapi useDocumentLayout 出现了多次执行，一直没找到触发的逻辑
  - 触发原因是自定义插件的文件名version.js/history.js，没分析出来是自定义文件而非库文件
  - console.trace比console.log提供更详细的调用栈
# more
