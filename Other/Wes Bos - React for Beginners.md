# Wes Bos - React for Beginners

_Code notes from this video are not listed because I built the project beside the lessons._

## Video 1

Generic high-level overview of the tools and course content.

## Video 2

React differs from other popular frameworks in that it isn't a framework, but a library. React doesn't use the MVC pattern: everything in React is a component. A component is essentialy a customized element. For example, we may use a `<Fish />` element that renders HTML displaying a menu card for fish. This component will render the content in a similar way that `<hr />` or any other HTML element functions.

Any time you have a "piece" of an application, it's generally good to have it built as a component.

## Video 3

In this lesson, we build our first component that allows a user to pick a store and then uses React render to point them to the URL of the store. To begin, we need to globally import React into our `index.js` file pulling from the `react` package.

### Classes and Mounting

Every component in React is a class. It's considered best practice to put a capital on the front of all of your classes. All of the classes inside of React require at least one method: `render()`, which determines what DOM elements are output. Within our `render()` method, we return the HTML we want.

Our classes will only display in the DOM when we mount our application; the idea behind react is that we never touch the DOM directly, but work in the shadow DOM to render to the page. The only time the DOM is touched is by mounting our main application from the package `react-dom`.

The reason `react` can be used without `react-dom` is because `react` is not DOM exclusive; it can be used outside of the browser, and the package `react-dom` is browser (DOM) exclusive.

```jsx
import { render } from 'react-dom';
// Aliased: import { render as ReactDOM } from 'react-dom';

render(<App />, document.querySelector('#app'));
// Aliased: ReactDOM(<App />, document.querySelector('#app'));
```

Once we're ready to mount our components, it's considered best practice to store your components in modular design rather than one big file. This aids in reusability while also keeping code more readable. When splitting these components into their `src/components` folder, it's usually a good idea to name them the same as your file name.

To make your modularized component usable, the module must be imported into the file chain. On our main application, we want to import our class to make it available to the render function. `React` **must always be imported into components** for a component to work, even when they're being imported to the main component. After importing React, you make the component you want, then export it via `export default MyClass`.

## Video 4

JSX, the syntax recognized by React to render elements from JavaScript, is recommended over using base React code, i.e. `React.createElement()` due to its simplicity and readability. It's important to keep im mind that using multi-lined entries for a `render() { return ... }` will automatically slap a semi-colon into the end of return if it's split into multiple lines. This can be avoided by wrapping the contents in `()`.

Components must be returned as a single element; these elements can have nested elements, but you can't return sibling elements. That being said, React 16 now offers the ability to wrap things in a `<React.Fragment>` tag which allows you to return a block of content inside of the fragment. The `<React.Fragment>` tag will render to _nothing_, leaving only the content inside. This replaced the workaround of having to use a `div` which was known to cause issues with CSS.

``` jsx
class StorePicker extends React.Component {
  render() {
    return (
      <React.Fragment>
        <p>Fish!</p>
        <form className="store-selector">
          <h2>Please Enter a Store</h2>
        </form>
      </React.Fragment>
    )
  }
}
```

Note that comments in JSX are not the same as HTML or JavaScript, you need to wrap the comments in curly brackets and use full-length JS commenting format: `{/* This comment will work. */}`.

## Video 5

Importing CSS can be done in a couple of different ways, there's arguments for importing it into the HTML, importing it into individual components, and importing it into the main application. All of these ways work, but most of the time you'll see a main import for the application entry. Part of the `react-scripts` package includes bundling through webpack, and webpack is able to recognize our `import 'style.css'` file and place it between a `style` tag. Due to the hot-reloading functionality, it automatically shows up into our live server.

## Video 6

We'll be creating our `<App />` component, which is kind of like the king of all other components. It imports and houses all of our individual pieces in one location. This is nested in the `components` folder and is home to `<OtherComponent />`, named for each component we import. We use the boilerplate `import ... class ... export` for each component, then import it into the App.js file. We can then use these imports a `<MyComponent />`.

