# Design Patterns

- https://refactoring.guru/design-patterns/catalog
- https://www.youtube.com/watch?v=pGq7Cr2ekVM

## Huge and dominate our frameworks

- Composite
- Chain of Responsibility
- Command
- Interpreter

## Small but useful

- Builder
- Adapter
- Flyweight

## Ambitious but fatally limited

- Facade

## Decompose big classes, but are obscure

- Bridge
- Decorator
- Mediator
- State

## Language built-ins

- Iterator
- Visitor

## Anti-patterns that obscure our data

- Proxy
- Memento
- Observer

## Useless if you have 1st-class functions

- Factory
- Template
- Prototype
- Singleton
- Strategy

### Composite

- give all nodes in a hierarchy the same interface

### Chain of Responsibility

- in a Composite UI hierarchy, pass unprocessed clicks and keystrokes up to your parent
- also known as "Bubbling" in the browser

### Command

- represent user actions as a list of objects that have both do() and undo() methods

### Interpreter

- uses the Composite Pattern to represent an Abstract Syntax Tree, and make it executable by giving each node a method

### Builder

- provides a single object whose API build and returns an object hierarchy for us

### Adapter

- when a class doesn't offer the interface you need, write a wrapper class that does, and have its methods call the underlying object

### Flyweight

- small read-only data can be shared between object instances

### Facade

- hide a complex system behind a single API class
- Facade: 1 object
- Real APIs: n objects

### Bridge

- one real-world object, but two classes

### Decorator

- a wrapper with the same interface as the object

### Mediator

- extra class to take action when widgets update

### State

- replace if-else stacks with separate objects

### Iterator

- producer offers a callback method, like next()
- consumer loops, calling next() over and over
- replaced by generators

### Visitor

- producer iterates across a data structure
- consumer offers one (or more) callback methods
- replaced by generators

### Proxy

- sends method calls across the network
- hides how data is passed across the network
- Network APIs between services should use a data format you understand

### Memento

- saves object state as binary string
- hides how data is persisted to disk
- Data should be persisted in a format that's independent of your programming language and that you can access directly using other tools

### Observer

- object offer subscriptions to its changes
- scatters data rather than unifying it
- Should we really be building forests of objects that are subscribed to each other's state changes?

### Factory

- Factory Method: Class inheritance
- Abstract Factory: Object Composition
- Abstract Factory > Factory Method
- Neither is used on modern languages, because of First-class functions and First-class types
- A programming language is said to have First-class functions when functions in that language are treated like any other variable
- You just pass the functions or the class instead of the constructor

### Template

- If Application needs you to give it three procedures, it should force you to write a subclass
- These three methods should live on a separate class

### Prototype

- Clone method to create a new instance of itself
- In modern languages you can just pass data structures

### Singleton

- Global objects that code needs to access to but you don't want to pass everywhere
- Do we need the pattern? To force the class to be a Singleton
- Just write the class normally

### Strategy

- Function as an argument solves this problem
