---
tags: [docs/react]
title: docs-react-router
created: '2019-08-01T16:03:46.390Z'
modified: '2020-06-30T12:40:22.711Z'
---

# docs-react-router

- React Router is a collection of navigational components that compose declaratively with your application. 

## dev-tips

- how to programmatically navigate using react router v4
	- 参考 https://stackoverflow.com/questions/42123261/programmatically-navigate-using-react-router-v4
	- In v4, for navigating programatically you need to access the history object, which is available through React context
	- as long as you have a `<BrowserRouter>` provider component as the top most parent in your application. 
	- The library exposes through context the router object, that itself contains history as a property. 
	- The history interface offers several navigation methods, such as  push, replace and goBack, among others.
	- https://reacttraining.com/react-router/web/api/history
	- The history object is mutable. Therefore it is recommended to access the location from the render props of `<Route>` , not from `history.location` . 
- Link vs Redirect
	- React Router's BrowserRouter maintains the history stack for you, which means that you rarely need to modify it manually.
	- You'll want to use Link or NavLink in almost all use cases
	- The Redirect will redirect the user from one route to a new route of your choosing, and then replace the last entry in the history stack with the redirected route.
		- redirect doesn't support  browser's back button
	- Link NavLink and Redirect all use the router's history api under the hood, using these components instead of history manually means that you are safe to any changes to the history api in the future. 
- how to route outside of the app
	- `<Route path='/external' component={() => window.location = 'https://external.com/path'}/>`
- how to scroll to top
	- https://reacttraining.com/react-router/web/guides/scroll-restoration/scroll-to-top

## resources

- docs 
  - https://reacttraining.com/react-router/web/guides/basic-components

## react-router docs

### Quick Start

``` js
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

const App = () => (
  <Router>
    <div>
      <Header />

      <Route exact path="/" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/topics" component={Topics} />
    </div>
  </Router>
);

const Home = () => <h2>Home</h2>;
const About = () => <h2>About</h2>;
const Topic = ({ match }) => <h3>Requested Param: {match.params.id}</h3>;
const Topics = ({ match }) => (
  <div>
    <h2>Topics</h2>

    <ul>
      <li>
        <Link to={ `${match.url}/components` }>Components</Link>
      </li>
      <li>
        <Link to={ `${match.url}/props-v-state` }>Props v. State</Link>
      </li>
    </ul>

    <Route path={ `${match.path}/:id` } component={Topic} />
    <Route
      exact
      path={match.path}
      render={() => <h3>Please select a topic.</h3>}
    />
  </div>
);
const Header = () => (
  <ul>
    <li>
      <Link to="/">Home</Link>
    </li>
    <li>
      <Link to="/about">About</Link>
    </li>
    <li>
      <Link to="/topics">Topics</Link>
    </li>
  </ul>
);

export default App;
```

### Basic Components

- There are three types of components in React Router: router components, route matching components, and navigation components.
- Routers
	- <BrowserRouter> and <HashRouter> routers both will create a specialized `history` object for you. 
	- you should use a <BrowserRouter> if you have a server that responds to requests and a <HashRouter> if you are using a static file server.
- Route Matching
	- There are two route matching components: <Route> and <Switch>.
	- Route matching is done by comparing a <Route>'s path prop to the current location’s pathname.
	- When a <Route> matches it will render its content and when it does not match, it will render null. 
	- A <Route> with no path will always match.
	- The <Switch> component is used to group <Route>s together.
	- A <Switch> will iterate over all of its children <Route> elements and only render the first one that matches the current location.
- Route Rendering Props
	- You have three prop choices for how you render a component for a given <Route>: component, render, and children.
	- component should be used when you have an existing component (either a React.Component or a stateless functional component) that you want to render.
	- render, which takes an inline function, should only be used when you have to pass in-scope variables to the component you want to render.
		- You should not use the component prop with an inline function to pass in-scope variables because you will get undesired component unmounts/remounts.
- Navigation
	- Wherever you render a <Link>, an anchor ( `<a>` ) will be rendered in your application's HTML.
	- The <NavLink> is a special type of <Link> that can style itself as "active" when its `to` prop matches the current location.
	- Any time that you want to force navigation, you can render a `<Redirect>` . When a `<Redirect>` renders, it will navigate using its to prop.

