# Libraries

## Standard Libraries

### collections

- namedtuple

```python
from collections import namedtuple

# Define a namedtuple
Person = namedtuple('Person', ['name', 'age', 'gender'])

# Create an instance
john = Person(name='John Doe', age=30, gender='Male')

print(john.name)  # Output: John Doe
```

- deque

```python
from collections import deque

d = deque('ghi')
d.append('j')        # add to the right
d.appendleft('f')    # add to the left
d.pop()              # remove from the right
d.popleft()          # remove from the left
```

- Counter

```python
from collections import Counter

c = Counter('abracadabra')
print(c)  # Output: Counter({'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1})
```

- OrderedDict

```python
from collections import OrderedDict

od = OrderedDict()
od['a'] = 1
od['b'] = 2
od['c'] = 3
print(od)  # Output: OrderedDict([('a', 1), ('b', 2), ('c', 3)])
```

- defaultdict

```python
from collections import defaultdict

dd = defaultdict(int)
dd['key_not_exist'] += 1
print(dd)  # Output: defaultdict(<class 'int'>, {'key_not_exist': 1})
```

- ChainMap

```python
from collections import ChainMap

dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}
combined = ChainMap(dict1, dict2)
print(combined['b'])  # Output: 2
```

### itertools

- count

```python
from itertools import count

for i in count(10):
    if i > 15:
        break
    print(i)

# Output:
# 10
# 11
# 12
# 13
# 14
# 15
```

- cycle

```python
from itertools import cycle

counter = 0
for item in cycle('ABC'):
    if counter > 5:
        break
    print(item)
    counter += 1

# Output:
# A
# B
# C
# A
# B
# C
```

- repeat

```python
from itertools import repeat

for _ in repeat('A', 3):
    print(_)

# Output:
# A
# A
# A
```

- chain

```python
from itertools import chain

for char in chain('ABC', 'DEF'):
    print(char)

# Output:
# A
# B
# C
# D
# E
# F
```

- compress

```python
from itertools import compress

data = ['A', 'B', 'C', 'D']
selectors = [True, False, True, False]

result = list(compress(data, selectors))
print(result)  # Output: ['A', 'C']
```

- dropwhile

```python
from itertools import dropwhile

for item in dropwhile(lambda x: x < 5, [1, 4, 6, 4, 1]):
    print(item)

# Output:
# 6
# 4
# 1
```

- takewhile

```python
from itertools import takewhile

for item in takewhile(lambda x: x < 5, [1, 4, 6, 4, 1]):
    print(item)

# Output:
# 1
# 4
```

- permutations

```python
from itertools import permutations

for p in permutations('AB'):
    print(p)

# Output:
# ('A', 'B')
# ('B', 'A')
```

- combinations

```python
from itertools import combinations

for combo in combinations('ABC', 2):
    print(combo)

# Output:
# ('A', 'B')
# ('A', 'C')
# ('B', 'C')
```

### functools

- lru_cache

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```

- cache

```python
from functools import cache

@cache
def factorial(n):
    return n * factorial(n-1) if n else 1
```

- cached_property

```python
from functools import cached_property

class Circle:
    def __init__(self, radius):
        self.radius = radius

    @cached_property
    def area(self):
        print("Calculating area...")
        return 3.14159 * self.radius ** 2
```

- partial

```python
from functools import partial

def multiply(x, y):
    return x * y

double = partial(multiply, 2)
print(double(4))  # Output: 8
```

- reduce

```python
from functools import reduce

def add(x, y):
    return x + y

result = reduce(add, [1, 2, 3, 4, 5])
print(result)  # Output: 15
```

- wraps

```python
from functools import wraps

def my_decorator(f):
    @wraps(f)
    def wrapper(*args, **kwargs):
        print("Before calling the function")
        result = f(*args, **kwargs)
        print("After calling the function")
        return result
    return wrapper

@my_decorator
def say_hello(name):
    """Greet someone."""
    print(f"Hello, {name}!")

print(say_hello.__name__)  # Output: say_hello
print(say_hello.__doc__)  # Output: Greet someone.
```

- singledispatch

```python
from functools import singledispatch

@singledispatch
def fun(arg, verbose=False):
    if verbose:
        print("Let me just say,", end=" ")
    print(arg)

@fun.register(int)
def _(arg, verbose=False):
    if verbose:
        print("Strength in numbers, eh?", end=" ")
    print(arg)

@fun.register(list)
def _(arg, verbose=False):
    if verbose:
        print("Enumerate this:")
    for i, elem in enumerate(arg):
        print(i, elem)

fun("Hello, world!")
fun([1, 2, 3], verbose=True)

# Output:
# Hello, world!
# Enumerate this:
# 0 1
# 1 2
# 2 3
```

### operator

- itemgetter

```python
from operator import itemgetter

pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
pairs.sort(key=itemgetter(1))
```

- methodcaller

```python
from operator import methodcaller

s = "The quick brown fox"
upcase = methodcaller('upper')
print(upcase(s))
```

## Third-party

- HTTPX: <https://github.com/encode/httpx>
- Dotenv: <https://saurabh-kumar.com/python-dotenv/>
- FastAPI: <https://fastapi.tiangolo.com/>
- Pydantic: Data validation <https://docs.pydantic.dev/latest/>
- SQLModel: ORM <https://sqlmodel.tiangolo.com/>
- Ruff: Linter and formatter <https://github.com/astral-sh/ruff>
- BeautifulSoup: Web scrapper <https://www.crummy.com/software/BeautifulSoup/>
- Pendulum: Datetimes made easy <https://pendulum.eustace.io/>
- Icecream: Print for dubgging <https://github.com/gruns/icecream>
- Loguru: Logging <https://github.com/Delgan/loguru>
- Seaborn: Statistical data visualization <https://github.com/mwaskom/seaborn>
- factory_boy: Create fake data <https://github.com/FactoryBoy/factory_boy>
- hug: Simple API framework <https://github.com/hugapi/hug>
- pyinstrument: Performance profiler <https://github.com/joerick/pyinstrument>
- gevent: Coroutine-based networking library <https://www.gevent.org/>
