# Lecture 3 - String Manipulation, Guess and Check, Approximations, Bisection

## More on Strings
* Strings can be thought of as a sequence of case-sensitive characters.
* Can compare with `==`, `>`, etc.
* `len()` is a function used to retrieve length of strings.
* Square brackets `[]` perform indexing into a string to return the value at a certain index. Indexing begins at 0.
* Strings can be pulled apart (slice) using `[start:stop:step]`.
* Strings can be iterated using `[start:stop], step=1`.
* Parameters can be omitted leaing just colons.

Length
``` py
s = 'abc'

>>>len(s)
3

>>>len('efghij')
6
```
Index
``` py
s = 'abc'

>>>s[0]
"a"
>>>s[1]
"b"
>>>s[2]
"c"
>>>s[3]
error
>>>s[-1]
"c"
>>>s[-2]
"b"
>>>s[-3]
"a"
```

Slicing
``` py
s = 'abcdefgh'
>>>s[3:6] '''same as s[3:6:1]'''
"def"
>>>s[3:6:2]
"df"
>>>s[::] '''same as s[0:len(s):1]'''
"abcdefgh"
>>>s[::-1] '''same as s[-1:-len(s)+1:-1]'''
"hgfedcba"
>>>s[4:1:2]
"ec"
```

Strings are immutable and cannot be modified.

``` py
s = 'hello'
s[0] = 'y' '''error'''
s = 'y'+s[1:len(s)] '''allowed with s bound to new object'''
```

Strings can be interated in a loop.

``` py
for char in s:
    if char == 'i' or char == 'u':
    print('There\'s an i or u.')
```

## Algorithm Samples

**Guess-and-Check Cube Root**

``` py
cube = 8
for guess in range(cube+1):
    if guess**3 >= cube:
        break
if guess**3 != abs(cube)
    print(cube, 'is not a perfect cube')
else:
    if cube < 0:
    guess = -guess
print('Cube root of ' + str(cube) + ' is ' + str(guess))
```

**Approximate Solution Cube Root**

* "Good enough" solution.
* Start with a guess and increment by a small value.

``` py
cube = 27
epsilon = 0.01
guess = 0.0
increment = 0.0001
num_guesses = 0
while abs(guess**3 - cube) >= epsilon and guess <= cube:
    guess += increment
    num_guesses += 1
print('num_guesses =', num_guesses)
if abs(guess**3 - cube) >= epsilon:
    print('Failed on cube root of', cube)
else:
    print(guess, 'is close to the cube root of', cube)
```

**Bisection Search**

* Half-interval searches per guess. (0-100, guessing 50).
* New guess is the half of the remaining numbers based on higher or lower.
* Time compleity is O(log n)

```py
cube = 27
epsilon = 0.01
num_guesses = 0
low = 0
high = cube
guess = (high + low)/2.0
while abs(guess**3 - cube) >= epsilon:
    if guess**3 < cube:
        low = guess
    else:
        high = guess
    guess = (high + low)/2.0
    num_guesses += 1
print 'num_guesses =', num_guesses
print guess, 'is close to the cube root of', cube
```