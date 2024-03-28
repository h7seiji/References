# Python

## Contents

- [Classes](Classes.md)
- [Functions](Functions.md)
- [Typing](Typing.md)
- [Asyncio](Asyncio.md)
- [FastAPI](FastAPI.md)
- [Pytest](Pytest.md)
- [Libraries](Libraries.md)

## Other

- Cheat Sheet <https://medium.com/@roelljr/ultimate-python-cheat-sheet-practical-python-for-everyday-tasks-c267c1394ee8>
- <https://github.com/cjolowicz/cookiecutter-hypermodern-python>
- <https://mitelman.engineering/blog/python-best-practice/automating-python-best-practices-for-a-new-project/>
- <https://blog.stackademic.com/20-python-concepts-i-wish-i-knew-way-earlier-40ed5674cd52>
  - Map, Filter, Reduce
  - Type Hinting
  - Context Managers
  - Walrus Operator
  - Namedtuples
  - enumerate
  - Zipping and Unzipping Lists
  - Dictionaries — get() and setdefault()
  - The **main** Guard
  - Virtual Environments
  - The Asterisk (\*) Operator
  - The `else` Clause in Loops
  - Deepcopy vs. Shallow Copy
  - Python's Underscore (\_) Uses
- Walrus Operator <https://betterprogramming.pub/should-you-be-using-pythons-walrus-operator-yes-and-here-s-why-36297be16907>
- Data Structures <https://www.deriveit.org/coding/cheat-sheets/87>
- BitwiseOperators <https://wiki.python.org/moin/BitwiseOperators>
- Exception Handling <https://medium.com/@saadjamilakhtar/5-best-practices-for-python-exception-handling-5e54b876a20>
- Cheatsheet <https://dranolia.medium.com/python-cheatsheet-51b552b56a81>

## venv

```bash
python -m venv env-name

.\env-name\Scripts\Activate.ps1
```

## List Comprehension

- <https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions>

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

## Threading

## Multiprocessing

Divide tasks written in python over multiple processes to help improve performance

- Multi-core

## Subprocess

Run and control other programs

- <https://www.datacamp.com/tutorial/python-subprocess>

## Frozenset

Use set as a dict key

```python
set_ex = frozenset({1, 2, 3})
dict_obj = {set_ex: "This is a Set"}

print(dict_obj[set_ex])
## Output - This is a Set
```

## Bytecode

- `dis` library
- <https://opensource.com/article/18/4/introduction-python-bytecode>
- <https://medium.com/@noransaber685/demystifying-python-bytecode-a-guide-to-understanding-and-analyzing-code-execution-6a163cb83bd1>
- <https://medium.com/@yonatanzunger/advanced-python-achieving-high-performance-with-code-generation-796b177ec79>
