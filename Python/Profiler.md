# Profilers

## profile

```bash
from profilehooks import profile

# stdout=False -> don't print anything in the terminal
# filname -> path to the output file with profiling results
@profile(stdout=False, filename='baseline.prof')
def baseline():
    ...
```

## SnakeViz

<https://github.com/jiffyclub/snakeviz>

## gprof2dot

<https://github.com/jrfonseca/gprof2dot>
