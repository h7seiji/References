# Functions

- Functions in Python are first-class citizens. That means you can work with functions as you would with any other variable. You can pass them as arguments to other functions, return them from functions, and even store them in variables.
- Functions are objects. Objects are instances of classes and contain methods and attributes.

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

## *args **kwargs

## Generators

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
