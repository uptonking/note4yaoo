---
title: lib-fwk-tanstack-docs
tags: [docs, tanstack]
created: 2025-12-16T06:25:36.794Z
modified: 2025-12-16T06:25:45.851Z
---

# lib-fwk-tanstack-docs

# guide

# overview

# overview

# router
- features
  - 100% inferred TypeScript support, Typesafe navigation
  - Nested Routing and layout routes (with pathless layouts)
  - File-based Route Generation
  - Mixed file-based and code-based routing
  - Parallel data loading
  - Automatic route prefetching
  - Built-in Route Loaders w/ SWR Caching
  - Designed for client-side data caches (TanStack Query, SWR, etc.)
  - Asynchronous route elements and error boundaries
  - Typesafe JSON-first Search Params state management APIs
  - middleware: Route matching/loading, earch param
  - Custom Search Param parser/serializer support

- search parameters are a first-class citizen in TanStack Router. 
  - While still based on standard URLSearchParams, TanStack Router uses a powerful parser/serializer to manage deeper and more complex data structures in your search params, all while keeping them type-safe and easy to work with.
  - It's like having useState right in the URL!

- TanStack Router provides a light-weight built-in caching layer that works seamlessly with the Router. This caching layer is loosely based on TanStack Query, but with fewer features and a much smaller API surface area.

- TanStack Router's router and route context is a powerful feature that allows you to define context that is specific to a route which is then inherited by all child routes. 
  - Even the router and root routes themselves can provide context.
  - Context can be built up both synchronously and asynchronously, and can be used to share data, configuration, or even functions between routes and route configurations. 

- TanStack Router's file-based routing approach is uniquely user-facing. Route configuration is generated for you either by the Vite plugin or TanStack Router CLI

- Every aspect of TanStack Router is designed to be as type-safe as possible. But to achieve this, we had to make some decisions that deviate from the norms in the routing world.
- Route configuration boilerplate?
  - You have to define your routes in a way that allows TypeScript to infer the types of your routes as much as possible.
  - Using `JSX` for defining your routes is out of the question, as TypeScript will not be able to infer the route configuration types of your router.
  - Maybe I could define my routes as a tree of nested objects as `json`?
  - At first glance, this seems like a good idea. It's easy to visualize the entire route hierarchy in one go.
  - It's not very scalable: As your application grows, the tree will grow and become harder to manage.
  - It's not great for code-splitting: You'd have to manually code-split each component and then pass it into the component property of the route, further complicating the route configuration with an ever-growing route configuration file.
  - What we found to be the best way to define your routes is to abstract the definition of the route configuration outside of the route-tree. Then stitch together your route configurations into a single cohesive route-tree that is then passed into the createRouter function.

- TypeScript module declaration for the router? You have to pass the Router instance to the rest of your application using TypeScript's module declaration.
  - Once you've constructed your routes into a tree and passed it into your Router instance (using createRouter) with all the generics working correctly, you then need to somehow pass this information to the rest of your application.
  - You could `import` the `Router` instance from the file where you created it and use it directly in your components. A downside to this approach is that you'd have to import the entire Router instance into every file where you want to use it. This can lead to increased bundle sizes and can be cumbersome to manage, and only get worse as your application grows
  - You could use TypeScript's `module` declaration to declare the Router instance as a module that can be used for type inference anywhere in your application without having to import it. We went with module declaration, as it is what we found to be the most scalable and maintainable approach

- Why push for file-based routing over code-based? We push for file-based routing as the preferred way to define your routes.
  - the configuration of the router has been done in a precise way that allows TypeScript to infer the types of your routes as much as possible.
  - TanStack Router requires all the routes (including the root route) to be stitched into a route-tree so that it may be passed into the createRouter function before declaring the Router instance on the module for type inference. 
  - Finally, comes the issue of code-splitting. As your application grows, you'll want to code-split your components to reduce the initial bundle size of your application. This can be a bit of a headache to manage when you're defining your routes in a single file or even across multiple files.
