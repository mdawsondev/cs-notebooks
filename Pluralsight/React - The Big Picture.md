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

## Why Not React
