# Functions

- Functions in Python are first-class citizens. That means you can work with functions as you would with any other variable. You can pass them as arguments to other functions, return them from functions, and even store them in variables.
- Functions are objects. Objects are instances of classes and contain methods and attributes.

## Arguments

### Default Arguments

```python
def greet(name, age=30):
    print(f"Hello, {name}. You are {age} years old.")

greet("John")

# Output: Hello, John. You are 30 years old.
```

#### Mutable Default Arguments

The default argument is only evaluated once, when the function is defined.

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item("apple"))    # ["apple"]
print(add_item("orange"))   # ["apple", "orange"]
```

### *args **kwargs

*args is used to pass a variable number of non-keyword arguments to a function.

**kwargs is used to pass a variable number of keyword arguments to a function.

Note: we don't need to use args and kwargs for the names, it is just convention.

```python
def add_numbers(*numbers):
    result = 0
    for number in numbers:
        result += number
    return result
print(add_numbers(1, 2, 3, 4, 5))

def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")
print_info(name="John", age=25, city="New York")
```

### Unpacking Arguments

```python
def greet(name, age):
    print(f"Hello, {name}. You are {age} years old.")

person = ("John", 25)
greet(*person)
```

## Lambda functions

## Decorators

```python
def my_logger(fun):
    def _inner_decorator(*args, **kwargs):
        print(f'{fun.__name__} is being called!')
        return fun(*args, **kwargs)

    return _inner_decorator

@my_logger
def my_function(n):
    return sum(range(n))

print(my_function(5))
# my_function is being called!
# 10
```

## Generators

### Creating Python Generators

1. Start with a Function
2. Yield, not Return
3. Call the Function
4. Loop over the Generator

### When to Use Generators

- Large Datasets: Process without consuming all memory.
- Streaming Data: Handle real-time data streams effectively.
- Expensive Computations: Compute values lazily, only when needed.
- Infinite Sequences: Produce values indefinitely.
- Pipeline Processing: Reduce memory in data processing chains.

### When Generators Might Not Be Ideal

- Random Access: Generators are linear, not for indexed access.
- Multiple Passes: Generators exhaust after one use; not for re-traversing.
- Short Data Sequences: Overkill for small, in-memory datasets.
- Complex State Management: This can lead to confusing code.
- Performance-Critical: Might introduce minor speed overheads.

### Generator Methods

#### next()

```python
def counter():
    i = 0
    while True:
        received = yield i
        if received is not None:
            i = received
        else:
            i += 1

gen = counter()

output1 = next(gen)  # This should output 0
output2 = next(gen)  # This should output 1
```

#### send()

```python
# Let's evaluate the output of the provided code using the counter generator
def counter():
    i = 0
    while True:
        received = yield i
        if received is not None:
            i = received
        else:
            i += 1

# Creating a generator instance
gen = counter()

# Evaluating the output
output1 = next(gen)  # This should output 0
output2 = gen.send(5)  # This should output 5
output3 = next(gen)  # This should output 6

output1, output2, output3
```

#### throw()

```python
class FraudDetected(Exception):
    pass

def transaction_processor():
    fraudulent_transactions = []  # List to store flagged transactions

    while True:
        try:
            transaction = yield
            # Process the transaction normally
        except FraudDetected as e:
            # Only print the fraud alert, no other output
            print(f"Fraud alert: {e}")
            fraudulent_transactions.append(transaction)  # Add to fraudulent transactions
        except GeneratorExit:
            return fraudulent_transactions  # Return the list when generator is closed

# Create and initialize the generator
processor = transaction_processor()
next(processor)  # Start the generator

# Process transactions and use throw() to simulate a fraud alert
fraudulent_list = []
try:
    for _, row in df.iterrows():
        transaction = row.to_dict()
        if transaction['Amount'] > 2000:
            # Simulate a fraud detection using throw()
            processor.throw(FraudDetected, f"Suspicious transaction detected: ${transaction['Amount']}")
        else:
            processor.send(transaction)
except StopIteration as e:
    fraudulent_list = e.value  # Capture the list of fraudulent transactions

# Close the generator
processor.close()
```

#### close()

```python
def sensor_data_monitor():
    try:
        while True:
            sensor_data = yield
            # Process sensor data
            print(f"Processing sensor data: {sensor_data}")
    except GeneratorExit:
        print("Sensor monitoring stopped. Performing cleanup.")
        # Add any necessary cleanup actions here

# Example Usage
monitor = sensor_data_monitor()
next(monitor)  # Start the generator

# Simulate receiving data
monitor.send({"temperature": 22, "humidity": 45})
monitor.send({"temperature": 23, "humidity": 50})

# Signal to stop monitoring
monitor.close()  # Close the generator
```
