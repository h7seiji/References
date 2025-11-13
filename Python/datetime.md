# datetime library

```python
from datetime import datetime, timedelta

# Current time
now = datetime.now()

# Parse a string to datetime
dt = datetime.fromisoformat("2025-09-16T11:00:00")  # or use strptime()

# Add/subtract time
five_minutes_ago = now - timedelta(minutes=5)
one_second_later = now + timedelta(seconds=1)

# Compare
if event_time >= five_minutes_ago:
    # inside window
    pass

# Get epoch timestamp
epoch = int(now.timestamp())  # seconds since 1970-01-01
```
