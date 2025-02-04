---
title: lib-saas-react-admin-docs
tags: [docs, react-admin]
created: 2023-12-19T17:30:20.678Z
modified: 2023-12-19T17:30:32.009Z
---

# lib-saas-react-admin-docs

# guide

# docs

## overview

- React-admin was built with customization in mind. 
  - You can replace any react-admin component with a component of your own, for instance to display a custom list layout, or a different edit form for a given resource.

- Using an API As Data Source
- Each resource maps a name to an endpoint in the API

- Data Fetching
  - You can build a react-admin app on top of any API, whether it uses REST, GraphQL, RPC, or even SOAP
  - This works because react-admin doesn’t use `fetch` directly. 
  - Instead, it uses a Data Provider object to interface with your API, and react-query to handle data fetching.

- react-admin delegates authentication logic to an authProvider.
  - Just like a dataProvider, an authProvider is an object that handles authentication and authorization logic. 
  - It exposes methods that react-admin calls when needed, and that you can call manually through specialized hooks

- The List view displays a list of records, and lets users search for specific records using filters, sorting, and pagination.

- React-admin provides many hooks and components to let you build custom user experiences for editing and creating records, leveraging Material UI and react-hook-form.
- A Field component displays a given property of a record. Such components are used in the List and Show views, but you can also use them anywhere in your application, as long as there is a RecordContext.

- An Input component displays an input, or a dropdown list, a list of radio buttons, etc. 

- React-admin contains a global, synchronous, persistent store for storing user preferences. Think of the Store as a key-value database that persists between page loads.

- The `ra-realtime` package supports various realtime infrastructures:
  - supabase, socket.io
# more