- The file-based routing approach is powered by the TanStack Router Bundler Plugin. It performs 3 essential tasks that solve the pain points in route configuration when using code-based routing:
  - Route configuration boilerplate: It generates the boilerplate for your route configurations.
  - Route tree stitching: It stitches together your route configurations into a single cohesive route-tree
  - Code-splitting: It automatically code-splits your route content components and updates the route configurations with the correct component. Additionally, at runtime, it ensures that the correct component is loaded when the route is visited.

- All other routes, other than the Root Route, are configured using the `createFileRoute` function, which provides type safety when using file-based routing
  - The reason for this pathname has everything to do with the magical type safety of TanStack Router. Without this pathname, TypeScript would have no idea what file we're in

- The root route is the top-most route in the entire tree and encapsulates all other routes as children.
  - It has no path
  - It is always matched
  - Its `component` is always rendered
- Basic routes match a specific path, for example /about, /settings, /settings/notifications are all basic routes, as they match the path exactly.

- Index routes specifically target their parent route when it is matched exactly and no child route is matched.

- Route path segments that start with a $ followed by a label are dynamic and capture that section of the URL into the params object for use in your application.
  - These params are then usable in your route's configuration and components
  - Dynamic segments work at each segment of the path. For example, you could have a route with the path of /posts/$postId/$revisionId and each $ segment would be captured into the params object

- A route with a path of only `$` is called a "splat" route because it always captures any remaining section of the URL pathname from the $ to the end. 
  - The captured pathname is then available in the params object under the special `_splat` property.
  - Why use $? Thanks to tools like Remix, we know that despite `*`s being the most common character to represent a wildcard, they do not play nice with filenames or CLI tools, so just like them, we decided to use $ instead.

- Optional path parameters allow you to define route segments that may or may not be present in the URL. They use the `{-$paramName}` syntax and provide flexible routing patterns where certain parameters are optional.

- Layout routes are used to wrap child routes with additional components and logic.
  - Since TanStack Router supports mixed flat and directory routes, you can also express your application's routing using layout routes within directories:
  - In this nested tree, the app/route.tsx file is a configuration for the layout route that wraps two child routes, app/dashboard.tsx and app/settings.tsx.

- Pathless Layout Routes are used to wrap child routes with additional components and logic. 
  - However, pathless layout routes do not require a matching `path` in the URL and are used to wrap child routes with additional components and logic without requiring a matching path in the URL
  - Pathless Layout Routes are prefixed with an underscore (_) to denote that they are "pathless".
  - unlike Layout Routes, since Pathless Layout Routes do not match based on URL path segments, this means that these routes do not support Dynamic Route Segments as part of their path and therefore cannot be matched in the URL.

- Pathless route group directories use () as a way to group routes files together regardless of their path. They are purely organizational and do not affect the route tree or component tree in any way.

- Non-nested routes can be created by suffixing a parent file route segment with a _ and are used to un-nest a route from its parents and render its own component tree.

- Files and folders can be excluded from route generation with a - prefix attached to the file name. 

- File-based routing is a way to configure your routes using the filesystem. 
  - Instead of defining your route structure via code, you can define your routes using a series of files and directories that represent the route hierarchy of your application.  
  - Most of the TanStack Router documentation is written for file-based routing
  - File-based routing allows TanStack Router to automatically code-split your routes for better performance.
  - Consistency: File-based routing enforces a consistent structure for your routes, making it easier to maintain and update your application and move from one project to another.
- If you find that the default file-based routing structure doesn't fit your needs, you can always use Virtual File Routes to control the source of your routes whilst still getting the awesome performance benefits of file-based routing.

- Code-based routing is no different from file-based routing in that it uses the same route tree concept to organize, match and compose matching routes into a component tree. 
  - The only difference is that instead of using the filesystem to organize your routes, you use code.

- The automatic code splitting feature in TanStack Router allows you to optimize your application's bundle size by lazily loading route components and their associated data.
  - TanStack Router's automatic code splitting works by transforming your route files both during 'development' and at 'build' time. It rewrites the route definitions to use lazy-loading wrappers for components and loaders, which allows the bundler to group these properties into separate chunks.
  - So when your application loads, it doesn't include all the code for every route. Instead, it only includes the code for the routes that are initially needed. As users navigate through your application, additional chunks are loaded on demand.
  - TanStack Router uses a concept called "Split Groupings" to determine how different parts of your route should be bundled together.
  - Split groupings are arrays of properties that tell TanStack Router how to bundle different parts of your route together. Each grouping is an list of property names that you want to bundle together into a single lazy-loaded chunk.
