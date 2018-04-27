# Learning React

## Chapter 1 - Welcome to React

React is a small library that doesn't ship with all of the tools you'd expect from traditional frameworks. It focuses on **functional programming** over OOP.

Nothing else noteworthy.

## Chapter 2 - Emerging JavaScript

This chapter briefly covers a lot of the ES6 content; not a lot of noteworthy points and it's not in-depth enough to warrant further study.

## Chapter 3 - Functional Programming with JavaScript

A lot of talk about how functions can be used through JavaScript; this actually isn't talking a whole lot about the concept behind Functional Programming though. As a note, when passing arrow functions to arrow functions, this creates higher-order functions.

`const createScream = logger => message => logger(message.toUpperCase() + "!!!")`

We can say that JavaScript is a functional language because its functions are data; they can ve saved, retrieved, or flow through applications like variables.

In the new era of JavaScript we tend to use arrow function declaration in place of function declaration. As to why, I have no idea - I can't seem to find a clear answer other than, "You use the right tools for the job."

### Imperative Versus Declarative

**Functional programming** is a subsection of **delcarative programming**, which is a style where applications are structured in a way that prioritizes describing _what_ should happen over defining _how_ it shouls happen.

**Imparative programming** is a style of programming only concerned with _how_ to achieve results with code.

An imparative example of making a string URL-friendly could typically be done like this in imparative programming.

``` js
var string = "This is the midday show with Cheryl Waters";
var urlFriendly = "";

for (var i=0; i<string.length; i++) {
  if (string[i] === " ") {
    urlFriendly += "-";
  } else {
    urlFriendly += string[i];
  }
}

console.log(urlFriendly);
```

Through imparative programming, the above loops through every character in the string and replaces spaces as they occur. Looking at the code does not tell us much and typically require a lot of comments.

``` js
const string = "This is the mid day show with Cheryl Waters";
const urlFriendly = string.replace(/ /g, "-");

console.log(urlFriendly);
```

In the above declarative block, we use a regular expression and can instantly tell what is happening by context. We don't care _how_ regular expression handles the replacement, all we care about is what is happening.

The actual reasoning behind the method is tucked away behind the scenes, making it much more readable and easily understood. This is called abstraction.

A good example of why imparative programming is not ideal: thinking about DOM construction. When we create an element via `document.createElement('DIV')`, we don't care about _how_ that method is creating a div. All we care about is that it's doing it.

React is declarative in the same way; we render functions in the instructions abstracting away the details of how the DOM is rendered.

``` jsx
const { render } = ReactDom

const Welcome = () => {
  <div id="welcome">
    <h1>Hello World</h1>
  </div>
}

render(
  <Welcome />,
  docment.getElementById('target')
)
```

### Core Concepts of Functional Programming

#### Immutability

In functional programming, data is immutable. If you want to edit original data, it should be cloned and manipulated, leaving the original content intact.

Rather than overwriting existing data, we can use functional patterns to define creation.

``` jsx
var rateColor = function(color, rating) {
  return Object.assign({}, color, {rating:rating})
}

console.log(rateColor(color_lawn, 5).rating) //5
console.log(color_lawn.rating) //4
```

By using the `Object.assign` method to change the color rating, we use the function as a "copy machine" taking a blank object and copying it to a new object with new input.

This can also be processed using the ES6/7 arrow function and spread operator, respectively.

``` jsx
const rateColor = (color, rating) =>
  ({
    ...color,
    rating
  })
```

These functions will treat color as an immutable object. Note, ew wrapped the returned object in parenthesis - for arrow functions, this is a required step since the arrow can't just point to an object's curley braces.

``` jsx
let list = [
  {title: "Rad Red"},
  {title: "Lawn"},
  {title: "Party Pink"}
]

<!-- var addColor = function(title, colors) {
  colors.push({title})
  return colors;
} -->

const addColor = (title, array) => array.concat({title})

console.log(addColor("Glam Green", list).length) //4
console.log(list.length) //3
```

In the example above, we take a list of colors and put them through a non-mutable function. By using `concat` instead, this takes a new object and adds it to a **copy** of the original array. The commented out function is not an immutable function, because `.push` is not immutable. That function will mutate the original array, which is bad.

