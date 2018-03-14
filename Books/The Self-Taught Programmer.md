# The Self-Taught Programmer

_I didn't see any particular reason to take notes on things I've already learned, so I didn't bother with large chunks of the first part of this book._

## Part I - Introduction to Programming

### Chapter 1: Introduction

Introduction to the book. Nothing noteworthy.

### Chapter 2: Getting Started

Brief discussion on high-level and low-level programming. Python installation guide. Nothing noteworthy.

### Chapter 3: Introduction to Programming

Introduction to primitives, `bool`, `int`, etc.; `None` is the Python-specific syntax for `null`.

Introduction to conditionals and syntax. Large list of vocabulary at end of the chapter. Other than that, nothing noteworthy.

### Chapter 4: Functions

General information about functions, parameters, that sort of thing. Python offers a keyword `Pass` in order to create an empty function you intend to return to.

Discussion on scope and exceptions, and brief discussion on docstrings (which I had not seen prior to working with Python).

### Chapter 5: Containers

**Lists** in Python are basically arrays. They can be called through `[]` or `list()` which will invoke the object. Functionally it looks the same as JavaScript, although lists can hold a mixture of different types. They seem to have a lot of similar methods, ex. `myList.append()`, `myList.pop()`, etc.

Lists can be checks through `myVar in myList` which will output true or false. `myVar not in myList` also works. They differ from tuples in that they are mutable and data can be changed.

**Tuples** `()` `tuple()` are immutable. Upon invoking a tuple it can not be modified which includes adding or removing items. 

**Dictionaries** `{}` `dict()` are mutable, but inlike lists and tuples they aren't ordered. Dictionaries are akin to JavaScript's object object `{}`. Each item in a dictionary must have a key-value pair.

``` py
>>>myDict = {"Apple": "Red", "Banana": "Yellow"}
>>>myDict["Apple"]
"Red"
>>>myDict["Apple"] = "Computer"
>>>myDict["Apple"]
"Computer"
```

### Chapter 6: String Manipulation.

Strings can cross lines with triple quotes, similar to JavaScript's back-tick. They are itterable, but immutable. Some various methods include `.upper()`, `.lower()`, and `.capitalize()`, as well as similar JavaScript methods like `.join()`, `.split()`, and `.replace()`.

``` py
"""this string spans
multiple lines and
is now capitalized.""".capitalize()
```

Strings can be formatted via `.format()`, similar to C#'s `{1}` or JavaScript's `${code}`.

``` py
"Python was created in {} by {} in {}.".format(year, creator, county)
```

`.index()` emulates JavaScript's `.indexOf()` syntax.

Strings can also be check through `in` and `not in` with a word potentially matching in an entire multi-line sentence. They can also be escaped with a backslash `\` and special characters are available, ex. `\n`.

Strings can be concat'd and multiplied.

### Chaptert 7: Loops

Generic loop discussion: `for`, `while`, `break`, `continue`. Not much of interest.

### Chapter 8: Modules

Basic introduction to modular importing. `import math` to import built-in modules; external modules must be stored via `.py` and are imported via `import file-location\math` if not in the same folder.

### Chapter 9: Files

Introduction to Python's iosteam features. "r" is used for read-only, "w" for write-only, and "w+" for read-write accesses.

Python accesses files via `myFile = open("my_file.txt", "w+")`, where the file object now has access to `.write()` and `.close()`.

Although you can store files this way, using `with` is the prefered method so the file is scoped and will close once out of scope.

``` py
with open('my_file.txt', 'w+') as myVar:
    myVar.write("Hello, world!")
```

To read lines from files, you can iterate through each line as `for line in myFile.read()`.

Python is also very comfortable working with .csv (Excel spreadsheet files), which can be accessed with the cvs module.

``` py
import cvs

with open('my_file.cvs', 'w') as csvfile:
    spamwriter = csv.writer(csvfile, delimiter = ',')
    spamwriter.writerow(['one', 'two', 'three'])
    spamwriter.writerow(['four', 'five', 'six'])