## Video 7

Components function in very much the same way as elements. If we took an `img` tag with the _attributes_ `src="dog.jpg"` and `alt="Dog"`, our `img` tag knows what to do with these attributes because it's been designed to process that specific data. In React, we now refer to those _attributes_ as **props**, or properties. We pass data through props to give it data - again, this is akin to passing information into an HTML tag. You can think of **state** and **props** as the "home" and the "car" of React. State is where data lives, and props is how it is passed from one component to another so it can be used where it's needed.

Props are entirely customized, there's nothing preset outside of reserved words so we can give it the name we want and tie it to the data we want. Props is passed as an object, so on a very fundamental level we can see this as `<Header tagline="My Words">` passing `{tagline: "My Words}`. Anything passed other than a string must be wrapped in curly brackets, e.g. `age={54}`.

We import passed props to their components via `this.props.myProp`, passed through curly brackets to signify that we're parsing JavaScript and not JSX. `this` in this context represents the component `this` is inside of.

**Components are just instanced objects!** You can view the content of the named object by taking a look at `$r` in the developer's tools the same way to look at `$0` for HTML (displayed as `== $0`).

## Video 8

Stateless functional components are another part of React that can be used instead of extending React.Component when there is no existing state on an object. Since we're returning with an arrow function, we can implicitly return our data by using a `()` wrapper which would indicate a `return` without having to include `{}`. We drop the render method and are left with a bare-bones function export.

``` jsx
const MyComponent = props => (
  <div>props.myProperty</div>
);
```

The `props` argument can also be further deconstructed to the only variables we need by using the deconstruction technique `= ({ prop1, prop2 })` and droping the `props.` from any property calls. Writing a stateless functional component isn't mandatory, but if you don't expect to need to expand the object to hold state it can save time and produces cleaner, faster code.

## Video 9

Since React isn't a framework, it doesn't come packaged with the ability to route components like Angular or Vue might. For this reason we need to use `react-router` or a similar routing tool that allows dynamic URL loading. Everything in React is a component, even the router. Since we're working with the DOM, we import `react-router-dom`. We import `{ BrowserRouter, Route, Switch }` from the package.

Routes take two main parameters, `path` and `component`, where `path` represents the URL location and the component is what is displayed when that location is hit. Adding `exact` to the arguments will ensure it loads the component only when the URL is an exact match. Adding a word behind a colon will dynamically give that location in the URL a param, i.e. `path="store/:storeid"` would render `storeid: '123'` when hitting `store/123`.

## Video 10

Helper functions don't typically need to be stored in a component and can instead be placed into a `helpers.js` file on the root of the application. React doesn't like having `value=""` called because it's supposed to be represented by state, but you can still give a default value by passing `defaultValue=""` on your inputs.

## Video 11

Events in React work like any other event, but they're wrapped in something called a SyntheticEvent that handles cross-browser compatability for the developer automatically. Events are handled in-line by passing `on` and the name of the event to look for, e.g. `onClick={this.handleClick}`. Our function is not called with `()` because that would cause it to fire as soon as the component mounts.

When working with React event calls, you may need to disable the default action of the effect. For example, on submitting a form the page will refresh. This can be deactivated by passing `event.preventDefault();` in the event handler.

To pull the value of our input box we want to pass a `ref` to our handler. React applications shouldn't touch the DOM, so using `document.querySelector()` is generally not a good idea. Using refs has been changed since original use, where string refs and function refs are depreciated in favor of a newer method: putting your ref in the component as a variable with `myVar = React.createRef();` and tagging the element with `ref={this.myVar}`. We can't call the `this` tag in our handler method yet though, because all custom methods that didn't come with React are not bound by default.

Binding `this` to custom methods can be done by passing them through a `constructor()`. ES6 proposes a better way by declaring a property and setting it with an arrow function since arrow functions automatically bind to their lexical container.

