# Union-Find (aka Disjoint Set Union, DSU)

## What it is

- Union-Find is a data structure to efficiently track connected components.
- Union(x, y): Merge the sets containing x and y
- Find(x): Return the representative (root) of the set containing x
- Connected(x, y): Check if x and y are in the same set

## When it’s useful

- Detect cycles in a graph (especially undirected)
- Count connected components
- Kruskal’s Minimum Spanning Tree
- Dynamic connectivity problems
Basically, anytime you want fast queries and merges of groups of nodes.

## Key ideas

- Each node points to a parent (initially itself)
- Path compression during find → flattens the tree, speeds up future finds
- Union by rank/size → attach smaller tree under larger → keeps tree shallow

## Implementation

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))  # each node is its own parent
        self.rank = [0] * n           # rank for union by rank

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # path compression
        return self.parent[x]

    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False  # already connected
        # union by rank
        if self.rank[px] < self.rank[py]:
            self.parent[px] = py
        elif self.rank[px] > self.rank[py]:
            self.parent[py] = px
        else:
            self.parent[py] = px
            self.rank[px] += 1
        return True

    def connected(self, x, y):
        return self.find(x) == self.find(y)
```

## Complexity

Nearly O(1) per operation thanks to path compression + union by rank
More precisely: O(α(n)), where α(n) is the inverse Ackermann function (super slow-growing, basically constant for all practical purposes)
