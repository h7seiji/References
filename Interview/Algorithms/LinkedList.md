# Linked List

## Advantages

Insertion and deletion of a node in the list (given its location) is O(1) whereas in arrays the following elements will have to be shifted.

## Disadvantages

Access time is linear because directly accessing elements by its position in the list is not possible (in arrays you can do arr[4] for example). You have to traverse from the start.

## Types of linked lists

- Singly linked list: A linked list where each node points to the next node and the last node points to null.
- Doubly linked list: A linked list where each node has two pointers, next which points to the next node and prev which points to the previous node. The prev pointer of the first node and the next pointer of the last node point to null.
- Circular linked list: A singly linked list where the last node points back to the first node. There is a circular doubly linked list variant where the prev pointer of the first node points to the last node and the next pointer of the last node points to the first node.

## Time complexity

Access: O(n)
Search: O(n)
Insert: O(1)
Remove: O(1)

## Common routines

- Counting the number of nodes in the linked list
- Reversing a linked list in-place
- Finding the middle node of the linked list using two pointers (fast/slow)
- Merging two linked lists together

## Corner cases

- Empty linked list (head is null)
- Single node
- Two nodes
- Linked list has cycles. Tip: Clarify beforehand with the interviewer whether there can be a cycle in the list. Usually the answer is no and you don't have to handle it in the code

## Techniques

- Sentinel/dummy nodes
- Two pointers
  - Getting the kth from last node
  - Detecting cycles
  - Getting the middle node
- Using space
- Elegant modification operations
  - Truncate a list
  - Swapping values of nodes
  - Combining two lists
