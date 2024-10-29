# Functional Programming

<https://docs.python.org/3/howto/functional.html>

- Most programming languages are procedural: programs are lists of instructions that tell the computer what to do with the program’s input. C, Pascal, and even Unix shells are procedural languages.
- In declarative languages, you write a specification that describes the problem to be solved, and the language implementation figures out how to perform the computation efficiently. SQL is the declarative language you’re most likely to be familiar with; a SQL query describes the data set you want to retrieve, and the SQL engine decides whether to scan tables or use indexes, which subclauses should be performed first, etc.
- Object-oriented programs manipulate collections of objects. Objects have internal state and support methods that query or modify this internal state in some way. Smalltalk and Java are object-oriented languages. C++ and Python are languages that support object-oriented programming, but don’t force the use of object-oriented features.
- Functional programming decomposes a problem into a set of functions. Ideally, functions only take inputs and produce outputs, and don’t have any internal state that affects the output produced for a given input. Well-known functional languages include the ML family (Standard ML, OCaml, and other variants) and Haskell.

Functional programming can be considered the opposite of object-oriented programming. Objects are little capsules containing some internal state along with a collection of method calls that let you modify this state, and programs consist of making the right set of state changes. Functional programming wants to avoid state changes as much as possible and works with data flowing between functions. In Python you might combine the two approaches by writing functions that take and return instances representing objects in your application (e-mail messages, transactions, etc.).

## What are the benefits of functional programming?

As said before, the code in functional programming tends to be more objective and shorter than in other paradigm types because you are able to isolate the pure functions that will obtain the logic of your business from the functions that are called mutable, which are operations that actually change the object, such as modifying data in a database, for example.

Another benefit is that, since it is based on mathematical functions, the functional paradigm prompts the use of the concept of immutability. An example of that would be a simple mathematical function, such as f(x) = x + 2. Whenever we use the same value for that function, it will provide an equal, immutable result.

Because of that, code maintenance and eventual changes are easier to apply. It is simpler to add tests and isolate a function in order to make analyses and correct flaws.

It may seem like a small detail, but by having an immutable code, we are sure that when we test it, the code will not act in an unexpected way in a production environment.

In addition to that, functional languages are friendlier to the implementation of parallel computing, meaning that different parts of the system are run smoothly by different processors. That can be explained by the fact that the codes are predictable and immutable, with no side effects.

- Formal provability.
- Modularity.
- Composability.
- Ease of debugging and testing.
