
# Typing

- <https://typing.readthedocs.io/en/latest/spec/>
- <https://medium.com/@ramanbazhanau/advanced-type-annotations-in-python-part-1-3c9a592e394>

## TypedDict

```python
from Typing import TypedDict, Unpack

class Employee(TypedDict, total=False): # total specifies that not all keys are required
    name: str
    id: int

employee1: Employee = {"id": 123}

def retrieve(**kwargs: Unpack[Employee]) -> None: ...
```

## Generic

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

## Protocol

```python
from typing import Protocol

class SupportsClose(Protocol):
    def close(self) -> None:
        pass

class FileResource:
    def close(self) -> None:
        print("File closed")

# This is valid, even though FileResource doesn't inherit from SupportsClose
def close_resource(resource: SupportsClose) -> None:
    resource.close()
```

## Annotated

```python
from typing import Annotated

Age = Annotated[int, "value should be between 0 and 120"]
```

### Validation

```python
def validate_age(value: Age) -> None:
    _, metadata = Age.__metadata__
    if not (0 <= value <= 120):
        raise ValueError(f"Invalid age. {metadata}")
```

### Documentation

```python
Coordinate = Annotated[tuple, "A tuple representing (x, y) coordinates on a 2D plane"]
```

### Serialization and Deserialization

```python
DateStr = Annotated[str, {"format": "YYYY-MM-DD"}]

def serialize_date(date: datetime.date) -> DateStr:
    format_str = DateStr.__metadata__[1]["format"]
    return date.strftime(format_str)
```

## TypeAlias

```python
from typing import List, Dict

# Using TypeAlias for better readability
Matrix = List[List[int]]
PersonData = Dict[str, Union[str, int, float]]
```

## Type Variable

```python
def first[T](elements: list[T]) -> T:
    return elements[0]
```

In the above function, if a list of integers is passed, Output will be an integer.
If we pass a list of strings, the output will be a String.
Also, note that we don’t need to declare the Typing in the above example.
Before 3.12 we had to declare `T = TypeVar('T')`.

## Literal

```python
from typing import Literal

def draw_shape(shape: Literal["circle", "square", "triangle"]) -> None:
    if shape == "circle":
        # Draw circle
        pass
    elif shape == "square":
        # Draw square
        pass
    # ... and so on
```

## Sequence

Any object that supports iteration and indexing, like lists or strings.

```python
from typing import Sequence

def first_element(items: Sequence) -> Any:
    return items[0]
```

## Mapping

Any object that maps keys to values, like dictionaries.

```python
from typing import Mapping

def get_value(data: Mapping, key: str) -> Any:
    return data.get(key)
```

## Type

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

## ParamSpec

```python
from typing import Callable, ParamSpec

P = ParamSpec("P")

def decorator(func: Callable[P, int]) -> Callable[P, int]:
    def wrapper(*args: P.args, **kwargs: P.kwargs) -> int:
        print("Before calling the function")
        result = func(*args, **kwargs)
        print("After calling the function")
        return result
    return wrapper
```

## TypeGuard

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
