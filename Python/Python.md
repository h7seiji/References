# Python

- <https://roadmap.sh/python>
- <https://hlop3z.github.io/interviews-python/>

## Contents

- [Classes](Classes.md)
- [Functions](Functions.md)
- [Typing](Typing.md)
- [Asyncio](Asyncio.md)
- [FastAPI](FastAPI.md)
- [Pytest](Pytest.md)
- [Libraries](Libraries.md)

## The Zen of Python

Beautiful is better than ugly.  
Explicit is better than implicit.  
Simple is better than complex.  
Complex is better than complicated.  
Flat is better than nested.  
Sparse is better than dense.  
Readability counts.  
Special cases aren't special enough to break the rules.  
Although practicality beats purity.  
Errors should never pass silently.  
Unless explicitly silenced.  
In the face of ambiguity, refuse the temptation to guess.  
There should be one-- and preferably only one --obvious way to do it.  
Although that way may not be obvious at first unless you're Dutch.  
Now is better than never.  
Although never is often better than *right* now.  
If the implementation is hard to explain, it's a bad idea.  
If the implementation is easy to explain, it may be a good idea.  
Namespaces are one honking great idea -- let's do more of those!  

## Garbage Collector

- <https://medium.com/@sylvain.tiset/demystifying-garbage-collection-algorithms-8f1ef1061207>

> Everything in Python is an object

Python variables do not actually contain the data; it is just the container holding address (pointer) which points to the location of the actual data object (in heap memory)

For a better way to think, variables are labels with names attached to objects.

The process of garbage-collector automatically runs in the background.

You can also manually control this process using the GC module if needed.

### Reference Counting (CPython)

Essentially, each object keeps count of how many references point to it. The object will be garbage-collected as soon as that ref count reaches zero.

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

## pyenv

- <https://github.com/pyenv/pyenv>
- <https://github.com/pyenv-win/pyenv-win>

```bash
pyenv update
pyenv install 3.13.0
pyenv global 3.13.0
```

## venv

```bash
python -m venv .venv

.venv\Scripts\Activate.ps1 # PowerShell
.venv\Scripts\activate.bat # WINDOWS
source .venv/bin/activate # LINUX/MAC
```

## List x Tuple x Set

- Duplicates: a Set cannot contain duplicates
- Sorting Order: Lists and Tuples are ordered sequences of objects
- Mutability: Tuples are immutable. We can only add elements to a Set
- Indexing: Tuple and List support indexing and slicing, while Set does not

### When to use List vs. Tuple?

#### Use List

- When you need to mutate your collection
- When you need to remove or add new items to your collection of items

#### Use Tuple

- If your data should or does not need to be changed
- Tuples are faster than lists. We should use a Tuple instead of a List if we are defining a constant set of values and all we are ever going to do with it is iterate through it
- If we need an array of elements to be used as dictionary keys, we can use Tuples. As Lists are mutable (unhashable type), they can never be used as dictionary keys

### When to use Set vs. List/Tuple?

As Set uses Hash Table as its underlying data structure, Set is blazingly fast when it comes to checking if an element is inside it.

Essentially, if you do not need to store duplicates, Set is going to be better than List.

## List Comprehension

- <https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions>

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

## Useful code excerpts

- Find first occurence in a list of Dictionaries

```python
result = next((item for item in data if item["key"] == value), None)
```
