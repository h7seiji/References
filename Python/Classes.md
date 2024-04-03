
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

## Metaclasses

### `__init__()`

### `__new__()`

### `__call__()`

## @dataclass

It provides a concise way to create classes primarily used for storing and managing data.
@dataclass automatically generates special methods such as __init__, __repr__, __eq__, and more based on the class attributes.
This reduces the need for writing repetitive and boilerplate code, making your codebase more readable and maintainable.
