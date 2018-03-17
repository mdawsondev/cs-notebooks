# Practical Design Patterns in JavaScript

[This course is available on Pluralsight](https://app.pluralsight.com/player?course=javascript-practical-design-patterns).

## About Design Patterns

JavaScript is meant to be designed around an OOP approach. Design patterns exist in various formats, the idea is to approach the problem with a specific pattern that will help the most.

The philosophy behind design pattern originated from an architect; it can be described as a problem/solution display.

> Problem: On/Off Traffic for Highways | Solution: Cloverleaf Interchanges
> 
> Problem: Pedestrian Traffic | Solution: Sidewalks
> 
> Problem: Entry and Exit for Public Buildings | Solution: Revolving Doors

In programming, a book was released to help translate this to code design.

> Problem: Designing Service Layers | Solution: Module Pattern
>
> Problem: Overly Complicated Object Interfaces | Solution: Facade Pattern (ex. jQuery)
>
> Problem: Visibility into State Changes | Solution: Observer Pattern

We should approach design with, "What's the problem were trying to solve?" and address it with a solution pattern.

**A pattern:**

* Solves a problem.
* Is a proven concept.
* Solution is not obvious.
* Describes a relationship.
* Has a significant human component.

Patterns should be used because: there's no reason to solve a problem that's already been solved, and it establishes a common vocabulary.

**Types of Patterns:**

* **Creational**: Deals with creation of instances.
  1. Constructor
  2. Module
  3. Factory
  4. Singleton
* **Structural**: Deal with makeup of objects themselves.
  1. Decorator.
  2. Facade.
  3. Flyweight.
* **Behavioral**: Deal with how objects relate.
  1. Command
  2. Mediator
  3. Observer

## Creational Design Patterns

### Constructor Pattern

The constructor pattern is used to create new objects with their own object scope. Focuses on the `new` keyword. Dropping `new` in front of any function invokes a constructor function.

* Creates a new object.
* Link to an object prototype.
* Binds `this` to the object scope.
* Implicity returns `this`.

The teacher of this course is using old syntax rather than ES6, so I'll be making my notes in ES6.

``` JS
class ObjectName {
  constructor(param1, param2) {
    this.param1 = param1;
    this.param2 = param2;
  };

  toString() {
    return `${this.param1} ${this.param2}`;
  };
}
```

The `this` keyword is binding our construction to the object's scope.

ES5 recommends extracting your functions from the constructor function and placing them into `ObjectName.prototype.myMethod = function() {}`, but this isn't necessary in ES6 because the object distributes the prototype data automatically. It isn't generating new methods with every instance.

Exporting classes from an external .js file is a good way to segregate and modularize code. `module.exports = ObjectName`.

### Module Pattern

* Simple way to encasulate similar methods.
* Creates a "Toolbox" of functions to use.

A module is best represented when you need "one of something," ex. a fetch service, database service, etc. Constructors are best left for things you will create multiple instances of.

``` JS
const MyModule = function() {
  const priateVar = 'I am private.';
  return {
    method: function() { ... },
    nextMethod: function() { ... }
  }
}
```

Modules are not called with a `new` call, they're meant to be created as a literal. **Modules always return methods!** When sliced out of the main code and into their own file, they are returned with `module.exports = myModule()`, where the function can be executed immediately and return the methods it houses.

An alternative to directly returning methods is by creating a "revealing module," where you distribute methods in the return but define them in the object itself.

``` JS
const MyModule = function() {
  const priateVar = 'I am private.';
  
  function method() { ... };
  function nextMethod() { ... };
  
  return {
    method: method;
    nextMethod: nextMethod.
  }
}
```

### Factory Pattern

* Simplifies object creation.
* Creating different objects based on need.

_Doc Saved._