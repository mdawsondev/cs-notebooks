# Lesson 7 - Testing, Debugging, Exceptions, and Assertions

## Approaching Bugs

The best way to approach bugs is to start before you even code. Make sure you keep the idea of modularization in your programs, and document as you go along. When an error arises, you can quickly find where it was sourced. This is called **defensive programming**.

### Testing

Testing is meant to prevent bugs by coming up with inputs and having it output expected results. You begin testing as soon as your program can run - this ensures you eliminate syntax and semantic errors before worrying about breaking the program with unusual actions.

* Make sure program can run.
* Come up with pairs of test cases: pairs of input and expected output.

### Classes of Testing

1. **Unit Testing** - Ensures each function runs according to specifications.
2. **Regression Testing** - Come up with test cases for uncovered bugs and run it through all of your unit tests again to catch reintroduced errors.
3. **Integration Testing** - Running your program as a whole; making sure all of your different pieces work together as expected.

The idea is that you build and test as you're building (TDD), ensuring each piece does what it's expected to, and then put everything together in the end like legos to make sure it all works.

### Testing Approaches

Variables should span a range of possibilities for testing; do standardized tests (expected reasonable input) then extreme testing where inputs are extremely large or small.

* **Random Testing** - What it sounds like, come on. 🤔
* **Set Boundaries** - Come up with intuitive expectations for your code and establish natural boundaries. For example, with two numbers you would expect both inputs to be an `int` type and could potentially set a boundary between a designated range, _0-100_.
* **Black Box Testing** - All you look at is the docstring and come up with test cases based on that. It should be designed without looking at the code. It can be done by someone other than the implementer to avoid biases and can be reused if implementation changes.
* **Glass Box Testing** - You have the code and try to hit all the available paths in the code. Having a test that goes through every single path of code is known as _path complete_. This can be problematic for loops.
  * Branches should exercise all parts of a conditional.
  * For loops should test for not entered, executed exactly once, and executed more than once.
  * While loops are the same as for loops; cases that catch all ways to exit loop. 

## Debugging

There are various ways to debug - print statements, stepping through code, monitoring variables. There are also other ways to quickly track down bugs, such as the bisection method.

The _bisection method_ can be used by placing a print statement about half-way through your code and monitoring variables to ensure that you output what's expected by that point. If you output the expectations, then you can discard the previous section and bisect the remaining code with the same technique.

### Debugging Steps

* Study the program code: Don't ask what's wrong - test cases would have figured out what's wrong.
* Scientific method: Study available data, form a hypothesis, create repeatable experiments and pick simple input to test with.

### Handling DB Errors

Most errors explain themselves via title (SyntaxError, NameError, TypeError, etc.), but LogicErrors will tend to be the most painful to correct.

There's a type of strategy called **Rubber Ducky Debugging** where the programmer literally explains their code to a rubber ducky (or to someone/something who doesn't understand anything). This forces you to explain things extremely carefully. 

### Summary of Dos and Don'ts

Don't:

* Write entire program.
* Test entire program.
* Debug entire program.
* Change code without backing up.
* Rely on memory alone for bugs.

Do:

* Unit testing.
* Write one function at a time.
* Test the fucntion, debug the function.
* Repeat until you have the lego pieces.
* Follow with integration testing.
* Backup code before changes.
* Write down or document potential/existing bugs.
* Compare new version with old version after testing.

## Errors

Errors are known as exceptions because they're considered exceptions to what the program was expecting.

* SyntaxError - Can't parse program.
* NameError - Local/global name not found.
* AttributeError - Attribute reference fails.
* TypeError - Operand doesn't have correct type.
* ValueError - Operand type is okay but value is illegal.
* IOError - IO system reports malfunction (e.g. file not found).

### Handling Exceptions

You can handle expections where you think you might get an error. A good example of this is user input; users are great at breaking things.

The way to manage this potential mis-input is to push code that might cause an error into a `try` block, and to throw an `exception` when the try condition fails. In JS this is `try` and `throw`/`catch`.

The exception will catch any type of error that pops up. You can control various errors by catching the type of error.

```py
try:
    a = int(input("Number: "))
    b = int(input("Another number: "))
    print("a/b= ", a/b)
    print("a+b= ", a+b)
except ValueError:
    print("Could not convert to a number.")
except ZeroDivisionError:
    print("Can't divide by zero.")
except:
    print("Something else went wrong.")
```

Other exceptions include `else`, where this is run if try completes with no exceptions, and `finally` where this code is always executed after try, else, and except calauses no matter what.

### What to do with Exceptions

* **Fail Silently**: substitute default values or just continue. This is considered a bad idea because the user has no warning.
* **Return an "error" value'**: will supplement the error with an error-type value (0, -1). Not a good idea either because it has to be controled with conditionals.
* **Stop execution, signal error condition**: This is raising an exception with a descriptive string.

You could also supply a default value as long as the user is made aware of the condition. This should be noted in the docstrings.

As control flow:

Don't return special values when an error occured and then check whether "error value" was returned. Instead, raise an exception when unable to produce a result consistant with function's specification.

`raise <exceptionName>(<arguments>)`
`raise ValueError("Something is wrong.")`

Try to make sure you account for all possible situations where data might not be the expected value. Example, an array of students and grades, but the student doesn't show up for one test and the input field is blank.

## Assertions

Assert statements assure that the computation on functions are exactly what they're expected to be. Assertions are great to ensure pre and post-conditions are correct. As soon as a function becomes false, it will terminate with an AssertionError. This is good because it prevents populating a program with bad values.

```py
def avg(grades):
    assert not len(grades) == 0, 'no grades data'
    return sum(grades)/len(grades)
    # This will raise an AssertionError, otherwise runs okay.
```

### Where to Use Assertions

* Use as a supplement to testing.
* Raise exceptions if users supply bad data.
* Check types of arguments or values.
* Check that invariants on data is met.
* Check constraints on return values.
* Check for violations of constraints (ex. no duplicates).