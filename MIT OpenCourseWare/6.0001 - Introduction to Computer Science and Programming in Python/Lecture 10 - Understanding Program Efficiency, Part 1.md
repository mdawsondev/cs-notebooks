# Lesson 10 - Understanding Program Efficiency, Part 1

_This lecture covers the concepts of complexity._

## Overview of Efficiency

We want to understand the efficiency of programs for two main reasons:

* How can we reason about an algorithm in order to predict the amount of time it will need to solve a problem of a particular size?
* How can we relate choices in algorithm design to the time complexity of the resulting algorithm?
  * Are there fundamental limits on the amount of time we will need?

The reason we want to ensure we can compensate for large quantities of data is because data sets are **constantly growing larger** as time moves forward. If our algorithm can not compensate for these changes, then our code will become worthless.

Efficiency is broken into two sections:

* **Time**: How much time an algorithm takes to process `n` data.
* **Space**: How much storage is required to compute output.

## Time Complexity

Meauring complexity can be calculated in three ways, though the first case is more flawed than the second, and the second case is more flawed than the third (most appropriate) way.

1. Time it. ❌
2. Count operations. ❌
3. Abstract notion of order of growth. ✔

### Timing a Program

Using Python's time module, we could import the time and start a clock, then stop the clock to measure how much time has passed. This can be done over a large number of inputs and come up with a sense of how much time an algorithm takes. The problem with using this method is that by adding or removing a couple of lines of commands, this needlessly considers the implementation of influence of time with the algorithmic influence of time. Worse than that, timing varies between computers - not all computers measure the same rates. Furthermore, time is not predictable based on small inputs; these values may change on large inputs.

``` py
import time

def c_to_f(c):
    return c*9/5 + 32

t0 = time.clocl()
c_to_f(100000)
t1 = time.clock() - t0
Print("t = ", t, ":", t1, "s,")
```

### Counting Operations

We can abstract timing a function by making the assumption that our computer handles things automatically (math, comparisons, assignments, accessing objects in memory). We assume that all of these primitive operations take about the same time in a machine; we then count the number of operations executed as function of size of input. This allows us to say that the machine in question doesn't matter; we explain how long an algorithm takes by the number of steps required. By counting our operations and pushing them into an equation, we can then calculate the output of operations based on the input of `x`, for example in the fllowing code if we ran input of 100, we could calculate 3(100)+2, or 302.

This is better than timing in that it changes based on the algorithm and is independant of the computer running the algorithm, however, it still relies on the implementation of code (`for` vs `while` have different number of operations) and has no clear definition of which operations to count.

```py
def c_to_f(c):
    return c*9.0/5 + 32 # 3 ops

def mysum(x):
    total = 0 # 1 op
    for i in range(x+1): # 1 op and loop x times
        total += i # 2 ops
    return total # 1 op

# Putting this together, mysum -> 3x+2 operations.
```

### Order of Growth

In order of growth we still count operations, but we ignore small variations and we focus on what happens when the size gets massive. We first need to understand what we are computing as the size of our problem; for example an input of an integer would change based on how large the integer grows, while if we're working with a list the size of the list would change. If a function takes **more than one argument**, we choose the parameter that is the most important part of the function.

When we calculate the complexity of time, we want to focus on the upper bound of the amount of time an algorithm can take. In the following example, a best case would have the element in the first position of a list, while worst case would yeild the element not in a list and iteration of the entire list. This longer complexity binds the cap of our time.

``` py
def search_for_elmt(L, e):
    for i in L:
        if i == e:
            return True
    return False
```

Given a list of `L` of some length `len(L)`:

* Best case: minimum running time over all possible inputs of a given size, `len(L)`
  * Constant for `search_for_elmt`.
  * First element in any list.

* Average case: average running time over all possible inputs of a given size, `len(L)`
  * Practical measure.

* **Worst case**: maximum running time over all possible inputs of a given size, `len(L)`
  * Linear in length of list for `search_for_elmt`.
  * Must search entire list and not find it.

## Big-O Notation

**Big-O** `O()` Notation describes the time-complexity of the worst-case for an algorithm.

In the following example, we will being by counting steps and compare that to `O()`. The calculation results in `5n+2` steps; we could have run our while loop differently causing a `6n+2` step count. The only thing we want to concern ourselves with is what changes to cause the most difference in time complexity, and in Big-O, this results in `O(n)`, where `n` is the variable of complexity. The reason we drop `5` and `2` are because **these variables do not matter for large growth**, when `n` is multiplied by x-factor, the time complexity grows linearly. We always ignore additive and multiplicative constants.

