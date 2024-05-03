# Interfaces

Python is somewhat different from other popular languages since there are no interfaces on a language level. But there are several library implementations.

## ABC

```python
from abc import ABC, abstractmethod

class Animal(ABC):
   @abstractmethod
   def eat(self, food) -> float:
       pass
   @abstractmethod
   def sleep(self, hours) -> float:
       pass
```

## Zope

```python
from zope.interface import Interface

class Animal(Interface):
   def eat(self, food) -> float:
       pass
   def sleep(self, hours) -> float:
       pass
```

## Protocol

```python
from typing import Protocol

class Animal(Protocol):
   def eat(self, food) -> float:
       ...
   def sleep(self, hours) -> float:
       ...
```
