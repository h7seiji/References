# Recursion

1. A base case (or cases) defined, which defines when the recursion is stopped - otherwise it will go on forever!
2. Breaking down the problem into smaller subproblems and invoking the recursive call

## Techniques

- Memoization

## Things to look out for

- Always remember to always define a base case so that your recursion will end.
- Recursion is useful for permutation, because it generates all combinations and tree-based questions. You should know how to generate all permutations of a sequence as well as how to handle duplicates.
- Recursion implicitly uses a stack. Hence all recursive approaches can be rewritten iteratively using a stack. Beware of cases where the recursion level goes too deep and causes a stack overflow (the default limit in Python is 1000).
- Number of base cases - In the fibonacci example above, note that one of our recursive calls invoke fib(n - 2). This indicates that you should have 2 base cases defined so that your code covers all possible invocations of the function within the input range. If your recursive function only invokes fn(n - 1), then only one base case is needed.

## Corner cases

- n = 0
- n = 1
- Make sure you have enough base cases to cover all possible invocations of the recursive function
