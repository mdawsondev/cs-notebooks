# Lecture 5 - Tuples, Lists, Aliasing, Mutability, and Cloning.md

## Tuples

Tuples are similar to an array in that they are a list of indexed data, however, a tuple can hold *any kind* of *any combination* of data.

* Ordered sequence.
* Immutable.
* Represented with parentheses. `()`

``` py
t = ()
t = (2, "abc", 3)
t[0] '''2'''
(2, "abc", 3) + (5, 6) '''(2, "abc", 3, 5, 6)'''
t[1:2] '''("abc",) single-element tupals have a comma'''
t[1:3] '''("abc", 3)'''
len(t) '''3'''
t[1] = 4 '''error, immutable'''
```

Tuples are great for swapping variables.

``` py
x = y
y = x '''error'''

temp = x
x = y
y = temp '''long'''

(x, y) = (y, x) '''spicy meatball'''
```

Functions can only return *one object*, but with tuple objects, we can return multiple data in one object.

``` py
def quotient_and_remainder(x, y):
    q = x // y '''this is a cast from result to int'''
    r = x % y
    return (q, r)
(quot, rem) = quotient_and_remainder(4,5) '''assigns quot and rem to result'''
```

_Saved._