### Philosophy  

- Static Routing
	- In these frameworks, you declare your routes as part of your app's initialization before any rendering takes place. 

	  React Router pre-v4 was also static (mostly). Let's take a look at how to configure routes in express:   
		

``` js
		// Express Style routing:
		app.get("/", handleIndex);
		app.get("/invoices", handleInvoices);
		app.get("/invoices/:id", handleInvoice);
		app.get("/invoices/:id/edit", handleInvoiceEdit);

		app.listen();
```

	- 静态路由，即在渲染发生前先定义路由

- Dynamic Routing
	- When we say dynamic routing, we mean routing that takes place as your app is rendering, not in a configuration or convention outside of a running app. 
	- That means almost everything is a component in React Router. 
	- example

``` js
	// react-native
	import { NativeRouter } from "react-router-native";

	// react-dom (what we'll use here)
	import { BrowserRouter } from "react-router-dom";

	ReactDOM.render(
	  <BrowserRouter>
		<App />
	  </BrowserRouter>,
	  el
	);

	const App = () => (
	  <div>
		<nav>
		  <Link to="/dashboard">Dashboard</Link>
		</nav>
		<div>
		  <Route path="/dashboard" component={Dashboard} />
		</div>
	  </div>
	);
```

- Nested Routes
	- Route is just a component, just like div. So to nest a Route or a div, you just do it

- Responsive Routes
	-  think about the `/invoices` url for different screen sizes. On a large screen, /invoices isn't a valid route, but on a small screen it is! 
	- React Router's previous versions' static routes didn't really have a composable answer for this.
	- When routing is dynamic, however, you can declaratively compose this functionality.
	- example

``` js
	const App = () => (
	  <AppLayout>
		<Route path="/invoices" component={Invoices} />
	  </AppLayout>
	);

	const Invoices = () => (
	  <Layout>
		{/* always show the nav */}
		<InvoicesNav />
	
		<Media query={PRETTY_SMALL}>
		  {screenIsSmall =>
			screenIsSmall ? (
			  // small screen has no redirect
			  <Switch>
				<Route exact path="/invoices/dashboard" component={Dashboard} />
				<Route path="/invoices/:id" component={Invoice} />
			  </Switch>
			) : (
			  // large screen does!
			  <Switch>
				<Route exact path="/invoices/dashboard" component={Dashboard} />
				<Route path="/invoices/:id" component={Invoice} />
				<Redirect from="/invoices" to="/invoices/dashboard" />
			  </Switch>
			)
		  }
		</Media>
	  </Layout>
	);
```

### Redux Integration

- example

``` js
import { withRouter } from 'react-router-dom'
export default withRouter(connect(mapStateToProps)(Something))
```

- All of these require deeper integration react-router with redux:
	- Synchronize the routing data with, and accessed from, the store.
	- Be able to navigate by dispatching actions.
	- Have support for time travel debugging for route changes in the Redux devtools.

- Our recommendation is not to keep your routes in your Redux store at all. Reasoning:
	- Routing data is already a prop of most of your components that care about it. Whether it comes from the store or the router, your component's code is largely the same.
	- In most cases, you can use `Link, NavLink and Redirect` to perform navigation actions. 
		- Sometimes you might also need to navigate programmatically, after some asynchronous task that was originally initiated by an action. 
		- For example, you might dispatch an action when the user submits a login form. 
		- Your thunk, saga or other async handler then authenticates the credentials, then it needs to somehow navigate to a new page if successful. 
		- The solution here is simply to include the `history` object (provided to all route components) in the payload of the action, and your async handler can use this to navigate when appropriate.
	- Route changes are unlikely to matter for time travel debugging. The only obvious case is to debug issues with your router/store synchronization, and this problem goes away if you don’t synchronize them at all.
- But if you feel strongly about synchronizing your routes with your store, you may want to try Connected React Router
- https://github.com/supasate/connected-react-router

### Dealing with Update Blocking

