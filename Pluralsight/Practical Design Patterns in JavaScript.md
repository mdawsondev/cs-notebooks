# Practical Design Patterns in JavaScript

[This course is available on Pluralsight](https://app.pluralsight.com/player?course=javascript-practical-design-patterns).

## About Design Patterns

JavaScript is meant to be designed around an OOP approach. Design patterns exist in various formats, the idea is to approach the problem with a specific pattern that will help the most.

The philosophy behind design pattern originated from an architect; it can be described as a problem/solution display.

> Problem: On/Off Traffic for Highways | Solution: Cloverleaf Interchanges
> 
> Problem: Pedestrian Traffic | Solution: Sidewalks
> 
> Problem: Entry and Exit for Public Buildings | Solution: Revolving Doors

In programming, a book was released to help translate this to code design.

> Problem: Designing Service Layers | Solution: Module Pattern
>
> Problem: Overly Complicated Object Interfaces | Solution: Facade Pattern (ex. jQuery)
>
> Problem: Visibility into State Changes | Solution: Observer Pattern

We should approach design with, "What's the problem were trying to solve?" and address it with a solution pattern.

**A pattern:**

* Solves a problem.
* Is a proven concept.
* Solution is not obvious.
* Describes a relationship.
* Has a significant human component.

Patterns should be used because: there's no reason to solve a problem that's already been solved, and it establishes a common vocabulary.

**Types of Patterns:**

* **Creational**: Deals with creation of instances.
  1. Constructor
  2. Module
  3. Factory
  4. Singleton
* **Structural**: Deal with makeup of objects themselves.
  1. Decorator.
  2. Facade.
  3. Flyweight.
* **Behavioral**: Deal with how objects relate.
  1. Command
  2. Mediator
  3. Observer

## Creational Design Patterns

### Constructor Pattern

The constructor pattern is used to create new objects with their own object scope. Focuses on the `new` keyword. Dropping `new` in front of any function invokes a constructor function.

* Creates a new object.
* Link to an object prototype.
* Binds `this` to the object scope.
* Implicity returns `this`.

The teacher of this course is using old syntax rather than ES6, so I'll be making my notes in ES6.

``` JS
class ObjectName {
  constructor(param1, param2) {
    this.param1 = param1;
    this.param2 = param2;
  };

  toString() {
    return `${this.param1} ${this.param2}`;
  };
}
```

The `this` keyword is binding our construction to the object's scope.

ES5 recommends extracting your functions from the constructor function and placing them into `ObjectName.prototype.myMethod = function() {}`, but this isn't necessary in ES6 because the object distributes the prototype data automatically. It isn't generating new methods with every instance.

Exporting classes from an external .js file is a good way to segregate and modularize code. `module.exports = ObjectName`.

### Module Pattern

* Simple way to encasulate similar methods.
* Creates a "Toolbox" of functions to use.

A module is best represented when you need "one of something," ex. a fetch service, database service, etc. Constructors are best left for things you will create multiple instances of.

``` JS
const MyModule = function() {
  const priateVar = 'I am private.';
  return {
    method: function() { ... },
    nextMethod: function() { ... }
  }
}
```

Modules are not called with a `new` call, they're meant to be created as a literal. **Modules always return methods!** When sliced out of the main code and into their own file, they are returned with `module.exports = myModule()`, where the function can be executed immediately and return the methods it houses.

An alternative to directly returning methods is by creating a "revealing module," where you distribute methods in the return but define them in the object itself.

``` JS
const MyModule = function() {
  const priateVar = 'I am private.';
  
  function method() { ... };
  function nextMethod() { ... };
  
  return {
    method,
    nextMethod
  }
}
```

### Factory Pattern

* Simplifies object creation.
* Creating different objects based on need.

In the example given, the teacher is pulling from multiple repositories. Rather than including three different repository requirements, a **factory pattern** can be used to generate these requests as needed.

``` JS
const taskRepo = require('./taskRepository');
const userRepo = require('./userRepository');
const projectRepo = require('./projectRepository');
```

These requires could instead be implemented via factory.

``` JS
const repoFactory = function() {
  this.getRepo = function(repoType) {
    // if (repoType === 'task') { // This would represent an uncached edition.
    //   var taskRepo = require('./taskRepository')();
    //   return taskRepo;
    // }
    if (repoType == 'task') {
      if (this.taskRepo) {
        return this.taskRepo;
      } else {
        this.taskRepo = require('./taskRepository')();
        return this.taskRepo;
      }
    }
    if (repoType === 'user') {
      var userRepo = require('./userRepository')();
      return userRepo;
    }
    if (repoType === 'project') {
      var projectRepo = require('./projectRepository')();
      return projectRepo;
    }
  }
}

module.exports = new repoFactory;
```

``` JS
const Task = require('./task');
const repoFactory = require('./repoFactory');

const task1 = new Task(repoFactory.getRepo('task').get(1));
const task2 = new Task(repoFactory.getRepo('task').get(2));
const user = repoFactory.getRepo('user').get(1));
const project = repoFactory.getRepo('project').get(1));
```

Summoning needed requirements this way means you can tether similar things together. Gulp offers a plugin that does exactly this, where your plugins are collected and then tied to the `plugins.myPlugin` object.

Cleaning a factory can be taken even further by injecting `.getRepo('thing')` into its own method for simplicity.

``` JS
const repoFactory = function() {
  const repos = this;
  const repoList = [{name: 'task', source: './tasksRepository'},
                    {name: 'user', source: './userRepository'},
                    {name: 'project', source: './projectRepository'}];

  repoList.forEach(function(repo) {
    repos[repo.name] = require(repo.source)()
  });
};

module.exports = new repoFactory;
```

``` JS
const Task = require('./task');
const repoFactory = require('./repoFactory');

const task1 = new Task(repoFactory.task.get(1));
const task2 = new Task(repoFactory.task.get(2));
const user = repoFactory.user.get(1));
const project = repoFactory.project.get(1));
```

### Singleton Pattern

* Used to restrict an object to one instance of that object across the application.
* Remembers the last time you used it.
* Hands back same instance from before.

``` JS
const TaskRepo = (function () {
  const taskRepo;
  function createRepo() {
    const taskRepo = new Object("Task");
    return taskRepo;
  }
  return {
    getInstance: function() {
      if (!taskRepo) {
        taskRepo = createRepo();
      }
      return taskRepo;
    }
  }
})();

const repo1 = TaskRepo.getInstance();
const repo2 = TaskRepo.getInstance();

if (repo1 === repo2) {
  console.log("Same TaskRepo");
}
```

## Structural Design Patterns

Structural design patterns are concerned with how objects are made up and simplify relationships between objects. On one end of the pattern, they're used to extend functionality. On the other end, they simplify it.

### Decorator Pattern

The decorator pattern is used to add new functionality to an existing object without being obtrusive. It solves the problem of adding functionaliy without breaking or changing something that's already working.

* More complete inheritance.
* Wraps an existing objects.
* Protects existing objects.
* Allows extended functionality.

``` JS
const Task = function (name) { . . . }

let myTask = new Task();
myTask.newProperty = 2; // This property didn't exist until right now.
                        // No other task objects will house this property.
```

Decorations also allow you to override a method's original functionality without damaging the original object the instanced object is made from.

The demos in this lesson are a bit inacurate since the teacher doesn't work with the `Class` feature of JavaScript. `Class` offers the ability to `extends` an already existing object and tether `super` to pass commands to the original prototype. There's a whole mess of information about `myObject.prototype.method` and stuff, but c'mon, Class is awesome.

### Facade Pattern

* Used to provide a simplified interface to a complicated system (Ajax, API, etc).
* Facade hides the chaos and complexity of the backend.
* Simplifies the interface.
* jQuery is an example; all it does is sit on the DOM rather than JS's native requirements.

A facade pattern does not change the functionality of the object, unlike the decorator pattern. Nothing is being added, things are just being "covered up" to have a better interface.

``` JS
const TaskServiceWrapper = function() {
  const completeAndNotify = (task) => {
    TaskService.complete(myTask);
    if (myTask.completed) {
      TaskService.setCompleteData(myTask);
      TaskService.notifyCompletion(myTask, myTask.user);
      TaskService.save(myTask);
    }
  }
  return { completeAndNotifiy }
}()

TaskServiceWrapper.completeAndNotify(myTask);
```
Rather than having to repeat these methods over and over, they can be served as a single method in a wrapper.

### Flyweight Pattern

* Conserves memory by sharing portions of an object between objects.
* Takes non-unique data and shares it.
* Only useful for a large number of objects.

_Aside: process.memoryUsage().heapUsed can be used before and after a large command to see how much memory is being pulled._

The codebase for this pattern was large so I'm just noting how it functions. In our Task object, the only thing unique about a task is its `this.name` property. Other features like the priority, project, user, and completed, have a limited number of possible answers.

What a flyweight does is process each instance of these duplication answers, and then checks it against a storage unit. If the object variation already exists, it returns the existing object rather than creating a new one, and if it doesn't exist, it stores it.

This means that for a very large number of objects (e.g. 100,000), the number of stored instances can be sliced down to only needing to store the unique name while pulling an already existing combination of other properties. And that's pretty neato, right?

``` JS
const Task = function (data) {
  this.flyweight = FlyWeightFactory.get(data.project, data.priority, data.user, data.completed);
  this.name = data.name;
}
```

## Behavioral Design Patterns

Concerned with the assignment of responsibilities between objects and how they communicate.

* Deal with responsibility of objects.
* Help objects cooperate.
* Assigns clear hierarchy.
* Can encapsulate requests.

### Observer Pattern

* Allows a collection of objects to watch an object and be notified of changes.
* Allows for loosely coupled system.
* One object is the focal point.
* Group of objects watch for changes on that one object.

**Observers** watch the target object for changes. The target object is known as the **subject** which is decorated with an `ObserverList{}` and a `Notify()` method. When something changes on our subject, it sends a **notification** to each of the observers. Our observers supply a callback that `Notify()` will execute.

I'm not writing the code for this pattern because he's speeding through it rapidly and I feel like I need another resource to really understand how to implement it. I understand the concept, but the instructor flew right through the setup.

### Mediator Pattern

* Controls communication between objects so neither object has to be couple to the others.
* Allows for a loosely coupled system.
* One object manages all of the communication.
* Offers many to many relationship.

The mediator pattern functions a lot like the observer pattern, except it extracts the notification out into its own object. 

### Command Pattern

* Encapsulates the calling of a method as an object.
* Fully decouples execution from implementation.
* Less fragile implementations.
* Supports undo operations.
* Supports auditing and logging of operations.

Again, this seems like a complicated idea that I intend to research more outside of this resource.