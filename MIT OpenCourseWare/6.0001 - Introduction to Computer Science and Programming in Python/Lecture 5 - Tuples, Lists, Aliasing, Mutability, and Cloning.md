# Lecture 5 - Tuples, Lists, Aliasing, Mutability, and Cloning.md

## Tuples

Tuples are similar to an array in that they are a list of indexed data, however, a tuple can hold *any kind* of *any combination* of data in an immutable ordered sequence.

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

(x, y) = (y, x) '''spicy meatball 🍝'''
```

Functions can only return *one object*, but with tuple objects, we can return multiple data in one object.

``` py
def quotient_and_remainder(x, y):
    q = x // y '''this is a cast from result to int'''
    r = x % y
    return (q, r)
(quot, rem) = quotient_and_remainder(4,5) '''assigns quot and rem to result'''
```

## Lists

Basically, they're JavaScript's arrays. Lists can hold elements of different types or lists of lists. They can be iterated. Can't index outside the length of a list.

As in JS, you don't need to iterate through the length, you can iterate with a simple `for i in List` which will output `i` as the element and prevent having to code `List[i]` as the iterable.

Lists can be combined with the `+` operator which will output a new list without mutating the active lists. `[1, 2] + [2, 1] = [1, 2, 2, 1]`.

_Some time is spent here talking about commands I'm familiar with._

Strings and lists can be cast to each other. `list(myString)` will cast a string to a list while `''.join(myList)` will cast a list to a string.

Lists can be sorted via `sort` and `sorted`, where one mutates the list and the other does not. `sorted(myList)` returns the sorted unmutated list where `myList.sort()` will mutate the list because it is not a function returning a value but a method acting on the object.

Variables of lists point to the list in memory, this is why they are mutated in place and must be cloned to maintain the original list. It's more like giving an array a nickname; that object is still the same object. Cloning can be done by `myClone = myList[:]`. Nested lists will still be mutated as well.