``` jsx
constructor() {
  super();
  this.goToStore = this.goToStore.bind(this);
}

// Do this instead, though:

goToStore = (event) => {
  console.log(this)
}
```

## Video 12

Now that we can grab out data via `this.myInput.current.value`, we want to work with changing the url. We can use what's known as push-state rather than refreshing the page via `window.location`, which will only update our page's content. Since we're already passing our store picker through the Router page, we can access all of the higher-level router functions via props: `this.props.history.push()`.

## Video 13

State is an object that stores data for a component; data can always be passed down, but not up. State and the method that updates state must live in the same component. Since we want to pass data to three of our components, we need to nest it in the top-level component, App. To set state you must use React's `this.setState` API or the state won't work appropriately. State should never be directly modified since React is a functional progrmaming language (no mutations). We can pass an existing copy of the state by setting the property to a variable, compiling the new data, then resetting the state.

## Video 14

Nothing new learned; imported the sample-fishes.js object into state.

## Video 15

In this lesson we import Fish to the CotD list. JSX doesn't have any kind of logic built into it (if, for, etc). To use logic, we need to use normal JS via `{}`. Since our state is an object, we can't `.map` over it, so it needs to be converted to an array via `Object.keys`.

Any time we output a list of data, we need to give each item a unique key for React to use as an identifier. Each fish has a unique name so we can just render `key` (e.g. "fish1") in out `key={}` output.

Because writing `this.props.thing.thing` can become exhausting, it's generally a good idea to set a variable to props by giving a const above the return like and below the render method. We can use ES6 destructuring to make this even cleaner.

## Video 16

It is possible to call a function without having to hardcode it via `$r.myFunction(myProps)`, where $r will hook into React via the console. We also want to pass our key in the function we use in this method. React will _not_ allow you to access a key without passing it as a prop with something other than `key`! `index={key}` is generally accepted.

## Video 17

We need to pass our data to the Order component. We can do this by individually calling everything in our state object, or we can pass this via an object spread. `{...this.state}` will pass everything in state. This isn't generally a good idea though, because when you make a modular component you want to know exactly what data is getting passed in.

## Video 18

Firebase is a backend-as-a-service containing real time data management, while MongoDB is a database with a rich query language that can be run locally. Firebase uses websockets so we can live-reload data rather than having to ping with AJAX for a change. In short, Firebase offers more than "just a database".

Firebase can be connected via `re-base` and `firebase` in React. `firebase` calls the specific database configuration, while `re-base` initializes the application. To have our state information passed into our database, we need to explore **lifecycle methods** so we can pass state once the App has actually been loaded.

We use `componentDidMount()` to execute our database the moment our `App` component is functional. Because firebase will live-listen for changes, it's important to make sure we stop listening once the component unmounts. This can be implemented through `componentWillUnmount()`.

## Video 19

While having persistant data for the store is useful in a database because it provides the users with an immediate update to inventory and availability, storing the user's local information isn't really something we need to do. We can instead store the user's local order in their _localstorage_ to help persist it across page use without having to store their information indefinitely on our database.

We can monitor for changes by using `componentDidUpdate()`, which won't fire on the initial render but will fire on any component updates.

Since we're trying to store `order` from our state, which is an object, we need to parse it with JSON to prevent it from logging `[object Object]` which is simply the `.toString()` call on our `order` object (i.e. useless). - `JSON.stringify(myObj)`.

Due to our `componentDidMount()` firing on pageload, which will trigger `componentDidUpdate` since we're setting new properties, we must first pull our localStorage from the existing local data for it to be used without being overwritten by a blank object. We stringified our object with JSON, so it needs to be converted back to an object to be of any use.

It's important to note that Firebase and localStorage have different sync times so localStorage should fill data after Firebase has provided what's needed.

## Video 20

