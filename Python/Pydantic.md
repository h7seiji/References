# Pydantic

## Field Customization

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(default="Unknown", max_length=100, description="Name of the item")
```

## Validators with `pre` and `post`

Sanitize data before validation or modify it after validation.

```python
from pydantic import BaseModel, validator

class TextModel(BaseModel):

    text: str

    @validator('text', pre=True)
    def sanitize_string(cls, value):
        return value.strip()

    @validator('text', post=True)
    def to_uppercase(cls, value):
        return value.upper()
```

## Root Validator

Allow for validation against the entire model, handy for inter-field consistency checks.

```python
from pydantic import BaseModel, root_validator

class Coordinate(BaseModel):

    x: float
    y: float

    @root_validator
    def check_coordinates(cls, values):
        x, y = values.get('x'), values.get('y')
        if x == y:
            raise ValueError('x and y cannot be the same.')
        return values
```

## Recursive Models

Design models that refer to themselves.

```python
from typing import List

class Comment(BaseModel):
    text: str
    replies: List['Comment'] = []

Comment.update_forward_refs()
```

## Dynamic Model Creation

```python
from pydantic import create_model

fields = {'name': (str, ...), 'age': (int, ...)}
DynamicUser = create_model('DynamicUser', **fields)
```

## Aliases

Good for non-Pythonic field names coming in from an API.

```python
from pydantic import BaseModel

class User(BaseModel):
    username: str = Field(alias='user-name')
```

## Generic Models

```python
from pydantic.generics import GenericModel
from typing import TypeVar

T = TypeVar('T')

class Wrapper(GenericModel, Generic[T]):
    content: T
```

## Settings Management

Manage app configurations sourced from environment variables, config files, and more.

```python
from pydantic import BaseSettings

class AppConfig(BaseSettings):

    app_name: str = "MyApp"
    debug: bool = False

    class Config:
        env_file = ".env"
```

## JSON Serialization Customization

```python
from pydantic import BaseModel, Field

class Fruit(BaseModel):

    name: str
    taste: str = Field(alias='flavor')

    class Config:
        json_encoders = {str: lambda v: v.upper()}
```

## Computed Fields

Compute model fields dynamically from other fields without any manual intervention.

```python
from pydantic import BaseModel

class FullName(BaseModel):

    first_name: str
    last_name: str

    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```
