# Algorithms Interview Tips

- https://www.youtube.com/user/mycodeschool

## Algorithms

- Recursion

  - Applications of Recursion: Tree and Graph Traversal, Towers of Hanoi, Divide and Conquer Algorithms, Merge Sort, Quick Sort, and Binary Search.

- DFS and BFS - Tree and Graphs Traversal

  - Basis for more complex algorithms like Djikstra

- Binary Search

  - Given sorted array search for a value
  - Get middle value in array, compare, then repeat on half of the array

- Sliding Window

  - Find Subarray or Substring

- Two Pointers:

  - Start/End - Searching pairs in a sorted array - Ex: Find if there exists any pair of elements in a sorted list such that their sum is equal to X. We take two pointers, one representing the first element and other representing the last element of the array, and then we add the values kept at both the pointers. If their sum is smaller than X then we shift the left pointer to right or if their sum is greater than X then we shift the right pointer to left, in order to get closer to the sum. We keep moving the pointers until we get the sum as X.

  - Fast/Slow - Ex: Find circle in Linked List. We have two pointers at the head of the list and move the slow pointer by one node and the fast by two nodes; if they reach the end (one node pointing to nil), there is no circle; if they meet, there is a circle.

- Backtracking

  - Find a solution incrementally by trying different options and undoing them if they lead to a dead end
  - Application of Backtracking: N Queen problem, Rat in a Maze problem, Knight’s Tour Problem, Sudoku solver, and Graph coloring problems.

- Divide and Conquer

  - Divide: This involves dividing the problem into smaller sub-problems.
  - Conquer: Solve sub-problems by calling recursively until solved.
  - Combine: Combine the sub-problems to get the final solution of the whole problem.

- Merge Sort

  - Divide the array into two halves, sort each half, and then merge the sorted halves back together

- Dynamic Programming

- Kadane

  - Maximum Subarray
  - O(n)
  - If we encounter a subarray with a negative sum, we discard it and we keep considering a subarray as long as it has a positive sum.

### Graph Algorithms

- DFS

- BFS

- Union Find

- Topological Sort

- Djikstra (Shortest path)

- Kruskal (Minimum Spanning Tree)

### Sorting Algorithms

- Quick Sort

- Merge Sort

- Bubble Sort

- Selection Sort

- Insertion Sort
