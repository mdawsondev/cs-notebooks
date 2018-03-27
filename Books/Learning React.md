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