# Array

## Time complexity

- Access: O(1)
- Search: O(n)
- Search (sorted array): O(log(n))
- Insert: O(n)
- Insert (at the end): O(1)
- Remove: O(n)
- Remove (at the end): O(1)

## Techniques

- Sliding window
- Two pointers
- Traversing from the right
- Sorting the array
- Precomputation
- Index as a hash key
- Traversing the array more than once

## Things to look out for

- Clarify if there are duplicate values in the array. Would the presence of duplicate values affect the answer? Does it make the question simpler or harder?
- When using an index to iterate through array elements, be careful not to go out of bounds.
- Be mindful about slicing or concatenating arrays in your code. Typically, slicing and concatenating arrays would take O(n) time. Use start and end indices to demarcate a subarray/range where possible.

## Corner cases

- Empty sequence
- Sequence with 1 or 2 elements
- Sequence with repeated elements
- Duplicated values in the sequence
