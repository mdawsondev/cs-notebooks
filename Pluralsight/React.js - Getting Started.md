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