- TanStack Router provides several options to customize how your routes are split into chunks, allowing you to optimize for specific use cases or performance needs.

- 
- 
- 
- 
- 
- 
- 
- 

# start
- features
  - Full-document SSR - Server-side rendering for better performance and SEO
  - Streaming - Progressive page loading for improved user experience
  - Server Routes & API Routes - Build backend endpoints alongside your frontend
  - Server Functions - Type-safe RPCs between client and server
  - Middleware & Context - Powerful request/response handling and data injection
  - Middleware & Context - Powerful request/response handling and data injection
  - Full-Stack Bundling - Optimized builds for both client and server code
  - End-to-End Type Safety - Full TypeScript support across the entire stack

- The only relevant limitation is that TanStack Start does not currently support React Server Components, but we are actively working on integration and expect to support them in the near future.

- Start uses TanStack Router's file-based routing approach to ensure proper code-splitting and advanced type-safety.

- All code in TanStack Start is isomorphic by default - it runs and is included in both server and client bundles unless explicitly constrained.
  - Route loaders are isomorphic - they run on both server and client, not just the server.

- Build components that work without JavaScript and enhance with client-side functionality

- Environment-Aware Storage

- Understanding when to use server functions vs server-only functions
  - `createServerFn`: RPC pattern - server execution, client callable
  - `createServerOnlyFn`: Crashes if called from client

- Environment Variable Exposure
  - const apiKey = createServerOnlyFn(() => process.env. SECRET_KEY)

- Client-exposed: Use `VITE_` prefix for client-accessible variables

- Server functions let you define server-only logic that can be called from anywhere in your application - loaders, components, hooks, or other server functions. They run on the server but can be invoked from client code seamlessly.

- Server routes can be defined in your `./src/routes` directory of your project right alongside your TanStack Router routes and are automatically handled by the TanStack Start server.
  - Because server routes can be defined in the same directory as your app routes, you can even use the same file for both!

- In TanStack Start, routes matching the initial request are rendered on the server by default. 
  - This means `beforeLoad` and `loader` are executed on the server, followed by rendering the route components. 
  - The resulting HTML is sent to the client, which hydrates the markup into a fully interactive application.

- TanStack Start's SPA mode completely disables server-side execution of beforeLoad and loader, as well as server-side rendering of route components. 
  - Selective SSR allows you to configure server-side handling on a per-route basis, either statically or dynamically.

- No SSR doesn't mean giving up server-side features! SPA modes actually pair very nicely with server-side features like server functions and/or server routes or even other external APIs. It simply means that the initial document will not contain the fully rendered HTML of your application until it has been rendered on the client using JavaScript.
- Client-side Only is simpler - No SSR means less to go wrong with hydration, rendering, and routing.

- Caveats of SPA mode
  - Slower time to full content - Time to full content is longer since all JS must download and execute before anything below the shell can be rendered.
  - Less SEO friendly 

- After enabling the SPA mode, running a Start build will have an additional prerendering step afterwards to generate the html shell
  - Prerendering your application's root route only
  - Where your application would normally render your matched routes, your router's configured pending fallback component is rendered instead.
  - The resulting HTML is stored to a static HTML page called /_shell.html (configurable)
  - Default rewrites are configured to redirect all 404 requests to the SPA mode shell

- Other routes may also be prerendered and it is recommended to prerender as much as you can in SPA mode, but this is not required for SPA mode to work.

- Since the shell is prerendered using the SSR build of your application, any loaders, or server-specific functionality defined on your Root Route will run during the prerendering process and the data will be included in the shell.
  - This means that you can use dynamic data in your shell by using a loader or server-specific functionality.

- Static prerendering is the process of generating static HTML files for your application. 
  - it allows you to serve pre-rendered HTML files to users without having to generate them on the fly or for deploying static sites to platforms that do not support server-side rendering.
  - All static paths will be automatically discovered and seamlessly merged with the specified pages config

- 
- 
- 

# query

# db

# virtual

# more
