# OOP

## Inheritance

```
Class Parent:
    def __init__(self, name: str, price: float, quantity=0):
        # Run validations to the received arguments
        assert price >= 0, f"Price {price} is not greater than or equal to zero!"
        assert quantity >= 0, f"Quantity {quantity} is not greater or equal to zero!"

        # Assign to self object
        self.__name = name
        self.__price = price
        self.quantity = quantity


Class Child(Parent):
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

```
Class Shape:
    def draw(self):
        return "Draw Shape"

Class Circle(Shape):
    def draw(self):
        return "Draw Circle"

Class Square(Shape):
    def draw(self):
        return "Draw Square"
```

## Encapsulation

```
Class Example:
    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name = value
```

## Abstraction

```
Class Example:
    def __private_method(self):
        return

    def public_method(self):
        self.__private_method()
        return
```
