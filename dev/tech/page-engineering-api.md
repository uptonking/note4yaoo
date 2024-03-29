---
title: page-engineering-api
tags: [api, engineering]
created: 2020-12-27T10:26:58.415Z
modified: 2020-12-27T10:32:58.026Z
---

# page-engineering-api

# [GitHub: To infinity and beyond: enabling the future of GitHub's REST API with API versioning_202211](https://github.blog/2022-11-28-to-infinity-and-beyond-enabling-the-future-of-githubs-rest-api-with-api-versioning/)

- We launched version 3 (“V3”) of our API more than a decade ago. 
  - It has served us well, 
  - but we haven’t had the right tools and processes in place to make occasional breaking changes AND give existing users a smooth migration path and plenty of time to upgrade their integrations.
- we’re introducing calendar-based versioning for the REST API.

- Versions will be named based on the date when they were released. 
  - We’ll only use versioning for breaking changes. 
  - Non-breaking changes will continue to be available across all API versions.
  - Picking what version you want to use is easy. 
  - You just specify the version you want to use on a request-by-request basis using the `X-GitHub-Api-Version` header.
- When a new REST API version is released, we’re committed to supporting the previous version for at least two years (24 months).
  - After two years, we reserve the right to retire a version
# [Material-UI API Design Approach](https://material-ui.com/guides/api/)
- As Sebastian Markbage pointed out, no abstraction is superior to wrong abstractions. 
  - We are providing low-level components to maximize composition capabilities.

- Composition
  - Using the `children` property is the idiomatic way to do composition with React.
  - Sometimes we only need limited child composition, 
    - for instance when we don't need to allow child order permutations(排列；数列). 
    - In this case, providing explicit properties makes the implementation simpler and more performant; 
    - for example, the `Tab` takes an `icon` and a `label` property.
  - API consistency matters.

- Spread
  - Props supplied to a component which are not explicitly documented, are spread to the root element; 
    - for instance, the `className` property is applied to the root.

- Avoid native properties
  - We avoid documenting native properties supported by the DOM like `className`.

- CSS Classes
  - All components accept a `classes` prop to customize the styles. 
  - The classes design answers two constraints: to make the classes structure as simple as possible, while sufficient to implement the Material Design specification.
  - The class applied to the root element is always called `root`.
  - All the default styles are grouped in a single class.
  - The classes applied to non-root elements are prefixed with the name of the element, e.g. `paperWidthXs` in the Dialog component.
  - The variants applied by a boolean property aren't prefixed, e.g. the rounded class applied by the `rounded` property.
  - The variants applied by an enum property are prefixed, e.g. the `colorPrimary` class applied by the `color="primary"` property.
  - A variant has one level of specificity. 
    - The color and variant properties are considered a variant.
    - The lower the style specificity is, the simpler it is to override.
  - We increase the specificity for a variant modifier. 
    - We already have to do it for the pseudo-classes (:hover, :focus, etc.). 
    - It allows much more control at the cost of more boilerplate. 
    - Hopefully, it's also more intuitive.

- Nested components
  - Nested components inside a component have their own
    - flattened properties
    - `xxxProps` property
    - `xxxComponent` property
    - `xxxRef` prop

- Property naming
  - The name of a boolean property should be chosen based on the default value.

- Controlled components
  - Most of the controlled component are controlled via the `value` and the `onChange` properties, 
  - however, the `open/onClose/onOpen` combination is used for display related state.

- boolean vs enum
  - There are two options to design the API for the variations of a component: 
    - with a boolean
      - This API enables the shorthand notation
    - or with an enum/联合类型
      - This API is more verbose
      - However it prevents an invalid combination from being used, bounds the number of properties exposed, and can easily support new values in the future.
  - Material-UI components use a combination of the two approaches according to the following rules:
    - A boolean is used when 2 possible values are required.
    - An enum is used when > 2 possible values are required, or if there is the possibility that additional possible values may be required in the future.

- Ref
  - The `ref` is forwarded to the root element. 
  - This means that, without changing the rendered root element via the `component` prop, it is forwarded to the outermost DOM element which the component renders. 
  - If you pass a different component via the `component` prop, the ref will be attached to that component instead.
# discuss
- ## 

- ## 

- ## I often hear "minimal APIs are just for toy apps" - I use them all the time and love them, for big and small projects, 
- https://twitter.com/TessFerrandez/status/1719376588825919826
  - so I decided to jolt down some quick notes about how we organize our minimal APIs to make them maintainable and testable
  - [Organizing ASP.NET Core Minimal APIs - If broken it is, fix it you should](https://www.tessferrandez.com/blog/2023/10/31/organizing-minimal-apis.html)
  - since minimal APIs were introduced in ASP.NET Core, I’ve been using them for all our projects, and I’ve been very happy with them. 
  - Before then, I have also used similar minimal apis in python (FastAPI and Flask).
- I always use Minimal APIs, pretty much the way you're describing, using an EndpointConfiguration file where all the routes are described, and separate endpoint files per feature. Using groups makes it even cleaner. Couldn't be happier with this approach!
- Often use minimal APIs where we compose multiple APIs behind one api gateway. Makes it easy to confidently and reliably develop, test and maintain
- I prefer minimal API too, however the lock in of System.Text.Json is a draw back when you need the power of Newtonsoft.Json

- ## Here are 6 tips for effective API design:
- https://twitter.com/mjovanovictech/status/1717149101509222598
  - Use resource names in plural (/todo/123 vs. /todos/123)
  - Pagination (/todos?page=1&pageSize=10)
  - Filtering (/todos?searchTerm='. NET')
  - Sorting (/todos?sort_col=deadline)
  - Use versioning (/v1/todos)
  - Rate limiting

- What are the benefits of plural vs singular?
