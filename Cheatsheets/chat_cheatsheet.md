Perfect — now I understand exactly what you’re asking for.

You don’t want a *list of DSA problem sets* (like Blind 75 or Striver’s Sheet).
You want the **pattern-recognition cheat sheets** — the ones that tell you:

> “If the question asks X → apply Y technique.”

These are “DSA decision-map” or “pattern-based reasoning” cheat-sheets that guide you toward the right approach just by recognizing the type of problem statement.
---

## 🧠 1. **General DSA Pattern-Mapping Cheat Sheets**

| Problem Clue / Wording                                                     | Likely Technique / Pattern        | Why                                                      |
| -------------------------------------------------------------------------- | --------------------------------- | -------------------------------------------------------- |
| “Find max/min subarray, longest substring, count of subarrays satisfying…” | **Sliding Window / Two Pointers** | Continuous sequence, optimize range dynamically.         |
| “Find k-th largest/smallest / median / top-K elements”                     | **Heap (Priority Queue)**         | You need efficient running min/max tracking.             |
| “Array is sorted / nearly sorted / search an index or value”               | **Binary Search**                 | Always check for sorted or monotonic property.           |
| “You need cumulative totals, subarray sums, balance, or prefix conditions” | **Prefix Sum / Difference Array** | Fast range queries.                                      |
| “All possible subsets / combinations / permutations / paths”               | **Backtracking / Bitmasking**     | Exponential possibilities, enumerate choices.            |
| “Optimize something with overlapping subproblems”                          | **Dynamic Programming**           | Overlaps or “reuse sub-results” hints DP.                |
| “Minimum operations / shortest path / reachability / levels”               | **BFS / Dijkstra**                | BFS = shortest steps in unweighted, Dijkstra = weighted. |
| “All paths / connected components / recursive exploration”                 | **DFS (Graph/Tree traversal)**    | Recursive/stack-based exploration.                       |
| “Intervals, meetings, merging, overlapping”                                | **Sorting + Greedy / Heap**       | Sort by start/end, manage ongoing intervals.             |
| “Task ordering with dependencies”                                          | **Topological Sort**              | Directed acyclic graph dependency resolution.            |
| “Union, groups, connected sets”                                            | **Union-Find (DSU)**              | Efficient merge/find structure.                          |
| “Next greater/smaller element, stock span, histogram”                      | **Monotonic Stack**               | Maintain increasing/decreasing property.                 |
| “Scheduling / choosing maximum number of non-conflicting”                  | **Greedy + Sorting by end time**  | Activity selection pattern.                              |
| “Subsequence, edit distance, knapsack”                                     | **DP with 2D table**              | Optimal substructure with two strings or dimensions.     |
| “Majority element, count frequency”                                        | **Hash Map / Boyer-Moore**        | Counting frequency patterns.                             |
| “Range minimum/maximum queries (static)”                                   | **Segment Tree / Sparse Table**   | Efficient range queries on static data.                  |
| “Stream of numbers, running median, online queries”                        | **Two Heaps / Balanced BST**      | Maintain real-time order statistics.                     |

---

## ⚡ 2. **Bitmasking-Specific “If Question Asks → Use This” Cheatsheet**

| Problem Asks / Mentions                                | Technique / Trick                                    |                                    
| ------------------------------------------------------ | ---------------------------------------------------- | 
| “Count number of set bits”                             | `__builtin_popcount(x)` or Brian Kernighan’s algo.   |                                    
| “Turn on/off/toggle bit i”                             | `x\|(1<<i)`/`x & ~(1<<i)`/`x ^ (1<<i)`              |
| “Check if i-th bit set”                                | `(x >> i) & 1`                                       |                                    
| “Find lowest set bit / drop it”                        | `x & -x` / `x & (x-1)`                               |                                    
| “Generate all subsets”                                 | Loop mask = 0..(1<<n)-1                              |                                    
| “Subsets of a given mask”                              | `sub = mask; sub = (sub-1) & mask` loop              |                                    
| “Find element appearing once when others appear twice” | XOR all elements.                                    |                                    
| “Find two unique elements where others twice”          | XOR partition trick.                                 |                                    
| “Represent subset state in DP”                         | Use bitmask DP: `dp[mask]` represents solved subset. |                                    
| “TSP or visiting all cities”                           | `dp[mask][i]` = cost of visiting mask ending at i.   |                                    

---

## 🧩 3. **Graph / Tree-Type Decision Sheet**