_Aside: you can also use the spread operator to concatenate arrays. `const addColor = (title, list) => [...title, {title}]`._

#### Pure Functions

**Pure functions** return a value that is computed based on its arguments. They take at least one argument and _always_ return a value or another function. They do not cause side effects, set global variables, or change anything about the application state. They treat arguments as immutable data and do not change the original input.

``` js
// An example of an impure function.

var frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
}

function selfEducate() {
  frederic.canRead = true;
  frederic.canWrite = true;
  return frederick
}

selfEducate()
```

The above does not take any arguments and does not return a value or function. It also changes a variable outside of its scope. Once run, something about the "world" has changed, and can cause side effects.

``` js
// Another impure example.

const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
}

const selfEducate = (person) => {
  person.canRead = true
  person.canWrite = true
  return person
}

console.log( selfEducate(frederick) )
console.log( frederick )

// {name: "Frederick Douglass", canRead: true, canWrite: true}
// {name: "Frederick Douglass", canRead: true, canWrite: true}
```

The above is impure because we are still mutating the original `frederick` object. This is a change being made outside of the function's environment.

``` js
// A pure function.

const frederick = {
  name: "Frederick Douglass",
  canRead: false,
  canWrite: false
}

const selfEducate = person => ({
  ...person,
  canRead: true,
  canWrite: true
})
```

This version is a pure function because it computes and returns values based on the argument it was sent. It returns a new person object without mutating the argument sent to it.

``` jsx
// Impure DOM manipulation.

function Header(text) {
  let h1 = document.createElement('h1');
  h1.innerText = text;
  document.body.appendChild(h1)
}

// Pure DOM manipulation in jsx.

const Header = (props) => <h1>{props.title}</h1>
```

In the above sample, the first function is impure because it creates a single element that changes the outside world. It doesn't return a value or function. The `jsx` example creates a new node object and returns it, allowing it to exist as a new object.

#### Data Transformations

This subsection talks a lot about how to use immutable functions over mutable ones, like `.filter` over `.pop` or `.splice`. There are a lot of examples for various methods of making mutable data immutable and clonable. Nothing really noteworthy.

#### Higher-Order Functions

**Higher-order functions** are functions that can manipulate other functions. They take functions as arguments, or return functions, or both.

The first category of these functions are functions that expect other functions as arguments. `Array.map`, `Array.filter`, etc all take functions as arguments.

``` js
const invokeIf = (condition, fnTrue, fnFalse) =>
  (condition) ? fnTrue() : fnFalse()

const showWelcome = () =>
  console.log("Welcome!!!")

const showUnauthorized = () =>
  console.log("Unauthorized!!!")

invokeIf(true, showWelcome, showUnauthorized)
InvokeIf(false, showWelcome, showUnauthorized)
```

In the sample above, we create our own higher-order function, `invokeIf`, that expects two callback functions as arguments.

_Currying_ is a functional technique that involves the use of higher-order functions; it's the practice of holding onto some values needed to complete an operation until the rest can be supplied at a later point. This is usually run through the use of a function that returns another function, the curried function.

``` js
// Currying example.

const userLogs = userName => message =>
  console.log(`${userName} -> ${message}`)

const log = userLogs("grandpa23")

log("attempted to load 20 fake members")
getFakeMembers(20).then(
  members => log(`successfully loaded ${members.length} members),
  error => log("encountered an error loading members")
)
```

#### Recursion

Recursion should be used over loops whenever possible, but large recursion may cause stack limitation errors. Recursion works well with asynchronous processes because they call themselves when ready.

Recustion is a great technique for searching data structures, and can be used to iterate through the HTML Dom until finding elements required.

There are some examples of recursion, but not a lot of other useful notes.

#### Composition

Functional programs break their logic into small pure functions that are focused on specific tasks. Composition is made of a number of different patters, implementations, and techniques. Chaining is a good example, because we can chain together returns which offer methods.

String replacement is a good example, where we could take a string, chain `.replace` methods to the end of each additional `.replace` method, and can continue being used.

The goal of composition is to generate higher order functions by combining simpler functions.

``` js
// Poor, confusing way of piping values.
const both = date => appendAMPM(civilianHours(date))

