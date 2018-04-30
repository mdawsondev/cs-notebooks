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