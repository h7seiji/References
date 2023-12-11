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
