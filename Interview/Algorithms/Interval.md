# Interval

Interval questions are a subset of array questions where you are given an array of two-element arrays (an interval) and the two values represent a start and an end value.

## Things to look out for

- Clarify with the interviewer whether [1, 2] and [2, 3] are considered overlapping intervals as it affects how you will write your equality checks.
- Clarify whether an interval of [a, b] will strictly follow a < b (a is smaller than b)

## Corner cases

- No intervals
- Single interval
- Two intervals
- Non-overlapping intervals
- An interval totally consumed within another interval
- Duplicate intervals (exactly the same start and end)
- Intervals which start right where another interval ends - [[1, 2], [2, 3]]

## Techniques

- Sort the array of intervals by its starting point
- Checking if two intervals overlap:

```
def is_overlap(a, b):
  return a[0] < b[1] and b[0] < a[1]
```

- Merging two intervals

```
def merge_overlapping_intervals(a, b):
  return [min(a[0], b[0]), max(a[1], b[1])]
```
