# Queue

- FIFO
- Python: queue library

## Time complexity

- Enqueue/Offer: O(1)
- Dequeue/Poll: O(1)
- Front: O(1)
- Back: O(1)
- isEmpty: O(1)

## Things to look out for

Most languages don't have a built-in Queue class which can be used, and candidates often use arrays (JavaScript) or lists (Python) as a queue. However, note that the dequeue operation (assuming the front of the queue is on the left) in such a scenario will be O(n) because it requires shifting of all other elements left by one. In such cases, you can flag this to the interviewer and say that you assume that there's a queue data structure to use which has an efficient dequeue operation.

## Corner cases

- Empty queue
- Queue with one item
- Queue with two items
