# Lesson 12 - Searching and Sorting

## Searching a Sorted List

Searching a sorted list is different than an unsorted list in the sense that an unsorted list must be sorted adding more operational time before running the search. Using *linear search* results in `O(n)` while *binary search* results in `O(log n)`, *but* it's assumed that this list is presorted.

To calculate the trade of sorting a list first then performing a binary search, we must consider whether our value `SORT + O(log n) < O(n)` to `SORT < O(n)-O(log n)` is less than a linear search. This **never** works! The reason this can't be true is because to sort a list we must look at each element at least one time, resulting in `O(n)`, which will still make the calculation equal the greatest time complexity.

That said, there are cases where you would want to sort before performing a search. This is typically when searching a very large list multiple times: sorting the list once and then running a binary search multiple times will lower the average cost, creating a worthy tradeoff.

## Efficently Sorting Lists

### Bad Example - Stupid Sort

To start, we look at a poorly optimized sort. This is called the Monkey Sort, or "bogosort", "stupid sort", etc. This sort is performed by taking a list, throwing it into a compleatly randomized new order, and checking to see if it's sorted. If it isn't sorted, the sort attempts to order the list again until order is achieved. This could ultimately result in an average `O(n^n)` if really lucky, which is like saying infinity.

### Bubble Sort

Bubble Sort is performed by starting at the beginning of the list and comparing each item pair-wise. Once an evaluation is made, the larger result is always moved further down the list.

Ex: `1, 11, 5, 6, 7` would initially look at `1` and `11`. Since this is sorted by size, we move on. `11` is compared to `5`. Due to `11` being larger, we swap positions and continue to the next numbers. `11` and `6` are compared and so on until ultimately the largest number is at the end of the list. We then repeat the list `n` number of times until the list is sorted.

#### Psuedo

``` psuedo
do
  swapped = false
  for i = 1 to indexOfLastUnsortedElement-1
    if leftElement > rightElement
      swap(leftElement, rightElement)
      swapped = true
while swapped
```

#### Python

``` py
def bubble_sort(L):
    swap = False
    while not swap:
        swap = True
        for j in range(l, len(L)):
            if L[j-l] > L[j]:
                swap = False
                temp = L[j]
                L[j] = L[j-1]
                L[j-1] = temp
```

#### JavaScript

``` js
const bubbleSort2 = (myArr) => {
  let finished = false;
  while (!finished) {
    finished = !finished; // Set true;
    myArr.forEach((e, i, a) => { // Move biggest to the end;
      if (a[i-1] > a[i]) {
        finished = !finished; // Set false;
        temp = a[i];
        a[i] = a[i-1];
        a[i-1] = temp;
      }
   });
  }
}
```

In our example, the inner loop is for comparisons and the outer loop is for doing multiple passes until there are no more swaps. This results in `O(n^2)`.

### Selection Sort

This sort is based on finding the smallest element in a remaining unsorted list and swapping it with the first unsorted position of the list.

Ex: `9, 3, 5, 1, 2` would find the smallest item, `1`, and convert the list to `1, 3, 5, 9, 2`. The sort would then find `2` and convert the list to `1, 2, 5, 9, 3`. It would then find `3` and convert to `1, 2, 3, 9, 5`. Finally it would output `1, 2, 3, 5, 9`.

This sort will still result in `O(n^2)` because the worst case would have to be going through the list `n` number of times per `n` number of loops. The outer loop is `O(n)`, the inner loop is `O(n)`. 

#### Psuedo

``` psuedo
repeat (numOfElements - 1) times
  set the first unsorted element as the minimum
  for each of the unsorted elements
    if element < currentMinimum
      set element as new minimum
  swap minimum with first unsorted position
```

``` py
def selection_sort (L):
    suffixSt = 0 # Point at position 0 of list.
    while suffixSt != len(L): # As long as we have items left, do the following.
        for i in range(suffixSt, len(L)): # Loop over everything.
            if L[i] < L[suffixSt]: # Compare to the thing at our first unused positon.
                L[suffixSt], L[i] = L[i], L[suffixSt] # Swap the two.
        suffixSt += 1 # Move to the next unsorted position.
```

``` JavaScript
function selectionSortX(myArr) {
  unsortedPosition = 0;
  while (unsortedPosition != myArr.length) {
    for (i = unsortedPosition; i < myArr.length; i++) {
      if (myArr[i] < myArr[unsortedPosition]) {
        const temp = myArr[i];
        myArr[i] = myArr[unsortedPosition];
        myArr[unsortedPosition] = temp;
      }
    }
  unsortedPosition++;
  }
}
```

### Merge Sort

This sort works by attacking a list with a "divide and conquer" appropach. The list is split into pairs (with a potential single remainder), then each list is sorted. We then take a pair of pairs and sort them by comparing the smallest of each pair, then return the smallest. When we finally clear one list, we can return the entire remaining list. **This is the fastest _worst-case_ sort algorithm known.**

* If the list is empty, or of length `1`, just return a copy of the list.
* Otherwise, find the middle point and split everything up to that point.
* Recursively pass these lists into the function and split in the same way.
* Once we get back our recursive return, merge them.
**Aside: recursive functions will execute via the deepest stack, so this collapses upwards with sorted lists.**
* Point to the beginning of the left list, and the right list.
* While there's still something in both lists, do the following:
  * Compare each and add the smaller result to the new result array.
  * Increase the counter of the list you moved.
  * Repeat until one of the lists are empty.
* If one of the lists is empty, append the other list to the end of the result.

This sorting method results in `O(n log(n))`.

Psuedo

``` Psuedo
split each element into partitions of size 1
recursively merge adjancent partitions
  for i = leftPartStartIndex to rightPartLastIndex inclusive
    if leftPartHeadValue <= rightPartHeadValue
      copy leftPartHeadValue
    else: copy rightPartHeadValue
copy elements back to original array
```

Python

``` py
def merge(left, right):
    result = []
    i,j = 0,0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    while (i < len(left)):
        result.append(left[i])
        i +=1
    while (j < len(right)):
        result.append(right[j])
        j += 1
    return result

def merge_sort(L):
    if len(L) < 2: # Base Case
        return L[:]
    else:
        middle = len(L)//2
        left = merge_sort(L[:middle]) # Divide recursively giving us the smallest problem.
        right = merge_sort(L[middle:])
        return merge(left, right) # Answer the problem and collapse upward.
```