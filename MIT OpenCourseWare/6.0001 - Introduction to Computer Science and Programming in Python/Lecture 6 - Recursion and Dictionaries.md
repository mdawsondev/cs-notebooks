# Lecture 6 - Recursion and Dictionaries

## Recursion

Recursion is a way to design solutions to problems by divide-and-conquer or decrease-and-conquer. We reduce a problem to simpler versions of the same problem. In programming, this is when a function calls itself. The goal is to **not** have infinite recursion. This means we must have 1 more more base cases and we must salve the same problem on some other input with the goal of simplifying the larger problem input.

A **base case** is used to ensure recusion stops.

### Multiplication Samples

Typical multiplication expanded into an iterative function:

```py
def mult_iter(a, b):
    result = 0
    while b > 0:
        result += a
        b -= 1
    return result
```

Recursion takes this idea and turns it into a simpler version of the same problem. Our base case is that we keep reducing the problem until we reach a simple case that can be solved directly: _when b = 1, a*b = a_.

```py
a*b = a + a + ... + a  #b times
    = a + (a + ... + a) #b-1 times
    = a + a * (b-1)
```

Same functions turned into recursion:

```py
def mult(a, b):
    if b == 1:
        return a
    else
        return a + mult(a, b-1)
```

Breaking a factorial into recursion, finding the base case of `n == 1` (below) will "unwind" the input until it reaches the base case, then it will return to each scope that dipped into the recursion. Large recursions (i.e. 400!) would have just as many returns.

```py
# n! = n * (n-1) * (n-2) * (n-3) * ... * 1

def fact(a, b):
    if n == 1:
        return 1
    else:
        return n*fact(n-1)
```

Testing recursion should return truthy to the base case by testing _0 or 1_ and any other much different input. I.e. run test cases.

Resursion can be thought of like the tower-stacking riddle, where you know that if you can move the largest ring by itself and then **all other rings at the same time** representing `n` and `n-1`, then you should be able to move them individually.

```py
def printMove(fr, to):
    print('move from ' + str(fr) + ' to ' + str(to))

def towers(n, fr, to, spare):
    if n== 1:
        printMove(fr, to)
    else:
        towers(n-1, fr, spare, to)
        towers(1, fr, to, spare)
        towers(n-1, spare, to, fr)
```

### Recursion with Multiple Base Cases

Teacher discusses converting the Fibonacci rabbit problem to recusion. After one month, _0_, we have one female. Second month, one female now pregnant. Third month, two females, one pregnant, one not.

In general, `females(n) = females(n-1) + females(n-2)`; this means there are two recusive calls.

| Month | Females |
|-------|---------|
|   0   |    1    |
|   1   |    1    |
|   2   |    2    |
|   3   |    3    |
|   4   |    5    |
|   5   |    8    |

### Recursion on Non-Numerics

Thinking about strings for palindrome solutions can be solved recursively. We adjust our base case to return a length of 0 or 1 (being a palindrome). Recursively, if the first character matches the last character, then it is a palendrome if the middle section is a palendrome.

```py
def isPalendrome(s):

    def toChars (s):
        s = s.lower()
        ans = ''
        for c in s:
            if c in 'abcdefghijklmnopqrstuvwxyz':
                ans = ans + c
        return ans

    def isPal(s):
        if len(s) <= 1:
            return True
        else:
            return s[0] == s[-1] and isPal(s[1:-1])

return isPal(toChars(s))
```

## Dictionaries

Dictionaries are key/value pairs. They're the same as JavaScript objects. 👌 Just a small note to show use of keys/values. Keys (immutable), values (mutable).

``` py
def lyric_to_frequencies(lyrics):
    myDict = {}
    for word in lyric:
        if word in myDict:
            myDict[word] += 1
        else:
            myDict[word] = 1
    return myDict
```

Making Fibonacci a dictionary call:

``` py
def fib_efficient(n, d):
    if n in d:
        return d[n]
    else:
        ans = fib_efficient(n-1, d) + fib_efficient(n-2, d)
        d[n] = ans
        return ans

d = {1:1, 2:2}
print(fib_efficient(6, d))
```