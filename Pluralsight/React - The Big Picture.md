# React: The Big Picture

This course covers the answers to three major questions about React.

1. Why should I choose React?
2. What tradeoffs am I making by choosing React?
3. Why shouldn't I choose react?

## Why React

* Flexibility
* Developer experience
* Corporate investment
* Community support
* Performance
* Testability

### Flexability

React can be used for a huge variety of platforms and use-cases. It's less "opinionated" than frameworks like Angular and Ember; it's also a library, not a framework.

React can be used for a variety of use-cases:

* Web apps
* Static sites
* Mobile
* Desktop
* Server-rendered
* Virtual Reality

React render is seperate from React itself. For webapps, you call `react-dom` to render HTML, React Native uses `react-native`, and React VR uses `react-vr`. There are a large number of renders available beyond the basics mentioned. React can also be used to render server-side technology. `ReactDomServer.renderToString()` can be invoked, and server-side tech is supported by multiple libraries, including Next.js, Gatsby, and Phenomic.

Due to the nature of react being a lightweight library, it can be used with existing applications as well. React was actually designed to be implemented piece by piece to replace Facebook's server-side rendered PHP application. Starting with small elements, moving to containers, and eventually stepping out to the full window is a great low-risk way to migrate an existing project to React.

### Developer Experience

React offers a simple API that's easy to remember; you'll likely very rarely reference the docs. React also approaches implementing HTML into JavaScript and JavaScript into HTML in a different way than other frameworks. Frameworks like Angular have their own system for implementing coding fundamentals (e.g. loops), where React just handles HTML with JavaScript.

* Angular: `<div *ngFor="let user of users">`
* Vue: `<div v-for="user in users">`
* Ember: `{{#each user in users}}`
* React: `{users.map(createUser)}`

Seeding a new application is also very simple, by calling the npm tool `create-react-app <application-name>` you can create a full React development environment. running `npm start` will immediately fire up a live server.

Each element is ATOMIC (stands alone). This means each component can be worked with in isolation. This enviornment will also throw compile errors straight to the browser for immediate debugging. React is also supported by places like CodeSandbox for a configureless development environment.

### Corporate Investment

Created and maintained by Facebook and is run in a very professional, detailed way by commited developers. Because of corporate reliance on React, the React team automatically publishes "code mods" to actively update code without causing problematic breaks. Facebook specifically relies on React, and this ensures any potential bugs are solved quickly so they don't break the platforms 30,000+ existing components.

### Community

Large active community with steady growth in use; React is one of the most popular repositories on GitHub with over 75,000 stars and 1,000 contributors. React's NPM package is downloaded over 1.5 million times every week. StackShare confirms nearly 5,000 companies are using React in their stack; at the time of recording, it's also the 8th most popular technology on all of StackShare.

React's official and unofficial developers are active in Reactiflux, which houses a community of over 20,000 developers. There are over 55,000 tags on StackOverflow tagged `reactjs`, as well as a hube variety of other React technologies. All of this matters because it means if you're trying to do something in React, it has likely been done before and you can find an example.

There are also a number of large libraries available for free React components. Microsoft open sourced their library for Office UI (Office UI Fabric). Material-UI uses Google's Material Design guidelines. React Bootstrap contains components meant to make it easy for combining React ith Bootstrap.

### Performance

The React team discovered that the DOM was slow, so they solved the issue by rendering a "Virtual DOM" behind the scenes. React minimizes DOM changes by finding and implementing the most efficient way of updating the DOM. This creates a number of benefits, like preventing layout thrashing, saves battery and CPU life, and enabling a simple programming model.

React is also as small as 45kb gzip, making it a strong use-case for mobile bandwidth development. If this isn't small enough, there are even more lightweight libraries such as Inferno sporting a 9kb size, or Preact weighing in at 3kb. They offer the same API but omit features to keep the size down.

### Testability

Traditionally front-end UI testing is difficult, but React manages this in different ways. The vast majority of React components return Pure Functions, which means they always return the same output for a given input. This makes it reliable, deterministic, and has no side-effects. Jest, also created by Facebook, syncs extremely well with React, making testing trivial.