- React Router has a number of location-aware components that use the current location object to determine what they render. 
- By default, the current location is passed implicitly to components using React's context model. 
- When the location changes, those components should re-render using the new location object from the context.
- React provides two approaches to optimize the rendering performance of applications:
	- the `shouldComponentUpdate` lifecycle method and the `PureComponent` . 
	- Both block the re-rendering of components unless the right conditions are met. 
	- Unfortunately, this means that React Router's location-aware components can become out of sync with the current location if their re-rendering was prevented.
- In order for a component that implements shouldComponentUpdate to know that it should update when the location changes, 
	- If you are implementing shouldComponentUpdate yourself, you could compare the location from the current and next context.router objects. 
- PureComponent / redux / mobx can use `withRouter()`
- Recommended Solution
	- The key to avoiding blocked re-renders after location changes is to pass the blocking component the location object as a prop.
	- `<UpdateBlocker location={location} />`
	- In order to pass the current location object as a prop to a component, you must have access to it. 

	  The primary way that a component can get access to the location is via a <Route> component. 
	  When a <Route> matches (or always if you are using the children prop), it passes the current location to the child element it renders.

- example

``` js
// the Blocker is a pure component, so it will only update when it receives new props
class Blocker extends React.PureComponent {
  render() {
    return (
      <div>
		<NavLink to="/oz">Oz</NavLink>
		<NavLink to="/kansas">Kansas</NavLink>
	  </div>
    );
  }
}

// The <Blocker>'s location prop will change whenever the location changes
// A component rendered directly by a <Route> does not have to worry about blocked updates because it has the location injected as a prop.
<Route path="/:place" component={Blocker} />

// A component rendered directly by a <Route> can pass that location prop to any child elements it creates.
<
Route path = "/parent"
component = { Parent }
/>;

const Parent = props => {
  // <Parent> receives the location as a prop. Any child element it creates can be passed the location.
  return (
    <SomeComponent>
	  <Blocker location={props.location} />
	</SomeComponent>
  );
};
```

- What happens when the component isn't being rendered by a `<Route>` and the component rendering it does not have the location in its variable scope?
  - Render a pathless <Route>, wrap your connected component in a pathless `<Route />`

``` js
	// pathless <Route> = <Blocker> will always be rendered
	const MyComponent = () => (
	  <SomeComponent>
		<Route component={Blocker} />
	  </SomeComponent>
	);
```

	- wrap a component with the `withRouter` higher-order component and it will be given the current location as one of its props.  

``` js
	const BlockAvoider = withRouter(Blocker);

	const MyComponent = () => (
	  <SomeComponent>
		<BlockAvoider />
	  </SomeComponent>
	);
```

##  API Reference

- `<StaticRouter>`
	- it is a Router that never changes location.
	- useful in server-side rendering scenarios

## changelog

- 4.4.0-2019
	- Removed the single-child restriction in `<Router>` so you can have multiple children, provided you're using React 16
	- Migrated our underlying infrastructure to use React's new context API. 
	- Both our CJS and ESM builds now use Rollup
	- Adds support for an array of paths in `<Route path>`
- 4.3.0-20180606
	- Expose generatePath
	- Use the pretty option in generatePath
	- Redirect with parameters
	- Escape NavLink path to allow special characters in path
	- Add invariant for missing "to" property on `<Link>`
	- Fix pathless route's match when parent is null
	- Use history.createLocation in `<StaticRouter>`
- 4.2.0-20170823
	- Prevent remounts on routes with the same component in renderRoutes
	- Case sensitive routes
	- Use Jest for testing     
	- Fix memory leak in ConnectedRouter during server side rendering
- 4.1.0-20170411
	- Add wrappedComponent to the component returned by withRouter
	- Add wrappedComponentRef prop to the component returned by withRouter
- 4.0.0-20170310
	- React Router v4 is a complete rewrite, so there is not a simple migration path.
	- react-router-redux  has been deprecated. It is recommended that you separate out Redux and React Router, as their state semantics don't match up exactly. 
		- But if you wish to attempt to keep them in sync, you can use a library such as connected-react-router.
	- Added support for `<Redirect>` as a child of a `<Switch>`
	- Removed subscriptions to avoid unnecessary rerendering in every `<Route>`
	- Added `<Switch location> and <Route location>` props so that "pure" route components can know when the location changes
	- Revert to using context.router for everything since Relay uses context.route