```

When the file is opened, you will see the following.

``` txt
one, two, three
four, fice, six
```

### Chapter 10: Bringing It All Together

This chapter discusses building a Hang Man project and explains in detail what the process is for creation. Notes aren't necessary, but the project was built as a .py file. It can be found here: [Hang Man Project](https://github.com/calthoff/tstp/blob/master/part_I/bringing_it_all_together/hangman.py).

### Chapter 11: Practice

Basic challenge recommendations; nothing that noteworthy, but here's a list of the suggestions.

1. Text-based game of a sport.
2. Text-based game based on another game (i.e. Heroes of Might and Magic III).
3. Text-based Magic 8-ball that users can "shake".
4. Input mood, output song recommendation.
5. Input brand, output trademark (ex. "Nike" -> "Just do it.").

## Part II: Introduction to Object-oriented Programming (OOP)

### Programming Paradigms

The major programming paradigms are:

* Imperative Programming
* Functional Programming
* Object-oriented Programming

**State** is another word for the data your program has access to.

**Imperative programming** can be thought of as "do this, then that." It's a sequence of steps moving toward a solution.

**Functional programming** originates from lambda calculus; it involved writing functions that when given the same input always return the same output. Functional program only uses functions, *classes are not used*.

These functions do not rely on data outside of the current function, and they don't change data that exists outside of the current function.

**Object-oriented programming** involves creating objects that interact with each other. Objects are created through classes, which can be thought of as the blueprint. Classes are defined through `class Variable:` declaration, and then can be invoked through `myVar = myClass()`, just like creating any other object (i.e. `myDict = dict()`).

Methods are added to classes via `def` within the scope of the class. They're called the same way other languages call them: through `myobject.mymethod()`.

Classes can also take advantage of the `self` property, which functions like JavaScript's `this` property. `self` is tethered to the object upon creation. This must be set inside the `__init__` function.

``` py
class Orange:
    print("Orange created!")

    def __init__ (self):
        self.color = "orange"
        self.weight = 10

    def print_orange (self):
        print(self)
        print(self.color)
        print(self.weight)

>>>orange.print_orange()
```

Alternatively, `__init__` can be passed variables like JavaScript's class constructors.

``` py
class Orange:
    def __init__(self, weight, color, mold):
        self.weight = weight
        self.color = color
```

`self` can be passed through any functions inside the object blueprint. `def rot(self, days, temperature)` would still pass a `self` referencing the object it resides inside.

### Chapter 13: The Four Pillars of Object-oriented Programming

Not all languages support every programming paradigm. Haskell, for example, is a functional language which does not support OOP. Python, Java, Ruby, and JavaScript are OOP languages that can support functional programming as well.

Python supports class inheritence, where the child object can adopt the properties of the parent object. Similar to how JavaScript's `extends` works, the main object an be passed as a parameter.

``` py
class Adult():
    def __init__ (self, name):
        self.name = name

    def print_name (self):
        print(self.name)

class Kid(Adult):
    def print_cartoon(self, favorite_cartoon):
        print('{}\'s favorite cartoon is {}'.format(self.name, favorite_cartoon))

son = Kid("John Smith")
print(son.name)
son.print_cartoon('DuckTales')
```

Python also supports **polymorphism**, which means it doesn't need to overload methods in order to pass different typed parameters.

In OOP, **abstraction** refers to the idea of *abstracting* an object into a blueprint. If we wanted to create a Person object, we would try to generalize what properties a person generally has (name, eye-color, etc.) and then build our blueprint around accepting a variety of properties.

In OOP, **encapsulation** means we don't expose internal data to outside influence. For example, we should scope data so it can't be accessed.

**Composition**, though not strictly part of the four pillars of OOP, is the concept of "has a" relationships. For example, if we have a class of Dog and a class of Person, we could pass Person("Mick Jagger") to dog through a param, tethering it together without causing immutability: `dog = Dog('Stanley', 'Pitbull', mick)` where `mick` is our instanced person.

### Chapter 14: More Object-oriented Programming

Python uses automatic garbage collection (not noted in the book), however it's important to understand how the concept of pointers work.

Variables "point" to an object, e.g. `number = 100` is a variable, `number` pointing to the integer object `100`. When `number` is reassigned, `100` is destroyed in data if it isn't been assigned to an additional variable.

Python differs from JavaScript in that all objects work like arrays *in the sense that they point to the original object*. If you create `x = 10` and `y = x`, mutating `x` will expose `y` to the same changes **because `y` is pointing to the integer object, not the value of `x`**. `x+=1` will cause `print(y)` to output 10, not 11, because `y` points to the object '10' while x is now pointing to the object '11'.

The keyword `is` can be used to check if two objects are the same object. `x is y` will return True or False.

`none` represents the absense of a value, the same as JavaScript's `null`. It can be used to set a variable, and is different than an undefined variable (NameError).

Just to note, classes are objects (because Python is an object-based language, just like JS).

**Classes** gift their variables to their instances, they're not pointers. If you change either the class variable or the instance's instanced variable, it will not chance the original or the gifted variable.

Knowing this, it means instances can **override** their parent methods and variables.

Python **does not have private variables**, but it's resolved by using convention. Giving a variable or method an underscore indicates it *shouldn't* be used outside of the object. This is still unsafe accessable data, whereas in a language like C#, this data is *protected* and **only** accessable by code inside the object itself. That's not mentioned in the book, but it really should be. This creates potential security flaws for systems that require data security, like banks.

Python supports the `super` function, which allows you to pass data to a parent class's functions. This grants the ability for sub-classes to have the original function with additional functionality.

``` py
class Mammal:
    hp = 100
    def myFunc (param):
        hp -= param

