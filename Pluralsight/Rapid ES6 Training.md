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

* `myString.startsWith('Word') // Boolean`
* `myString.endsWith('Word') // Boolean`
* `myString.includes('letters') // Boolean`

* `'\u{1f3c4}'` Unicode is available in what's called "astral plane values".
* `myString.normalize()` will handle unusual characters more accurately.
* `myString.repeat(n)` will repeat the string n-times.

### Number Extensions

* `Number.parseInt` and `Number.parseFloat` are equal to their originals, but you're better off not using the global calls.
* `Number.isNaN` will compare accurate NaN comparison.
* `Number.isFinite` checks against finite numbers; it won't translate strings to numbers.
* `Number.isInteger(3)` check against real ints.
* `Number.isSafeInteger(a)` checks if floating point will return safe ints.

Number constants exist now too.

### Math Extensions

A number of math extensions have been added for arithmetic and trug. `cbrt()` for cube root for example. There's many, and I'm not writing them down. 👍

* `Math.sign(n)` checks against the sign of the number available.
* `Math.trunc(n)` is good for cutting the integer out; good for random.

### RegExp Extensions

* `/regex/.test('word')` will return a bool. If using a unicode, we need to add the flag `/u` to our pattern.
* The new `//y` flag will test the pattern against the last index. You can define the lastIndex of your pattern to test against the location, where `/900/y.lastIndex = 3` testing against `'800900'` will return true.
* Regular expressions now hoave the `.flag` property. The flags will always be returned in the order `gimuy`.

### Function Extensions

Functions now offer the `.name` property. Anonymous functions return their variable property. Classes will return their name, and the name of a method will return the method name. `Function.name` isn't writable, but it can be configured with `Object.defineProperty()`.

## Iterators, Generators, and Promises

This section focuses heavily on Generators, and I don't feel like I learned enough to justify taking notes here because the whole lesson went a bit over my head. This will be revisited in another course and I may return to make more notes here after that.

### Iterators

See header note.

### Generators

See header note.

### Yeilding in Generators

See header note.

### throw and return

See header note.

### Promises

See header note.

### More Promise Features

See header note.

## Arrays and Collections

### Array Extensions

Arrays used to have an issue where passing a single numerical value to an `Array(n)` function would return an array of n-length. Passing a number like 90000 would create an array with 90000 empty positions. This has been fixed in ES6 with `Array.of(n)` where `.of` passes a new array with the contents, and not the count.

`Array.from` works similarly. Without having him say it, I think it works a lot like `myArr.map()` where you're acting against the individual items of an existing array and then passing them to a new array.

``` js
let amounts = [800, 810, 820];
let salaries = Array.from(amounts, v => v+100);
```

We're taking the amounts array, passing the elements to the lambda function, and then creating a new array with the results. `.from` also takes a third parameter, an object, which will become the lexical `this` in the funtion. This must be passed with `function()`, because arrow functions don't allow changes from `this`.

Arrays offer a new `.fill()` property that will fill an array's **existing positions**. It accepts a second parameter that says where to start filling via index. `[,,,].fill(900, 1)`. A third param is also available, offering a non-inclusive index to stop at. Negative parameters can be passed to start from the other end of the array.

`myArray.find(value => value > 5)` is another array feature that will return the **first truthy value** to pass the logic test. This differs from `.filter()`, which will return **all** elements that pass the logic. This couples with `.findIndex()` returning the first value. `.findIndex()` differs from `.indexOf()`, where `.indexOf()` expects a value as the first parameter, and `.findIndex()` expects a callback.

`myArray.copyWithin(a, b)` will copy the value TO index `a` FROM index `b` in the same array. Passing a third param, `c`, allows you to copy the number of positions from the start destination. This is **not** a single positional copy! The array will copy everything FROM point `b` and onward.

Passing the spread operator on an array and invoking `.entries()` will display each entry and the index of that entry; each of these results are an array. `let ids = ['a', 'b', 'c']; console.log(...ids.entries()); //[0, 'a'], [1, 'b'], [2, 'c']`

`.keys()` is also available to pass to a spread operator on an array, returning the keys. On a standard array this will only return the index. Alternatively, calling `.values()` will return the values of the array.

### ArrayBuffers and Typed Arrays

