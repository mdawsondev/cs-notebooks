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

_Saved._