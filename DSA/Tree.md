# Tree

## Common terms you need to know

- Neighbor - Parent or child of a node
- Ancestor - A node reachable by traversing its parent chain
- Descendant - A node in the node's subtree
- Degree - Number of children of a node
- Degree of a tree - Maximum degree of nodes in the tree
- Distance - Number of edges along the shortest path between two nodes
- Level/Depth - Number of edges along the unique path between a node and the root node
- Width - Number of nodes in a level

## Binary Tree

### Binary tree terms

- Complete binary tree - A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible.
- Balanced binary tree - A binary tree structure in which the left and right subtrees of every node differ in height by no more than 1.

### Traversals

- In-order traversal - Left -> Root -> Right
- Pre-order traversal - Root -> Left -> Right
- Post-order traversal - Left -> Right -> Root

## Binary search tree (BST)

- In-order traversal of a BST will give you all elements in order.
- Be very familiar with the properties of a BST and validating that a binary tree is a BST. This comes up more often than expected.
- When a question involves a BST, the interviewer is usually looking for a solution which runs faster than O(n).

### Time complexity

- Access: O(log(n))
- Search: O(log(n))
- Insert: O(log(n))
- Remove: O(log(n))

## Things to look out for

You should be very familiar with writing pre-order, in-order, and post-order traversal recursively. As an extension, challenge yourself by writing them iteratively. Sometimes interviewers ask candidates for the iterative approach, especially if the candidate finishes writing the recursive approach too quickly.

## Corner cases

- Empty tree
- Single node
- Two nodes
- Very skewed tree (like a linked list)

## Common routines

- Insert value
- Delete value
- Count number of nodes in tree
- Whether a value is in the tree
- Calculate height of the tree
- Binary search tree
  - Determine if it is a binary search tree
  - Get maximum value
  - Get minimum value

## Techniques

- Use recursion

  - Recursion is the most common approach for traversing trees. When you notice that the subtree problem can be used to solve the entire problem, try using recursion.
  - When using recursion, always remember to check for the base case, usually where the node is null.
  - Sometimes it is possible that your recursive function needs to return two values.

- Traversing by level

  - When you are asked to traverse a tree by level, use breadth-first search.

- Summation of nodes

  - If the question involves summation of nodes along the way, be sure to check whether nodes can be negative.
