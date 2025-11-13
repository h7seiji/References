# Matrix

Questions involving matrices are usually related to dynamic programming or graph traversal.

## Techniques

- Creating an empty N x M matrix
  - For questions involving traversal or dynamic programming, you almost always want to make a copy of the matrix with the same size/dimensions that is initialized to empty values to store the visited state or dynamic programming table.
- Transposing a matrix

## Corner cases

- Empty matrix. Check that none of the arrays are 0 length
- 1 x 1 matrix
- Matrix with only one row or column

## Python

- Copy Matrix:

```python
copied_matrix = [row[:] for row in matrix]
```

- Transpose Matrix:

```python
transposed_matrix = zip(*matrix)
```

- Empty Matrix:

```python
# Assumes that the matrix is non-empty
zero_matrix = [[0 for _ in range(len(matrix[0]))] for _ in range(len(matrix))]
```