An **ArrayBuffer** is an array of 8-bit bytes. _Typed_ arrays, which refer to numeric types, exist on top of ArrayBuffers. This allows us to have arrays of integers and floats.

We use bracket notation of ArrayBuffers just as we would a normal array. Calling a number into a new ArrayBuffer will create an array of that size in bytes.

``` JS
let buffer = new ArrayBuffer(1024);
buffer.byteLength // 1024
buffer[0] = 0xff;
console.log(buffer[0]); // 255
```

Once we have an ArrayBuffer set up with 8-bit bytes, we can add a typed array on top and use those bytes.

* `Int8Array()`
* `Uint8Array()` Unsigned.
* `Uint8ClampedArray()` Clamped forces high of 255 and low of 0.
* `Int16Array()`
* `Uint16Array()`
* `Int32Array()`
* `Uint32Array()`
* `Float32Array()`
* `Float64Array()`

``` JS
let buffer = new ArrayBuffer(1024);
let a = new Int8Array(buffer);
a[0] = 0xff;
console.log(a[0]); // -1 since it's signed.
```

Who am I kidding, I have almost no idea what's going on here. I'll have to revisit this nonsense. 👎

### DataView and Endianness

In **big endian** the most significant byte is stored first, in **little endian** the least significant is stored first.

**DataView** offers a variety of methods for looking at the endianness of ArrayBuffers.

What does this mean? Who knows. ¯\\\_(ツ)_/¯

### Map and WeakMap

ES6 offers two new classes, `Map` and `WeakMap`. `Map` is technically used all the time in JavaScript - every object can be considered a map of keys and values. In an `Object`, however, these keys must be strings or numbers. You can't use an object as a key - this is what `Map` was created for.

``` JS
let employee1 = { name: 'Jake' };
let employee2 = { name: 'Janet' };

let employees = new Map();
employees.set(employee1, 'ABC');
employees.set(employee2, '123');

console.log(employees.get(employee1));
```

Methods include `.set()` to add entries, `.delete()` to remove entries, `.clear()` to remove **all** entries, `.size` to call Map size. `.has()` will check and return a Boolean based on whether the map contains the item. `.values()`, `.keys()`, and `.entries()` (which is a combination of the full entry) also exist as methods on the Map object.

Passing `Map` an iterable, like an array of arrays, will cast the internal array into the map. `arr = [ [emp1, 'abc'], [emp2, '123] ]` will output the two inner arrays into the map.

`WeakMap` will only store data until it gets garbage collected. If you set an entry to `null` so it gets picked up by the GC cycle, it'll disappear. That said, you can't check the `size` of a WeakMap. Once something is GC'd, it's impossible to find a reference to it.

### Set and WeakSet

`Set` and `WeakSet` are meant to deal with single values or objects. They hold exactly one copy of whatever is injected into them - there's no mapping of a key/value relationship. `Set` is used to **ensure uniqueness**, and `WeakSet` functions like `WeakMap`, dumping data upon garbage collection. Like `Map`, `Set` can take an iterator in its constructor and will spread the data into the Set.

The available methods are `.add()` to add items, `.size`, `.remove()`, `.has()` returning a Boolean, `.keys()`, `.values()` both of which display each item because the items are treated the same, and `.entries()` which returns two of each item since the key and value are the same.

``` JS
let perks = new Set([
  { id: 800 },
  { id: 800 }
]);

console.log(perks.size); // 2
```

This returns two since both objects, while the same content, are actually two unique object literals in memory.

### Subclassing

