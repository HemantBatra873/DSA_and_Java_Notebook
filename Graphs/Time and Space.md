Graph Algorithms Cheat Sheet (Time & Space Complexity + Reasoning)

Notation

- V = Number of Vertices
- E = Number of Edges

---

1. Breadth First Search (BFS)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Every vertex is visited once.
- Every edge is explored once.
- Queue may contain up to V vertices.

Use Cases

- Shortest path in unweighted graphs
- Level-order traversal
- Connectivity checking

---

2. Depth First Search (DFS)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Every node is visited once.
- Every edge is traversed once.
- Recursion stack can grow up to V.

Use Cases

- Connected Components
- Cycle Detection
- Topological Sort
- SCC Detection

---

3. Topological Sort (DFS)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- DFS visits every node and edge once.
- Stack stores nodes by finishing time.

Use Cases

- Course Schedule
- Dependency Resolution
- DAG Processing

---

4. Topological Sort (Kahn's Algorithm)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Every node enters queue once.
- Every edge decreases indegree once.

Use Cases

- DAG Ordering
- Directed Cycle Detection

---

5. Cycle Detection (Undirected Graph - DFS)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Standard DFS traversal.
- Parent tracking avoids false cycle detection.

---

6. Cycle Detection (Undirected Graph - BFS)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Queue-based traversal.
- Every node and edge processed once.

---

7. Cycle Detection (Directed Graph - DFS)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Uses visited[] and pathVisited[] arrays.
- Each node processed once.

---

8. Cycle Detection (Directed Graph - Kahn's Algorithm)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Topological sorting processes all nodes.
- If processed nodes < V, cycle exists.

---

9. Bipartite Graph Check

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Two-coloring via BFS/DFS.
- Every node and edge visited once.

---

10. Disjoint Set Union (Union Find)

Time Complexity

- Find → O(α(N))
- Union → O(α(N))

Space Complexity

O(N)

Reasoning

- Path Compression
- Union by Rank / Size
- α(N) ≈ Constant

Use Cases

- Kruskal
- Dynamic Connectivity

---

11. Kruskal's Algorithm

Time Complexity

O(E log E)

Space Complexity

O(V)

Reasoning

1. Sort edges → O(E log E)
2. DSU operations → O(E α(V))

Sorting dominates.

Use Cases

- Minimum Spanning Tree

---

12. Prim's Algorithm

Time Complexity

O(E log V)

Space Complexity

O(V)

Reasoning

- Priority Queue stores candidate edges.
- Heap operations cost O(log V).

Use Cases

- Minimum Spanning Tree

---

13. Dijkstra's Algorithm

Time Complexity

O(E log V)

Space Complexity

O(V)

Reasoning

- Every edge may relax once.
- Heap operations dominate.

Condition

- No negative-weight edges.

Use Cases

- Single Source Shortest Path

---

14. Bellman-Ford Algorithm

Time Complexity

O(V × E)

Space Complexity

O(V)

Reasoning

- Relax all edges exactly V−1 times.
- Extra pass checks negative cycle.

Condition

- Supports negative edges.

Use Cases

- Shortest Path
- Negative Cycle Detection

---

15. Floyd-Warshall Algorithm

Time Complexity

O(V³)

Space Complexity

O(V²)

Reasoning

Triple nested loops:

for k
   for i
      for j

Use Cases

- All-Pairs Shortest Paths
- Negative Cycle Detection

---

16. Shortest Path in DAG

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

1. Topological Sort → O(V + E)
2. Relax each edge once.

Use Cases

- Fast shortest paths in DAGs

---

17. Kosaraju Algorithm (SCC)

Time Complexity

O(V + E)

Space Complexity

O(V + E)

Reasoning

1. DFS ordering
2. Reverse graph
3. DFS on transpose

All linear operations.

Use Cases

- Strongly Connected Components

---

18. Tarjan Algorithm (SCC)

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Single DFS traversal.
- Uses discovery and low arrays.

Use Cases

- Strongly Connected Components

---

19. Bridges in Graph

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- DFS computes discovery and low values.

Use Cases

- Critical Connections

---

20. Articulation Points

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- DFS with low-link values.

Use Cases

- Critical Vertices

---

21. Connected Components

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Run DFS/BFS from each unvisited node.

---

22. Multi-Source BFS

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Same as BFS.
- Multiple starting nodes.

Use Cases

- Nearest Distance Problems

---

23. 0-1 BFS

Time Complexity

O(V + E)

Space Complexity

O(V)

Reasoning

- Uses Deque.
- Each edge processed once.

Condition

- Edge weights only 0 or 1.

Use Cases

- Faster than Dijkstra for 0/1 weights.

---

Quick Revision Table

Algorithm| Time| Space
BFS| O(V+E)| O(V)
DFS| O(V+E)| O(V)
Topological Sort| O(V+E)| O(V)
Cycle Detection| O(V+E)| O(V)
Bipartite Check| O(V+E)| O(V)
DSU| O(α(N))| O(N)
Kruskal| O(E log E)| O(V)
Prim| O(E log V)| O(V)
Dijkstra| O(E log V)| O(V)
Bellman-Ford| O(VE)| O(V)
Floyd-Warshall| O(V³)| O(V²)
DAG Shortest Path| O(V+E)| O(V)
Kosaraju| O(V+E)| O(V+E)
Tarjan SCC| O(V+E)| O(V)
Bridges| O(V+E)| O(V)
Articulation Points| O(V+E)| O(V)
Multi-Source BFS| O(V+E)| O(V)
0-1 BFS| O(V+E)| O(V)