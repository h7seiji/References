# Python

- Cheat Sheet <https://medium.com/@roelljr/ultimate-python-cheat-sheet-practical-python-for-everyday-tasks-c267c1394ee8>
- <https://github.com/cjolowicz/cookiecutter-hypermodern-python>
- <https://mitelman.engineering/blog/python-best-practice/automating-python-best-practices-for-a-new-project/>
- <https://blog.stackademic.com/20-python-concepts-i-wish-i-knew-way-earlier-40ed5674cd52>
  - Map, Filter, Reduce
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
- Walrus Operator <https://betterprogramming.pub/should-you-be-using-pythons-walrus-operator-yes-and-here-s-why-36297be16907>
- Data Structures <https://www.deriveit.org/coding/cheat-sheets/87>
- BitwiseOperators <https://wiki.python.org/moin/BitwiseOperators>
- Exception Handling <https://medium.com/@saadjamilakhtar/5-best-practices-for-python-exception-handling-5e54b876a20>
- Cheatsheet <https://dranolia.medium.com/python-cheatsheet-51b552b56a81>

## venv

```bash
python -m venv env-name

.\env-name\Scripts\Activate.ps1
```

## List Comprehension

- <https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions>

## Generators

### When to Use Generators

- Large Datasets: Process without consuming all memory.
- Streaming Data: Handle real-time data streams effectively.
- Expensive Computations: Compute values lazily, only when needed.
- Infinite Sequences: Produce values indefinitely.
- Pipeline Processing: Reduce memory in data processing chains.

### When Generators Might Not Be Ideal

- Random Access: Generators are linear, not for indexed access.
- Multiple Passes: Generators exhaust after one use; not for re-traversing.
- Short Data Sequences: Overkill for small, in-memory datasets.
- Complex State Management: This can lead to confusing code.
- Performance-Critical: Might introduce minor speed overheads.

## Functions

- Functions in Python are first-class citizens. That means you can work with functions as you would with any other variable. You can pass them as arguments to other functions, return them from functions, and even store them in variables.
- Functions are objects. Objects are instances of classes and contain methods and attributes.

### Lambda functions

### Decorators

```python
def my_logger(fun):
    def _inner_decorator(*args, **kwargs):
        print(f'{fun.__name__} is being called!')
        return fun(*args, **kwargs)

    return _inner_decorator

@my_logger
def my_function(n):
    return sum(range(n))

print(my_function(5))
# my_function is being called!
# 10
```

### *args **kwargs

## Classes

### @staticmethod

The @staticmethod decorator allows you to define static methods within a class. These methods don’t have access to the instance or class itself but can be called without instantiating an object.

```python
class MathUtils:
    @staticmethod
    def square(x):
        return x ** 2

print(MathUtils.square(3))  # Output: 9
```

### @classmethod

The @classmethod decorator defines methods that receive the class itself as the first argument instead of the instance.

```python
class MathUtils:
    @classmethod
    def cube(cls, x):
        return x ** 3

print(MathUtils.cube(3))  # Output: 27
```

### Metaclasses

#### `__init__()`

#### `__new__()`

#### `__call__()`

## Asyncio

- <https://github.com/timofurrer/awesome-asyncio>
- <https://blog.devgenius.io/mastering-asynchronous-programming-in-python-a-comprehensive-guide-ef1e8e5b35db>

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

- <https://www.datacamp.com/tutorial/python-subprocess>

## Frozenset

Use set as a dict key

```python
set_ex = frozenset({1, 2, 3})
dict_obj = {set_ex: "This is a Set"}

print(dict_obj[set_ex])
## Output - This is a Set
```

## Typing

- <https://typing.readthedocs.io/en/latest/spec/>
- <https://medium.com/@ramanbazhanau/advanced-type-annotations-in-python-part-1-3c9a592e394>

### TypeAlias

```python
from typing import List, Dict

# Using TypeAlias for better readability
Matrix = List[List[int]]
PersonData = Dict[str, Union[str, int, float]]
```

### Type Variable

```python
def first[T](elements: list[T]) -> T:
    return elements[0]
```

