# React.js - Getting Started

## Introduction

React is a library, not a framework. It was designed to build user interfaces (anything the user interacts with), and it does that one thing extremely well. With React, we're basically just "describing" what we want and use it as an interface. A lot of people like to think of React as the View in an MVC design, but React is challenging the "MVC" theology.

React has 3 main design concepts.

* Components
  * Like functions.
  * Resuable and composable.
  * Can manage a private state.
* Reactive updates
  * React will react to changes.
  * Take updates to the browser.
* Virtual views in memory
  * Write HTML in JavaScript.
  * Tree reconciliation.

### First Components

A React component can be a **Function Component** or a **Class Component**. Sometimes these are described as stateless and stateful.

A function component is the simplest component in React; it's a simple component with a simple contract. It receives an object of properties (props) and returns JSX.

A class component is a more featured way to define a component, it receives props and can hold a private internal state to return JSX. States and props differ in that states can be changed while props are fixed values.

JSX is optional, and React can be used without JSX. JSX is translated into JavaScript.

A simple, fundamental component is just a function that returns DOM information. To use a component, it must be given a name for reference. Once we assign it a reference, we don't want to change it, so we assign it as constant.

``` jsx
const Button = function () {
  return (
    <button>Go</button>
  );
}
```

The syntax to display a component in the browser is `ReactDOM.render()` which takes two arguments, the component to render and the element where the component is rendered. `ReactDOM.render(<Button />, mountNode)`. In React, variables must be capitalized; React uses this to catch the difference of components and regular HTML.

React component functions receive one argument: `props`. This argument allows us to pass attributes so the function is reusable. Using arrow functions is also preferable.

``` jsx
const Button = props => {
  return (
    <button>{props.label}</button>
  );
}

ReactDOM.render(<Button label="Go" />, mountNode);
```

For the next example, we will make a button that increments its numeric value when clicked. Since this is part of the component, it belongs to the state of the component. This means the component needs to re-render itself every time the counter changes. Prop can't be used here because component properties are immutable.

Since function components can not have state, we must upgrade to a class component.

