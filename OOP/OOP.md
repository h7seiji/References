# OOP

## Class

A blueprint for creating objects, defining their attributes (data) and methods (behavior).

## Object

An instance of a class that encapsulates data and behavior.

## Inheritance

A mechanism in OOP that allows a class to inherit properties and behaviors from another class, promoting code reusability and establishing a parent-child relationship.

```python
class Parent:
    def __init__(self, name: str, price: float, quantity=0):
        # Run validations to the received arguments
        assert price >= 0, f"Price {price} is not greater than or equal to zero!"
        assert quantity >= 0, f"Quantity {quantity} is not greater or equal to zero!"

        # Assign to self object
        self.__name = name
        self.__price = price
        self.quantity = quantity


class Child(Parent):
    def __init__(self, name: str, price: float, quantity=0, broken_phones=0):
        # Call to super function to have access to all attributes / methods
        super().__init__(
            name, price, quantity
        )

        # Run validations to the received arguments
        assert broken_phones >= 0, f"Broken Phones {broken_phones} is not greater or equal to zero!"

        # Assign to self object
        self.broken_phones = broken_phones
```

## Polymorphism

The ability for objects of different classes to be treated as objects of a common superclass, enabling methods to be invoked dynamically based on the type of object.

```python
class Shape:
    def draw(self):
        return "Draw Shape"

class Circle(Shape):
    def draw(self):
        return "Draw Circle"

class Square(Shape):
    def draw(self):
        return "Draw Square"
```

## Encapsulation

The process of hiding complex implementation details and exposing only the essential features of an object, making it easier to understand and use.

```python
class Example:
    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name = value
```

## Abstraction

The bundling of data and methods within a class, restricting access to the internal state of an object and promoting data integrity by controlling how data is accessed and modified.

```python
class Example:
    def __private_method(self):
        return

    def public_method(self):
        self.__private_method()
        return
```
