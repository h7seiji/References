# Coding Interview Tips

https://www.techinterviewhandbook.org/coding-interview-prep/

## Criteria

- Communication - Asking clarifying questions, communication of approach and tradeoffs clearly such that the interviewer has no trouble following.
- Problem solving - Understanding the problem and approaching it systemically, logically and accurately, discussing multiple potential approaches and tradeoffs. Ability to accurately determine time and space complexity and optimize them.
- Technical competency - Translating discussed solutions to working code with no significant struggle. Clean, correct implementation with strong knowledge of language constructs.
- Testing - Ability to test code against normal and corner cases, self-correcting issues in code.

## Steps During Interview

1. Make a good self introduction at the start of the interview
   - Introduce yourself in a few sentences under a minute or 2.
   - Sound enthusiastic!
2. Upon receiving the question, make clarifications
   - Paraphrase and repeat the question back at the interviewer.
   - Clarify assumptions.
   - Clarify input value range.
   - Clarify input value format.
   - Work through a simplified example to ensure you understood the question.
3. Work out and optimize your approach with the interviewer
   - Explain a few approaches that you could take at a high level. Discuss the tradeoffs of each approach with your interviewer as if the interviewer was your coworker and you all are collaborating on a problem.
   - State and explain the time and space complexity of your proposed approach(es).
   - Agree on the most ideal approach and optimize it. Identify repeated/duplicated/overlapping computations and reduce them via caching.
4. Code out your solution while talking through it.
   - Only start coding after you have explained your approach and the interviewer has given you the green light.
   - Explain what you are trying to achieve as you are coding / writing. Compare different coding approaches where relevant.
   - Code / write at a reasonable speed so you can talk through it - but not too slow.
   - Write actual compilable, working code where possible, not pseudocode.
   - Write clean, straightforward and neat code with as few syntax errors / bugs as possible.
   - Use variable names that explain your code.
   - Ask for permission to use trivial functions without having to implement them.
   - Write in a modular fashion, going from higher-level functions and breaking them down into smaller helper functions.
   - If you are cutting corners in your code, state that out loud to your interviewer and say what you would do in a non-interview setting (no time constraints).
5. After coding, check your code and add test cases
   - Scan through your code for mistakes - such as off-by-one errors.
   - Brainstorm edge cases with the interviewer and add additional test cases.
   - Step through your code with those test cases.
   - Look out for places where you can refactor.
   - Reiterate the time and space complexity of your code.
   - Explain trade-offs and how the code / approach can be improved if given more time.
6. At the end of the interview, leave a good impression
   - Ask good final questions that are tailored to the company.
   - Thank the interviewer.

## Techniques to solve problems

1. Visualize the problem by drawing it out
2. Think about how you would solve the problem by hand
3. Come up with more examples
4. Break the question down into smaller independent parts
5. Apply common data structures and algorithms at the problem
   - Hash Maps: Useful for making lookup efficient. This is the most common data structure used in interviews and you are guaranteed to have to use it.
   - Graphs: If the data is presented to you as associations between entities, you might be able to model the question as a graph and use some common graph algorithm to solve the problem.
   - Stack and Queue: If you need to parse a string with nested properties (such as a mathematical equation), you will almost definitely need to use stacks.
   - Heap: Question involves scheduling/ordering based on some priority. Also useful for finding the max K/min K/median elements in a set.
   - Tree/Trie: Do you need to store strings in a space-efficient manner and look for the existence of strings (or at least part of them) very quickly?
   - Routines:
     - Sorting
     - Binary search: Useful if the input array is sorted and you need to do faster than O(n) searches
     - Sliding window
     - Two pointers
     - Union find
     - BFS/DFS
     - Traverse from the back
     - Topological Sorting

## Optimizing solutions

### How to optimize time complexity

1. Identify the Best Theoretical Time Complexity of the solution
2. Identify overlapping and repeated computation
3. Try different data structures
4. Identify redundant work

### How to optimize space complexity

1. Changing data in-place/overwriting input data
2. Change a data structure

## Coding Patterns

https://levelup.gitconnected.com/dont-just-leetcode-follow-the-coding-patterns-instead-4beb6a197fdb

- Sliding Window: When we need to handle the input data in a specific window size
- Islands (Matrix Traversal): Describes all the efficient ways of traversing a matrix (or 2D array)
- Two Pointers: Uses two pointers to iterate input data. Generally, both pointers move in the opposite direction at a constant interval
- Fast & Slow Pointers: Uses two pointers that traverse the input data at different speeds
- Merge Intervals: Used to deal with overlapping intervals
- Cyclic Sort: Used to solve array problems where the input data lies within a fixed range
- In-place Reversal of a LinkedList: Describes an efficient way to reverse the links between a set of nodes of a LinkedList. Often, the constraint is that we need to do this in-place
- Tree Breadth-First Search: Used to solve problems involving traversing trees or graphs in a breadth-first search manner
- Tree Depth First Search: Used to solve problems involving traversing trees or graphs in a depth-first search manner
- Two Heaps: We are given a set of elements that can be divided into two parts. We are interested in knowing the smallest element in one part and the biggest element in the other part. This technique uses a Min-Heap to find the smallest element and a Max-Heap to find the biggest element
- Subsets: Used when the problem asks to deal with permutations or combinations of a set of elements
- Modified Binary Search: Used to search a sorted set of elements efficiently
- Bitwise XOR: Uses the XOR operator to manipulate bits to solve problems
- Top ‘K’ Elements: Used to find top/smallest/frequently occurring 'K' elements in a set
- K-way Merge: Helps us solve problems that involve a list of sorted arrays
- Topological Sort: Used to find a linear ordering of elements that have dependencies on each other
- 0/1 Knapsack: Used to solve optimization problems. Use this technique to select elements that give maximum profit from a given set with a limitation on capacity and that each element can only be picked once
- Fibonacci Numbers: Used to solve problems that follow the Fibonacci numbers sequence
- Palindromic Subsequence: Used to solve optimization problems related to palindromic sequences or strings
- Longest Common Substring: Used to find the optimal part of a string/sequence or set of strings/sequences