| Problem Language                                          | Likely Algorithm                          |
| --------------------------------------------------------- | ----------------------------------------- |
| “Find if path exists / shortest path unweighted”          | BFS                                       |
| “Find shortest weighted path”                             | Dijkstra                                  |
| “Find shortest path negative edges”                       | Bellman-Ford                              |
| “All pairs shortest paths”                                | Floyd–Warshall                            |
| “Detect cycle / count components / connected regions”     | DFS / Union-Find                          |
| “Find MST (minimum spanning tree)”                        | Kruskal / Prim                            |
| “Find topological order / dependency order”               | Topological Sort                          |
| “Tree sum / diameter / ancestor / lowest common ancestor” | DFS with parent tracking / Binary Lifting |
| “Grid traversal / flood fill / islands”                   | BFS / DFS on matrix                       |

---

## 🧮 4. **Dynamic Programming “Question → Pattern” Map**

| Question Type                                   | DP Category                            |
| ----------------------------------------------- | -------------------------------------- |
| “Longest increasing / decreasing / subsequence” | LIS Pattern (`dp[i] = 1 + max(dp[j])`) |
| “Edit distance / convert string A→B”            | 2D DP on strings                       |
| “Subset sum / partition / knapsack”             | 0-1 Knapsack pattern                   |
| “Count ways to reach target / climb stairs”     | Simple recurrence DP                   |
| “Minimum cost path / grid path / triangle”      | Grid DP                                |
| “Palindrome partition / substring DP”           | 2D substring DP                        |
| “Tiling / cutting / rod cutting”                | 1D DP                                  |
| “Choose elements under constraint”              | Bitmask DP                             |

---

## 🧠 5. **String-Specific “If asks → use this” Map**

| Problem Wording                                      | Technique                                |
| ---------------------------------------------------- | ---------------------------------------- |
| “Find anagram / longest substring with unique chars” | Sliding window + hashmap                 |
| “Pattern matching / substring search”                | KMP / Rabin–Karp                         |
| “Smallest window containing pattern”                 | Sliding window + counter                 |
| “Palindrome check / longest palindrome substring”    | Two pointers / expand around center / DP |
| “Count distinct substrings”                          | Suffix Trie / Suffix Array               |
| “Longest common prefix / suffix”                     | Trie / Sorting                           |
| “String compression / encoding / decoding”           | Stack or two-pointer manipulation        |

---

## 💥 6. **Common DSA “Trigger Words” Map**

| Trigger words in question                               | Try this pattern                   |
| ------------------------------------------------------- | ---------------------------------- |
| “Minimum / maximum” (and it’s about subarrays or range) | Sliding window / heap / DP         |
| “K-th”                                                  | Heap / Quickselect / Binary search |
| “All possible”                                          | Recursion / Backtracking / Bitmask |
| “Ways to” / “Count number of ways”                      | DP / recursion with memoization    |
| “Reach from X to Y”                                     | BFS / DFS / DP                     |
| “Partition / split / divide”                            | DP / prefix sum / binary search    |
| “Intervals / overlapping”                               | Sort + Greedy / Merge intervals    |
| “Online stream / data arrives”                          | Heaps / deque / sliding window     |
| “Pairs / triplets”                                      | Two pointers / Hashmap / Sorting   |
| “Majority / frequency”                                  | Hashmap / Counting / Boyer-Moore   |
| “Matrix / grid traversal”                               | DFS / BFS / DP on grid             |
| “Parentheses / brackets / nested structure”             | Stack                              |
| “Next greater / smaller”                                | Monotonic stack                    |

---

## 🔗 7. **Places These Cheat-Sheets Exist Online**

| Resource                                                                | What It Gives                                      |
| ----------------------------------------------------------------------- | -------------------------------------------------- |
| **“Algorithm Patterns for Coding Interviews” by Sean Prashad (GitHub)** | Visual flow of “if question asks X → do Y”.        |
| **“LeetCode Pattern Collection” (Kunaal Naik, Medium)**                 | Type-to-pattern map + example problems.            |
| **NeetCode.io Patterns**                                                | Interactive list mapping problem types → patterns. |
| **Tech Interview Handbook – Algorithm Cheatsheet**                      | Quick pattern summary + templates.                 |
| **CP-Algorithms / AlgoMonster**                                         | Pattern-based explanations and code templates.     |
| **“DSA Pattern Decision Tree” on GitHub** (several repos)               | Flowchart-style “decision tree” cheat sheets.      |

---

   ```
   Is it array-based?
     ├─ sorted? → Binary search
     ├─ continuous range? → Sliding window
     ├─ subset combinations? → Backtracking/Bitmask
     └─ dynamic optimal? → DP
   ```
3. **Practice categorization drills:** read random problem statements and guess pattern before solving.
4. **Create a one-page summary (trigger → pattern)** for review before interviews.

---