``` jsx
class Button extends React.Component {
  render () {
    return (
      <button></button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

In a class component, the render fucntion returns the components JSX. Once the class component is rendered, we can use a private state in the component. To do this, we need to initialize the state; we do this inside the constructor in the component. We call the `super` property to honor the inhertiance of the component then initilize the state.

The state exists per component creation since the class is a blueprint. We can call our state values via `this.state.property`.

``` jsx
class Button extends React.Component {
  constructor(props) {
    super(props);
    this.state = { counter: 0 };
  }
  render () {
    return (
      <button>{ this.state.counter }</button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

This can be further simplified by avoiding the constructor call and just use the class property method. This is not officially part of the JS language, but signs point to it becoming part of it.

``` jsx
class Button extends React.Component {
  state = { counter: 0 };
  render () {
    return (
      <button>
        { this.state.counter }
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

React comes with normalized events that are easy to implement. For this case we will use the `onClick` event. Unlike DOM event handlers which use a string, React uses actual JS functions. The standard practice is to define the function on the class itself. We can use React's `setState` method inside of our function with the `this` caller to set the live update of the state changes.

``` jsx
class Button extends React.Component {
  state = { counter: 0 };

  handleClick = () => {
    this.setState({
      counter: this.state.counter + 1
    })
  };

  render () {
    return (
      <button onClick={this.handleClick}>
        {this.state.counter}
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

React's `setState` method is async, meaning it only schedules an update and multiple setState calls might be bad. The general rule of thumb is whenever you need to update the state value using the current state, use the other contract of `setState` which is a function instead of an object.

``` jsx
class Button extends React.Component {
  state = { counter: 0 };

  handleClick = () => {
    this.setState(prevState => ({
        counter: prevState.counter + 1
    }));
  };

  render () {
    return (
      <button onClick={this.handleClick}>
        {this.state.counter}
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

You only need to use this syntax if your update depends on the current state. Since we're only returning an object, we can use the arrow functions short syntax `()` instead of forcing `return`.

### Reusable Components

In this subsection, we split the single component into two: one as the button incrementer, and one to display the result. Since our result component has no state of its own, we can use the function component syntax. To have it display along with our button component, we must render it.

``` jsx
const Result = (props) => {
  return (
    <div>...</div>
  );
};
```

To include multiple components, we'll create a new App component that houses the rest of our built components. We use the class syntax because we intend to introduce a state object. The parent div housing the other elements is not optional; a react component can only return one element.

``` jsx
class App extends React.Component {
  render() {
    return (
      <div>
        <Button />
        <Result />
      </div>
    );
  }
}

ReactDOM.render(<App />, mountNode);
```

Now that we've separated the button from the result, we can change the label to `+1` rather than displaying the output. The problem is **the state of a component can only be acessed by that component**. In order to allow a sibling component to access another component, we need to move it one level up into the parent of both sibling elements.

We also need to move the function to the parent function. But, to make the button component able to increment the parent state we pass it a reference parameter.

`onClickFunction` can be named anything, technically.

``` jsx
class App extends React.Component {
  state = { counter: 0 };

  incrementCounter = () => {
    this.setState(prevState => ({
        counter: prevState.counter + 1
    }));
  }

  render() {
    return (
      <div>
        <Button onClickFunction={this.incrementCounter} />
        <Result />
      </div>
    );
  }
}

ReactDOM.render(<App />, mountNode);
```

Now that we've passed the reference to our function down to `Button`, we can use it via the onClick value. This function will sit on the button's `this.props` property. It should be noted that accessing the properties _of a class component_ is `this.props`.

``` jsx
class Button extends React.Component {
  render () {
    return (
      <button onClick={this.props.onClickFunction}>
        +1
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

To have our Result component read the value, we can use the same passing method that we used for our Button component. `<Result counter={this.state.counter}>` To access this property in our _function component_, we only need to access the argument we passed (`props.passedArguments`). It should be noted that the `props.counter` property is not a state, its just a value that the App counter state is passing to it.

``` jsx
const Result = (props) => {
  return (
    <div>{props.counter}</div>
  );
};
```

#### Reusability

Since the idea of components is to make them as resuable as possible, we want our button component to be able to pass any addition value, not just "+1". To do this, we want to pass the argument into our button as a property. We can then pull the value as a `this.props` property, making our button dynamic for any passed values.

`<Button incrementValue={1} onClickFunction={this.incrementCounter} />`
`<Button incrementValue={5} onClickFunction={this.incrementCounter} />`
`<Button incrementValue={10} onClickFunction={this.incrementCounter} />`
`<Button incrementValue={100} onClickFunction={this.incrementCounter} />`

``` jsx
class Button extends React.Component {
  render () {
    return (
      <button onClick={this.props.onClickFunction}>
        +{this.props.incrementValue}
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

To have these buttons work, our `this.incrementCounter` function now needs to be passed an argument to dynamically create the value changes.

``` jsx
  incrementCounter = (incrementValue) => {
    this.setState(prevState => ({
        counter: prevState.counter + incrementValue
    }));
  }
```

Every Button component needs to invoke this function with an argument now, since we're calling for a parameter. This parameter has nothing to do with the attribute property and can be named whatever you want, but it should be kept the same to avoid confusion. This property can be passed with a simple inline function.

``` jsx
class Button extends React.Component {
  render () {
    return (
      <button onClick={() =>
        this.props.onClickFunction(this.props.incrementValue)
      }>
        +{this.props.incrementValue}
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

This is better solved by using a pre-existing function, though, so we're not creating a new anonymous function every time we invoke an event. Since we need to have a class to encapsulate a function to a component, we can keep Button as a class component even though it has no state of its own.

``` jsx
class Button extends React.Component {
  handleClick = () => {
    this.props.onClickFunction(this.props.incrementValue);
  }

  render () {
    return (
      <button onClick={this.handleClick}>
        +{this.props.incrementValue}
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

## Working with Data

Before beginning a project, it's important to try and conceptualize your components. In the application we're building, we're making a list of GitHub cards. That's a hint that we need a component for each card, and a component to house the list itself.

You can start with any component you want, but usually it's easier to start at the deepest point in the tree. Sometimes, however, it's useful to start from the top and work towards the depper parts.

A side note: if a component will not have interactivity and isn't a top-level component housing state, the component can be started as a function.

``` jsx
const Card = (props) => {
  return (
    <div>
      <img src="http://placehold.it/75" />
      <div>
        <div>Name here</div>
      </div>
    </div>
  )
}

ReactDOM.render(<Card />, mountNode);
```

React components can be styled in a few different ways. A .css file can be included as normal, or you can write CSS inside of React directly. This can be done with the React property `style` which is passed a JS object. `style={{display: 'inline-block'}}`, for example. If you use inline JavaScript styling, you can use the power of JavaScript like you would any other code.

The card components are then housed inside a card list component.

``` jsx
const Card = (props) => {
  return (
    <div>
      <img src="http://placehold.it/75" />
      <div>
        <div>Name here</div>
      </div>
    </div>
  )
}

const CardList = (props) => {
  return (
    <div>
      <Card />
    </div>
  )
}

ReactDOM.render(<CardList />, mountNode);
```

If we render `<Card />` more than once at this point, they will all render the same default component. Instead, passing `props` to the component will allow you to dynamically call data with `props.myProperty`.

``` jsx
const CardList = (props) => {
  return (
    <div>
      <Card name="Jason" id="123" />
    </div>
  )
}
```

To pass multiple entries to a component so we aren't hardcoding each item, we can pass this through a loop. To begin, we assume we have the desired data in an array housing an object housing each entry.

``` js
let data = [
  {name: 'Jason', id='123'},
  {name: 'Carol', id='456'},
  {name: 'Sarah', id='789'}
]

const CardList = (props) => {
  return (
    <div>
      {props.cards.map(card => <Card {...card} />)}
    </div>
  )
}

ReactDOM.render(<CardList cards={data} />, mountNode);
```

We used the `...` spread feature here instead of individually passing `<Card name={card.name} id={card.id}>` because it distributes the data in an easier to read way; this will also help compensate for large numbers of attributes.

## Taking Input from the User

When we take user input, we use the component feature so we can store state. Each component should have its own category, so we don't render this in our CardList. Rather than rendering our form in the wrong location, we use a parent component called `App`.

``` jsx
class Form extends React.Component {
  render() {
    <form>
        <input type="text" placeholder="Github username" />
        <button type="submit">Add card</button>
    </form>
  }
}
```

``` jsx
class App extends React.Component {
  render() {
    return (
      <div>
        <Form />
        <CardList cards={data} />
      </div>
    )
  }
}

ReactDOM.render(<App />, mountNode);
```

In our current sample, our `data` array is part of the global scope which is bad practice. Since it is part of the application, it should be part of the `App` state.

``` jsx
class App extends React.Component {
  state = {
    cards: [
      { name: "Someone",
        avatar: "link",
        company: "Company" }
    ]
  }
  render() {
    return (
      <div>
        <Form />
        <CardList cards={this.state.cards} />
      </div>
    )
  }
}

ReactDOM.render(<App />, mountNode);
```

Adding functionality to our button is as easy as adding an `onClick` or `onSubmit` event handler. Every React event function receives an event argument which can be passed to the handler. The handler is a wrapper around the native event JavaScript object. To prevent the default behavior of the event, we pass `preventDefault()`. To grab the value from our input, we use React's `ref` property to grab a reference to the element, rather than using a DOM call. `ref` takes a function that is executed when the element is mounted; this function is given a reference to the element, so we can store the reference in the form component instance. The reference can be accessed with `this.userNameInput.value`.

```jsx
    handleSubmit = e => {
      event.preventDefault();
    }
    // ...
    <form onSubmit={this.handleSubmit}>
        <input type="text" ref={(input) => this.userNameInput = input} placeholder="Github username" />
        <button type="submit">Add card</button>
    </form>
```

A better alternative to using `ref` is passing controlled components.

```jsx
    state = { username: ''}
    handleSubmit = e => {
      event.preventDefault();
    }
    // ...
    <form onSubmit={this.handleSubmit}>
        <input type="text" value={this.state.userName} onChange={(e) => this.setState({userName: event.target.value})} placeholder="Github username" />
        <button type="submit">Add card</button>
    </form>
```

Once we've set up our app to take data from an AJAX get request, we can pass our new user card data to the `Card` component by passing it first through the App. Our parent function becomes a property of App and can be passed on the `.props` list. To append the new information to our previously existing information, we can attach it through the `.setState` method via `this.prevState.cards.concat(cardInfo)`, which will attach it to the currently existing information. In our `Form` component, we can set the state back to an empty string via the state.

It should also be noted that we need a unique `key` for each dynamically generated element to help React find the content internally.

``` jsx
// App.js

addNewCard = (cardInfo) => {
  this.setState(prevState => {
    cards: this.prevState.cards.concat(cardInfo)
  });
}

<Form onSubmit={this.addNewCard} />

// Form.js

this.props.onSubmit(data);
this.setState({userName: ''});

// Card.js

{props.cards.map(card => <Card key={card.id} {...card} />)}
```

## Building the Game Interface

To begin this project, we need to start with our basic components. Typically the first component is the `App` component that hosts other components internally. We then build a Game component that can be isolated inside the App.

``` jsx
class App extends React.Component {
  render() {
    return (
      <div>
        <Game />
      </div>
    )
  }
}

class Game extends React.Component {
  render() {
    return (
      <div>
        <h3>Play Nine</h3>
      </div>
    )
  }
}

ReactDOM.render(<App />, mountNode);
```

After creating our main components, we create our sub-components. In this game, we are using star icons as part of the structure, so we'll create a stars component that is nested into the Game component. We also need to show our button and answer box.

``` jsx
class Game extends React.Component {
  render() {
    return (
      <div>
        <h3>Play Nine</h3>
        <Stars />
        <Button />
        <Answers />
      </div>
    )
  }
}

const Stars = (props) => {
  return (
    <div className="col-5">
      <i className="fa fa-star"></i>
    </div>
  )
}

const Button = (props) => {
  return (
    <div className="col-2">
      <button>=</button>
    </div>
  )
}

const Numbers = (props) => {
  return (
    <div className="card text-center">
      <div>
        <span>1</span>
        <span className="selected">2</span>
        <span>3</span>
      </div>
    </div>
  )
}

const Answer = (props) => {
  return (
    <div className="col-5">
      ...
    </div>
  )
}
```

Once our layout and basic placeholders have been made, we can add real functionality to the cards. We can create these elements by pushing them into an array and displaying them in the render; React handles this automatically and it can be called with `{stars}`. React encourages the use of `.map` and other `forEach`-esque functions rather than `for` loops, so while we're adding information we apprach the Numbers component with an array.

``` jsx
const Stars = (props) => {
  const numberOfStars = 1 + Math.floor(Math.random() * 9);

  let stars = [];
  for (let i=0; i<numberOfStars; i++) {
    stars.push(<i key={i} className="fa fa-star"></i>);
  }
  return (
    <div className="col-5">
      {stars}
    </div>
  )
}

const Numbers = (props) => {
  const arrayOfNumbers = _.range(1, 10) //lodash
  return (
    <div className="card text-center">
      <div>
        {arrayOfNumbers.map((number, i) =>
          <span key={i}>{number}</span>
        )}
      </div>
    </div>
  )
}
```

While this works fine, we don't really want to render the constant arrayOfNumbers every time we render a Numbers object, so it makes it a good candidate for putting it on the Number object as a property. This should be done any time you have a constant shared across all components but no logic is being done on the variable.

``` jsx

Numbers.list = _.range(1, 10)

const Numbers = (props) => {
  return (
    <div className="card text-center">
      <div>
        {Numbers.list.map((number, i) =>
          <span key={i}>{number}</span>
        )}
      </div>
    </div>
  )
}
```

## Numbers Selection

To trigger a re-render in React, we must put something in the state and modify it with an action. Since both Answer and Numbers need a re-render, it makes the most sense to place the state on the parent component: Game. Side note, objects are typically faster for data lookup but arrays are fine for small structures. When working to construct a component, it's also suggested to start with fake data and work your way towards including real data once the fake data is working.

This state is needed by two components. The Answers component needs to display the selected numbers, and the Numbers component needs to disable them from selection once used. To access the state in a parent component, the parent component needs to pass the state to the child component as a property.

When we pass our property to Numbers, we need to check whether it exists in the array and give it a different class. We can do this by passing a function into class name that will return the class we want if the number exists in our existing state.

``` jsx
class Game extends React.Component {
  state = {
    selectedNumbers: [2, 4],
  };

  render() {
    return (
      <div>
        <h3>Play Nine</h3>
        <Stars />
        <Button />
        <Answers selectedNumbers={this.selectedNumbers} />
        <Numbers selectedNumbers={this.selectedNumbers} />
      </div>
    )
  }
}

const Answer = (props) => {
  return (
    <div className="col-5">
      {props.selectedNumbers.map((number, i) =>
        <span key={i}>{number}</span>
      )}
    </div>
  )
}

const Numbers = (props) => {
  const numberClassName = (number) => {
    if (props.selectedNumbers.indexOf(number) >= 0) {
      return 'selected';
    }
  }

  return (
    <div className="card text-center">
      <div>
        {Numbers.list.map((number, i) =>
          <span key={i} className={numberClassName(number)}>{number}</span>
        )}
      </div>
    </div>
  )
}
```

Once we're able to display the sample data, we can start working on the feature of adding numbers when they've been clicked. We can add this feature by putting a new function in the Game component since we need to pass the results into our `selectedNumbers` state.

``` jsx
class Game extends React.Component {
  state = {
    selectedNumbers: [2, 4],
  };
  selectNumber = (clickedNumber) => {
    this.setState(prevState => ({
      selectedNumbers: prevState.selectedNumbers.concat(clickedNumber)
    }))
  };
  render() {
    return (
      <div>
        <h3>Play Nine</h3>
        <Stars />
        <Button />
        <Answers selectedNumbers={this.this.selectedNumbers} />
        <Numbers selectNumber={this.selectNumber} selectedNumbers={this.this.selectedNumbers} />
      </div>
    )
  }
}

const Numbers = (props) => {
  const numberClassName = (number) => {
    if (props.selectedNumbers.indexOf(number) >= 0) {
      return 'selected';
    }
  }

  return (
    <div className="card text-center">
      <div>
        {Numbers.list.map((number, i) =>
          <span key={i} className={numberClassName(number)}
              onClick={() => props.selectNumber(number)}>
            {number}
          </span>
        )}
      </div>
    </div>
  )
}
```

At this point we've introduced two problem: the Game component rerenders every time we click a number which causes our stars to rerender a random number, and we haven't disabled the ability to click numbers more than one time. When Game rerenders, all of its children are rerendered as well. To solve the first issue, we need to move the star generation up one leven and maintain it on the Game component itself. For our second issue, we simply don't update the state and instead just return.

``` jsx
class Game extends React.Component {
  state = {
    selectedNumbers: [2, 4],
    randomNumberOfStars: 1 + Math.floor(Math.random() * 9)
  };
  selectNumber = (clickedNumber) => {
    if (this.state.selectedNumber.indexOf(clickedNumber) >= 0) { return; }
    this.setState(prevState => ({
      selectedNumbers: prevState.selectedNumbers.concat(clickedNumber)
    }))
  };
  render() {
    return (
      <div>
        <h3>Play Nine</h3>
        <Stars numberOfStars={this.state.randomNumberOfStars} />
        <Button />
        <Answers selectedNumbers={this.selectedNumbers} />
        <Numbers selectNumber={this.selectNumber} selectedNumbers={this.selectedNumbers} />
      </div>
    )
  }
}

const Stars = (props) => {
  return (
    <div className="col-5">
      {_.range(props.numberOfStars).map(i =>
        <i key={i} className="fa fa-star"></i>
      )}
    </div>
  )
}
```

Once the numbers are clickable, we need to allow the user to change their answer. We can add this feature by allowing a player to roll back their selection if they click a number in the Answer component (since the state is in the parent, the function will be passed as a prop).

``` jsx
const Answer = (props) => {
  return (
    <div className="col-5">
      {props.selectedNumbers.map((number, i) =>
        <span key={i} onClick={() => props.unselectNumber(number)}>{number}</span>
      )}
    </div>
  )
}

// App.js

unselectNumber = (clickedNumber) => {
  this.setState(prevState => ({
    selectedNumbers: prevState.selectedNumbers.filter(number => number !== clickedNumber)
  }))
}

<Answers selectedNumbers={this.selectedNumbers} unselectNumber={this.unselectNumber} />
```

We can (and should) also refactor our code to be more readable and usable.

```jsx
class Game extends React.Component {
  state = {
    selectedNumbers: [2, 4],
    randomNumberOfStars: 1 + Math.floor(Math.random() * 9)
  };
  selectNumber = (clickedNumber) => {
    if (this.state.selectedNumber.indexOf(clickedNumber) >= 0) { return; }
    this.setState(prevState => ({
      selectedNumbers: prevState.selectedNumbers.concat(clickedNumber)
    }))
  };
  render() {
    const { selectedNumbers, randomNumberOfStars } = this.state; // Deconstructing these!
    return (
      <div>
        <h3>Play Nine</h3>
        <Stars numberOfStars={randomNumberOfStars} />
        <Button />
        <Answers selectedNumbers={selectedNumbers} />
        <Numbers selectNumber={this.selectNumber} selectedNumbers={selectedNumbers} />
      </div>
    )
  }
}
```

## Game State

I'm stopping notes at this point due to the rest of the course being about finishing the game and not implementing any new React techniques.

To summarize the chapter, the host adds functionality to the button based on a `switch` case for true and false correct answers. Once the button is given functionality, the host adds functionality to creating "used" into our used numbers. Due to the construction of our game, we will eventually run out of possible answers before we've used all of the numbers. To bypass this issue, the host adds a refresh button that redraws the number of stars. We then pass a `doneStatus` variable to display the results of finishing the game. To create a challenge, the refresh button is given a limited number of clicks that when exhausted will display a loss. Once a win or loss has been reached, the user can reset the game.