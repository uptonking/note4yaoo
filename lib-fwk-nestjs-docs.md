---
title: lib-fwk-nestjs-docs
tags: [docs, nestjs]
created: '2020-12-17T09:10:52.151Z'
modified: '2020-12-17T09:11:31.952Z'
---

# lib-fwk-nestjs-docs

- Node.js framework for building scalable server-side applications.

# guide

# Overview

- Nestjs uses progressive JavaScript, is built with and fully supports TypeScript (yet still enables developers to code in pure JavaScript) 
  - and combines elements of OOP (Object Oriented Programming), FP (Functional Programming), and FRP (Functional Reactive Programming).
- Under the hood, Nest makes use of robust HTTP Server frameworks like Express (the default) 
  - and optionally can be configured to use Fastify as well!
  - Nest provides a level of abstraction above these common Node.js frameworks (Express/Fastify), 
  - but also exposes their APIs directly to the developer. 
  - This gives developers the freedom to use the myriad of third-party modules which are available for the underlying platform.
- On the server-side, while there are a lot of superb libraries, helpers and tools for Node, none of them effectively solve the main problem - the architecture.
- **Nest aims to provide an application architecture out of the box** which allows for effortless creation of highly testable, scalable, loosely coupled and easily maintainable applications. 
  - The architecture is heavily inspired by Angular.

- Here's a brief overview of those core files:
  - `app.controller.ts`
    - A basic controller with a single route.
  - `app.module.ts`
    - The root module of the application.
  - `app.service.ts`
    - A basic service with a single method.
  - `main.ts`
    - The entry file of the application 
    - which uses the core function `NestFactory` to create a Nest application instance.
    - The static `create()` method returns an application object
    - This object provides a set of methods which are described in the coming chapters. 

- Nest aims to be a platform-agnostic framework.
  - Technically, Nest is able to work with any Node HTTP framework once an adapter is created. 
  - There are two HTTP platforms supported out-of-the-box: express and fastify.
  - Whichever platform is used, it exposes its own application interface. 
  - These are seen respectively as `NestExpressApplication` and `NestFastifyApplication`.

# Controllers

- A controller's purpose is to receive specific requests for the application. 
- Controllers are responsible for handling incoming requests and returning responses to the client.
- The routing mechanism controls which controller receives which requests. 
  - Frequently, each controller has more than one route, 
  - and different routes can perform different actions.
- In order to create a basic controller, we use classes and decorators. 
  - Decorators associate classes with required metadata and enable Nest to create a routing map 
  - (tie requests to the corresponding controllers).

- `@Controller()` decorator is required to define a basic controller. 
  - We can specify an optional route path prefix
  - Using a path prefix in a `@Controller()` decorator allows us to easily group a set of related routes, and minimize repetitive code. 
- `@Get()` decorator before the method tells Nest to create a handler for a specific endpoint for HTTP requests.
  - The endpoint corresponds to the HTTP request method (GET in this case) and the route path. 
  - Note that the method name we choose here is completely arbitrary. 
  - We obviously must declare a method to bind the route to, 
  - but Nest doesn't attach any significance to the method name chosen.
- The route path for a handler is determined by concatenating the (optional) prefix declared for the controller, and any path specified in the request decorator. 
- This method will return a 200 status code and the associated response
  - we'll first introduce the concept that Nest employs two different options for manipulating responses
- Standard
  - Using the built-in method
  - when a request handler returns a JavaScript object or array, it will automatically be serialized to JSON. 
  - When it returns a JavaScript primitive type (e.g., string, number, boolean), however, Nest will send just the value without attempting to serialize it. 
  - This makes response handling simple: just return the value, and Nest takes care of the rest.
  - Furthermore, the response's status code is always 200 by default, except for POST requests which use 201. 
  - We can easily change this behavior by adding the `@HttpCode(...)` decorator at a handler-level
- Library-specific
  - We can use the library-specific (e.g., Express) response object, 
  - which can be injected using the `@Res()` decorator in the method handler signature (e.g., findAll(@Res() response)). 
  - With this approach, you have the ability to use the native response handling methods exposed by that object. 
  - For example, with Express, you can construct responses using code like `response.status(200).send()`.

- Nest detects when the handler is using either `@Res()` or `@Next()`, indicating you have chosen the library-specific option
  - If both approaches are used at the same time, the Standard approach is automatically disabled for this single route and will no longer work as expected.
  - To use both approaches at the same time, you must set the `passthrough` option to true in the `@Res({ passthrough: true })` decorator.
    - (for example, by injecting the response object to only set cookies/headers but still leave the rest to the framework)
- Handlers often need access to the client request details. 
  - Nest provides access to the request object of the underlying platform (Express by default). 
  - We can access the request object by instructing Nest to inject it by adding the `@Req()` decorator to the handler's signature.
  - The request object represents the HTTP request and has properties for the request query string, parameters, HTTP headers, and body (read more here). 
  - In most cases, it's not necessary to grab these properties manually. 
  - We can use dedicated decorators instead, such as `@Body()` or `@Query()`, which are available out of the box. 
- For compatibility with typings across underlying HTTP platforms (e.g., Express and Fastify), Nest provides `@Res()` and `@Response()`decorators. 
  - `@Res()` is simply an alias for `@Response()`. 
  - Both directly expose the underlying native platform response object interface.
  - Note that when you inject either `@Res()` or `@Response()` in a method handler, you put Nest into Library-specific mode for that handler, and you become responsible for managing the response
  - When doing so, you must issue some kind of response by making a call on the response object (e.g. `res.json(...)` or `res.send(...)`), or the HTTP server will hang.

- Nest provides decorators for all of the standard HTTP methods: `@Get(), @Post(), @Put(), @Delete(), @Patch(), @Options(), and @Head()`. 
  - In addition `@All()` defines an endpoint that handles all of them.

- Pattern based routes are supported as well.
  -  The characters `?, +, *, and ()` may be used in a route path, and are subsets of their regular expression counterparts. 
  -  The hyphen (`-`) and the dot (`.`) are interpreted literally by string-based paths.