Most built-in objects (Array, RegExp, Function, Number, etc.) can be subclassed, or extended. Before working with subclasses (as with most things) be sure the target platform can handle it. [CanIUse](https://caniuse.com) and [Kangax's Chart](https://kangax.github.io/compat-table/es6/) should give an indication of availability.

Subclassing is essentially using `extends` as you would on any standard `class` object.

``` JS
class Perks extends Array {}
let a = Perks.from([5, 10, 15]); // Works exactly like Array.
```

## The Reflect API

### Construction and Method Calls

`Reflect` is an non-function object (i.e. not constructible) that provides methods for operations. When arguments are passed to the construct method, they need to be array elements.

`Reflect.construct(target, argumentsList[, newTarget])`

``` JS
class Restaurant {}
let r = Reflect.construct(Restaurant);
console.log(r instanceof Restaurant); // true
```

``` JS
class Restaurant {
  constructor(name, city) {
    console.log(`${name} in ${city}`);
  }
}
let r = Reflect.construct(Restaurant, ["Zoey's", "Goleta"]);
```

The third argument of construct (optional `newTarget`) will replace the value of `new.target` in the construction class. This means in the example below, restaurantMaker is not being _invoked_ `()`, so it simply prints the function in place of the `new.target` value.

``` JS
class Resturant {
  constructor() {
    console.log(`new.target: ${new.target}`); // Points to the call point.
  }
}
function restaurantMaker() {
  console.log(`in restaurantMaker`);
}
let r = Reflect.construct(Restaurant,
          ["Zoey's", "Goleta"], restaurantMaker);
```

We can call functions with `Reflect.apply(target, thisArgument, argumentsList)` through our class construction. By accessing `Restaurant.prototype.show` below, we can pass the id through the method. `Reflect.apply()` is a low level function that doesn't need an instance of a class to interact with the class constructor.

``` JS
class Restaurant {
  constructor() {
    this.id = 33;
  }
  show(param) { // Accepts from argumentList of .apply.
    console.log(this.id);
  }
}
Reflect.apply(Restaurant.prototype.show, { id: 99 }, ['REST:']);
// REST: 22
```

### Reflect and Prototypes

`Reflect.getPrototypeOf(target)` which will pull the prototype of an object/function.

```JS
class Location {
  constructor() {
    console.log('constructing Location');
  }
}
class Restaurant extends Location {}
console.log(Reflect.getPrototypeOf(Restaurant)); // Logs Location's constructor().
```

`Reflect.setPrototypeOf(target, prototype)` allows for passing of new prototypes.

``` JS
class Restaurant {}
let setup = {
  getId() { return 88; }
}

let r = new Restaurant();
Reflect.setPrototypeOf(r, setup);
console.log(r.getId()); // Passes 88 because the literal was attached.
```

### Reflect and Properties

`Reflect.get(target, propertyKey[, receiver])` will get a property's value.

This whole section is losing me since I've never played with `Reflect` before so I'm just skipping ahead and will return to studying these weird new objects in another resource.

### Reflect and Property Extensions

Me no smart. Has emoji instead. 👾

## The Proxy API

### Proxies Defined

Proxy is an object that wraps another object or function. With the proxy we can monitor access to the object or function inside the proxy. This is great for security.

The technical term for the object wrapper is the "handler," which is what we give access to. A proxy will allow you to intercept various calls to the target object and return handler properties rather than the internal object's properties.

_Aside: The main use of the Reflect API is to work with the Proxy API (handler objects)._

### Available Traps

The Proxy API can trap the following calls: `handler.construct()`, `handler.apply()`, `handler.getPrototypeOf()`, `handler.setPrototypeOf`.

Additionally the handler can intercept `.get()`, `.set()`, `.has()`, `.ownKeys()`.

Can't trap comparisons, `typeof`, `instanceof`, operations (target+""), or object calls `string("")`.

### Get by Proxy

Approval Proxy:
``` JS
function Employee () {
  this.name = "Milton Waddams";
  this.salary = 0;
}
var e = new Employee();
var p = new Proxy(e, {
  get: function(target, prop, rexeiver) {
    return Reflect.get(target, prop, receiver);
  }
})
console.log(p.salary); // Returns 0, proxy passes through reflect.
```

Denial Proxy:
``` JS
function Employee () {
  this.name = "Milton Waddams";
  this.salary = 0;
}
var e = new Employee();
var p = new Proxy(e, {
  get: function(target, prop, rexeiver) {
    if (prop === 'salary') return 'Denied';
    return Reflect.get(target, prop, receiver);
  }
})
console.log(p.salary); // Returns Denied.
```

### Calling Functions by Proxy

This is beyond me at this point; will return to this in another course.

### A Proxy as a Prototype

This is beyond me at this point; will return to this in another course.

### Revocable Proxies

This is beyond me at this point; will return to this in another course.

_Note to self: need to revisit **generators**, **Reflect/Proxy**, and **iterators/promises** in external sources!_

_"Meow."_ - 🦑