// Elegant approach.
const compose = (...fns) => (arg) =>
    fns.reduce((composed, f) => f(compsed), arg)

const both = compose(civilianHours, appendAMPM)
both(new Date())
```

The first example is a poor way of piping values because, although functional, it gets confusing. If we had to pipe 20 functions, this would be a huge confusing mess.

The second method takes a higher order function `compose` that can take any number of arguments and allow easy implementation.

`compose` takes in functions and returns a single functions; in this implementation a spread operator is used to break arguments into their own `fns` and then the array is piped starting with the first argument following down the list. Eventually, it will return a single value.

#### Putting it all together

This section discusses using the concepts above to build a ticking clock. I've built this externally on [GitHub Gist as ticking-clock.js](https://gist.github.com/mdawsondev/7d3d4ee66b9670490fe3889ed99a3a9c).

## Chapter 4 - Pure React

To work with React in the browser, you must include two libraries: React, and ReactDOM. React is the library for creating views, and ReactDOM is the library used to actually render the UI. ReactDOM was split from React and must now be imported for browser use.

An HTML element that ReactDOM will hook to must also be supplied. Both libraries are available on Facebook CDN as import scripts.

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
  <title>Pure React Samples</title>
</head>
<body>
  <!-- Target container -->
  <div class="react-container"></div>
  <!-- React library & ReactDOM-->
  <script src="https://unpkg.com/react@15.4.2/dist/react.js"></script>
  <script src="https://unpkg.com/react-dom@15.4.2/dist/react-dom.js"></script>
  <script>
  // Pure React and JavaScript code
  </script>
</body>
</html>
```

### Virtual DOM

Traditionally websites were made of independant HTML elements; with AJAX came the implementation of SPA (Single Page Applications). In an SPA, the browser loads one HTML document and JS destroys and creates new UI as the user interacts with the page. The DOM API is a collection of objects used to render and manipulate the DOM (document.createElement, for example). This process is taxing on the website, and can cause slowness.

React was designed to update the browser DOM for us; it doesnt involve complexities associated with standard SPAs. We don't interact with the DOM API; instead, we interact with the **virtual dom** which allows us to construct the UI and update the browser behind the scenes.

### React Elements

The DOM is made of DOM elements, while React's DOM is made of React elements. They look the same, but they're not. A react element is a description of what the actual DOM element should look like. They're the instructions for how the DOM should be created.

React elements are created using `React.createElement`, where we can create an `h1` element by writing `React.createElement('h1', null, 'Baked Salmon')`. The first argument defines the type, the second argument represents the elements properties, and the third argument represents the element's children nodes. During the render, React will convert the element into an actual DOM element `<h1>Baked Salmon</h1>`.

When an element has attributes, they can be described with properties, for example: `React.createElement("h1", {id: "recipe-0", "data-type": "title"}, "Baked Salmon")` will output `<h1 data-reactroot id="recipe-0" data-type="title">Baked Aslmon</h1>`.

`data-reactroot` appears as an attribute of the root element in your React component.

Logging the element created by React will yeild the object. The `type` property of the React element tells what type of SVG or HTML element to create. The `props` property represents the data and child elements required to construct a DOM element. The `children` property is for displaying other nested elements as text.

``` js
{
$$typeof: Symbol(React.element),
  "type": "h1",
  "key": null,
  "ref": null,
  "props": {"children": "Baked Salmon"},
  "_owner": null,
  "_store": {}
}
```

### ReactDOM

ReactDOM contains the tools required to render React elements in a browser. It contains the `render` method as well as `renderToString` and `renderToStaticMarkup`. React elements and their children can be rendered with the `ReactDOM.render` call. The element we want is passed as the first argument, and the second argument is the targe node.

```js
var dish = React.createElement("h1", null, "Baked Salmon")
ReactDOM.render(dish, document.getElementById('react-container'))
```

ReactDOM allows you to render a single element to the DOM; it tags this as `data-reactroot`, and all other React elements are composed into a single element using nesting. React renders child elements when using `props.children`. We can also render other elements as children nodes, creating a tree of elements known as a _component tree_. For example, we can make a parent `ul` element and nest six `li` elements inside by the following method.

