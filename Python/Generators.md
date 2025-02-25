# Generators

## Generator Functions

```python
def squares(length):
    for n in range(length):
        yield n ** 2
```

## Generator Expressions

```python
squares = (n** 2 for n in range(5))
```