- To specify a custom response header, you can either use a `@Header()` decorator or a library-specific response object (and call `res.header()` directly).

- Routes with static paths won't work when you need to accept dynamic data as part of the request
- In order to define routes with parameters, we can add route parameter tokens in the path of the route to capture the dynamic value at that position in the request URL. 
  - Route parameters declared in this way `@Get(':id')` can be accessed using the `@Param()` decorator, which should be added to the method signature.

- The `@Controller` decorator can take a `host` option to require that the HTTP host of the incoming requests matches some specific value.
  - Since Fastify lacks support for nested routers, when using sub-domain routing, the (default) Express adapter should be used instead.

- For people coming from different programming language backgrounds, it might be unexpected to learn Scopes in Nest, 
  - almost everything is shared across incoming requests. 
  - We have a connection pool to the database, singleton services with global state, etc. 
  - Remember that Node.js doesn't follow the request/response Multi-Threaded Stateless Model in which every request is processed by a separate thread. 
  - Hence, using singleton instances is fully safe for our applications.
  - However, there are edge-cases when request-based lifetime of the controller may be the desired behavior, for instance per-request caching in GraphQL applications, request tracking or multi-tenancy.

- We love modern JavaScript and we know that data extraction is mostly asynchronous.
  - Every async function has to return a Promise. 
  - This means that you can return a deferred value that Nest will be able to resolve by itself. 
  - Nest route handlers are even more powerful by being able to return RxJS observable streams. 
  - Nest will automatically subscribe to the source underneath and take the last emitted value (once the stream is completed).

- Our previous example of the POST route handler didn't accept any client params. 
  - Let's fix this by adding the `@Body()` decorator here.
  - But first, we need to determine the DTO (Data Transfer Object) schema.
  - A DTO is an object that defines how the data will be sent over the network.
  - We could determine the DTO schema by using TypeScript interfaces, or by simple classes.
  - Interestingly, we recommend using classes here. 
  - Classes are part of the JavaScript ES6 standard, and therefore they are preserved as real entities in the compiled JavaScript. 
  - Since TypeScript interfaces are removed during the transpilation, Nest can't refer to them at runtime.
  - This is important because features such as Pipes enable additional possibilities when they have access to the metatype of the variable at runtime.

- Controllers always belong to a module, which is why we include the controllers array within the `@Module()` decorator. 

