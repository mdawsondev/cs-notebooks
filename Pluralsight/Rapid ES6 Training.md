# Rapid ES6 Training

## New ES6 Syntax

### let, const, and Block Scoping

`let` and `const` do not support hoisting; this enforces declaration before use. Nothing else noteworthy.

### Arrow Functions

Arrows can return single-lines without using `return` but `return` is required for blocks. `this` is scoped to the context of the area it's called in. Arrow functions do not create objects with a `.prototype` field.

`this` can be scoped to an object with arrow functions `=>` via locking their scope internally. New objects can not be bound via `.bind()`, `.call()`, nor `.apply()` to an arrow function.

``` JS
const invoice = {
  number: 123,
  process() {
    return () => console.log(this.number);
  };
};
```

### Default Parameters

Default params can be set via `function(myParam = 1000)`. Passing in `undefined` to default parameters will yeild the use of the default parameter.

Declaring a defult allows the parameter to access other parameters. `(price, tax = price * 0.07)` would still allow tax to access the price parameter within the declaration.

External variables and functions can be accessed for specifying defaults.

``` JS
'use strict';
let generateBaseTax = () => 0.07;
let getTotal = function(price, tax = price * generateBaseTax() ) {
  console.log(price + tax);
}

getTotal(5.00); // Returns 5.35.
```

Accessing arguments via `arguments` is not considered best practice. `arguments` ignores default parameters and only returns information the function was passed.

### Rest and Spread

Rest refers to gathering parameters and putting them into an array. Spread is the opposite, where it distributes the contents of an array.

Rest
```JS
var showCategories = function (productID, ...categories) {
  console.log(categories);
}

showCategories(123, 'search', 'advertisting');
// Result ['search', 'advertising'] 
```

Rest parameters will always output an array, even if nothing is being passed for it to collect. It'll simply output an empty array `[]`.

Spread
```JS
var prices = [12, 20, 18, 5];
var maxPrice = Math.max(...prices);
console.log(maxPrice); // 20
```

Spread will also work on strings.

```JS
var codeArray = ['a', ...'bcd', 'e'];
console.log(codeArray); // ['a', 'b', 'c', 'd', 'e']
```

### Object Literal Extensions

Declaring object literals with key:values that match can be done with a single param call now. `price: price` can just be `price`.

Shorthand notation within method declaration works like an arrow function, where `this` will not point to the object, but the encasing area. `calculateValue() { return this.price }` needs a `function()` call to pass `this` accurately.

You can have a space in property names as long as it's wrapped in quotes. `"calculate value"` can be called with `myObj["calculate value"]()`. Additionally bracket notation can be used within the object itself.

``` JS
var field = 'dynamic field';
var price = 5.99;
var productView = {
  [field + '-001']: price
};

console.log(productView) // {'dynamic field-001': 5.99}
```

### for ... of Loops

Basically like iterating over an object except for arrays. `for (var item of categories)`, instead of `in`, which is exclusive to objects. `for ... of` can also be used to iterate through a string.

_Aside: JavaScipt lets arrays end with a comma `,`, so [,,] will output two `undefined`, not three._

### Octal and Binary Literals

With strict mode enabled, octals are now exposed with `0o`, like hex being exposed with `0x`. For example, `010` wouldn't work with strict mode, but `0o10` will now output 8 (the octal value of 10). Binary can now be accessed by `0b`, where `0b10` would output 2.

### Template Literals

Template literals are displayed with backticks in place of quotations marks for strings. They can have variables pushed into their string via `${myVar}`, where anything between `${...}` can execute valid JavaScript. Template literals also support new lines without the need for adding `+`. Interpolation takes place before the template literal is passed as a parameter into functions.

When passing a template literal, although interpolation takes place before parameter distribution, only unique values are passed into directly invoked parameters, where our `${}` values are picked up with a rest parameter.

``` JS
function processInvoice(segments, ...values) {
  console.log(segments);
  console.log(values);
}

let invoiceNum = '1350',
    amount = '2000';

processInvoice `Invoice: ${invoiceNum} for ${amount}`;

// ["Invoice: ", " for ", ""]
// [1350, 2000]
```

### Destructuring

Destructuring is basically witchcraft.

``` JS
let salary = ['32000', '50000', '75000'];
let [ low, average, high ] = salary;
console.log(average) /// 50000
```

If you try to deconstruct a value that doesn't exist and call the variable it returns undefined, were the variable was initiated but there wasn't anything to store inside of it. Additionally, elements can be skipped by providing an extra comma and not granting the space a variable name, ex. `let [ low, , high ] = salary` would only pluck the first and last values from the sample above.

Rest parameters can also be used when pulling apart through deconstruction. `let [low, ...remaining] = salary` would return `remaining` as an array of the remaining variables.

Defaults can be used when deconstructing as well; if there's nothing to fill the variable, the default is used instead.

Deconstruction works for nested arrays, and can also be used to deconstruct input parameters. `function reviewSalary([low, average], high = '88000')` passed with `['32000', '50000']` will deconstruct these values as `low` and `average` for use within the function.

To destructure objects `{}`, the format is essentially the same, except curly braces are used in place of brackets. Properties can be reassigned, as well.

``` JS
let salary = {
  low: '32000',
  average: '50000',
  high: '75000'
};

let { low: newLow, average: newAverage, high: newHigh } = salary;
console.log(newHigh) // 75000.
```

## ES6 Modules and Classes

### Module Basics

Importing: `import { projectId } form 'module1.js';`
Exporting: `export let projectId = 99;`

