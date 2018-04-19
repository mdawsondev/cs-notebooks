# Lesson 11 - Understanding Program Efficiency, Part 2

## Expansion on Concepts

### Constant Complexity

Constant Complexity O(1) is independant of inputs; typically there are few interesting algorithms in this class. It can have loops or recursion **only if** the number of iterations is independant of the size of input.

### Logarithmic Complexity

Logarithmic Complexity O(log(n)) grows logarithmically with the size of input. Examples include **Binary Search**, and **Bisection Search**.

#### Bisectional Search Sample

1. Pick an index, `i`, that divides list in half.
2. Ask if `L[i] == e`.
3. If not, ask if L[i] is larger or smaller than `e`.
4. Depending on answer, search left or right half of `L` for `e`.

Using this theory, we break our problem into smaller versions of the problem and include simple operations. Answer to the smaller question is the answer to the original problem.

##### Bisection Search 1

It's important to keep in mind that complexity can be misleading. Due to the way Python copies lists when dividing them, this creates a real complexity of O(n) which dominates the complexity of the O(log(n)) complexity.

``` py
def bisect_search1(L, e):
    if L == []:
        return False
    elif len(L) == 1:
        return L[0] == e
    else:
        half = len(L)//2
        if L[half] > 3:
            return bisect_search1(L[:half], e)
        else:
            return bisect_search1(L[half:], e)
``` 

##### Bisection Search 2

Rather than implementing the concept of cutting the list itself, we can instead use pointer locations to describe our boundaries in the list, this would create a constant of O(1), though it is negated by the lower-level O(log(n)), causing this complexity to ultimately be the latter.

``` py
def bisect_search2(L, e):
    def bisect_search_helper(L, e, low, high):
        if high == low:
            return L[low] == e
        mid = (low + high)//2
        if L[mid] == e:
            return True
        elif L[mid] > e:
            if low == mid: #nothing left to search
                return False
            else:
                return bisect_search_helper(L, e, low, mid - 1)
        else:
            return bisect_search_helper(L, e, mid + 1, high)
    if len(L) == 0:
        return False
    else:
        return bisect_search_helper(L, e, 0, len(L) - 1)
```

A good way of keeping the complexities in mind is the following: something that has to iterate over a whole list is linear, something that divides the remaining problem is logarithmic, and something that is unchanging is constant.

##### Logarithmic Complexity Sample

``` py
def intToStr(i):
    digits = '0123456789'
    if i == 0:
        return '0'
    result = ''
    while i > 0:
        result = digits[i%10] + result
        i = i//10
    return result
```

### Linear Complexity

Linear complexity O(n) is dependant on the number of iterative calls. The growth comes from the size of our input. Regardless of whether we loop or use recursion in the following examples, they still have the same order of growth. One may be slightly slower than the other on a small scale due to operation steps, but ultimately the different doesn't matter.

``` py
def fact_iter(n):
    prod = 1
    for i in range(1, n+1):
        prod *= i
    return prod
``` 

``` py
def fact_recur(n):
    """assume n>= 0"""
    if n <= 1:
        retuen 1
    else:
        return n * fact_recur(n-1)
```

### Log-Linear Complexity

This complexity is discussed in the next lecture due to its common use with sorting algorithms.

### Polynomial Complexity

This complexity O(n^2) commonly occurs when we have nested loops; most common polynomial algorithms are quadratic (or grows with square of size of input).

### Exponential Complexity

This complexity occurs when we have recursive functions where more than one recursive call exists for each size of the problem. Although undesireable, many important problems are inherently exponential. The cost of these algorithms can be very high and should push us to consider that approximate solutions may provide a reaonsable answer more quickly.

Towers of Hanoi are an example of exponential complexity.

``` py
def genSubsets(L):
    if len(L) == 0:
        return [[]]
    smaller = genSubsets(L[:-1])
    extra = L[-1:]
    new = []
    for small in smaller:
        new.append(small+extra)
    return smaller+new
``` 