- The second way of manipulating the response is to use a library-specific response object. 
  - In order to inject a particular response object, we need to use the `@Res()` decorator
  - This approach should be used with care
  - The main disadvantage is that 
    - your code become platform-dependent (as underlying libraries may have different APIs on the response object), 
    - and harder to test (you'll have to mock the response object, etc.).
  - Also, in the example above, you lose compatibility with Nest features that depend on Nest standard response handling, such as Interceptors and @HttpCode() / @Header() decorators. 
    - To fix this, you can set the `passthrough` option to true
    - Now you can interact with the native response object (for example, set cookies or headers depending on certain conditions), but leave the rest to the framework.

``` JS
import { Controller, Get, Post, Res, HttpStatus } from '@nestjs/common';
import { Response } from 'express';

@Controller('cats')
export class CatsController {
  @Post()
  create(@Res() res: Response) {
    res.status(HttpStatus.CREATED).send();
  }

  @Get()
  findAll(@Res() res: Response) {
    res.status(HttpStatus.OK).json([]);
  }

  @Get()
  findAll2(@Res({ passthrough: true }) res: Response) {
    res.status(HttpStatus.OK);
    return [];
  }
}
```

# Providers

- Providers are a fundamental concept in Nest. 
  - Many of the basic Nest classes may be treated as a provider – services, repositories, factories, helpers, and so on. 
  - The **main idea of a provider is that it can inject dependencies**; 
  - this means objects can create various relationships with each other, 
    - and the function of "wiring up" instances of objects can largely be delegated to the Nest runtime system. 
  - A provider is simply a class annotated with an `@Injectable()` decorator.

- Controllers should handle HTTP requests and **delegate more complex tasks to providers**. 
  - Providers are plain JavaScript classes with an `@Injectable()` decorator preceding their class declaration.
  - `@Injectable()` decorator attaches metadata, which tells Nest that this class is a Nest provider.

- Since Nest enables the possibility to design and organize dependencies in a more OO-way, we strongly recommend following the SOLID principles.

- Nest is built around the strong design pattern commonly known as Dependency injection
- Providers normally have a lifetime ("scope") synchronized with the application lifecycle. 
  - When the application is bootstrapped, every dependency must be resolved, and therefore every provider has to be instantiated. 
  - Similarly, when the application shuts down, each provider will be destroyed. 
  - However, there are ways to make your provider lifetime request-scoped as well. 
- Nest has a built-in inversion of control ("IoC") container that resolves relationships between providers. 
  - This feature underlies the dependency injection feature 
- Occasionally, you might have dependencies which do not necessarily have to be resolved. 
  - For instance, your class may depend on a configuration object, 
  - but if none is passed, the default values should be used
  - In such a case, the dependency becomes optional, because lack of the configuration provider wouldn't lead to errors.
  - To indicate a provider is optional, use the `@Optional()` decorator in the constructor's signature.

- The technique we've used so far is called constructor-based injection, as providers are injected via the constructor method. 
  - In some very specific cases, property-based injection might be useful. 
  - For instance, if your top-level class depends on either one or multiple providers, passing them all the way up by calling super() in sub-classes from the constructor can be very tedious
    - In order to avoid this, you can use the `@Inject()` decorator at the property level.
  - If your class doesn't extend another provider, you should always prefer using constructor-based injection.

- we need to register the service with Nest so that it can perform the injection
  - We do this by editing our module file (`app.module.ts`) and adding the service to the providers array of the `@Module()` decorator.

# Modules

- A module is a class annotated with a `@Module()` decorator. 
-  The `@Module()` decorator provides metadata that Nest makes use of to organize the application structure.
- Each application has at least one module, a root module. 
  - The root module is the starting point Nest uses to build the application graph
    - the internal data structure Nest uses to resolve module and provider relationships and dependencies. 
  - While very small applications may theoretically have just the root module, this is not the typical case. 
  - We want to emphasize that modules are strongly recommended as an effective way to organize your components. 
  - Thus, for most applications, the resulting architecture will employ multiple modules, each encapsulating a closely related set of capabilities.

- A feature module simply organizes code relevant for a specific feature, keeping code organized and establishing clear boundaries. 
  - This helps us manage complexity and develop with SOLID principles, especially as the size of the application and/or team grow.
- The last thing we need to do is import this module into the root module (the `AppModule`, defined in the `app.module.ts` file).

- In Nest, modules are singletons by default, and thus you can share the same instance of any provider between multiple modules effortlessly.
  - Every module is automatically a shared module. 
  - Once created it can be reused by any module. 

- Modules can export their internal providers. 
  - In addition, they can re-export modules that they import. 

- A module class can inject providers as well (e.g., for configuration purposes)
  - However, module classes themselves cannot be injected as providers due to circular dependency .

- Unlike in Nest, Angular providers are registered in the global scope. 
  - Once defined, they're available everywhere. 
  - Nest, however, encapsulates providers inside the module scope. 
  - You aren't able to use a module's providers elsewhere without first importing the encapsulating module.
- The `@Global()` decorator makes the module global-scoped. 
  - Global modules should be registered only once, generally by the root or core module. 
  - Global modules are available to reduce the amount of necessary boilerplate. 
  - The imports array is generally the preferred way to make the module's API available to consumers.

- dynamic modules feature enables you to easily create customizable modules that can register and configure providers dynamically
- Note that the properties returned by the dynamic module extend (rather than override) the base module metadata defined in the `@Module()` decorator. 

# Middleware

- Middleware is a function which is called before the route handler. 
  - Middleware functions have access to the request and response objects, and the `next()` middleware function in the application’s request-response cycle. 
  - The next middleware function is commonly denoted by a variable named `next`.

- Nest middleware are, by default, equivalent to express middleware.
- Middleware functions can perform the following tasks:
  - execute any code.
  - make changes to the request and the response objects.
  - end the request-response cycle.
  - call the next middleware function in the stack.
  - if the current middleware function does not end the request-response cycle, it must call next() to pass control to the next middleware function. 
    - Otherwise, the request will be left hanging.

- You implement custom Nest middleware in either a function, or in a class with an `@Injectable()` decorator. 
  - The class should implement the NestMiddleware interface, while the function does not have any special requirements.
- Nest middleware fully supports Dependency Injection. 
  - Just as with providers and controllers, they are able to inject dependencies that are available within the same module.
  - we set them up using the `configure()` method of the module class. 
- The `MiddlewareConsumer` is a helper class. 
  - It provides several built-in methods to manage middleware. 
  - All of them can be simply chained in the fluent style. 

- The LoggerMiddleware class we've been using is quite simple. 
  - It has no members, no additional methods, and no dependencies. 
  - Why can't we just define it in a simple function instead of a class? 
  - This type of middleware is called functional middleware. 
- in order to bind multiple middleware that are executed sequentially, simply provide a comma separated list inside the `apply()` method
- If we want to bind middleware to every registered route at once, we can use the `use()` method that is supplied by the `INestApplication` instance

# Exception filters

- Nest comes with a built-in exceptions layer which is responsible for processing all unhandled exceptions across an application
- When an exception is not handled by your application code, it is caught by this layer, which then automatically sends an appropriate user-friendly response.
- Out of the box, this action is performed by a built-in global exception filter, which handles exceptions of type `HttpException` (and subclasses of it). 
- When an exception is unrecognized (is neither HttpException nor a class that inherits from HttpException), the built-in exception filter generates the following default JSON response

``` JSON
{
  "statusCode": 500,
  "message": "Internal server error"
}
```

- For typical HTTP REST/GraphQL API based applications, it's best practice to send standard HTTP response objects when certain error conditions occur.

- While the base (built-in) exception filter can automatically handle many cases for you, you may want full control over the exceptions layer. 
  - Exception filters are designed for exactly this purpose. 
  - They let you control the exact flow of control and the content of the response sent back to the client.

# Pipes

- A pipe is a class annotated with the `@Injectable()` decorator. 
- Pipes should implement the `PipeTransform` interface.
- Pipes have two typical use cases:
  - transformation
    - transform input data to the desired form (e.g., from string to integer)
  - validation
    - evaluate input data and if valid, simply pass it through unchanged; 
    - otherwise, throw an exception when the data is incorrect
- In both cases, pipes operate on the arguments being processed by a controller route handler. 
- Nest interposes a pipe just before a method is invoked, 
  - and the pipe receives the arguments destined for the method and operates on them. 
  - Any transformation or validation operation takes place at that time, after which the route handler is invoked with any (potentially) transformed arguments.
  - Nest comes with a number of built-in pipes that you can use out-of-the-box. You can also build your own custom pipes. 
- Nest comes with six pipes available out-of-the-box:
  - ValidationPipe
  - ParseIntPipe
  - ParseBoolPipe
  - ParseArrayPipe
  - ParseUUIDPipe
  - DefaultValuePipe
- To use a pipe, we need to bind an instance of the pipe class to the appropriate context.
  - we can bind the pipe at the method parameter level
- Passing an in-place instance is useful if we want to customize the built-in pipe's behavior by passing options

- To allow an endpoint to handle missing querystring parameter values, we have to provide a default value to be injected before the Parse* pipes operate on these values. 
  - The `DefaultValuePipe` serves that purpose. 
  - Simply instantiate a `DefaultValuePipe` in the `@Query()` decorator before the relevant Parse* pipe

# Guards

- A guard is a class annotated with the `@Injectable()` decorator. 
- Guards should implement the `CanActivate` interface.
- Guards have a single responsibility. 
  - They determine whether a given request will be handled by the route handler or not, depending on certain conditions (like permissions, roles, ACLs, etc.) present at run-time. 
  - This is often referred to as authorization. 
- Authorization (and its cousin, authentication, with which it usually collaborates) has typically been handled by middleware in traditional Express applications. 
  - Middleware is a fine choice for authentication, since things like token validation and attaching properties to the request object are not strongly connected with a particular route context (and its metadata).
  - But middleware, by its nature, is dumb. 
  - It doesn't know which handler will be executed after calling the `next()` function. 
- On the other hand, Guards have access to the `ExecutionContext` instance, and thus know exactly what's going to be executed next. 
  - They're designed, much like exception filters, pipes, and interceptors, to let you interpose(插入；插进) processing logic at exactly the right point in the request/response cycle, and to do so declaratively. 
  - This helps keep your code DRY and declarative.
- Guards are executed after each middleware, but before any interceptor or pipe.
  - middleware > guard > interceptor
- authorization is a great use case for Guards 
  - because specific routes should be available only when the caller (usually a specific authenticated user) has sufficient permissions. 
  - The `AuthGuard` that we'll build now assumes an authenticated user (and that, therefore, a token is attached to the request headers). 
  - It will extract and validate the token, and use the extracted information to determine whether the request can proceed or not.

- Every guard must implement a `canActivate()` function. 
  - This function should return a boolean, indicating whether the current request is allowed or not. 
  - It can return the response either synchronously or asynchronously (via a Promise or Observable). 
  - Nest uses the return value to control the next action:
  - if it returns true, the request will be processed.
  - if it returns false, Nest will deny the request.

# Interceptors

- An interceptor is a class annotated with the `@Injectable()` decorator. 
- Interceptors should implement the `NestInterceptor` interface.
- Interceptors have a set of useful capabilities which are inspired by the Aspect Oriented Programming (AOP) technique. 
- They make it possible to:
  - bind extra logic before/after method execution
  - transform the result returned from a function
  - transform the exception thrown from a function
  - extend the basic function behavior
  - completely override a function depending on specific conditions (e.g., for caching purposes)
- Each interceptor implements the `intercept()` method, which takes two arguments. 
- The first one is the `ExecutionContext` instance (exactly the same object as for guards).
  - we saw that it's a wrapper around arguments that have been passed to the original handler, and contains different arguments arrays based on the type of the application. 
- The second argument is a `CallHandler`. 
  - The CallHandler interface implements the` handle()` method, which you can use to invoke the route handler method at some point in your interceptor. 
  - If you don't call the `handle()` method in your implementation of the `intercept()` method, the route handler method won't be executed at all.
  - This approach means that the `intercept()` method effectively wraps the request/response stream. 
  - As a result, you may implement custom logic both before and after the execution of the final route handler. 
- Because the `handle()` method returns an Observable, we can use powerful RxJS operators to further manipulate the response. 
  - Using Aspect Oriented Programming terminology, the invocation of the route handler (i.e., calling `handle()`) is called a Pointcut, indicating that it's the point at which our additional logic is inserted.
- The first use case we'll look at is to use an interceptor to log user interaction 
  - (e.g., storing user calls, asynchronously dispatching events or calculating a timestamp).
- Interceptors have great value in creating re-usable solutions to requirements that occur across an entire application. 
  - For example, imagine we need to transform each occurrence of a `null` value to an empty string `''`. 
  - We can do it using one line of code and bind the interceptor globally so that it will automatically be used by each registered handler.
- There are several reasons why we may sometimes want to completely prevent calling the handler and return a different value instead. 
  - An obvious example is to implement a cache to improve response time.

# Request lifecycle

- Nest applications handle requests and produce responses in a sequence we refer to as the request lifecycle.
- With the use of middleware, pipes, guards, and interceptors, it can be challenging to track down where a particular piece of code executes during the request lifecycle, especially as global, controller level, and route level components come into play. 

- In general, **a request flows through middleware to guards, then to interceptors, then to pipes and finally back to interceptors** on the return path (as the response is generated).
- Middleware is executed in a particular sequence. 
  - First, Nest runs globally bound middleware (such as middleware bound with app.use) and then it runs module bound middleware
  - Middleware are run sequentially in the order they are bound, similar to the way middleware in Express works
  - the middleware bound to the root module will run first, and then middleware will run in the order that the modules are added to the imports array.
- Guard execution starts with global guards, 
  - then proceeds to controller guards, and finally to route guards. 
  - As with middleware, guards run in the order in which they are bound. 
- Interceptors, for the most part, follow the same pattern as guards, 
  - with one catch: as interceptors return RxJS Observables, the observables will be resolved in a first in last out manner. 类似堆栈
  - So inbound requests will go through the standard global, controller, route level resolution, 
  - but the response side of the request (i.e., after returning from the controller method handler) will be resolved from route to controller to global. 
  - Also, any errors thrown by pipes, controllers, or services can be read in the catchError operator of an interceptor.
- Pipes follow the standard global to controller to route bound sequence, 
  - with the same first in first out in regards to the `@usePipes()` parameters. 
  - However, at a route parameter level, if you have multiple pipes running, they will run in the order of the last parameter with a pipe to the first. 
  - This also applies to the route level and controller level pipes. 
- Filters are the only component that do not resolve global first. 
  - Instead, filters resolve from the lowest level possible, meaning execution starts with any route bound filters and proceeding next to controller level, and finally to global filters. 
  - Note that exceptions cannot be passed from filter to filter; 
  - if a route level filter catches the exception, a controller or global level filter cannot catch the same exception. 
  - The only way to achieve an effect like this is to use inheritance between the filters.
  - Filters are only executed if any uncaught exception occurs during the request process. 

- In summary, the request lifecycle looks like the following:
  - Incoming request
  - Globally bound middleware
  - Module bound middleware
  - Global guards
  - Controller guards
  - Route guards
  - Global interceptors (pre-controller)
  - Controller interceptors (pre-controller)
  - Route interceptors (pre-controller)
  - Global pipes
  - Controller pipes
  - Route pipes
  - Route parameter pipes
  - Controller (method handler)
  - Service (if exists)
  - Route interceptor (post-request)
  - Controller interceptor (post-request)
  - Global interceptor (post-request)
  - Exception filters (route, then controller, then global)
  - Server response

# Custom route decorators

- Nest is built around a language feature called decorators.
- An ES2016 decorator is an expression which returns a function and can take a target, name and property descriptor as arguments. 
  - You apply it by prefixing the decorator with an `@` character and placing this at the very top of what you are trying to decorate. 
  - Decorators can be defined for either a class, a method or a property.
- Nest provides a set of useful param decorators that you can use together with the HTTP route handlers. 
- When the behavior of your decorator depends on some conditions, you can use the data parameter to pass an argument to the decorator's factory function
- Passing data
- Working with pipes
- Decorator composition#

# Custom providers

- Dependency Injection is built in to the Nest core in a fundamental way. 
- Dependency injection is an inversion of control (IoC) technique wherein you delegate instantiation of dependencies to the IoC container (in our case, the NestJS runtime system), instead of doing it in your own code imperatively
- One key feature is that dependency analysis (or "creating the dependency graph"), is transitive. 
  - In the above example, if the CatsService itself had dependencies, those too would be resolved. 
  - The dependency graph ensures that dependencies are resolved in the correct order - essentially "bottom up". 
  - This mechanism relieves the developer from having to manage such complex dependency graphs.
- Custom providers
  - You want to create a custom instance instead of having Nest instantiate (or return a cached instance of) a class
  - You want to re-use an existing class in a second dependency
  - You want to override a class with a mock version for testing
- The `useValue` syntax is useful for injecting a constant value, putting an external library into the Nest container, or replacing a real implementation with a mock object. 
- Sometimes, we may want the flexibility to use strings or symbols as the DI token
- The `useClass` syntax allows you to dynamically determine a class that a token should resolve to. 
- The `useFactory` syntax allows for creating providers dynamically. 
- The `useExisting` syntax allows you to create aliases for existing providers. 
- While providers often supply services, they are not limited to that usage. 
  - **A provider can supply any value**.
  - For example, a provider may supply an array of configuration objects based on the current environment, 

# Asynchronous providers

- At times, the application start should be delayed until one or more asynchronous tasks are completed. 
  -  For example, you may not want to start accepting requests until the connection with the database has been established. 
  - You can achieve this using asynchronous providers.
- The syntax for this is to use `async/await` with the `useFactory` syntax. 
  - The factory returns a Promise, and the factory function can await asynchronous tasks. 
  - Nest will await resolution of the promise before instantiating any class that depends on (injects) such a provider.
- Asynchronous providers are injected to other components by their tokens, like any other provider. 

# Dynamic modules

- Modules define groups of components like providers and controllers that fit together as a modular part of an overall application. 
  - They provide an execution context, or scope, for these components. 
- All the information Nest needs to wire together the modules has already been declared in the host and consuming modules.
  - We'll refer to this as static module binding. 
- With static module binding, there's no opportunity for the consuming module to influence how providers from the host module are configured. 
  - Why does this matter? 
  - Consider the case where we have a general purpose module that needs to behave differently in different use cases. 
  - This is analogous to the concept of a "plugin" in many systems, where a generic facility requires some configuration before it can be used by a consumer.
- A good example with Nest is a configuration module. 
  - Many applications find it useful to externalize configuration details by using a configuration module. 
  - This makes it easy to dynamically change the application settings in different deployments, dev/prod
  - By delegating the management of configuration parameters to a configuration module, the application source code remains independent of configuration parameters.
- The challenge is that the configuration module itself, since it's generic (similar to a "plugin"), needs to be customized by its consuming module. 
  - This is where dynamic modules come into play.
  - Using dynamic module features, we can make our configuration module dynamic so that the consuming module can use an API to control how the configuration module is customized at the time it is imported.
- dynamic modules provide an API for importing one module into another, and customizing the properties and behavior of that module when it is imported, 
  - as opposed to using the static bindings we've seen so far.

# Injection scopes

- Remember that Node.js doesn't follow the request/response Multi-Threaded Stateless Model in which every request is processed by a separate thread. 
- Hence, using singleton instances is fully safe for our applications.
- However, there are edge-cases when request-based lifetime may be the desired behavior, for instance per-request caching in GraphQL applications, request tracking, and multi-tenancy. 
  - Injection scopes provide a mechanism to obtain the desired provider lifetime behavior.
- Using singleton scope is recommended for most use cases. 
  - Sharing providers across consumers and across requests means that an instance can be cached and its initialization occurs only once, during application startup.
- Using request-scoped providers will have an impact on application performance. 
  - While Nest tries to cache as much metadata as possible, it will still have to create an instance of your class on each request. 
  - Hence, it will slow down your average response time and overall benchmarking result. 
  - Unless a provider must be request-scoped, it is strongly recommended that you use the default singleton scope.

# Circular dependency

- A circular dependency occurs when two classes depend on each other. 
- Circular dependencies can arise in Nest between modules and between providers.
- Nest enables resolving circular dependencies between providers in two ways. 
- we describe using forward referencing as one technique, 
  - and using the ModuleRef class to retrieve a provider instance from the DI container as another.
- A circular dependency might also be caused when using "barrel files"/index.ts files to group imports. 
  - Barrel files should be omitted when it comes to module/provider classes. 
  - For example, barrel files should not be used when importing files within the same directory as the barrel file, i.e. `cats/cats.controller` should not import `cats` to import the `cats/cats.service` file. 
- A forward reference allows Nest to reference classes which aren't yet defined using the `forwardRef()` utility function
  - For example, if `CatsService` and `CommonService` depend on each other, both sides of the relationship can use `@Inject()` and the `forwardRef()` utility to resolve the circular dependency. 
  - WARNING: The order of instantiation is indeterminate. 
  - Make sure your code does not depend on which constructor is called first.
- An alternative to using `forwardRef()` is to refactor your code 
  - and use the `ModuleRef` class to retrieve a provider on one side of the (otherwise) circular relationship

# Module reference

- Nest provides the `ModuleRef` class to navigate the internal list of providers and obtain a reference to any provider using its injection token as a lookup key. 
  - The `ModuleRef` class also provides a way to dynamically instantiate both static and scoped providers. 
  - `ModuleRef` can be injected into a class in the normal way
- The `ModuleRef` instance (hereafter we'll refer to it as the module reference) has a `get()` method. 
  - This method retrieves a provider, controller, or injectable (e.g., guard, interceptor, etc.) that exists (has been instantiated) in the current module using its injection token/class name.
- Occasionally, you may want to resolve an instance of a request-scoped provider within a request context. 
  - In order to share the same DI container sub-tree, you must obtain the current context identifier instead of generating a new one 
  - To obtain the current context identifier, start by injecting the request object using `@Inject()` decorator.
- To dynamically instantiate a class that wasn't previously registered as a provider, use the module reference's `create()` method.
  - This technique enables you to conditionally instantiate different classes outside of the framework container.

# Execution context

- Nest provides several utility classes that help make it easy to write applications that function across multiple application contexts (e.g., Nest HTTP server-based, microservices and WebSockets application contexts). 
- These utilities provide information about the current execution context which can be used to build generic guards, filters, and interceptors that can work across a broad set of controllers, methods, and execution contexts.

- The `ArgumentsHost` class provides methods for retrieving the arguments being passed to a handler. 
  - It allows choosing the appropriate context (e.g., HTTP, RPC (microservice), or WebSockets) to retrieve the arguments from. 
  - The framework provides an instance of `ArgumentsHost`, typically referenced as a `host` parameter, in places where you may want to access it.
- `ArgumentsHost` simply acts as an abstraction over a handler's arguments.
  - For example, for HTTP server applications (when `@nestjs/platform-express` is being used), the `host` object encapsulates Express's `[request, response, next]` array, 
    - where `request` is the request object, 
    - `response` is the response object, 
    - and `next` is a function that controls the application's request-response cycle. 
  - On the other hand, for GraphQL applications, the `host` object contains the `[root, args, context, info]` array.
- When building generic guards, filters, and interceptors which are meant to run across multiple application contexts, we need a way to determine the type of application that our method is currently running in. 
  - Do this with the `getType()` method of `ArgumentsHost`
  - 常用type是http、rpc、graphql

- `ExecutionContext` extends `ArgumentsHost`, providing additional details about the current execution process. 
  - Like `ArgumentsHost`, Nest provides an instance of `ExecutionContext` in places you may need it, such as in the `canActivate()` method of a guard and the `intercept()` method of an interceptor
- The `getHandler()` method returns a reference to the handler about to be invoked. 
- The `getClass()` method returns the type of the Controller class which this particular handler belongs to.
- it gives us the opportunity to access the metadata set through the `@SetMetadata()` decorator from within guards or interceptors. 

- Nest provides the ability to attach custom metadata to route handlers through the `@SetMetadata()` decorator. 
  - We can then access this metadata from within our class to make certain decisions.
  - Reflector can be injected into a class in the normal way
  - The Reflector#get method allows us to easily access the metadata by passing in two arguments: a `metadata` key and a `context` (decorator target) to retrieve the metadata from. 

# Lifecycle events

- A Nest application, as well as every application element, has a lifecycle managed by Nest. 
- Nest provides lifecycle hooks that give visibility into key lifecycle events, and the ability to act (run registered code on your module, injectable or controller) when they occur.
- We can divide the overall lifecycle into three phases: initializing, running and terminating. 
- Using this lifecycle, you can plan for appropriate initialization of modules and services, manage active connections, and gracefully shutdown your application when it receives a termination signal.
- Lifecycle events happen during application bootstrapping and shutdown. 
- Nest calls registered lifecycle hook methods on modules, injectables and controllers at each of the following lifecycle events 
- Nest also calls the appropriate underlying methods to begin listening for connections, and to stop listening for connections.

# Platform agnosticism

- Nest is a platform-agnostic framework. 
- This means you can develop reusable logical parts that can be used across different types of applications.
- The Overview section of the documentation primarily shows coding techniques using HTTP server frameworks (e.g., apps providing a REST API or providing an MVC-style server-side rendered app). 
- However, all those building blocks can be used on top of different transport layers (microservices or websockets).
- In addition, the application context feature helps to create any kind of Node.js application - including things like CRON jobs and CLI apps - on top of Nest.

- By default, Nest makes use of the Express framework. 
  - Nest also provides compatibility with other libraries such as, for example, Fastify. 
  - Nest achieves this framework independence by implementing a framework adapter whose primary function is to proxy middleware and handlers to appropriate library-specific implementations
  - In order for a framework adapter to be implemented, the target library has to provide similar request/response pipeline processing as found in Express.
- Fastify is much faster than Express, achieving almost two times better benchmarks results.
- Express is widely-used, well-known, and has an enormous set of compatible middleware, which is available to Nest users out-of-the-box.

# Standalone applications

- There are several ways of mounting a Nest application. 
  - You can create a web app, a microservice or just a bare Nest standalone application (without any network listeners). 
- The Nest standalone application is a wrapper around the Nest IoC container, which holds all instantiated classes. 
  - We can obtain a reference to any existing instance from within any imported module directly using the standalone application object. 
  - Thus, you can take advantage of the Nest framework anywhere, including, for example, scripted CRON jobs. 
  - You can even build a CLI on top of it.

- The standalone application object allows you to obtain a reference to any instance registered within the Nest application

# Database

- Nest is database agnostic, allowing you to easily integrate with any SQL or NoSQL database. 
- At the most general level, connecting Nest to a database is simply a matter of loading an appropriate Node.js driver for the database, just as you would with Express or Fastify.
- You can also directly use any general purpose Node.js database integration library or ORM, such as Sequelize, Knex.js, TypeORM, and Prisma
- For convenience, Nest provides tight integration with TypeORM and Sequelize out-of-the-box, also @nestjs/mongoose
- For integrating with SQL and NoSQL databases, Nest provides the `@nestjs/typeorm` package.
  - Nest uses TypeORM because it's the most mature Object Relational Mapper (ORM) available for TypeScript

# Configuration

- Applications often run in different environments. 
- Depending on the environment, different configuration settings should be used. 
- Since configuration variables change, best practice is to store configuration variables in the environment.
- Externally defined environment variables are visible inside Node.js through the `process.env` global. 
  - This can quickly get unwieldy(笨拙的，不灵活的), especially in the development and testing environments where these values need to be easily mocked and/or changed.
- In Node.js applications, it's common to use `.env` files, holding key-value pairs where each key represents a particular value, to represent each environment. 
  - Running an app in different environments is then just a matter of swapping in the correct `.env`file.
- A good approach for using this technique in Nest is to create a `ConfigModule` that exposes a `ConfigService` which loads the appropriate `.env` file. 
  - While you may choose to write such a module yourself, for convenience Nest provides the `@nestjs/config` package out-of-the box. 

# HTTP module

- Axios is richly featured HTTP client package that is widely used.
- Nest wraps Axios and exposes it via the built-in `HttpModule`.
  - The `HttpModule` exports the `HttpService` class, which exposes Axios-based methods to perform HTTP requests. 
  - The library also transforms the resulting HTTP responses into Observables.
- To use the `HttpService`, first import `HttpModule`.
  - All `HttpService` methods return an `AxiosResponse` wrapped in an Observable object.
  - Axios can be configured with a variety of options to customize the behavior of the `HttpService`.

# Caching

- Caching is a great and simple technique that helps improve your app's performance. 
- It acts as a temporary data store providing high performance data access.
- Nest provides a unified API for various cache storage providers. 
  - The built-in one is an in-memory data store. 
  - However, you can easily switch to a more comprehensive solution, like Redis.
- The `cache-manager` package supports a wide-range of useful stores
  - https://github.com/BryanDonovan/node-cache-manager

- You may want to asynchronously pass in module options instead of passing them statically at compile time. 
  - In this case, use the `registerAsync()` method, which provides several ways to deal with async configuration.

# Serialization

- Serialization is a process that happens before objects are returned in a network response. 
- This is an appropriate place to provide rules for transforming and sanitizing the data to be returned to the client.
- Nest provides a built-in capability to help ensure that these operations can be performed in a straightforward way.
- While this chapter shows examples using HTTP style applications (e.g., Express or Fastify), the `ClassSerializerInterceptor` works the same for WebSockets and Microservices, regardless of the transport method that is used.

# Cookies

- An HTTP cookie is a small piece of data stored by the user's browser. 
  - Cookies were designed to be a reliable mechanism for websites to remember stateful information. 
  - When the user visits the website again, the cookie is automatically sent with the request.
- The middleware will parse the `Cookie` header on the request and expose the cookie data as the property `req.cookies`

# Session

- HTTP sessions provide a way to store information about the user across multiple requests, which is particularly useful for MVC applications.
- apply the `express-session` middleware as global middleware
  - The default server-side session storage is purposely not designed for a production environment. 
  - It will leak memory under most conditions, does not scale past a single process, and is meant for debugging and developing.

# Compression

- Compression can greatly decrease the size of the response body, thereby increasing the speed of a web app.
  - For high-traffic websites in production, it is strongly recommended to offload(卸载；清除) compression from the application server - typically in a reverse proxy (e.g., Nginx). 
  - In that case, you should not use compression middleware.
- Use the express compression middleware package to enable gzip compression.

# File upload

- To handle file uploading, Nest provides a built-in module based on the multer middleware package for Express. 
- Multer handles data posted in the `multipart/form-data` format, which is primarily used for uploading files via an HTTP POST request.
  - Multer cannot process data which is not in the `multipart/form-data` format

# Task Scheduling

- Task scheduling allows you to schedule arbitrary code (methods/functions) to execute at a fixed date/time, at recurring intervals, or once after a specified interval. 
  - In the Linux world, this is often handled by packages like `cron` at the OS level. 
  - For Node.js apps, there are several packages that emulate cron-like functionality. 
  - Nest provides the `@nestjs/schedule` package, which integrates with the popular Node.js `node-cron` package.

# Queues

- Queues are a powerful design pattern that help you deal with common application scaling and performance challenges. 
- Some examples of problems that Queues can help you solve are:
  - Smooth out processing peaks. 
    - For example, if users can initiate resource-intensive tasks at arbitrary times, you can add these tasks to a queue instead of performing them synchronously. 
  - Break up monolithic tasks that may otherwise block the Node.js event loop. 
    - For example, if a user request requires CPU intensive work like audio transcoding, you can delegate this task to other processes
  - Provide a reliable communication channel across various services. 
    - For example, you can queue tasks (jobs) in one process or service, and consume them in another. 
    - You can be notified (by listening for status events) upon completion
- Nest provides the `@nestjs/bull` package as an abstraction/wrapper on top of `Bull`, a popular, well supported, high performance Node.js based Queue system implementation.
  - Bull uses Redis to persist job data, so you'll need to have Redis installed on your system. 
  - Because it is Redis-backed, your Queue architecture can be completely distributed and platform-independent

# Events

- `@nestjs/event-emitter` provides a simple observer implementation, allowing you to subscribe and listen for various events that occur in your application. 
- Events serve as a great way to decouple various aspects of your application, since a single event can have multiple listeners that do not depend on each other.
- `EventEmitterModule` internally uses the `eventemitter2` package.

# Model-View-Controller

- Nest, by default, makes use of the Express library under the hood. 
- Hence, every technique for using the MVC (Model-View-Controller) pattern in Express applies to Nest as well
- In order to create an MVC app, we also need a template engine to render our HTML views
- If the application logic must dynamically decide which template to render, then we should use the `@Res()` decorator, and supply the view name in our route handler, rather than in the `@Render()` decorator
  - When Nest detects the `@Res()` decorator, it injects the library-specific `response` object. 
  - We can use this object to dynamically render the template.

# Server-Sent Events

- Server-Sent Events (SSE) is a server push technology enabling a client to receive automatic updates from a server via HTTP connection. 
- Each notification is sent as a block of text terminated by a pair of newlines
- To enable Server-Sent events on a route (route registered within a controller class), annotate the method handler with the `@Sse()` decorator.
- Server-Sent Events routes must return an Observable stream.
- The `sse` method returns an Observable that emits multiple `MessageEvent`
  - (in this example, it emits a new `MessageEvent` every second).
  - we can now create an instance of the `EventSource` class in our client-side application
  - `EventSource` instance opens a persistent connection to an HTTP server, which sends events in `text/event-stream` format. 
  - The connection remains open until closed by calling `EventSource.close()`.

``` typescript
export interface MessageEvent {
  data: string | object;
  id?: string;
  type?: string;
  retry?: number;
}

@Sse('sse')
sse(): Observable<MessageEvent> {
  return interval(1000).pipe(map((_) => ({ data: { hello: 'world' } })));
}

const eventSource = new EventSource('/sse');
eventSource.onmessage = ({ data }) => {
  console.log('New message', JSON.parse(data));
};
```

# Authentication

- Passport is the most popular node.js authentication library, 
- At a high level, Passport executes a series of steps to:
  - Authenticate a user by verifying their "credentials" (such as username/password, JSON Web Token (JWT), or identity token from an Identity Provider)
  - Manage authenticated state (by issuing a portable token, such as a JWT, or creating an Express session)
  - Attach information about the authenticated user to the Request object for further use in route handlers
- Passport has a rich ecosystem of strategies that implement various authentication mechanisms.
- `@nestjs/passport `module wraps and standardizes this pattern into familiar Nest constructs.

- For this use case, clients will start by authenticating with a username and password. 
  - Once authenticated, the server will issue a JWT that can be sent as a bearer token in an authorization header on subsequent requests to prove authentication. 
  - We'll also create a protected route that is accessible only to requests that contain a valid JWT.

# Authorization

- Authorization refers to the process that determines what a user is able to do. 
- Authorization is orthogonal and independent from authentication.
- However, authorization requires an authentication mechanism.
- Role-based access control (RBAC) is a policy-neutral access-control mechanism defined around roles and privileges. 
  - In this section, we'll demonstrate how to implement a very basic RBAC mechanism using Nest guards.
  - This example is named "basic" as we only check for the presence of roles on the route handler level. 
  - In real-world applications, you may have endpoints/handlers that involve several operations, in which each of them requires a specific set of permissions. 
  - In this case, you'll have to provide a mechanism to check roles somewhere within your business-logic, making it somewhat harder to maintain as there will be no centralized place that associates permissions with specific actions.
- Claims-based authorization
  - When an identity is created, it may be assigned one or more claims issued by a trusted party. 
  - A claim is a name-value pair that represents what the subject is, not what the subject can do.
  - instead of checking for specific roles, you should compare permissions. 
  - Every user would have a set of permissions assigned. 
  - Likewise, each resource/endpoint would define what permissions are required (for example, through a dedicated `@RequirePermissions()` decorator) to access them.
- CASL is an isomorphic authorization library which restricts what resources a given client is allowed to access. 
  - It's designed to be incrementally adoptable and can easily scale between a simple claim based and fully featured subject and attribute based authorization.

# Rate limiting

- A common technique to protect applications from brute-force attacks is rate-limiting. 
- Many Express packages exist to provide a rate-limiting feature. 
- A popular one is express-rate-limit.

# WebSockets

- In Nest, a gateway is simply a class annotated with` @WebSocketGateway()` decorator. 
- Technically, gateways are platform-agnostic which makes them compatible with any WebSockets library once an adapter is created. 
- There are two WS platforms supported out-of-the-box: `socket.io` and `ws`.
- Gateways can be treated as providers; 
  - this means they can inject dependencies through the class constructor. 
  - Also, gateways can be injected by other classes (providers and controllers) as well.
  - WARNING: Gateways are not instantiated until they are referenced in the providers array of an existing module.
- In general, each gateway is listening on the same port as the HTTP server, unless your app is not a web application, or you have changed the port manually. 
  - This default behavior can be modified by passing an argument 

- The only difference between the HTTP exception filter layer and the corresponding web sockets layer is that instead of throwing `HttpException`, you should use `WsException`.

- There is no fundamental difference between regular pipes and web sockets pipes. 
- There is no fundamental difference between web sockets guards and regular HTTP application guards. 
- There is no difference between regular interceptors and web sockets interceptors. T

- The WebSockets module is platform-agnostic, 
  - hence, you can bring your own library (or even a native implementation) by making use of `WebSocketAdapter` interface. 

# Microservice

- In addition to traditional (sometimes called monolithic) application architectures, Nest natively supports the microservice architectural style of development
- Wherever possible, Nest abstracts implementation details so that the same components can run across HTTP-based platforms, WebSockets, and Microservices.

- In Nest, a microservice is fundamentally an application that uses a different transport layer than HTTP.
  - Microservices use the TCP transport layer by default.

- Nest supports several built-in transport layer implementations, called transporters, which are responsible for transmitting messages between different microservice instances. 
  - Most transporters natively support both request-response and event-based message styles. 
  - Nest abstracts the implementation details of each transporter behind a canonical interface for both request-response and event-based messaging. 
  - This makes it easy to switch from one transport layer to another

- Microservices recognize both messages and events by patterns. 
  - A pattern is a plain value, for example, a literal object or a string. 
  - Patterns are automatically serialized and sent over the network along with the data portion of a message. 
  - In this way, message senders and consumers can coordinate which requests are consumed by which handlers.

- The request-response message style is useful when you need to exchange messages between various external services. 
  - With this paradigm, you can be certain that the service has actually received the message (without the need to manually implement a message ACK protocol).
  - However, the request-response paradigm is not always the best choice. 
  - For example, streaming transporters that use log-based persistence, such as Kafka or NATS streaming, are optimized for solving a different range of issues, more aligned with an event messaging paradigm

- If you just want to publish events without waiting for a response. 
  - In that case, you do not want the overhead required by request-response for maintaining two channels.
  - Suppose you would like to simply notify another service that a certain condition has occurred in this part of the system. 
  - This is the ideal use case for the event-based message style.