``` JS
import { projectId as id, projectName } from 'module1.js'
console.log(`${projectName} has id: ${id}`)

export let projectId = 99;
export let projectName = "Builder";
```

If you alias an import, the original export ID will not work; the alias is the new name in the import module. Additionally, import statements get hoisted.

When importing a default, `import anyVariable from 'module1.js';` will import the default export with the designated variable. Lack of curly braces `{}` indicates loading an export default. `export default projectBlah;`.

Alternatively, you can keep the braces and import default via `import { default as myprojectName } from 'module1.js';`.

When importing ambigious values (i.e. two exports but no default), the module loader sets your variable to `undefined`. It is possible to export as default in a chain of exports: `export { projectId as default, projectName };`.

Importing with a `*` wildcard as a variable will import a list of objects from the export module. `import * as values from 'module1.js';` and logging `values` will return everything that was exported. In our examples, the properties would be accessed via `values.projectId`.

### Named Exports in Modules

Importing an export and setting it to a variable means it is registered as a read-only property. You can't change the value of designated variables: `import { imReadOnly } from 'module1.js';`. **Properties** can be changed, however, so the following would be acceptable.

``` JS
import { project } from 'module1.js';
project.projectId = 8000;
console.log(project.projectId); // 8000.
---
export let project = {
  projectId: 99
};
```

When we grab an object out of one module and change it in a second module, the two modules stay in sync. Running a function that checks against the property of an object in the export module, having that property changed in the import module, then calling that function will still output the **new, updated property value**.

### Class Fundamentals

Basic discussion of class functionality, nothing new learned so nothing noteworthy.

### extends and super

When extending a class with a subclass, you can pass params to the original class through initialization. However, if the subclass has a `constructor`, you **must** call `super()` on the subclass or you'll be thrown a ReferenceError.

Extending with methods and variables can also have the ability to overwrite the original variable. If you define a function and then define the same function in the subclass, it'll automatically overwrite the old one.

Additionally, if calling super under a return, you can access the parent prototype's properties and use them in subclass methods. `return super.getTaskCount() + 6` is perfectly valid syntax.

**`super` can be used with object literals!** The object can extend another object by calling `Object.setPrototypeOf(myExtensionObject, mySuperObject)`.

### Properties for Class Instances

Nothing new mentioned, just note that `this` is used in the constructor method to define new properties.

### Static Members

By declaring a method as static it's attached directly to the class object, not instances. You can access static methods by `MyObject.myStaticMethod()`. If the class has a static method, these methods **are not passed on to their instances**.

### new.target

`new.target` points directly to the constructor of the class that calls it. While not useful within its own class, it's useful when you combine it with inheritance. Even if you don't offer a constructor to an extension, JavaScript provides you with one anyway.

`new.target` is used to call static outputs from extensions on the construction of subclasses.

``` js
class Project {
  constructor() {
    console.log(new.target);
  }
}
class SoftwareProject extends Project {
}

var p = new SoftwareProject();
```

This will log the default constructor of the SoftwareProject class because it's initializing the `new.target` command inside of the initialization.

```js
constructor(...args) {
  super(...args);
}
```

## New Types and Object Extensions

### Symbols

Symbols are a bit of an abstract idea where they generate a string that is **always** unique. We have no way to access it, but we know it's unique. Giving symbols a string parameter is mostly used for debugging; JavaScript stores `Symbol` as a unique ID internally.

We can call `mySyombol.toString()` to call what the original string parameter was, but it's only used as an identifier. It doesn't tell us anything about the unique character of `mySymbol`. **There is no way to access this unique ID**.

```js
let s = Symbol('event');
let s2 = Symbol('event');

console.log(s === s2); // false
```

The internam symbol registry can be accessed using `Symbol.for('')`; this means you can set two values to be represented by the same symbol; in the example above, if we had set `s2` to `Symbol.for('event')`, our console would log true because these variables point at the *same symbol*. If the symbol doesn't already exist, `Symbol` will just create a new symbol and assign it to the variable.

When trying to find the original symbol value, you can invoke Symbol.keyFor(mySymbol) to check the original debug string passed as a parameter. In our case above, it would return `event`.

### Well-known Symbols

Need to revisit this; much confuse.

### Object Extensions

`Object.setPrototypeOf(a, b)` will set the prototype of `a` to point at `b`. If `b` has `y: 2`, we could then call `a.y` to display `2`.

`Object.assign(target, a, b);` will populate the variable `target` (`target = {}`) with the parameters that exist inside of `a` and `b`. This is essentially like concating two objects together and outputting the result. If `a` and `b` share properties, `b` will be given priority. If a property is not enumerable, it's ignored.

`Object.assign` looks **directly** at the properties of an object; it doesn't walk the prototype chain, and therefore pointing at `setPrototypeOf` will have no effect on the output.

`Object.is(a, b)` will compare two `typeof` with `===`, this fixes the `NaN` issue and compares `0` to `-0` accurately.

### String Extensions

### Number Extensions

### RegExp Extensions

### Function Extensions

## Iterators, Generators, and Promises

### Iterators

### Generators

### Yeilding in Generators

### throw and return

### Promises

### More Promise Feaatures

## Arrays and Collections

### Array Extensions

### Array Buffers and Typed Arrays

### DataView and Endianness

### Map and WeakMAp

### Set and WeakSet

### Subclassing

## The REflect API

### Construction and Method CAlls

### Reflect and Prototypes

### Reflect and Properties

### Reflect and Property Extensions

## The Proxy API

### Proxies Defined

### Available Traps

### Get by Proxy

### Calling Functions by Proxy

### A Proxy as a Prototype

### Revocable Proxies

🦑 Meow.