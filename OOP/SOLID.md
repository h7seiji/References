# SOLID

- <https://akhileshmj.medium.com/solid-principles-go-design-pattern-6af77d665b8e>
- <https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898>

## Single Responsibility Principle (SRP)

- A class should have only one reason to change. In other words, it should do one thing, and do it well.
- If a class is doing multiple unrelated things, changes in one feature might break another.
- SRP makes classes easier to maintain, test, and extend.

### Example (violating SRP)

```python
class VehicleManager:
    def __init__(self, vehicle):
        self.vehicle = vehicle

    def drive_vehicle(self):
        print(f"{self.vehicle} is driving")

    def save_to_database(self):
        print(f"{self.vehicle} saved to DB")
```

Problem:

- VehicleManager has two responsibilities:
  - Driving the vehicle
  - Persisting it to a database

If database logic changes, VehicleManager changes unnecessarily.

### Example (following SRP)

```python
class VehicleDriver:
    def drive(self, vehicle):
        print(f"{vehicle} is driving")

class VehicleRepository:
    def save(self, vehicle):
        print(f"{vehicle} saved to DB")
```

- VehicleDriver handles driving.
- VehicleRepository handles persistence.
- Changes in one area don’t affect the other.

### Benefits of SRP

- Code is modular
- Easier to test
- Easier to extend

## Open/Closed Principle (OCP)

- A class should be open for extension, but closed for modification.
- This means you can add new functionality without changing existing code.
- Helps prevent introducing bugs in code that’s already working.

### Example (violating OCP)

```python
class Vehicle:
    def drive(self):
        print("Driving vehicle")

class VehicleManager:
    def drive_vehicle(self, vehicle):
        if isinstance(vehicle, Car):
            print("Driving car")
        elif isinstance(vehicle, Motorcycle):
            print("Driving motorcycle")
```

Problem:

- Every time you add a new vehicle type, you must modify VehicleManager.
- Violates OCP — code isn’t closed for modification.

### Example (following OCP)

```python
class Vehicle(ABC):
    @abstractmethod
    def drive(self):
        pass

class Car(Vehicle):
    def drive(self):
        print("Driving car")

class Motorcycle(Vehicle):
    def drive(self):
        print("Driving motorcycle")

class VehicleManager:
    def drive_vehicle(self, vehicle: Vehicle):
        vehicle.drive()  # polymorphism handles the type
```

- Now VehicleManager never needs to change.
- Add a new class Truck(Vehicle) → no change to VehicleManager.
- This uses polymorphism to follow OCP.

### Benefits of OCP

- Reduces risk of breaking working code
- Encourages extensible design
- Works nicely with abstract classes and factories

## Liskov Substitution Principle (LSP)

- Objects of a subclass should be usable anywhere the base class is expected, without breaking functionality.
- In other words, a subclass should be a true subtype.
- If substituting breaks behavior or expectations → LSP is violated.

### Violating LSP

```python
class Vehicle:
    def drive(self):
        print("Driving vehicle")

class Car(Vehicle):
    def drive(self):
        print("Driving car")

class Boat(Vehicle):
    def drive(self):
        raise NotImplementedError("Boats can’t drive on roads!")
```

Problem:

- A Boat is not substitutable for a Vehicle in all cases.

### Following LSP

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def move(self):
        pass

class Car(Vehicle):
    def move(self):
        print("Car driving on the road")

class Boat(Vehicle):
    def move(self):
        print("Boat sailing in the water")
```

- Now both Car and Boat respect the contract (move).
- They can be used interchangeably without unexpected behavior.

## Interface Segregation Principle (ISP)

- Clients (classes using an interface/abstract class) should not be forced to depend on methods they don’t use.
- Instead of one large interface, break it into smaller, specific ones.

### Violating ISP

```python
from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self):
        pass
    
    @abstractmethod
    def eat(self):
        pass

class Robot(Worker):
    def work(self):
        print("Robot working hard!")
        
    def eat(self):
        raise NotImplementedError("Robots don’t eat!")
```

Problem:

- Robot is forced to implement eat(), even though it doesn’t make sense.
- The interface is too fat.

### Following ISP

```python
from abc import ABC, abstractmethod

class Workable(ABC):
    @abstractmethod
    def work(self):
        pass

class Eatable(ABC):
    @abstractmethod
    def eat(self):
        pass

class Human(Workable, Eatable):
    def work(self):
        print("Human working")
    
    def eat(self):
        print("Human eating")

class Robot(Workable):
    def work(self):
        print("Robot working")
```

- Now Human implements both Workable and Eatable.
- Robot only implements Workable.
- Nobody is forced to implement methods they don’t need.

## Dependency Inversion Principle (DIP)

- High-level modules (business logic) should not depend on low-level modules (details).
- Both should depend on abstractions.
- This makes code flexible, testable, and less coupled.

### Violating DIP

```python
class MySQLDatabase:
    def save(self, data):
        print(f"Saving {data} to MySQL database")

class Report:
    def __init__(self):
        self.db = MySQLDatabase()  # Direct dependency on MySQL

    def generate(self, data):
        self.db.save(data)
```

Problems:

- Report directly depends on MySQLDatabase.
- If you switch to PostgreSQL or a file system, you must change Report.

### Following DIP

```python
from abc import ABC, abstractmethod

# Abstraction
class Database(ABC):
    @abstractmethod
    def save(self, data):
        pass

# Low-level modules
class MySQLDatabase(Database):
    def save(self, data):
        print(f"Saving {data} to MySQL database")

class FileDatabase(Database):
    def save(self, data):
        print(f"Saving {data} to file")

# High-level module depends on abstraction
class Report:
    def __init__(self, db: Database):
        self.db = db  # Inject dependency

    def generate(self, data):
        self.db.save(data)

# Usage
report1 = Report(MySQLDatabase())
report1.generate("Sales Report")

report2 = Report(FileDatabase())
report2.generate("Inventory Report")
```

- Report no longer cares how data is saved.
- You can swap MySQLDatabase → FileDatabase → PostgresDatabase without touching Report.
- Easy to test with a mock database.