class Tiger(Mammal):
    def tigFunc (param):
        print("Printing!")
        super ().myFunc(20)

>>>myTiger = Tiger()
>>>myTiger.tigFunc(20)
"Printing!"
>>>myTiger.hp
80
>>>myTiger.myFunc(20)
>>>myTiger.hp
60
```

Like `__init__`, `__repr__` adds additional structure to our classes. By passing a return into `__repr__` we can call the object and have it change the default call value when we type `myInstancedObject`, which would normally print out object data in the terminal.

``` py
def __repr__ (self):
    return self.name '''or whatever'''
```

### Chapter 15: Bringing It All Together

This chapter built a couple of card games, nothing noteworthy of writing.

### Chapter 16: Practice

This chapter mentioned a couple of exercises.

1. Build an OOP Blackjack.
2. Build a web scraper.
3. Find a Python project on pip and use it in a program.

## Part III: Introduction to Programming Tools

### Chapter 17: Bash

Lots of light notes on the bash CLI and a subsection on Vim. Not really worth making notes over because I intend to read an entirely different book on vi and Vim. Did note `less file.txt` to read files in the terminal, easier than `cat`.

There was also mention of script, `$PATH` and pipes `|`.

### Chapter 18: Regular Expressions

A brief introduction to `grep` and regular expressions. Didn't learn a lot of new information, but in grep, character ranges are done with [[:alpha:]] and grep can pipe results into another grep.

To use regular expressions in Python, you need to call `import re`. It's enclosed in quotes, rather than in `//` like JavaScript.

Overall, RegEx in Python and Grep follow similar standards as other languages.

### Chapter 19: Package Managers

There's a quick introduction to `apt-get` and `Homebrew` which function for Linux and Macs, respectively. Not listed, but `choco` is similar on Windows if installed; Windows 10 does offer `OneGet`, but no one seems to like it at this time.

Python features `pip` which works very similarly to NodeJS's `npm`. Pip is included with Python and can be invoked via `pip <command> [options]`, where commands are install and download. You can specify the packages you want by tagging them with `==`, or just omit the version call which will download the most recent version. You may need to invoke `sudo` on linux.

`sudo pip install Flask==0.10.1` would install v0.10.1 of Flask.

Installed packages are stored in a folder called `../site-packages` which exists in the Python path; when you `import` in python, it looks in this folder for dependancies.

Flask could then be used as `from flask import Flask` to set the `Flask` variable for use.

Packages you've installed can be viewed with `pip freeze`, and can be written into a file with `pip freeze > mytext.txt`. Uninstalling packages can be done with `pip uninstall [package]`.

### Chapter 20: Version Control

Fundamental discussion on GitHub repositories and `git`. `SVN` is briefly mentioned, but not covered. Basic functionality of version control (`add`, `pull`, `commit`, `push`) is covered, but nothing noteworthy.

### Chapter 21: SQLite

Basic discussion of databases (NoSQL vs SQL is briefly mentioned). The author mentioned investing time into NoSQL; if anyone's reading this, MongoDB is worth looking at.

