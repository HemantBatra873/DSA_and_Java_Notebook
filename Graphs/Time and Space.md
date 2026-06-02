# Graph Algorithms — Time & Space Complexity

## Traversal Algorithms

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **BFS** (Breadth-First Search) | O(V + E) | O(V) | Queue-based; explores level by level |
| **DFS** (Depth-First Search) | O(V + E) | O(V) | Stack/recursion; O(V) for call stack |

---

## Shortest Path Algorithms

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Dijkstra's** (binary heap) | O((V + E) log V) | O(V) | Single-source; non-negative weights only |
| **Dijkstra's** (Fibonacci heap) | O(E + V log V) | O(V) | Theoretically optimal; rarely used in practice |
| **Bellman-Ford** | O(V · E) | O(V) | Single-source; handles negative weights |
| **Floyd-Warshall** | O(V³) | O(V²) | All-pairs shortest paths |
| **Johnson's Algorithm** | O(V² log V + VE) | O(V²) | All-pairs; better than Floyd-Warshall on sparse graphs |
| **A\*** | O(E log V) | O(V) | Heuristic-guided; optimal with admissible heuristic |
| **SPFA** (Shortest Path Faster) | O(VE) worst case | O(V) | Bellman-Ford with queue optimization; fast in practice |

---

## Minimum Spanning Tree (MST)

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Kruskal's** | O(E log E) | O(V + E) | Sort edges + Union-Find |
| **Prim's** (adjacency matrix) | O(V²) | O(V) | Best for dense graphs |
| **Prim's** (binary heap) | O(E log V) | O(V) | Best for sparse graphs |
| **Prim's** (Fibonacci heap) | O(E + V log V) | O(V) | Optimal asymptotically |
| **Borůvka's** | O(E log V) | O(V + E) | Parallel-friendly |

---

## Topological Sort

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Kahn's Algorithm** (BFS-based) | O(V + E) | O(V) | Works on DAGs only; detects cycles |
| **DFS-based Topo Sort** | O(V + E) | O(V) | Post-order DFS traversal |

---

## Strongly Connected Components (SCC)

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Kosaraju's** | O(V + E) | O(V) | Two DFS passes; intuitive |
| **Tarjan's** | O(V + E) | O(V) | Single DFS pass with stack |
| **Gabow's** | O(V + E) | O(V) | Variation of Tarjan's |

---

## Network Flow

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Ford-Fulkerson** (DFS) | O(E · max_flow) | O(V + E) | Can be slow with irrational capacities |
| **Edmonds-Karp** (BFS) | O(V · E²) | O(V + E) | Ford-Fulkerson + BFS augmentation |
| **Dinic's Algorithm** | O(V² · E) | O(V + E) | Much faster in practice |
| **Push-Relabel** | O(V² · √E) | O(V + E) | Generally fastest in practice |
| **Hungarian Algorithm** | O(V³) | O(V²) | Min-cost bipartite matching |

---

## Cycle Detection

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **DFS-based** (directed) | O(V + E) | O(V) | Uses recursion stack coloring |
| **DFS-based** (undirected) | O(V + E) | O(V) | Tracks parent node |
| **Floyd's Cycle Detection** | O(V) | O(1) | For linked lists; not general graphs |
| **Union-Find** (undirected) | O(E · α(V)) ≈ O(E) | O(V) | α is inverse Ackermann; near-constant |

---

## Bipartite / Matching

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Bipartite Check** (BFS/DFS) | O(V + E) | O(V) | Two-color the graph |
| **Hopcroft-Karp** | O(E · √V) | O(V + E) | Maximum bipartite matching |
| **Kuhn's Algorithm** | O(V · E) | O(V + E) | Simpler max bipartite matching |

---

## Other Important Algorithms

| Algorithm | Time Complexity | Space Complexity | Notes |
|-----------|----------------|-----------------|-------|
| **Bridges / Articulation Points** | O(V + E) | O(V) | Tarjan's bridge-finding |
| **Euler Path/Circuit** (Hierholzer's) | O(V + E) | O(V + E) | Requires Eulerian conditions |
| **Hamiltonian Path** | O(2ᵛ · V²) | O(2ᵛ · V) | NP-Complete; bitmask DP |
| **Coloring** (Greedy) | O(V + E) | O(V) | Not always optimal |
| **Union-Find** (with path compression) | O(α(V)) per op | O(V) | Near O(1); used in many graph algorithms |

---

## Notation Reference

| Symbol | Meaning |
|--------|---------|
| **V** | Number of vertices (nodes) |
| **E** | Number of edges |
| **α(V)** | Inverse Ackermann function — effectively constant |
| **log V** | Base-2 logarithm of V |

> **Dense graph:** E ≈ V²  
> **Sparse graph:** E ≈ V

---

*Space complexity generally excludes the input graph itself (adjacency list = O(V + E), adjacency matrix = O(V²)).*
