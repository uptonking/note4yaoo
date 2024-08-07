---
title: lib-saas-strapi-issues
tags: [issues, strapi]
created: 2024-02-15T05:46:16.207Z
modified: 2024-02-15T05:46:32.456Z
---

# lib-saas-strapi-issues

# guide

# issues-done
- ## [Deleting/Updating content-type doesn't drop/migrate the database _201805](https://github.com/strapi/strapi/issues/1114)
- we don't delete your tables we just create new ones, therefore the behavior you described is the correct one.

- Fixed in v4, marking as closed
  - There is no configuration for this as we will just delete the column/table on reboot when it's deleted. We did discuss a warning or a safer method but opted not to do it in v4. 
  - When you use v4 we will simply clean up the database for you.

- Yes this is currently intended (as you deleted the schema effectively), the best method to hold onto the data is take a database backup.
  - If you are simply renaming a content-type or field then you will have to (for now) write a custom migration

- [Data Loss in Content-Type Table After Schema Modification _202401](https://github.com/strapi/strapi/issues/19141)
  - In Strapi v5 D&P and i18n won't be able to be disabled (though they don't have to be used) so technically in v5 the D&P delete issue won't be a problem anymore since it'll be forced on for all content-types (though you'll have the option to auto-publish by default or if new content should be a draft state).

- ## [Can't install strapi - Questions and Answers - Strapi Community Forum](https://forum.strapi.io/t/cant-install-strapi/33500)
- TypeError: Cannot read properties of undefined (reading 'addBreadcrumb')

```shell
# cd to your project and
npm install --legacy-peer-deps
npm run develop
```

# rfc
- ## 

- ## [Allow customization of Primary Key (ID) type and name | Developer Experience | Strapi _202203](https://feedback.strapi.io/developer-experience/p/allow-customization-of-primary-key-id-type-and-name)

- ## [Conditional fields | Content Editing XP | Strapi _202203](https://feedback.strapi.io/customization/p/conditional-fields)
  - Display a field only if some conditions are met.

- [Conditionally hide/show collection type fields based on other fields - Questions and Answers - Strapi Community Forum](https://forum.strapi.io/t/conditionally-hide-show-collection-type-fields-based-on-other-fields/28474)

- ## [Setting for collapsing/expanding components in the admin panel by default | Voters | Strapi _202306](https://feedback.strapi.io/feature-requests/p/setting-for-collapsingexpanding-components-in-the-admin-panel-by-default)
  - For content type structures that feature a lot of components, this makes the page very very long.

# issues-not-yet-vip
- ## 

- ## [fix: document service find many pagination ](https://github.com/strapi/strapi/pull/20178)
  - We allowed page & pageSize parameters on find Many, but those params were not properly converted to the offset & limit database params.
  - This PR proposes a fix, which always converts pagination params to offset and limit, so both page & pagesize, and start & limit works on the findMany method, or any other that accepts pagination.

- 
- 

- ## 🔌 [Disable Email and Upload plugins _202208](https://forum.strapi.io/t/disable-email-and-upload-plugins/21128/2)
- I would like to know this as well. I tried setting `enabled: false` for the upload plugin in my plugins.js, but it does not do the trick.

- ## [Custom dropdowns _202301](https://forum.strapi.io/t/custom-dropdowns/24905)
- Do you want this for the strapi admin panel or for a custom frontend
  - Also to my knowledge it is not possible with out changing the core admin code 
  - Only option I see for you is to change the core/admin code directly to get this to work

- ## [Update EditView onClick ](https://forum.strapi.io/t/update-editview-onclick/26871)
- I just managed to do it with React’s router:

```JS
import { useHistory } from 'react-router-dom';
const Component = () => {
  const history = useHistory();
  history.push(`contentype/path/:id`)
}
```

- ## [How to update frontend when content in Strapi is changed _202208](https://forum.strapi.io/t/how-to-update-frontend-when-content-in-strapi-is-changed/21270)
- Maybe you can try using socket.io 

- ## [How to trigger a page refresh in the Admin UI after a Lifecycle Hook _202209](https://forum.strapi.io/t/how-to-trigger-a-page-refresh-in-the-admin-ui-after-a-lifecycle-hook/21766)
- I may found a solution. You could register a `injectContentManagerComponent` in a plugin and register a react component to inject into a injection zone inside of the ContentManager edit window. 
  - inside of the injection zone you could call `window.location.reload()` what will trigger a reload of the whole page you should be able to see initialData from `useCMEditViewDataManager` change as soon as you save it should change. 
  - You should be able to use that to check for when a save happens and call a reload.

- 
- 
- 
- 
- 

# issues-not-yet
- ## 

- ## [TypeError: Cannot read property 'mutations' of undefined _202006](https://github.com/quilljs/parchment/issues/87)
  - This error is occurring in Quill when the list of nodes are, somehow, problematic.
  - Because what happens is that this particular node doesn't exists, so a mutation property is, of course, undefined.

- ## [Pagination parameters not working in Users endpoint ](https://github.com/strapi/strapi/issues/12911)

- ## one of the major issues i’ve had with Strapi is that you cannot reliably add calculated fields (from other data sources) to responses. 
- https://discord.com/channels/811989166782021633/811989167357689922/1222502997121175602
  - You can't do it through services, hooks or the query engine. 
  - You could arguably do it through middleware, and check the response body to see if a particular entity was populated and then add the calculated fields, but this isn't great either because it relies on the name of the relation rather than the actual content type.
  - I’m wondering what the official Strapi position on this is, and how they recommend going about this?
- Middlewares, model lifecycles, or soon in Strapi 5 the document service middlewares.
  - Tbh this use-case is extremely niche and is basically known as API federation, it's better handled with a proper custom field that links to that external system (mux custom field plugin is a great example)
- Lifecycles don't run on relations so that wouldn't be a reliable approach. Is it really that niche? I can think of loads of scenarios where you'd want to alter the response to have a field that isn't isn't stored permanently within the model

- Aren't custom fields global rather than scoped to a specific content type?

- ## 🔒 [Field Level Permissions - End User management | Voters | Strapi _202203](https://feedback.strapi.io/feature-requests/p/field-level-permissions-end-user-management)
  - The current Users-permissions plugin is very limited in the control you have over accessing fields or even nested relations, components, and dynamic zones.

- 
- 

- ## [Webhook by content type | Voters | Strapi _202203](https://feedback.strapi.io/feature-requests/p/webhook-by-content-type)
- 
- 
- 

- ## 📈 [Add a "folder-like" group function to organize content types | Voters | Strapi _202205](https://feedback.strapi.io/feature-requests/p/add-a-folder-like-group-function-to-organize-content-types)

- [User interface - Grouping Collection Types _202212](https://forum.strapi.io/t/user-interface-grouping-collection-types/24304)
  - Unfortunately this is not possible yet

- ## 📈 [Organize entities into folders ](https://github.com/strapi/strapi/issues/10545)
- Marking as closed as this isn't likely something we will do _202203

- ## [can i hide left menu nav? _202302](https://github.com/strapi/strapi/issues/15658)
  - i want to only show right content area and hide left area?
- Right now this is not possible. If you need it, it would be great if you could open a feature request

- ## [Issue with PNPM Workspaces and Strapi Plugins in Monorepo _202401](https://github.com/strapi/strapi/issues/19176)
  - The problem arises specifically when installing plugins or custom fields located within my monorepo. 
- I use file:// to link plugin dependency has no this issue. I only use --shamefully-hoist option to install.

- ## 💾 [Can I save and upload media file with google drive?](https://forum.strapi.io/t/can-i-save-and-upload-media-file-with-google-drive/24817)
- I guess you could but you would have to make your own plugin for it.

- ## 🖼️ [Issue installing sharp glib-object.h: No such file or directory · lovell/sharp](https://github.com/lovell/sharp/issues/4003)
- [Update sharp package to version v0.33.2 · strapi/strapi](https://github.com/strapi/strapi/pull/19311)

- 💡 变通方法

```JSON
{
  "overrides": {
    "sharp": "0.33.2"
  }
}
```

- ## [Concurrency issue with two nodes Postgres cluster _202309](https://github.com/strapi/strapi/issues/17929)
- Knex don't natively support clusters

- I've not used PG-Pool before (as I'm more of a MariaDB user) but I have used ProxySQL (which is a MySQL/MariaDB tool that is very similar).
  - Generally the "sync" in a DB cluster is typically non-blocking but it will depend on the cluster setup. You have a primary PG node and a read-replica yeah?
- Read-replicas should never be syncing back to master, it should be a one-way sync from master -> slave and that should be async.

- TBH for multi-node speed and fault tolerance I would generally recommend MariaDB. PG is best for single-node performance but their clusters are less than great (personal bias here).
  - MariaDB's Galera cluster (with multi-master support) is far superior especially if your application is write heavy.

- ## [Strapi won't start on a pooled database  _202103](https://github.com/strapi/strapi/issues/9546)
- There is a difference between connection pooling and database pooling
  - Connection pooling is a group of connections to a database that can be reused (instead of opening a connection, requesting data, and closing it will keep the connection alive to request more data on another request.) Connection pooling is about reducing connection latency
  - Database pooling AKA Database clustering is entirely different and typically means you have a primary database node and multiple read-replicas. Knex.js doesn't support Database pooling.

- How about separating the read and write database connections at the application level? When there are more collection types, the initial startup time for strapi becomes very slow or unable to start even with connection pooling. Separating the read connections to a scalable read replica set could solve this issue. (I'm using Postgres in my case)
  - EG: ProxySQL or MariaDB Maxscale which allow for read/write splitting, monitoring, logging, and even caching which far exceed anything we can (or will do) at the application level

- ## [Why doesn't Strapi have a built-in refresh token feature? - Questions and Answers - Strapi Community Forum _202304](https://forum.strapi.io/t/why-doesnt-strapi-have-a-built-in-refresh-token-feature/27543)
- JWTs usually have an expiration time (e.g., 15 minutes, 1 hour) to limit their validity. 
  - When a token expires, the client needs to obtain a new one. 
  - This is often done using a refresh token, which is a separate, longer-lived token that the client can exchange for a new JWT. 
  - This is a standard procedure that pretty much every api uses. 
  - So, why is no such feature implemented in Strapi?

- ## [Sharp - Media Upload Memory Leak](https://github.com/strapi/strapi/issues/14417)

- ## 🐛 [Inconsistency between responses gotten from the REST API and the Entity service API_202401](https://forum.strapi.io/t/inconsistency-between-responses-gotten-from-the-rest-api-and-the-entity-service-api/34975)
- strapi-plugin-transformer plugin was what I was going to recommend. Another approach you can use, is to write a transformer function to flatten the response.

- Yes, the transform plugin is the way to go. 
  - But I’ve recently learned that it’s all a joke. 
  - You see, core controllers invoke the transformResponse function which iterates over the service response and produces this highly impractical data/meta/attributes structure. This takes time. Then, the middleware offered by the transform plugin iterates again over that transformed response and flattens it. Which takes time again. 
  - A performant way would be to disable that transformResponse function alltogether, or at least the part that wraps all non-id field within attributes. Maybe patch-package could be used for that.

- ## 🏘️ [Multi-tenancy | Voters | Strapi _202202](https://feedback.strapi.io/feature-requests/p/multi-tenancy)
