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