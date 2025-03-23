# Asyncio

- <https://github.com/timofurrer/awesome-asyncio>
- <https://blog.devgenius.io/mastering-asynchronous-programming-in-python-a-comprehensive-guide-ef1e8e5b35db>

```python
import asyncio
import httpx

async def example():
    async with httpx.AsyncClient() as client:
        r = await client.get('https://www.example.com/')

async def main():
    await asyncio.gather(example(), example(), example())

if __name__ == "__main__":
    import time
    s = time.perf_counter()
    asyncio.run(main())
    elapsed = time.perf_counter() - s
    print(f"{__file__} executed in {elapsed:0.2f} seconds.")
```

## Top-Level asyncio Functions

### create_task()

You can use `create_task()` to schedule the execution of a coroutine object, followed by `asyncio.run()`

```python
import asyncio

async def task(name, delay):
    await asyncio.sleep(delay)
    return f"{name} completed"

async def main():
    # Create tasks explicitly
    task1 = asyncio.create_task(task("Task A", 2))
    task2 = asyncio.create_task(task("Task B", 1))
    
    # Process results individually
    result1 = await task1
    result2 = await task2
    
    print(f"Results: {result1}, {result2}")

asyncio.run(main())
```

### gather()

`gather()` is meant to neatly put a collection of coroutines (futures) into a single future.
As a result, it returns a single future object, and, if you `await asyncio.gather()` and specify multiple tasks or coroutines, you’re waiting for all of them to be completed.
The result of `gather()` will be a list of the results across the inputs.

```python
import asyncio

async def task(name, delay):
    await asyncio.sleep(delay)
    return f"{name} completed"

async def main():
    # Create tasks implicitly
    results = await asyncio.gather(
        task("Task A", 2),
        task("Task B", 1)
    )
    
    print(f"Results: {results}")

asyncio.run(main())
```

### as_completed()

You probably noticed that `gather()` waits on the entire result set of the Futures or coroutines that you pass it.
Alternatively, you can loop over `asyncio.as_completed()` to get tasks as they are completed, in the order of completion.
he function returns an iterator that yields tasks as they finish.

```python
import asyncio

async def task(name, delay):
    await asyncio.sleep(delay)
    return f"{name} completed"

async def main():
    tasks = [
        task("Task A", 2),
        task("Task B", 1),
        task("Task C", 3)
    ]
    
    for future in asyncio.as_completed(tasks):
        result = await future
        print(result)

asyncio.run(main())
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

## Theory

### The Rules of Async IO

The syntax `async def` introduces either a native coroutine or an asynchronous generator.
The expressions `async with` and `async for` are also valid.

The keyword `await` passes function control back to the event loop.
It suspends the execution of the surrounding coroutine.
If Python encounters an `await f()` expression in the scope of `g()`, this is how await tells the event loop, “Suspend execution of `g()` until whatever I’m waiting on—the result of `f()`—is returned. In the meantime, go let something else run.”

### Coroutine

A coroutine is a specialized version of a Python generator function.
A coroutine is a function that can suspend its execution before reaching return, and it can indirectly pass control to another coroutine for some time.

### Event Loop

You can think of an event loop as something like a while True loop that monitors coroutines, taking feedback on what's idle, and looking around for things that can be executed in the meantime.
It is able to wake up an idle coroutine when whatever that coroutine is waiting on becomes available.
