# Pytest

Import modules from current directory

```bash
python -m pytest
```

Run only one test

```bash
pytest test_file.py::test_function
```

## Fixtures

```python
# conftest.py
import pytest

@pytest.fixture
def db_connection():
  yield
```

```python
# test_example.py
def test_db_connection(db_connection):
  assert True
```

## Monkeypatching

```python
def test_mytest(monkeypatch):
  monkeypatch.setattr(app_onboarding, "username_moderation", mock_moderation)
```