In the above function, if a list of integers is passed, Output will be an integer.
If we pass a list of strings, the output will be a String.
Also, note that we don’t need to declare the Typing in the above example.
Before 3.12 we had to declare `T = TypeVar('T')`.

### Type

Used to indicate that something is a class rather than an instance of a class.

```python
from typing import Type

class Animal:
    @classmethod
    def make_sound(cls):
        pass

def mimic(animal_class: Type[Animal]):  # animal_class is a class, not an instance
    animal_class.make_sound()

mimic(Animal)
```

### TypedDict

```python
from Typing import TypedDict, Unpack

class Employee(TypedDict, total=False): # total specifies that not all keys are required
    name: str
    id: int

employee1: Employee = {"id": 123}

def retrieve(**kwargs: Unpack[Employee]) -> None: ...
```

### Generic

```python
from typing import Generic, TypeVar

T = TypeVar('T')

class Box(Generic[T]):
    def __init__(self, item: T):
        self.item = item

class Container(Generic[T]):
    def __init__(self, value: T):
        self.value = value

box_int = Box(5)  # box_int: Box[int], class Box(item: int)
box_str = Box("Hello")  # box_str: Box[str], class Box(item: str)

# This allows for type-safe operations on the container
int_container = Container[int](5)
str_container = Container[str]("Hello")
```

### TypeGuard

- A function that returns TypeGuard[T] is essentially telling the type checker: "If this function returns True, then the variable you passed in is of type T."
- The function returning TypeGuard[T] should not have any side effects. It should only perform checks and return a boolean value.

```python
from typing import List, Union, TypeGuard

def is_string_list(values: List[Union[int, str]]) -> TypeGuard[List[str]]:
    return all(isinstance(value, str) for value in values)

def process(values: List[Union[int, str]]):
    if is_string_list(values):
        # Within this block, 'values' is treated as List[str] by the type checker
        concatenated = " ".join(values)
        print(concatenated)
    else:
        # Here, 'values' is still List[Union[int, str]]
        print("List contains non-string values.")
```

## Bytecode

- `dis` library
- <https://opensource.com/article/18/4/introduction-python-bytecode>
- <https://medium.com/@noransaber685/demystifying-python-bytecode-a-guide-to-understanding-and-analyzing-code-execution-6a163cb83bd1>
- <https://medium.com/@yonatanzunger/advanced-python-achieving-high-performance-with-code-generation-796b177ec79>

## FastAPI

- Mongo + FastAPI: <https://www.mongodb.com/languages/python/pymongo-tutorial>

## Pytest

Import modules from current directory

```bash
python -m pytest
```

Run only one test

```bash
pytest test_file.py::test_function
```

### Fixtures

```python
# conftest.py
import pytest

@pytest.fixture
def db_connection():
  yield
```

```python
# test_example.py
def test_db_connection(db_connection):
  assert True
```

### Monkeypatching

```python
def test_mytest(monkeypatch):
  monkeypatch.setattr(app_onboarding, "username_moderation", mock_moderation)
```

## Libraries

- HTTPX: <https://github.com/encode/httpx>
- Dotenv: <https://saurabh-kumar.com/python-dotenv/>
- FastAPI: <https://fastapi.tiangolo.com/>
- Pydantic: Data validation <https://docs.pydantic.dev/latest/>
- SQLModel: ORM <https://sqlmodel.tiangolo.com/>
- Ruff: Linter and formatter <https://github.com/astral-sh/ruff>
- BeautifulSoup: Web scrapper <https://www.crummy.com/software/BeautifulSoup/>
- Pendulum: Datetimes made easy <https://pendulum.eustace.io/>
- Icecream: Print for dubgging <https://github.com/gruns/icecream>
- Loguru: Logging <https://github.com/Delgan/loguru>
- Seaborn: Statistical data visualization <https://github.com/mwaskom/seaborn>
- factory_boy: Create fake data <https://github.com/FactoryBoy/factory_boy>
- hug: Simple API framework <https://github.com/hugapi/hug>
- pyinstrument: Performance profiler <https://github.com/joerick/pyinstrument>
- gevent: Coroutine-based networking library <https://www.gevent.org/>
