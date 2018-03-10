# Lesson 1: What is Computation?

> In this lecture, Dr. Bell introduces the theory of computation and explains some aspects of computational thinking. Programming languages are discussed, with an emphasis on basic Python syntax and data structures.

## Computers

### What Does a Computer Do

* Performs calculations and remembers results.
* Calculates low-level language, as well as defined languages.
* Computers only do what you tell them to do.

### Types of Knowledge

* Declarative knowledge: statement of fact.
* Imperative knowledge: a recipe.

### Types of Computers

* Fixed program computers: ex. calculator.
* Stored program computers: modern computers.

### Basic Machine Architecture

* Input
  * Initiates process.
* Memory
  * Contains data.
  * Contains instructions.
* Control Unit
  * A sequential counter.
  * Takes instructions and sends to ALU.
* Arithmetic Logic Unit
  1. Pulls data.
  2. Commits primitive operations and tests.
  3. Returns data.
  4. Increases or resets CU counter.
* Output
  * Returns upon completion.

## Programs

### Algorithms

1. A sequence of simple steps.
2. Flow of controll process that specifies when each step is executed.
3. A means to determining when to stop.

### Primitives

* Anything can be computed with **6** primitives.
  1. Move Left
  2. Move Right
  3. Read
  4. Write
  5. Scan
  6. Do Nothing
* Modern programming languages have more convenient primitives.
* Can abstract methods into new primitives.

If you can computer something in one language, in theory, you can computer the program in any other language.

### Creating Recipes
* Programming languages provide primitives.
* Combine primitives into complex combinations called expressions.
* Expressions and computations have values and  meaning in programming.

*Syntax* is a grammatically correct expression.
*Semantics* are valid phrases with meaning.

Computers only have valid or invalid semantics - they don't make assumptions, they do what they're told or output an error.

### Errors
* Syntactic: Common, easily caught.
* Static Semantic: Can cause unpredictable behavior; some languages check for this.
* No syntactic or semantic errors but different behavior than expected (crash, infinite loop, wrong answer).

*Programs* are the sequence of definitions and commands executed.
*Commands* are statements made to the interpreter.

## Python

### Objects

* Programs manipulate data objects.
* Objects have a type that defines the kind of things programs can do to them.
* Scalar - can't be subdivided, ex: `5`.
* Non-scalar - have internal structures that can be accessed, made of partse. Ex: array of numbers `1, 2, 3, 4, 5`.

``` Psuedocode
Type: Human
Actions: Walk, talk, etc.

Type: Wookie
Actions: Walk, roar, etc.
```

### Scalar Objects

* **int** - Integers
* **float** - Real Numbers
* **bool** - True/False
* **NoneType** - None

`type(param)` exposes the type of an object.

```Python
>>>type(3.0)
float
```

Type conversion (**cast**) can be used to convert object of one type to another.

`float(3)` converts int to float, `int(3.9)` converts float to int.

`print` can be used to output to the terminal/console.

```Python
>>>3+2 '''Does not print outside of the terminal.'''
5

>>>print(3+2) '''Prints to the terminal from scripts.'''
5
```

### Operators on ints and floats

* `i+j` = sum
* `i-j` = difference
* `i*j` = product
* `i/j` = division (always float)
* `i%j` = modulo (remainder)
* `i**j` i to power of j

### Variables

* Equal sign is an assignment of a value to variable name.
* Assignment is known as *bind*.
* Right-hand side is always an *expression* or *value*.
* Left-hand side is always a *variable*.
* Variables can be re-bound with new assignments.
* Values may be stored in memory but lose their name.
* Value does not change until you recalculate or reassign.

```pi = 3.14159
pi_approx = 22/7
radius = 2.2
area = pi*(radius**2)

>>>pi
3.14159

>>>pi_approx
3.142857142857143

>>>area
15.205295600000001
```

