# Python

- https://cjolowicz.github.io/posts/hypermodern-python-01-setup/
- https://mitelman.engineering/blog/python-best-practice/automating-python-best-practices-for-a-new-project/
- https://blog.stackademic.com/20-python-concepts-i-wish-i-knew-way-earlier-40ed5674cd52
  - List Comprehension
  - Lambda Functions
  - Map, Filter, Reduce
  - Decorators
  - Generators
  - f-Strings
  - \*args and \*\*kwargs
  - Type Hinting
  - Context Managers
  - Walrus Operator
  - Namedtuples
  - enumerate
  - Zipping and Unzipping Lists
  - Dictionaries — get() and setdefault()
  - The **main** Guard
  - Virtual Environments
  - The Asterisk (\*) Operator
  - The `else` Clause in Loops
  - Deepcopy vs. Shallow Copy
  - Python's Underscore (\_) Uses
- List comprehension https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions
- Walrus Operator https://betterprogramming.pub/should-you-be-using-pythons-walrus-operator-yes-and-here-s-why-36297be16907
- `asyncio` https://github.com/timofurrer/awesome-asyncio
- `httpx` over `requests` https://www.datasciencebyexample.com/2023/04/06/httpx-vs-requsts-in-pyton/
  - mainly due to asyncio support
- subprocess https://www.datacamp.com/tutorial/python-subprocess
- Data Structures https://www.deriveit.org/coding/cheat-sheets/87
- BitwiseOperators https://wiki.python.org/moin/BitwiseOperators
- Exception Handling https://medium.com/@saadjamilakhtar/5-best-practices-for-python-exception-handling-5e54b876a20
- Cheatsheet https://dranolia.medium.com/python-cheatsheet-51b552b56a81

## Classes

### **init**()

### @staticmethod

The @staticmethod decorator allows you to define static methods within a class. These methods don’t have access to the instance or class itself but can be called without instantiating an object.

```
class MathUtils:
    @staticmethod
    def square(x):
        return x ** 2

print(MathUtils.square(3))  # Output: 9
```

### @classmethod

The @classmethod decorator defines methods that receive the class itself as the first argument instead of the instance.

```
class MathUtils:
    @classmethod
    def cube(cls, x):
        return x ** 3

print(MathUtils.cube(3))  # Output: 27
```

## Asyncio

### Coroutine

### Event Loop

### Future

### Task

## Threading

## Multiprocessing

Divide tasks written in python over multiple processes to help improve performance

- Multi-core

## Subprocess

Run and control other programs

## Typing

- https://realpython.com/python312-typing/
- https://medium.com/@ramanbazhanau/advanced-type-annotations-in-python-part-1-3c9a592e394

## Libraries

- factory_boy: Create fake data https://github.com/FactoryBoy/factory_boy
- BeautifulSoup: Web scrapper https://www.crummy.com/software/BeautifulSoup/
- hug: Simple API framework https://github.com/hugapi/hug
- pyinstrument: Performance profiler https://github.com/joerick/pyinstrument
