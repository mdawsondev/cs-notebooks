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