Traditional UI Testing

* Hassle to set up.
* Requires browser.
* Slow.
* Brittle integration tests.
* Time-consuming to write, maintain.


React

* Little to no config required.
* Run in-memory via Node.
* Fast.
* Reliable, deterministic unit tests.
* Write quickly, update easily.

## Tradeoffs

React offfers a lot of good reasons for use, but it also makes tradeoffs for its environment.

* Framework vs. Library
* Concise vs. Explicit
* Template-centric vs. JavaScript-centric
* Separate vs. Single File
* Standard vs. Non-standard
* Community vs. Corporate

### Framework vs. Library

Frameworks are typically used to build a major project from the ground up ensuring stability, while libraries can be systematically implemented into existing projects. React can replace components one at a time in existing apps without creating a lot of overhead or destroying existing structure. 

Frameworks:

* Clear opinions
* Less decision fatigue
* Less setup overhead
* More cross-team consistency

Library

* Light-weight
* Sprinkle on existing apps
* Pick what you need
* Choose best tech
* Popular boilerplates exist

Existing boilerplates can also turn react into a framework. React is focused on components, where normal frameworks focus on a variety of areas. Where react focuses on components, a framework like Angular focuses on components in addition to testing, HTTP library, routing, i18n, animation, and form validation. These missing features mean react functions explicitly as a library, however, it can be bundled with other technologies to cover the ground (this is where boilerplates take shape).

### Consise 

React trades conciseness for explicitness. The standard before react was via _two-way binding_, while React features _one-way binding_. Two-way binding required less code and was automatic, but one-way offers more control per event and is more explicit (clearly states what happens).

### Template-centric vs. JavaScript-centric

Frameworks like Angular and Vue aim to make HTML more powerful by implementing their own syntax into HTML. React does the opposite, where it uses the power of JavaScript to handle HTML.

Conditional Differences:

* Angular: `<h1 *ngIf="isAdmin">Hi Admin</h1>`
* Vue: `<h1 v-if="isAdmin">Hi Admin</h1>`
* Ember: `<h1>{{if isAdmin 'Hi Admin'}}</h1>`
* React: `{isAdmin && <h1>Hi Admin</h1>}`

Loop Differences:

* Angular: `<div *ngFor="let user of users">{{user.name}}</div>`
* Vue: `<div v-for="user in users">{{user.name}}</div>`
* Ember: `{{#each user as |user|}}<div>{{user.name}}</div>{{/each}}`
* React: `users.map(user => <div>{user.name}</div>)`

Event Differences:

* Angular: `<button (click)="delete()">Delete</button>`
* Vue: `<button v-on:click="delete">Delete</button>`
* Ember: `<button onclick={{action 'delete'}}>Delete</button>`
* React: `<button onClick={delete}>Delete</button>`

Since react is plain JS, this offers autocomplete support and error support. Attribute names in JSX follow camelCase since it follows JavaScript rules.

Template-centric approach

* Little JS knowledge required.
* Avoid confusion with JS binding
* Rule of least power

JavaScript-centric

