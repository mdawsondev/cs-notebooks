# Lesson 2: Branching and Iteration

## More Types and Comparisons

### Strings

* Any combination of letters, special characters, digits.
* Enclosed in single or double quotation marks.
* Can be concatenated.
* Can have operations performed on them.

``` Python
hi = 'hello there'
name = 'ana'
greet = hi + name
greeting = hi + ' ' + name
silly = hi + ' ' + name * 3

>>>hi
'hello there'

>>>name
'ana'

>>>greet
'hello thereana'

>>>greeting
'hello there ana'

>>>silly
'hello there anaanaana'
```

### Print

* Can print variables.
* Can express commas as spaces.
* Using variables through commas means they can be integers; plus concatenation converts to strings.

``` Python
word = 'word'
words = 'A bunch of words.'

>>>print(word, words)
'word A bunch of words.'

>>>print(word + ' SOUP ' + words)
'word SOUP Abunchofwords.'
```

### Input

* Accept input from the user.
* Prints whatever is in quotes.
* User input is stores *as a string*. Numbers are strings, they must be cast to a number value.
* Can be bound to a variable.


```Python
myWords = input("Say something: ")
print(myWords)
```

## Conditionals

### Comparison Operators

* `i` and `j` are variables.
* Comparisons evaluate to Boolean.
* `i > j` 
* `i >= j`
* `i < j`
* `i <= j`
* `i == j` Equality Test
* `i != j` Inequality Test

Comparison of numbers to strings throw an error.
Comparison of string to a string compares lexigraphically.

### Control Flow

* `if`
* `else`
* `elif`

These code blocks are based on conditionals. Any conditional holding an `else` statement will always meet one condition. 

`if` statements
``` Python
if <condition>:
    <expression>
    <expression>
    ...
```
`else` statements
``` Python
if <condition>:
    <expression>
    <expression>
else:
    <expression>
    <expression>
    ...
```
`elif` statements
``` Python
if <condition>:
    <expression>
    <expression>
elif <condition>:
    <expression>
    <expression>
else:
    <expression>
    <expression>
    ...
```

### Indentation and Sample

* Indentation matters in Python (four spaces).
* Is used to denote blocks of code.

``` Python
x = float(input('Enter a number for x: '))
y = float(input('Enter a number for y: '))
if x == y:
    print('x and y are equal')
    if y != 0:
        print('therefore, x/y is', x/y)
elif x < y:
    print('x is smaller')
else:
    print('y is smaller')
print('thanks!')
```

*There was a pretty sweet Zelda example next, but I'm not going to copy it because literally nobody is ever going to read this. If a programmer writes code in the woods and no one's around to see it, does it still compile?*

## Iteration

### While Loops

* While loops repeat until the condition is false.
* Great for situations where you don't know how many times the loop will repeat.
* Can use a counter but it must be declared before loop and incremented inside of it.
* Loop counter must have an increment to avoid an infinite loop.

Loop counters are not recommended for while conditionals because there is a better loop for this (`for`), therefore it's best to use an unknown that will turn false.

``` Python
while <condition>:
    <expression>
    <expression>
    ...

n = 5 '''Declaration'''
while n > 0:
    print(n)
    n = n - 1 '''Prevent infinite loop'''
print('Blast off!') 
```
### For Loop

* For loops are best used for known numbers of iteration.
* Undeclared variables iterate from 0.
* For loop's range can have params: `range(start, stop, step)`
* `stop` is obligatory for a custom range, `step` is optional and will iterate + 1.
* `stop` is the value - 1.
* For loops can always be rewritten using a while loop, but a while loop may not always be rewritten using a for loop.

``` python
for <variable> in range(<some_num>):
    <expression>
    <expression>
    ...

for n in range(5):
    print(n)
print('Blast off!')

mysum = 0
for i in range(5, 11, 2):
    mysum += i
print(mysum) '''5, 7, 9''
```

### break Statement

* Immediately exits whatever loop it sits inside.
* Skips remaining expressions in block.
* Exits **innermost** loop.

``` py
while <condition_1>:
    while <condition_2>:
        <expression_a>
        break
        <expression_b> '''Never evaluated!'''
    <expression_c>
```



