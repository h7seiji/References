# Math

## Things to look out for

- If code involves division or modulo, remember to check for division or modulo by 0 case.
- Check for and handle overflow/underflow if you are using a typed language like Java and C++. At the very least, mention that overflow/underflow is possible and ask whether you need to handle it.
- Consider negative numbers and floating point numbers. This may sound obvious, but under interview pressure, many obvious cases go unnoticed.

## Corner cases

- Division by 0
- Multiplication by 1
- Negative numbers
- Floats

## Common formulas

- Check if a number is even: num % 2 == 0
- Sum of 1 to N: 1 + 2 + ... + (N - 1) + N = (N+1) \* N/2
- Sum of Geometric Progression: 20 + 21 + 22 + 23 + ... 2n = 2n+1 - 1
- Permutations of N: N! / (N-K)!
- Combinations of N: N! / (K! \* (N-K)!)

## Techniques

- Multiples of a number

  - When a question involves "whether a number is a multiple of X", the modulo operator would be useful.

- Comparing floats

  - When dealing with floating point numbers, take note of rounding mistakes. Consider using epsilon comparisons instead of equality checks. E.g. abs(x - y) <= 1e-6 instead of x == y.

- Fast operators
  - If the question asks you to implement an operator such as power, square root or division and want it to be faster than O(n), some sort of doubling (fast exponentiation) or halving (binary search) is usually the approach to go. Examples: Pow(x, n), Sqrt(x)