In this video we passed our fish data into an editable form for updating existing fish. This causes an issue, however, because React doesn't allow you to have state in two places (the input and state). This can be resolved by having a handler on each edit.

If we pass a `name=""` property into our inputs, we can call that on the event fire via `event.currentTarget.name` which will allow you to dynamically update the properties in your event. To pass the data back upstream we need to pass down a method that can be called from the update form.

## Video 21

To allow items to be removed, we need to pass the method down from App again. Firebase requires you to remove items by setting them to `null`, but you can simply use `delete thing[key]` when working with localstorage.

## Video 22

This video talks about animation via CSSTransitions and TransitionGroup, both of which I intend to read the docs on. It's from `react-transition-group` which makes animations in React much easier. Wes also uses Stylus (similar to Sass) which needs to be "ejected" to complile from npm scripts.

CSSTransition and TransitionGroup add timed classes to our nodes that will fire on an enter and exit time. They can be targeted with the selected classNames, e.g. `.order-enter` and `.order-exit` for a starting state, and `.order-enter-active` for a finish state (which is appended immediately following the first class).

If you're using multiple transitions, it's typically pointless to duplicate the data so you can just pass it to a variable and then spread it into the object with `{...transitionOptions}`.

## Video 23

Prop types works like TypeScript in that it allows you to pass in information ahead of use by declaring the property type. This can be imported from the package `prop-types` which is no longer included with `create-react-app` due to some people using things like TypeScript or Flow and not making it necessary.

Prop types will not be deployed to production, so any errors or warnings will be confined to the development space. Prop types for a stateless component must be placed after via `MyStateless.propTypes = { myVar: PropTypes.theType}`. In a full class we can simply add it as a static property via `static propTypes`.

The reason we use `static` is to prevent having to duplicate the proptypes information for every single instance so they can just pull the same data instantly.

When we pass an object as a property we could call `PropTypes.object`, but it's better to pass `PropTypes.shape` to ensure the properties are internally correct.

## Video 24

To begin with Authentication in Firebase, we need to enable the processes and implement our API key calls from the sites we want to use. Once enabled, you need to create an auth provider for each thing that's been enabled due to various templating differences.

The authenticator is pulled from the `firebase` package under the `.auth` method. `const authProvider = new firebase.auth[`${provider}AuthProvider`]()`.

The default enabled rules are only provided client side, which won't lock-down our authentication on Firebase. To do this, we need to change the rules to require real authentication.

## Video 25

Wes discusses the build process from running `npm run build`. Nothing new worth taking notes on.

## Video 26

Hosting on Zeit's Now is simple but requires two packages: `now` as a global package, and `serve` as a server. Now does not provide an internal server and has limited capabilities in size without having a paid plan. Now will run `build` and then `start` when uploaded.

## Video 27

This section covers deployment to Netlify. Their global CLI can be installed with `npm i netlify-cli -g`. Netfliy has issues with router, so you need to include a `_redirects` file inside `./build` with `/* /index.html 200`. These sites don't require a login to upload the plan, and will upload straight from your build files so there's no need to run npm scripts internally.

## Video 28

Uploading to an Apache server is also easy if you're using one through a host. The site must be uploaded to a *subdomain* to be valid, but that subdomain can be aliased through your host. After running a build, simply drag-and-drop the `./build` folder into your FTP client pointing at the appropriate directory. After the upload finished, a refresh should load the content. Any authentications put on unvalidated URLs must be added to the Firebase URL whitelist.

The Apache server will unfortunately suffer the same issue as Netlify, where it looks for folders as part of the URL string, i.e. `store/my-site-name`. This can be resolved through your `.htaccess` file by adding the following lines for a single-page application using router.

``` md
RewriteBase /
RewriteRule ^index\.html$ -[L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```

## Lesson 29

`create-react-app` comes with a script to eject all of the build files it uses. This is handy when you need to customize your build and workflow more, but it's recommended that this is done on another branch because once it's run it can't be undone.