```py
def fact_iter(n):
    """assumes n an int >= 0"""
    answer = 1 # 1
    while n > 1: # n & 1
        answer *= n # 2
        n -= 1 # 2
    return answer # 1

# This suggests our steps are 1 + 5n + 1, or 5n + 2.
```

Regardless of our algorithm, we always focus on the **dominant terms**.

* `n^2 + 2n + 2` = `O(n^2)`
* `n^2 + 1000000n + 3^1000` = `O(n^2)`
* `log(n) + n + 4` = `O(n)`
* `0.0001*n*log(n) + 300n` = `O(n log n)`
* `2n^30 + 3^n` = `O(3^n)`

### Analyzing Program Complexity

* **Combine** complexity classes.
  * Analyze satements inside functions.
  * Apply some rules, focus on dominant terms.

### Law of Addition

* Used with **sequential** statements.
* `O(f(n)) + O(g(n))` is `O(f(n) + g(n))`.

For example, in the following algorithm we can say `O(n) + O(n*n)` = `O(n+n^2)` = `O(n^2)` becase of dominant term.

``` py
for i in range(n): # O(n)
    print('a')
for j in range(n*n): # O(n*n)
    print('b')
```

### Law of Multiplication

With nested statements, we figure out the complexity of the inner part and the order of the outer part, then multiply the two to find out complexity. _Aside: Nested loops typically have quadratic behavior._

* Used with **nested** statements.
* `O(f(n)) * O(g(n))` is `O(f(n) * g(n))`

For example, in the following algorithm we can say `O(n) * O(n)` = `O(n*n)` = `O(n^2)` because the outer loop goes `n` times and the inner loop goes `n` times for each outer loop iteration.

``` py
for i in range(n): # O(n)
    for j in range(n): # O(n)
        print('a')
```

## Complexity Classes

The following list orders complexity by rank of best to worst; `n` as input and `c` as constant.

* `O(1)`: **Constant**
* `O(log n)`: **Logarithmic**
* `O(n)`: **Linear**:
* `O(n log n)`: **Log-Linear**
* `O(n^c)`: **Polynomial** - These are bad!
* `O(c^n)`: **Exponential** - These are really bad!

### Linear Search on Unsorted List

The worst case here would look through every element to decide what we're looking for isn't in the list. We know that this search is **linear** because it loops `n` times through the list, causing this to be the most important operation in the complexity; `O(n)`. We could consider returning our value of true immediately which would increase the _average_ time, but this doesn't change the worst case behavior (which is the key detail).

It's important to note that Python can calulate list-access as a constant time; not all languages do this and it must be taken into consideration.

```py
def linear_search(L, e):
    found = False
    for i in range(len(L)):
        if e == L[i]:
            found = True
    return found
```

### Linear Search on Sorted List

In this situation, we must only look until we reach a number greater than `e`. We know the list is sorted, so we can calculate our worst complexity as `O(len(L))` as the loop times `O(1)` to test if `e == L[i]`. The overall complexity is then calculated to be `O(n)`, where n is `len(L)`.

For **linear search**, the order of growth is the same, though the run time may differ for two search methods. This is because for our worst case, we must still go through the entire list.

```py
def search(L, e):
    for i in range(len(L)):
        if L[i] == e:
            return True
        if L[i] > e:
            return False
    return False
```

#### Linear Complexity Review

* Searching a list in a sequence to see if an element is present.
* Add characters of a string, assumed to be composed of decimals.
* Complexity often depends on number of iterations.
* **Standard loops are typically linear.**

### Quadratic Complexity

This would typically be looping through a loop, i.e. **nested loops**. In the following example, we consider our worse case of where L1 and L2 are of the same length and the element isn't in either list. This would cause the loop to check every position; multiplying `O(n)` with `O(n)` returns `O(n^2)`.

```py
def isSubset(L1, L2):
    for e1 in L1: # O(len(L1)) or O(n)
        matched = False
        for e2 in L2: # O(len(L2)) or O(n)
            if e1 == e2:
                matched = True
                break
        if not matched:
            return False
    return True
```

``` py
def intersect(L1, L2):
    tmp = []
    for e1 in L1: # O(n) Quadratic Loop
        for e2 in L2: # O(n)
            if e1 == e2:
                tmp.append(e1)
    res = []
    for e in tmp: # O(n) Quadratic Loop
        if not(e in res): # O(n)
            res.append(e)
    return res
```
