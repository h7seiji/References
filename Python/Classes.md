
# Classes

## @staticmethod

The @staticmethod decorator allows you to define static methods within a class. These methods don’t have access to the instance or class itself but can be called without instantiating an object.

```python
class MathUtils:
    @staticmethod
    def square(x):
        return x ** 2

print(MathUtils.square(3))  # Output: 9
```

## @classmethod

The @classmethod decorator defines methods that receive the class itself as the first argument instead of the instance.

```python
class MathUtils:
    @classmethod
    def cube(cls, x):
        return x ** 3

print(MathUtils.cube(3))  # Output: 27
```

## Magic or Dunder Methods

<https://www.tutorialsteacher.com/python/magic-methods-in-python>

### `__init__()`

Always executed when the class is being initiated.

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("John", 36)
```

### `__str__()`

Controls what should be returned when the class object is represented as a string.

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def __str__(self):
    return f"{self.name}({self.age})"

p1 = Person("John", 36)
print(p1)
```

### `__new__()`

Returns a new object, which is then initialized by `__init__()`.

```python
class Employee:
    def __new__(cls):
        print ("__new__ magic method is called")
        inst = object.__new__(cls)
                return inst
    def __init__(self):
        print ("__init__ magic method is called")
        self.name='Satya'
```

### `__del__()`

Destructor method.

## @dataclass

It provides a concise way to create classes primarily used for storing and managing data.
@dataclass automatically generates special methods such as __init__, __repr__, __eq__, and more based on the class attributes.
This reduces the need for writing repetitive and boilerplate code, making your codebase more readable and maintainable.

```python
@dataclass(frozen=True)
class ImmutablePoint:
    x: int
    y: int
```