SQLite is a lightweight database using SQL. The author says `sqlite` is already available in the CLI, but that's a lie. [The latest version of SQLite can be downloaded here](https://www.sqlite.org/download.html), but needs to be installed via the Windows path command. I'm lazy, so [here's SQLite online](https://sqliteonline.com/).

I couldn't get this section to play nicely with either the installed SQLite3 nor the emulator online, so I just passed by it. I intend to review SQL elsewhere and this brief overview doesn't seem necessary to the next section.

### Chapter 22: Bringing it All Together

This section discusses creating a webscraper. There's a light primer on HTML and a discussion on using `beautifulsoup` for parsing HTML from Google News. I'll complete the project on the side - no noteworthy content.

### Chapter 23: Practice

Almost no content in this chapter, the exercises listed are as follows.

1. Build a scraper for another side (not Google News).
2. Write a program and checkout an old version (use git).
3. Download pylint with pip, read the documentation and try it out.

## Part IV: Introduction to Computer Science

### Chapter 24: Data Structures & Algorithms

Light discussion on algorithms, time complexity, and modulo; various algorithms are given samples.

* **Bubble Sort** - Not very effective, but good for understanding sort algorithms.
* **Sequential Search** _O(n)_ - Going through each item one-by-one until a match is found.
* **Binary Search** _O(log(n))_ - Dividing remaining positions by half each time until a match is found.
* **Recursion** - Recursive algorithms follow three laws of recursion: they have a **base case**, they change the state and move toward the base case, it calls itself recursively.

Note, a **base case** is what stops the algorithm from running. There's a lot of side notes about recursive algorithms here, but I already understand the gist and I'm far too lazy to take more notes where they're not needed. 👌

**Abstract data types** can be thought of like classes to objects. Abstraction of data is the "idea" of a certain type of data structure. A list, for example, is an abstraction that can be implemented in ways like an array or linked list.

**Nodes** can be thought of as a point on a graph, and are used in linked lists, trees, and graphs.

**Stacks** is a last-in-first-out data structure, best thought of like a stack of dishes - to get the dish on the bottom, you have to remove any dish on top. Stacks are great for recursion and reversing things.

**Linked lists** are made of a series of nodes where each node points to the next node in the list. In a **singly linked list**, all nodes know bout the node ahead of them, but don't keep track of the previous node. A **doubly linked list** is the same concept, except it additionally keeps track of the node behind it. Singly linked lists can be navigated by opening the next node until there is no next node; doubly linked lists can keep track of their previous node by setting it to memory.

An array must have all of the same data types; Python's list data structure is built internally in C as an array of pointers.

A *tree** is a data structure that could best be thought of as a tree. The file system on a computer is an example. **Binary trees** are made of nodes containing data, and can house a left and right child node. Child nodes keep track of their parents.

Navigation of a binary tree can be done using the *breadth first search* and *depth first search* algorithms. Thinking of trees as a table, a breadth first search will navigate each row one by one, while a depth first search will navigate by column.

**Hash tables** are instances store via a hash function, which will return or process a hashed line to instantly retrieve data. Python's dictionary object is built around hash tables. The book poorly explains this concept though, and I feel like I need to pull external sources to help better understand this concept.

### Chapter 25: Relational Database Design

### Chapter 26: Computer Architecture

### Chapter 27: Network Programming

### Chapter 28: Bringing It All Together

### Chapter 29: Practice

## Part V: Programming for Production

### Chapter 30: Testing

Development processes can be thought of as a way of "splitting software development into distinct phases containing activities with the intent of better planning and management." The **Waterfall** model is linear design pattern that is made of five phases.

1. Planning and Requirements Analysis
2. Defining Requirements
3. System Design
4. Implementation and Deployment
5. System Testing and System Maintenance.

**Phase 1** is about carefully planning around the problem you need to resolve. What are your requirements, what do you need to complete the task? TL;DR: Brainstorming.

**Phase 2** is about defining and documenting requirements.

**Phase 3** is about discussing different design approaches and outlining a development process in a document called *Design Document Specifications*. This stage discusses the architectual design of the project (modules, implementation, etc.).

**Phase 4** is about building the product based on the DDS.

**Phase 5** is the final phase where the product is tested and put into production.

#### On Testing

**Assertions** are statements programmers expect to be True, and throw exceptions if they are False. Python uses the `assert` keyword. If the `assert` keyword returns false, an AssertionError is thrown.

Testing is usually done in four phases.

1. Unit Testing
2. Integration Testing
3. System Testing
4. Acceptance Testing

**1: Unit Testing** is the act of creatining individual tests that will test against one aspect in a piece of code with an assertion. Unit tests tackle code by pieces, such as function, and run through a general use-case for all functions, classes, and methods. This means testing against things you aren't expecting (like passing an int where a string is being called), and testing boundary conditions (what happens when a list gets too full).

Unit testing is usually done within a unit testing framework; in JavaScript's case, I chose to use Jest for this aspect. Python has a built-in unit testing framework called `unittest` which comes with various assertion methods.

**2: Integration testing** follows unit testing - it's the act of ensuring modules function together as expected. In banking, you might check transfer modules against balance modules to ensure each module is passing data correctly.

**3: System testing** follows integration testing, where the application is tested against system limitations. GUI issues, heavy workloads, etc. A good example would be beta releases or throwing a small number of early access users at a server.

**4: Acceptance testing** is the final stage of testing, which checks to make sure the project meets the agreements of the stakeholders. It's got almost nothing to do with programming, but it's still an important process in development.

In addition to the testing workflow, there's also the theory of **Test Driven Development**, or TDD. TDD is a development technique that requires the programmer to write unit tests *before writing their programs.* This enforces the idea that you can't avoid unit testing, and forces you to think about your design requirements before starting to code.

*There's a large section here about unit testing in Python that I don't feel is worth taking notes on, but will be practice in a code along.*

**Writing good tests** means tests are **repeatable across any environment**. OS X should work on Windows without having to make any changes; an example of violation would be hard-coded directory paths (Windows and OS X use different pathing systems). Tests that can not be processed on multiple platforms need to be rewritten. They should also be **fast**, **run often** and **should not affect one another**.

**Code coverage** is the percentage of code covered by testing. While it doesn't measure efficiency, it's useful for finding untested parts of code. This is generally expected to be at or above 80%.

The idea behind testing while you build is to save yourself time from having to run a full program half a million times just to test various inputs. Note to self: you know what you did; stop doing that and write test codes.

### Chapter 31: Best Programming Practices

### Chapter 32: Bringing It All Together

## Part VI: Land a Job

### Chapter 33: Your First Programming Job

This chapter houses some typical information about the difference of front and back-end programming, as well as advice for getting started. Doing basic programming work for someone you know on Upwork is a good start, as is contributing to open source projects on GitHub.

Interviews are discussed a bit; focus is put on LinkedIn and networking with recruiters. Start connecting with recruiters and talk to them about open positions - you don't always need to *search* for positions! Networking has benefits too. **Talk to recruiters!**

Typical processes with recruitment start with a non-technical formal interview with the recruiter, then a technical phone screen with one or more members of the entineering team. Typically if they can't white board you in person, they'll send you to a link where you can edit code and ask you to solve a problem.

There may be a third round of interviewing where you meet-and-greet the team, possibly have lunch, and talk about your technical skills. You may be further challenged.

Interviews are typically focused on two sections: **data structures** and **algorithms**. LeetCode is mentioned as a platform for practicing.

### Chapter 34: Working on a Team

General information about working on a team: master the basics and don't constantly ask your coworkers things you can google. It's important to "tread lightly" around another programmer's code and don't spend a ton of time fixing someone else's code if it works. The best way to feel around this subject is to ask the company about their "engineering culture". If you think you're a better fit with another company, seek them out and leave the one you're in.

[Improve Code Without Anyone Hating You](https://medium.com/@mscccc/jr-developers-5-how-to-improve-code-without-anyone-hating-you-34a7218b387f) was a recommended article in this section.

Everyone experiences imposter syndrome; don't feel overwhelmed. Stay humble, admit when you don't know something, and try to learn it.

Other than that, continue learning; these resources are recommended (in addition to [Hacker News](https://news.ycombinator.com/)).

* The Progmatic Programmer
* Design Patterns
* Code Complete
* Compilers: Principles, Techniques, and Tools
* Introduction to Algorithms
* Problem Solving with Data Structures and Algorithms