``` js
React.createElement(
  "ul",
  null,
  React.createElement("li", null, "1 lb Salmon"),
  React.createElement("li", null, "1 cup Pine Nuts"),
  React.createElement("li", null, "2 cups Butter Lettuce"),
  React.createElement("li", null, "1 Yellow Squash"),
  React.createElement("li", null, "1/2 cup Olive Oil"),
  React.createElement("li", null, "3 cloves of Garlic")
)

{
"type": "ul",
  "props": {
  "children": [
    { "type": "li", "props": { "children": "1 lb Salmon" } … },
    { "type": "li", "props": { "children": "1 cup Pine Nuts"} … },
    { "type": "li", "props": { "children": "2 cups Butter Lettuce" } … },
    { "type": "li", "props": { "children": "1 Yellow Squash"} … },
    { "type": "li", "props": { "children": "1/2 cup Olive Oil"} … },
    { "type": "li", "props": { "children": "3 cloves of Garlic"} … }
  ]
  ...
  }
}
```

Any element that has an HTML class attribute uses `className` for the property instead of `class` because `class` is a reserved word in JS.

### Constructing Elements with Data

Since React is just JavaScript we can use code to store data like we would normally do. Rather than creating several hard-coded elements, we can map items from an array in a loop. Passing an array without key properties will throw a warning, however. React likes your elements to have keys, so we can bypass this warning by providing a unique key.

``` js
var items = [
  "1 lb Salmon",
  "1 cup Pine Nuts",
  "2 cups Butter Lettuce",
  "1 Yellow Squash",
  "1/2 cup Olive Oil",
  "3 cloves of Garlic"
]

React.createElement(
  "ul",
  { className: "ingredients" },
  items.map((ingredient, i) =>
    React.createElement("li", {key: i}, ingredient)
)
```

### React Components

Every UI is made of parts; in React we call these parts components. Components allow us to reuse structures. When building an interface, look for opportunities to break the elements into reusable pieces. For example, a recipe app might be composed of a component containing ingredients, a component containing instruction, and those components are wrapped into an indexing card.

### React.createClass

`React.createClass` may be depreciated in the future so I have no idea why the author is talking about this, but: we can create a React component using React.createClass that returns an element. `displayName` is our element's name, in the case below, `<IngredientsList></IngredientsList>`.

``` js
const IngredientsList = React.createClass({
  displayName: "IngredientsList",
  render() {
    return React.createElement("ul", {className: "ingredients"},
      this.props.items.map((ingredient, i) =>
        React.createElement("li", { key: i }, ingredient)
      )
    )
  }
})

const items = [
  "1 lb Salmon",
  "1 cup Pine Nuts",
  "2 cups Butter Lettuce",
  "1 Yellow Squash",
  "1/2 cup Olive Oil",
  "3 cloves of Garlic"
]

ReactDOM.render(
  React.createElement(IngredientsList, {items}, null),
  document.getElementById('react-container')
)
```

Components are objects; they can be used to encapsulate code just like classes. We can create a method that renders a single list item and use that to build out the list. This is also the idea of views in MVC languages; everything that is associated with the UI for IngredientsList is encapulated into one component; everything we need is right there.

```js
const IngredientsList = React.createClass({
  displayName: "IngredientList",
  renderListItem(ingredient, i) {
    return React.createElement("li", {key:i}, ingredient)
  },
  render() {
    return React.createElement("ul", {className: "ingredients"},
      this.props.items.map(this.renderListItem)
    )
  }
})
```

### React.Component

One of the key features included in the ES6 spec is `React.Component`, an abstract class that we use to build new components. We create custom components through inheritance by extending this class with ES6 syntax.

``` js
class IngredientsList extends React.Component {
  renderListItem(ingredient, i) {
    return React.CreateElement("li", {key:i}, ingredient)
  }

  render() {
    return React.createElement("ul", {className: "ingredients"},
      this.props.items.map(this.renderListItem)
    )
  }
}
```

### Stateless Fucntional Components

