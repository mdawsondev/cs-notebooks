# JavaScript Best Practices

[This lesson is available on Pluralsight](https://app.pluralsight.com/player?course=javascript-best-practices).

## Syntax

### Semicolons

Semicolons are not "strictly speaking" necessary due to automatic semicolon insertion. When JavaScript parses code and notices an invalid character following a designation, it places a semicolon where expected.

That said, not including semicolons will cause problems **when the syntax is still allowed**.

``` JS
var a = 12 // Automatic semicolon.
var b = 13 // Automatic semicolon.
var c = b + a // Will throw an error.
// The brackets from the array become tethered to `a` without a semicolon.
['menu', 'items', 'listed']
  .forEach(function (element) {
    console.log(element) // Automatic semicolon.
  })
```

This could also occur by accident when you're bundling multiple JavaScript files. Immediately invoked functions may end up tethering together unexpectedly. Additionally, restricted words (`return`, `continue`, `break`) will automatically adopt a semicolon even when they're not wanted. That's why it's important to follow standards.

``` JS
if (somethingTrue)
{
  return // This will adopt a semicolon and break the code.
  {
    hi: 'hello'
  }
}
```

### Linting

Scans code to detect potential problems and errors. This section talks about installing JS Hint or ESLint; I already use ESLint so I'm not listing notes here.

### Curly Braces

Basically nagging at .NET developers who put braces on next lines rather than tethering them to the same line. 😛

### Equality

Talks about `==` and `===`, I'm already familiar with the consept and oddities behind equality so nothing noteworthy. Mentioned on the side, `typeof var` should be used for checking existance.

### JSHint Config

Nothing noteworthy.

### Variables

This section talks about hoisting and scope. I'm familiar with this but I'm going to make a nore anyway.

``` JS
console.log(myVar);
const myVar = 12;
```

What happens here is that myVar is checked to see if it exists and isn't defined until it's actually set. `myVar` is created as `undefined` until it actually crosses the declarative `const` line.

### Functions

Functions are objects and this causes oddities in the syntax. There are two types of functions: **declarations** and **expressions**.

The compiler will hoist declarations `function myFunc()` meaning functions can be called from any point in the code. However, function expressions `var myFunc = function ()` are **not** hoisted in context because the function isn't assigned until it's called on a line-by-line basis.

## Behaviors

### Global Variables

If a variable isn't declared and is passed a parameter it'll be hoisted into the global scope out of its lexical function scope. Nothing else noteworthy here but that was kind of interesting.

### Strict Mode

The instructor descripted `'use strict';` as "JavaScript is trying to help... don't." This will allow errors that might have otherwise been ignored to be thrown.

`'use strict';` can also be contained to a functional scope. It doesn't have to be global, you can place it anywhere and it takes the appropriate scope.

### Read Only Properties

This discusses the `writable` property of objects. This allows objects to be read only; unchangeable. `'use strict';` will force writeable to throw an error if it's rewritten - otherwise JavaScript will usually ignore this because it wants to help.

Like a sentient, happy robot. 🤖👍

### Deleting Properties

Not using strict mode will also cause problems when trying to delete objects. You can only delete something from an object; you **can't delete objects themselves**.

``` JS
let obj = { a: 100, b: 200 };
delete obj.a // Does in fact delete 'obj.a'.
delete obj // Not deleted.
```

### Duplicates

Running a function with duplicate parameter names won't throw an error without strict mode enabled. `function x(a,b,a)` will lock `a` as the last submitted variable.

### Octals and Hexidecimals

If you place a `0` in front of a number in JS, it will treat the number as an **octal number**. Example: `012` in octal is 10, and will not output 12.

Adding an `x` after the `0` (e.g. `0x12`) will produce a hexidecimal number. `0x12` in hex outputs 18. If you really want to use octal, you should use `parseInt(12, 8)` to obey the standards of `use strict`.

### With

`with` has been depreciated and **should not be used** for security reasons.

Don't use `with`.

``` JS
with(obj.a.b) {
  console.log
}
```

Instead, pass the object through a function.

``` JS
(function(newVar){
  console.log(newVar);
}(obj.a.b.c))
```

### What is `this`

`this` refers to the object it's associated with. `this` has been removed from the lexical scope of arrow functions `=>` and `function()` should still be used if `this` is needed in a function outside of a class or object.

When `this` can't attach itself to the instance of an object, it hoists itself to the first object it finds, and that potentially becomes the global object (such is the case with arrow funcs).

### ```this``` in New Objects

`this` creates a pointer to the original object when it's called from a function declaration. I'm pretty sure that's not the case when using Class objects, though.

## Async Patterns

### Callbacks

Anonymous functions are not required for callbacks and this creates what people call "christmas tree hell" when stuffing anonymous function inside of anonymous functions.

* Named functions are a much cleaner way to support callbacks.
* Pass callbacks through the format `function(error, results)` or whatever is consistant in your environment.
* Return your callbacks.

### Promises

Typically JavaScript sends a callback to execute a string of async commands.

``` JS
function asyncMethod(message, cb){ 
  setTimeout(function() {
    console.log(message);
    cb();
  }, 500)
}

asyncMethod('Open DB Connection', function() {
  asyncMethod('Find User', function() {
    asyncMethod('Validate User'), function() {
      asyncMethod('Do Stuff', function(){});
    }
  });
});
```

With the inclusion of `Promise` in ES6, callbacks can be replaced in favor of the `.then()` method.

``` JS
function asyncMethod(message) {
  return new Promise(function (fulfill, reject) {
    setTimeout(function() {
      console.log(message);
      fulfill();
    }, 500);
  });
}

asyncMethod('Open DB Connection').then(function () {
  asyncMethod('Find User').then(function () {
    asyncMethod('Validate User').then(function () {})
  })
})
```

However, combining callbacks with `Promise` offers even a better solution.

``` JS
function asyncMethod(message) {
  return new Promise(function (fulfill, reject) {
    setTimeout(function() {
      console.log(message);
      fulfill();
    }, 500);
  });
}


asyncMethod('Open DB Connection')
  .then(findUser, err)
  .then(validateUser, err);
```

### ES6 and Babel

Just talks about transpilation from ES6 through Babel; nothing noteworthy.

### Async - Await

Fundamentally, this eliminates the need for callbacks and promises. Async mentality still works off of `Promise`. Async await is what other languages technically do; they wait for completion.

``` JS
async function main() {
  const one = await asyncMethod('Open DB Connection');
  const two = await asyncMethod('Find User');
  const three = await asyncMethod('Validate User');
}

main();
```

## Production Code

### NPM

Basic info about using `npm`, nothing noteworthy.

### Environmental Variables

Talks a bit about `process.env` environmental variables. I'm not really sure why he's diving into this, because it suddenly starts talking about Express and modules that weren't addressed before now.

### Cross Platform Concerns

Some brief information about running things crossplatform; name things lowercase for files.

### Simplify Your World

Basically, use tools that make things easier for you - there's no reason to force yourself to use tools that you don't need.