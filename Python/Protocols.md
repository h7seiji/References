# Protocols

A protocol is a set of methods or attributes that an object must have in order to be considered compatible with that protocol.
Protocols enable you to define interfaces without explicitly creating a class or inheriting from a specific base class.

```python
from typing import Protocol

class Printable(Protocol):
    def print(self) -> None:
        pass
```

In this example, we define a protocol named Printable that requires an object to have a print method.
The Protocol class allows you to define abstract methods (in this case, just print) that must be implemented by objects conforming to the protocol.

```python
class Book:
    def __init__(self, title: str):
        self.title = title

    def print(self) -> None:
        print(f"Book Title: {self.title}")
```

In this example, the Book class implements the Printable protocol by providing the required print method.
Any instance of the Book class can be treated as a Printable object.

```python
def print_object(obj: Printable) -> None:
    obj.print()
```

In this example, the print_object function takes an argument obj of type Printable.
This means that any object passed to this function must implement the print method defined in the Printable protocol.

You can also define a protocol that combines multiple other protocols.

```python
class Serializable(Protocol):
    def serialize(self) -> str:
        pass

class PrintableAndSerializable(Printable, Serializable):
    pass
```
