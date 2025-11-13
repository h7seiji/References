# Graph

A graph is a structure containing a set of objects (nodes or vertices) where there can be edges between these nodes/vertices. Edges can be directed or undirected and can optionally have values (a weighted graph). Trees are undirected graphs in which any two vertices are connected by exactly one edge and there can be no cycles in the graph.

## Graph representations

You can be given a list of edges and you have to build your own graph from the edges so that you can perform a traversal on them. The common graph representations are:

- Adjacency matrix
- Adjacency list
- Hash table of hash tables

## Time Complexity

|V| is the number of vertices while |E| is the number of edges.

- Depth-first search: O(|V| + |E|)
- Breadth-first search: O(|V| + |E|)
- Topological sort: O(|V| + |E|)

## Things to look out for

- A tree-like diagram could very well be a graph that allows for cycles and a naive recursive solution would not work. In that case you will have to handle cycles and keep a set of visited nodes when traversing.
- Ensure you are correctly keeping track of visited nodes and not visiting each node more than once. Otherwise your code could end up in an infinite loop.

## Corner cases

- Empty graph
- Graph with one or two nodes
- Disconnected graphs
- Graph with cycles

## Graph search algorithms

- Common - Breadth-first Search, Depth-first Search
- Uncommon - Topological Sort, Dijkstra's algorithm
- Almost never - Bellman-Ford algorithm, Floyd-Warshall algorithm, Prim's algorithm, Kruskal's algorithm. Your interviewer likely doesn't know them either.
