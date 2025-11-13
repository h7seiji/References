# Heap

- A heap is a specialized tree-based data structure which is a complete tree that satisfies the heap property.
- Max heap - In a max heap, the value of a node must be greatest among the node values in its entire subtree. The same property must be recursively true for all nodes in the tree.
- Min heap - In a min heap, the value of a node must be smallest among the node values in its entire subtree. The same property must be recursively true for all nodes in the tree.
- In the context of algorithm interviews, heaps and priority queues can be treated as the same data structure. A heap is a useful data structure when it is necessary to repeatedly remove the object with the highest (or lowest) priority, or when insertions need to be interspersed with removals of the root node.

- Python: heapq

## Time Complexity

- Find max/min: O(1)
- Insert: O(log(n))
- Remove: O(log(n))
- Heapify (create a heap out of given array of elements): O(n)

## Techniques

- Mention of top or lowest k

```python
import heapq

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        dic = {}
        for num in nums:
            dic[num] = dic.get(num, 0) + 1
        heap = [(-value, key) for key, value in dic.items()]
        heapq.heapify(heap)
        return [heapq.heappop(heap)[1] for _ in range(k)]
```

```python
import heapq

def three_largest(nums):
    # create a min-heap with the first 3 elements
    heap = nums[:3]
    heapq.heapify(heap)
    
    # iterate through the remaining elements
    for num in nums[3:]:
        if num > heap[0]:
            heapq.heappop(heap)
            heapq.heappush(heap, num)
    
    return heap
```
