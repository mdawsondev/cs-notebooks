# Lesson 9 - Python Classes and Inheritance

_This is a continuation from Lesson 8._

Using OOP, each instance of a class is considered a different object. As a different object, you can associate each object with its own unique attributes. This means, for example, if we had a class representing `animal`, we could distribute common properties among _cat_ and _dog_, but give them their own unique data structures common to that specific subclass.

## Getters and Setters

On top of instancing and passing attributes, we can use **getters and setters**. These should be used outside of a class to access data attributes, so the attributes are not being accessed directly. `get` essentially returns the value of any data attributes, and `set` sets the value of those attributes. `def get_age(self): return self.age` to pull the data, and `def set_age(self, newage): self.age = newage` to set the data. Parameters can also be given a default value by including an `=` in the list, ex. `def set_name(self, newname="")`. Getters and setters are used to prevent bugs if someone changes the object's data.

`myClass.myAttribute` is allowed, but not recommended: `myClass.get_myAttribute()` would be the preferred way of accessing data. One of the points of using a class is to abstract the content away from the user; this includes abstracting away the data.

Accessing data `print(myVar.age)`, writing data `myVar.age = 'infinite'`, or creating attributes `myVar.newAtt = 'tiny'`, outside of the class definition are all considered **bad style**.

## Inheritance

Inheritance plays a role in further expanding abstraction. For example, say we have the group `animal`, but we also have _cats_, _bunnies_, and _people_ all in that class. Those animals in themselves can be sub-classes of animals with their own common groups. To further break this down, in our `animal` -> `people` class, we might have `students` that would have sub-properties that differ from `people`.

* Parent Class (superclass)
* Child Class (subclas)
  * Inherits all data and behaviors of parent class.
  * Adds more info.
  * Adds more behavior.
  * Override behavior.

``` py
class Animal(object):
  def __init__(self, age):
    self.age = age
    self.name = none
  # Include getters, setters, and __str__

class Cat(Animal):
  def speak(self):
      print("meow")
  def __str__(self):
      return "cat:"+str(self.name)+":"+str(self.age)
```

If you keep adding further child classes, Python will treat the method calls via scope. If the method does not exist in the current definition, it checks the next parent and so on until it breaks to the global scope.

```py
class Person(Animal):
    def __init__(self, name, age):
        Animal.__init__(self, age) # We already call the age parameter in Animal, so we reuse it here.
        self.set_name(name)
        self.friends = []
    def get_friends(self):
        return self.friends
    def add_friend(self, fname):
        if fname not in self.friends:
            self.friends.append(fname)
    def speak(self):
        print("hello")
    def age_diff(self, other):
        diff = self.age - other.age
        print(abs(diff), "year difference")
    def __str__(self):
        return "person:"+str(self.name)+":"+str(self.age)

# This can further be sub-categorized

import random

class Student(Person):
    def __init(self, name, age, major=None):
        Person.__init__(self, name, age)
        self.major = major
    def change_major(self, major):
    self.major = major
    def speak(self):
        r = random.random()
        if r < 0.25:
            print("I have homework")
        else:
            print("I am watching tv")
    def __str__(self):
        return "student:"+str(self.name)+":"str(self.age)"
```

## Class Variables

Class variables differ from instance variables in that while an instance has the `self.myAttr` attribute, a class variable stays with the class object itself, and is not distributed to instances inless called.

```py
class Rabbit(Animal):
    tag = 1 # Class variable
    def __init__(self, age, parent1=None, parent2=None):
        Animal.__init__(self, age)
        self.parent1 = parent1
        self.parent2 = parent2
        self.rid = Rabbit.tag
        Rabbit.tag += 1
    def get_rid(self):
        return str(self.rid).zfill(3) # .zfill() pads the beginning with zeros
    def get_parent1(self):
        return self.parent1
    def get_parent2(self):
        return self.parent2
    def __add__(self, other):
        return Rabbit(0, self, other)
    def __eq__(self, other):
        parents_same = self.parent1.rid == other.parent1.rid \
                       and self.parent2.rid == other.parent2.rid
        parents_opposite = self.parent2.rid == other.parent1.rid \
                           and self.parent1.rid == other.parent2.rid
        return parents_same or parents_opposite
```
