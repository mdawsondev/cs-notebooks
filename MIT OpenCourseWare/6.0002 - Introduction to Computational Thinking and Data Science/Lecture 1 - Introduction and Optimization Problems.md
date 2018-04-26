# Lesson 1: Introduction and Optimization Problems

## Computational Models

A computational model is the idea of experimentation based on optimization models, statistical models, and simulation models.

### Optimization Models

We start with an objective that is to be maximized or minimized: ex finding the fastest route that minimizes total travel time. The **objective function** would be the number of minutes in transite getting from A to B.

On top of our objective function, we typically have to layer on **contraints** that must be obeyed. In our travel example, it would be like having only $100 to spend, so a plane would be out of the option.

Another example would be a burglar who wants to steal a room full of valuables, but only has enough room for a handful of items. In this situation, the burglar must be selective due to their constraints.

This problem, known as the **knapsack problem** has two varients, the _0/1_ and the _fractional/continuous_ problem; _0/1_ being you take the object, or you dont, and _fractional_ being you take things in parts. Example, a gold bar may not fit but you can shave it down.

**Continuous problems** can be completed with what's known as a _"greedy algorithm"_. The idea is that you take the best thing first as long as you can and then move on to the next thing.

The knapsack problem can be solved in a couple of ways once formulated into an equation represending the constraints and goals.

#### Brute Force Algorithm

1. Enumerate all possible combinations of items (i.e. generate all subsets). This is called the **power set**.
2. Remove all the combinations whos total units exceeds the allowed weight.
3. From the remaining combinations, choose any one whos value is the largest.

This algorithm, while it will give you an answer, is usually not practical. If you're working with a large power set, the posibilities grow exponentially larger.

Surprisingly, for the knapsack problem, there is not a better algorithm in terms of running time. Many optimization problems are exponential by nature.

#### Greedy Algorithm

The philosophy of the greedy algorithm is, "while the knapsack is not full, put the best available item in the bag." Another example beyond the knapsack problem would be choosing from a variety of foods to eat but constraining your calorie limitations. You would likely choose your favorites that were still within the limited constraint.

Assume that we have an object that contains a list of food, each given the value weighted in terms of favoritism and then valued with calories.

```py
class Food(object):
    def __init(self, n, v, w):
        self.name = n
        self.value = v
        self.calories = w

    def getValue(self):
        return self.value

    def getCost(self):
        return self.calories

    def density(self):
        return self.getValue()/self.getCost()

    def __str__(self):
        return self.name + ': <'+ str(self.value)\
            + ', ' +  str(self.calories) + '>'

def buildMenu(names, values, calories):
    menu = []
    for i in range(len(values)):
        menu.append(Food(names[i], values[i], calories[i]))
    return menu

def greedy(items, maxCost, keyFunction):
    itemsCopy = sorted(items, key = keyFunction, reverse = True)

    result = []
    totalValue, totalCost = 0.0, 0.0

    for i in range(len(itemsCopy)):
        if (totalCost+itemsCopy[i].getCost()) <= maxCost:
            result.append(itemsCopy[i])
            totalCost += itemsCopy[i].getCost()
            totalValue += itemsCopy[i].getValue()

    return (result, totalValue)

def testGreedy(items, constraint, keyFunction):
    taken, val = greedy(items, constraint, keyFunction)
    print('Total value of items taken = ', val)
    for item in taken:
        print(' ', item)

def testGreedys(maxUnits):
    print('Use greedy by value to allocate', maxUnits, 'calories')
    testGreedy(foods, maxUnits, Food.getValue)
    print('Use greedy by cost to allocate', maxUnits, 'calories')
    testGreedy(foods, maxUnits, lambda x: 1/Food.getCost(x))
    print('Use greedy by density to allocate', maxUnits, 'calories')
    testGreedy(foods, maxUnits, Food.density)

names = ['wine', 'beer', 'pizza', 'burger', 'fries', 'cola', 'apple', 'donut', 'cake']
values = [89,90,95,100,90,79,50,10]
calories = [123,154,258,354,365,150,95,195]
foods = buildMenu(names, values, calories)

testGreedys(foods, 750)
```

_Aside: `lambda` is used to create an anonymous function, just like in JavaScript you can call `function() {}` internally without naming it explicitly._

The problem with greedy algorithms is that they are functionally designed to select a local optimal point rather than a global optimum. Depending on which results are seen first by sort may cause variation in the true optimum value on a global range.