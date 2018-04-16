# Lesson 8 - Object Oriented Programming

## Objects

Everything in Python is an object (and has a type). With this, we can create new objects of some type, we can manipulate existing objects, and we can destroy objects by explicitly using "del" or just ignoring them. Python will reclaim destroyed objects with "garbage collection".

Objects are simply a _data abstraction_ that captures: an **internal representation** through attributes and an **interface** for interaction through methods. Typically, the interface is abstracted away because the user doesn't need to know "how" things work, but rather what the methods do.

The high-level idea is that you are able to compile this data into a bundle; you can combine the data and interactions into "packages".

## Classes

Classes are split as the class itself an an instance of the class (or blueprint and then the creation). Creating a class involves defining the name and attributes, and using that class involved creating instances of objects and doing operations on the instances. When you create an instance of this class, it has the `type` of the name of your class.

To begin, we define a class by calling the definition, giving it a name, and passing the class parent. Generally we will pass `object` as it's the very basic type everything else is built on.

```py
class Name(object):
  #define attributes here
```

We then add _attributes_ to the class. Attributes are data and procedures that belong to the class. Data attributes can be thought of as other objects that make up the class, for example, a coordinate is made up of two numbers. Methods (procedural attributes) can be thought of as functions that only work with this class. They define how to interact with the object; for example, you can define a distance between towo coordinate objects but there is no meaning to a distance between two `list` objects.

In Python, attributes are defined in a special method called `__init__`, which is similar to JavaScript's `constructor() {}`. We also call `self` (similar to JavaScript's `this`) to define these properties existing to the instance of the class. The `self` parameter can technically be passed as any name, but by convention it's known as `self`. Paramaters beyond this initial param are just normal parameters that belong to the definition.

```py
class Coordinate(object):
    def __init__(self, x, y):
      self.x = x
      self.y = y
```

Since Python does not offer type enforcement, we could include information about what these values are supposed to be in the docstring, or we could pass them through an `assert` to make sure they are actually the type expected. When we create an instance of our class, we simply call `c = Coordinate(3,4)` passing only two parameters to fill our definition beyond `self`, where `self` will take the place of `c`

``` py
class Corrdinate(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def distance(self, other):
      x_diff_sq = (self.x-other.x)**2
      y_diff_sq = (self.x-other.y)**2
      return (x_diff_sq + y_diff_sq)**0.5
```

To calculate the distance in our example, we can call this method thusly:

``` py
c = Coordinate(3,4)
zero = Coordinate(0,0)
print(c.distance(zero))

# Equivalent to

c = Coordinate(3,4)
zero = Coordinate(0,0)
print(Coordinate.distance(c, zero))
```

In Python, when we print the representation of an object we aren't provided useful information other than the memory pointer location. We can change this by passing data to `__str__` within our class, which is called when `print` is invoked on the object. `__str__` must return a string. You can also print whether an object is an instance of a class with the function `print(isinstance(myVar, myClass))`.

```py
class Corrdinate(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __str__():
        return "<"+str(self.x)+","+str(self.y)+">"
    def distance(self, other):
      x_diff_sq = (self.x-other.x)**2
      y_diff_sq = (self.x-other.y)**2
      return (x_diff_sq + y_diff_sq)**0.5
```

In addition to `__str__` you can override other default operators (assume wrapped by `__`, ex. `__add__(self, other)`): `add`, `sub`, `eq`, `lt`, `len`, `str`, etc.; all of these will then allow you to pass your own customized functions.