# Lecture 4 - Decomposition, Abstraction, and Functions

**Abstraction**: don't need to know how something works to use it. Ex., you don't know how a projector is built or functions, but you're still able to connect it to a computer and use it.

The idea behind abstraction is that the instructions are enough; there's no need to know how to rebuild a thing.

In programming, we think of a piece of code as a "black bos" in which we:
* Cannot see details.
* Do not need to see details.
* Do not want to see details.
* Hide tedious coding details.

Absctraction is achieved with function specifications or docstrings.

---

**Deconstruction**: different devices working together to achieve an end goal; taking a thing and breaking it into smaller parts that still complete the same outcome.

In programming, we divide code into **modules**, which are:
* Self-contained.
* Used to break up code.
* Intended to be reusable.
* Used to keep code oranized.
* Used to keep code coherent.

## Functions

**Functions**: reusable chunks of code that are called/invoked to perform their action.

Function have these characteristics:
* A name: should be descriptive.
* Parameters (0+): arguments into the function.
* Docstring (very recommended): specifications in triple quotes.
* A body: the code that processes the parameters or runs defined script.
* Return: potentially return a value.

``` py
def is_even(i):
    """
    Input: i, a positive int
    Returns True if i is even, otherwise False
    """
    print("inside is_even")
    return i%2 == 0

is_even(6)
```

### Variable Scope

* A formal parameter gets bound to the value of the actual parameter when the function is invoked.
* New scope/frame/environment created when we enter a function.
* Scope is the mapping of names to objects.
* If no `return` is provided, `None` is returned, which represense the absense of a value (i.e. `Null` in JavaScript). There's never "no return," as `None` will still be returned.
* When a variable is called but not defined **inside of its own scope**, it jumps up one scope to see if it exists.
* Modifying global variables inside a scope is frowned upon because it makes a function non-modular.

``` py
def f(x):
    x = x+1
    print('in f(x): x =', x)
    return x

x = 3
z = f(x)
```

### Mapping Functions as Arguments

Due to the nature of Python being an **object-oriented language**, functions can be passed as arguments of functions (i.e. `func(func2))`).

In the following code, func_a is mapped to parameter `z` and then replaces `z` in the return line, once returned, it takes the place of the original function thus calling `func_a` once it's hit. `func_a` is then expanded into its own scope and since it returns nothing (i.e. `None`), it returns `None` to `func_a` and `func_a` then returns that same `None`.

``` python
def func_a():
    print 'inside func_a'

def func_b(z)
    print 'inside func_b'
    return z()

print func_c(func_a)
```

**Side Node**: Python allows nested functions; in general, these are best used when kept small and are clearly only useful in the enclosing function.