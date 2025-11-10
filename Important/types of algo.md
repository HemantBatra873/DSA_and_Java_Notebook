# Algorithm Types and Properties (DSA Exam Guide)

This document explains the **four major classifications** of algorithms that are commonly asked in DSA exams.

---

## 1. Online vs Offline Algorithms

| Type        | Meaning                                                                     | Example                                                 |
| ----------- | --------------------------------------------------------------------------- | ------------------------------------------------------- |
| **Online**  | Processes input as it arrives; does not know the entire input in advance.   | KMP string matching, running median, streaming problems |
| **Offline** | Has full access to all inputs before processing; can plan or reorder steps. | Binary Search, Merge Sort, Dijkstra’s algorithm         |

### Key Idea

* **Online** algorithms must make *immediate decisions* without future knowledge.
* **Offline** algorithms can *analyze the complete dataset* and optimize accordingly.

### Example

**Online median problem:** Print median after every number input.
**Offline median problem:** Sort all numbers first, then compute median.

---

## 2. Stable vs Unstable Algorithms

| Type         | Meaning                                                       | Example                                 |
| ------------ | ------------------------------------------------------------- | --------------------------------------- |
| **Stable**   | Maintains the relative order of equal elements after sorting. | Merge Sort, Insertion Sort, Bubble Sort |
| **Unstable** | May change the order of equal elements.                       | Quick Sort, Heap Sort, Selection Sort   |

### Example

If input = `[A(1), B(1), C(2)]`, after sorting by number:

* **Stable sort** → `[A(1), B(1), C(2)]`
* **Unstable sort** → `[B(1), A(1), C(2)]`

---

## 3. In-place vs Out-of-place Algorithms

| Type             | Meaning                                       | Example                    |
| ---------------- | --------------------------------------------- | -------------------------- |
| **In-place**     | Uses constant extra space (O(1)).             | Quick Sort, Selection Sort |
| **Out-of-place** | Requires additional memory beyond input size. | Merge Sort, Counting Sort  |

### Key Idea

* **In-place:** modifies data structure directly.
* **Out-of-place:** creates new structures or arrays for computation.

---

## 4. Deterministic vs Non-deterministic Algorithms

| Type                  | Meaning                                                           | Example                                   |
| --------------------- | ----------------------------------------------------------------- | ----------------------------------------- |
| **Deterministic**     | Produces the same output for the same input every time.           | Binary Search, Merge Sort                 |
| **Non-deterministic** | May produce different outcomes (due to randomness or heuristics). | Randomized Quick Sort, Genetic Algorithms |

### Key Idea

* **Deterministic:** predictable and repeatable.
* **Non-deterministic:** includes random choices or probability.

---

### ✅ Summary Table

| Property              | Online vs Offline                 | Stable vs Unstable | In-place vs Out-of-place | Deterministic vs Non-deterministic |
| --------------------- | --------------------------------- | ------------------ | ------------------------ | ---------------------------------- |
| Input Access          | Partial (online) / Full (offline) | –                  | –                        | –                                  |
| Relative Order        | Maintained / Not maintained       | ✓                  | –                        | –                                  |
| Space                 | Constant / Extra                  | –                  | ✓                        | –                                  |
| Output Predictability | –                                 | –                  | –                        | Same / Randomized                  |

---

**Tip:** In exams, always mention both *definition* and *one clear example* for full marks.