Functional components are functions, not objects, therefore they don't have a `this` scope. They are simple, pure functions and will be used frequently. They take in a property and return a DOM element. They're a good way to practice the rules of functional programming; they should take in props and return an element without causing side effects.


```js
const IngredientsList = ({items}) =>
  React.createElement("ul", {className: "ingredients"},
    items.map((ingredient, i) =>
      React.createElement("li", { key: i }, ingredient)
    )
  )
```

### DOM Rendering

This section just talks about how React replaces sectional changes rather than rerendering the entire DOM; nothing really noteworthy.

### Factories

A `factory` is a special object used to abstract away the details of instancing objects. React has built-in factories for all the commonly supported HTML and SVG DOM elements, and you can create your own via `React.createFactory`.

`React.DOM.h1(null, "Baked Salmon")`.

```js
var items = [
  "1 lb Salmon",
  "1 cup Pine Nuts",
  "2 cups Butter Lettuce",
  "1 Yellow Squash",
  "1/2 cup Olive Oil",
  "3 cloves of Garlic"
]

var list = React.DOM.ul(
  { className: "ingredients" },
  items.map((ingredient, key) =>
    React.DOM.li({key}, ingredient)
  )
)

ReactDOM.render(
  list,
  document.getElementById('react-container')
)
```

### Using Factories with Components

Factories can quickly render React elements; however factories are almost exclusively used for non-JSX design. This this example React quickly renders elements with the `Ingredients` factory.

``` js
const { render } = ReactDOM;
const IngredientsList = ({ list }) =>
  React.createElement('ul', null,
    list.map((ingredient, i) =>
      React.createElement('li', {key: i}, ingredient)
    )
  )

const Ingredients = React.createFactory(IngredientsList)

const list = [
  "1 lb Salmon",
  "1 cup Pine Nuts",
  "2 cups Butter Lettuce",
  "1 Yellow Squash",
  "1/2 cup Olive Oil",
  "3 cloves of Garlic"
]

render(
  Ingredients({list}),
  document.getElementById('react-container')
)
```

## Chapter 5 - React with JSX

Alternatively to typing out verbose `React.createElement` calls is JSX, a JavaScript extension which lets us use React elements that look similar to HTML.

### React Elements as JSX

JSX looks functionally similar to HTML. For example, a simple `<ul> <li></li> <ul>` DOM stack will render in JavaScript under JSX. JSX works with components as well; we simply define the component using the class name. When we pass objects to a component, we surround it with curly braces.

``` js
React.createElement(IngredientsList,{list:[...]});
// Equal:
<IngredientsList list={[...]}/>
```

### JSX Considerations

Although JSX looks similar to HTML, it's not exactly the same.

* *Nested components:* React allows for nesting components inside of eachother.
* *className:* `class` is a reserved word in JavaScript, so we use `className="name"` instead.
* *JavaScript expressions:* JS is wrapped in curly braces to indicate where variables are evaluated. Ex: `<h1>{this.props.title}</h1>`.
* *Evaluation:* JS added between curly braces gets evaluated. This means operations such as concantenation or addition will occur.
* *Mapping arrays to JSX:* JSX can be called directly inside of JS functions; see example below.

```jsx
<ul>
  {this.props.ingredients.map((ingredient, i)) =>
    <li key={i}>{ingredient}</li>}
  )}
</ul>
```

### Babel

There's some high-level talk about Babel and discussion what it is and who uses it, but this is about the implementation of including `babel-core` for non-npm build projects. Calling libraries like this will let you avoid having to run complex builds for testing new features.

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>React Examples</title>
</head>

<body>
  <div class="react-container"></div>
  <!-- React Library & React DOM -->
  <script src="https://unpkg.com/react@15.4.2/dist/react.js"></script>
  <script src="https://unpkg.com/react-dom@15.4.2/dist/react-dom.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.29/browser.js"></script>

  <script type="text/babel">
// JSX code here. Or link to separate JavaScript file that contains JSX.
  </script>
</body>
</html>
```

### Recipes as JSX

Writing in JSX and using React to build a modular architecture is great because it clearly communicates how the application functions. The problem is the browser doesn't understand JSX, so it must be transpiled into pure React.

