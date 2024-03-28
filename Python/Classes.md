
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