* Little framework-specific syntax
* Fewer concepts to learn (it's JS).
* Less code, easier to read.

### Separate vs. Single File

Patterns like MVC popularize separating the **M**odel (JS), **V**iew (HTML), and **C**ontroller (JS). The Model contains the data, and the Controller controls the interactions with the model. In **React**, each component stands on its own as JS and JSX. This means markup and logic are co-located in the same file. React doesn't force styling into the same file, either - it can be handled externally if desired.

React handles the separation of concerns differently. Traditonally each technology is places in a seperate file (HTML, CSS, JS), but in React, all of these technologies are intertwined as a component rather than a language (Button, Datepicker, Accordian, etc.). Each component is a separate concern.

React is used to construct **nested components**. This is best thought of like a Russian Doll set, where each doll contains a smaller doll inside; React keeps this idea in line by creating components that can be used together in a rich reusable way. Components should be thought of in the ATOMIC design. On the author page of Pluralsight, you might construct it in this way.

Star Rating -> Course Summary -> Author Courses
Author Photo -> Author Summary
Nav Link -> Sidebar Navigation

### Standard vs. Non-standard

The standard of HTML5 components has not been fully embraced by the community; people still prefer non-standard frameworks. The biggest reason people aren't using standard web components is because browser support requires pollyfills. Browser support is very unsupported and after years of waiting it's become clear that browser vendors have shown little interest in implementing HTML5 components. Additionally, web components don't offer anything new - everything you can do with web components can be done using modern libraries.

### Community vs. Corporate Backing

While React is an open source project, it's backed and maintained by Facebook; this means React is driven by Facebook's needs. It does however mean you get the support of a full-time development staff.

## Concerns to Not Use Reaction

* HTML and JSX Differ
* Build Step Required
* Version Conflicts
* Outdated Resources Online
* Decision Fatigue

### HTML and JSX Differ

JSX compiles to JS. `<h1 color="red">Heading here</h1>` will compile into `React.createElement("h1", {color: "red"}, "Heading here")`. Technically, JSX is optional because it always compiles into JS. This concern is a misconception because the difference of HTML and JSX are trivial. Converting HTML to JSX is trivial.

| HTML | JSX |
|------|-----|
|for|htmlFor|
|class|className|
|<style color="blue">|<style={{color:'blue'}}|
|\<!-- Comment -->|{\*/Comment/\*}|

### Build Step Required

The argument is that React requires a build step. This is a pointless argument, though, since nearly any modern web application requires a build step to minify, transpile, and linting code. Both Babel and TypeScript can transpile JSX and boilerplates exist to make it easy to include a build step.

### Version Conflicts

Having a runtime creates potential version conflicts. You can't have two versions of React running at the same time on the same page; this means all react components must be in the same version. Standard web components don't require a runtime, but that comes with the negatives outlined above. However, React is often used with other React sources like React Router; this means you **must** run a recent version of React to support the other imports. This is usually not an issue due to the nature of React's code mod support, though.

### Old Stuff Online

There's a concern that old samples will show up in searches since it's evolved from its conception. Some features have been extracted from React Core to keep the library lean. `react-dom` was moved to a different package, `React.createClass` was extracted to `create-react-class`, `PropTypes` was extracted to `prop-types`, `mixins` were removed for higher order components and render props.

### Decision Fatigue

Due to React's design, it means one thing can be done in many ways. This is abstractly different than a framework where there are designated solutions. There are five fundamental ideas that you need to choose upfront.

* Dev environment
* ES class or createClass
* Types
* State
* Styling

#### Developer Environment

There are over 100 React boilerplates; `create-react-app` is the suggested basic configuration, but having so many options means that picking the exact environment can be a chore.

#### ES Classes or createClass

Each has its advantages. `createClass` is typically friendlier to beginners since avoids confusion around JavaScript's `this` keyword by autobinding functions, while `ES Class` is the most popular and powerful method.

```jsx
// createClass
var createReactClass = require('create-react-class');

var Greeting = createReactClass({
  render: function() {
    return <h1>Hello</h1;
  }
})

// ES Class
import React from 'react';

class Greeting extends React.Component {
  render() {
    return <h1>Hello</h1>;
  }
}
```

#### Types

There are three ways to handle types in React: React PropTypes, TypeScript, or Flow. With PropTypes, types are only checked at runtime, and only during development. TypeScript follows the standard typing method of `<var-name>: <type>`, and checks types at compile time so you find out earlier about type relations. Flow intelligently checks types by annotating `// @flow` at the top of any file you want it to check, then passing the same `<var-name>: <type>` pattern; types are checked when flow is run.

PropTypes is generally recommended, followed by TypeScript, then Flow.

#### State Management

State (data) is generally handled by four management systems: Plain React, FLux, Redux, and MobX. React handles component state fine by itself, so the other systems are optional. Flux will offer centralized state, Redux does the same and is the most popular choice by offering Flux's ability in a better way, and MobX offers observable state.

#### Styling

There are countless suggested stylings for React, but the recommendation is to just use what you already know.
