# Design Patterns

## Creational Patterns (object creation)

- Singleton → Ensure only one instance exists.
- Factory / Factory Method / Abstract Factory → Create objects without specifying exact classes.
- Builder → Step-by-step construction of complex objects.
- Prototype → Create new objects by copying existing ones.

## Structural Patterns (object composition)

- Adapter → Make one interface compatible with another.
- Decorator → Dynamically add behavior to objects.
- Facade → Simplify a complex subsystem behind a single interface.
- Composite → Treat individual objects and compositions uniformly.
- Proxy → Control access to another object.

## Behavioral Patterns (object interaction)

- Strategy → Encapsulate interchangeable behaviors.
- Observer → Notify multiple objects of state changes.
- Command → Encapsulate requests as objects.
- Iterator → Access elements sequentially without exposing internal structure.
- Template Method → Define skeleton of an algorithm, let subclasses override steps.
- State → Change behavior when object state changes.
- Chain of Responsibility → Pass a request along a chain of handlers.

## Factory

Instead of directly instantiating the classes, we create a factory that decides which class to instantiate.
This way, your code depends only on the factory, not on all possible classes.

```python
class VehicleFactory:
    @staticmethod
    def create_vehicle(vehicle_type):
        if vehicle_type == "car":
            return Car("Toyota", "Corolla")
        elif vehicle_type == "motorcycle":
            return Motorcycle("Yamaha", "R1")
        elif vehicle_type == "boat":
            return Boat()
        else:
            raise ValueError("Unknown vehicle type")

vehicle = VehicleFactory.create_vehicle("car")
print(vehicle)     # Toyota Corolla
vehicle.drive()    # Engine starting... Toyota Corolla is now driving!
```

## Strategy

- You define an interface (PaymentProcessor).
- Implement multiple strategies (CreditCardPayment, PayPalPayment, etc).
- At runtime, you can swap strategies without changing the Trip logic.

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount: float):
        pass

class CreditCardPayment(PaymentProcessor):
    def pay(self, amount: float):
        print(f"💳 Processing Credit Card payment of ${amount}...")
        
class PayPalPayment(PaymentProcessor):
    def pay(self, amount: float):
        print(f"💻 Processing PayPal payment of ${amount}...")
        
class CryptoPayment(PaymentProcessor):
    def pay(self, amount: float):
        print(f"🪙 Processing Crypto payment of ${amount}...")

class Trip:
    def __init__(self, payment_strategy: PaymentProcessor):
        self.payment_strategy = payment_strategy  # inject the strategy
        
    def start(self, amount: float):
        self.payment_strategy.pay(amount)

# Choose strategy at runtime
payment_method = PayPalPayment()

trip = Trip(payment_method)
trip.start(42.50)

# Switch strategy without touching Trip
trip.payment_strategy = CryptoPayment()
trip.start(30.00)
```

## Singleton

- Ensure that a class has only one instance and provide a global point of access to it.
- Common use cases: configuration managers, logging systems, database connections, thread pools.

```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super().__new__(cls)
        return cls._instance

# Usage
s1 = Singleton()
s2 = Singleton()

print(s1 is s2)  # True
```

```python
def singleton(cls):
    instances = {}
    def wrapper(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return wrapper

@singleton
class Logger:
    def log(self, message):
        print(f"LOG: {message}")

# Usage
logger1 = Logger()
logger2 = Logger()
print(logger1 is logger2)  # True
logger1.log("Singleton works!")
```

## Decorator

- Add new responsibilities to objects dynamically, without modifying their structure.
- It’s like wrapping a gift → the gift stays the same, but the wrapper adds extra behavior.

```python
class Car:
    def drive(self):
        return "Driving a car"

# Base Decorator
class CarDecorator(Car):
    def __init__(self, car: Car):
        self._car = car

    def drive(self):
        return self._car.drive()

# Concrete Decorators
class GPSDecorator(CarDecorator):
    def drive(self):
        return f"{super().drive()} with GPS"

class HeatedSeatsDecorator(CarDecorator):
    def drive(self):
        return f"{super().drive()} with Heated Seats"

# Usage
car = Car()
car_with_gps = GPSDecorator(car)
car_with_gps_and_seats = HeatedSeatsDecorator(car_with_gps)

print(car.drive())  # Driving a car
print(car_with_gps.drive())  # Driving a car with GPS
print(car_with_gps_and_seats.drive())  # Driving a car with GPS with Heated Seats
```

```python
import functools

def log_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}...")
        result = func(*args, **kwargs)
        print(f"{func.__name__} finished.")
        return result
    return wrapper

@log_decorator
def process_data(data):
    print(f"Processing {data}")

process_data("vehicle info")
```

## Observer

- Defines a one-to-many relationship between objects.
- When the subject (a.k.a. observable) changes, all its observers (listeners/subscribers) are notified automatically.
- Think: You subscribe to a YouTube channel → every time they upload, you get notified.

```python
from abc import ABC, abstractmethod

# Observer Interface
class Observer(ABC):
    @abstractmethod
    def update(self, message: str):
        pass

# Concrete Observers
class Driver(Observer):
    def __init__(self, name):
        self.name = name

    def update(self, message: str):
        print(f"Driver {self.name} received update: {message}")

class Mechanic(Observer):
    def __init__(self, name):
        self.name = name

    def update(self, message: str):
        print(f"Mechanic {self.name} received update: {message}")

# Subject (Observable)
class VehicleTracker:
    def __init__(self):
        self._observers = []

    def attach(self, observer: Observer):
        self._observers.append(observer)

    def detach(self, observer: Observer):
        self._observers.remove(observer)

    def notify(self, message: str):
        for observer in self._observers:
            observer.update(message)

# Usage
tracker = VehicleTracker()

driver = Driver("Alice")
mechanic = Mechanic("Bob")

tracker.attach(driver)
tracker.attach(mechanic)

tracker.notify("Vehicle speed exceeded limit!")
```
