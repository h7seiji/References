# Generators

Generators are special functions in Python that can produce a sequence of values over time, rather than computing them all at once and returning them in a list.
They're particularly useful when dealing with large datasets or when you need to generate values on-the-fly.

In a regular function, all values are computed at once and returned as a list.
In contrast, a generator produces values one at a time, preserving its state between each value.
When `next()` is called, execution resumes from where it left off, allowing the generator to remember its previous state.

## Generator Functions

```python
def get_numbers(n):
    for i in range(n):
        yield i

numbers = get_numbers(1000000)
print(next(numbers))  # Prints: 0
print(next(numbers))  # Prints: 1
```

## Generator Expressions

```python
squares = (n** 2 for n in range(5))
```

## Async generators

```python
async def async_generator():
    for i in range(3):
        await asyncio.sleep(1)  # Simulate IO-bound operation
        yield i

async def main():
    async for item in async_generator():
        print(f"Received: {item}")

# Run the program
import asyncio
asyncio.run(main())
```
