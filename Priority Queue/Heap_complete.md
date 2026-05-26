# Heap Data Structure

## Introduction

A **Heap** is a special type of **Complete Binary Tree** that satisfies a specific ordering property.

A heap is mainly used to efficiently retrieve either:

* The maximum element
* The minimum element

Heaps are widely used in:

* Priority Queues
* Scheduling Algorithms
* Dijkstra’s Algorithm
* Heap Sort
* Top K Problems

---

# Complete Binary Tree

A heap must always be a **Complete Binary Tree**.

A Complete Binary Tree is a binary tree where:

* All levels are completely filled except possibly the last level.
* The last level is filled from left to right.

Example:

```text
        50
      /    \
    40      20
   /  \
  10   5
```

This tree is complete because nodes are filled left to right.

---

# Types of Heap

There are two main types of heaps:

1. Max Heap
2. Min Heap

---

# Max Heap

In a **Max Heap**:

* Parent node is always greater than or equal to its children.
* The largest element remains at the root.

Example:

```text
        50
      /    \
    40      20
   /  \
  10   5
```

Properties:

```text
Parent >= Children
```

Root contains the maximum element.

---

# Min Heap

In a **Min Heap**:

* Parent node is always smaller than or equal to its children.
* The smallest element remains at the root.

Example:

```text
         5
      /     \
    10       20
   /  \
  40   50
```

Properties:

```text
Parent <= Children
```

Root contains the minimum element.

---

# Heap Representation Using Array

A heap is generally implemented using an array.

Example:

```text
        50
      /    \
    40      20
   /  \
  10   5
```

Array Representation:

```text
[50, 40, 20, 10, 5]
```

---

# Index Relationships

For a node at index `i`:

```text
Left Child  = 2*i + 1
Right Child = 2*i + 2
Parent      = (i - 1)/2
```

Example:

```text
Array = [50, 40, 20, 10, 5]
```

For index `1`:

```text
Value = 40

Left Child  = 3 -> 10
Right Child = 4 -> 5
Parent      = 0 -> 50
```

---

# Heap Operations

| Operation   | Time Complexity |
| ----------- | --------------- |
| Insert      | O(log n)        |
| Delete Root | O(log n)        |
| Peek        | O(1)            |
| Heapify     | O(log n)        |
| Build Heap  | O(n)            |

---

# Heapify Concept

Heapify means restoring heap properties.

There are two types:

## 1. Heapify Up

Used during insertion.

Example:

Insert `60`:

```text
        50
      /    \
    40      20
   /
 60
```

Since `60 > 40`, swap upward.

Final Heap:

```text
        60
      /    \
    50      20
   /
 40
```

---

## 2. Heapify Down

Used during deletion.

Remove root `50`:

Move last element to root:

```text
        20
      /
    40
```

Since `40 > 20`, swap downward.

Final Heap:

```text
        40
      /
    20
```

---

# Max Heap Implementation in Java

```java
import java.util.ArrayList;

class MaxHeap {

    private ArrayList<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    // Parent Index
    private int parent(int i) {
        return (i - 1) / 2;
    }

    // Left Child Index
    private int leftChild(int i) {
        return 2 * i + 1;
    }

    // Right Child Index
    private int rightChild(int i) {
        return 2 * i + 2;
    }

    // Swap Elements
    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Insert Element
    public void insert(int value) {

        heap.add(value);

        int current = heap.size() - 1;

        // Heapify Up
        while (current > 0 &&
               heap.get(current) > heap.get(parent(current))) {

            swap(current, parent(current));
            current = parent(current);
        }
    }

    // Get Maximum Element
    public int peek() {

        if (heap.isEmpty()) {
            throw new RuntimeException("Heap is Empty");
        }

        return heap.get(0);
    }

    // Remove Maximum Element
    public int extractMax() {

        if (heap.isEmpty()) {
            throw new RuntimeException("Heap is Empty");
        }

        int max = heap.get(0);

        // Move last element to root
        heap.set(0, heap.get(heap.size() - 1));

        // Remove last element
        heap.remove(heap.size() - 1);

        // Heapify Down
        heapify(0);

        return max;
    }

    // Heapify Down
    private void heapify(int i) {

        int largest = i;

        int left = leftChild(i);
        int right = rightChild(i);

        if (left < heap.size() &&
            heap.get(left) > heap.get(largest)) {

            largest = left;
        }

        if (right < heap.size() &&
            heap.get(right) > heap.get(largest)) {

            largest = right;
        }

        if (largest != i) {
            swap(i, largest);
            heapify(largest);
        }
    }

    // Print Heap
    public void printHeap() {
        System.out.println(heap);
    }

    // Heap Size
    public int size() {
        return heap.size();
    }
}

public class Main {

    public static void main(String[] args) {

        MaxHeap heap = new MaxHeap();

        heap.insert(10);
        heap.insert(40);
        heap.insert(20);
        heap.insert(5);
        heap.insert(50);

        System.out.println("Heap:");
        heap.printHeap();

        System.out.println("Maximum Element: " + heap.peek());

        System.out.println("Removed Element: " + heap.extractMax());

        System.out.println("Heap After Removal:");
        heap.printHeap();
    }
}
```

---

# Output

```text
Heap:
[50, 40, 20, 5, 10]

Maximum Element: 50

Removed Element: 50

Heap After Removal:
[40, 10, 20, 5]
```

---

# Min Heap Using Java PriorityQueue

Java provides built-in heap support using `PriorityQueue`.

Default behavior:

```text
Min Heap
```

Example:

```java
import java.util.PriorityQueue;

public class Main {

    public static void main(String[] args) {

        PriorityQueue<Integer> minHeap =
                new PriorityQueue<>();

        minHeap.add(40);
        minHeap.add(10);
        minHeap.add(30);
        minHeap.add(5);

        System.out.println(minHeap.peek());
    }
}
```

Output:

```text
5
```

---

# Max Heap Using PriorityQueue

```java
import java.util.Collections;
import java.util.PriorityQueue;

public class Main {

    public static void main(String[] args) {

        PriorityQueue<Integer> maxHeap =
                new PriorityQueue<>(Collections.reverseOrder());

        maxHeap.add(40);
        maxHeap.add(10);
        maxHeap.add(30);
        maxHeap.add(50);

        System.out.println(maxHeap.peek());
    }
}
```

Output:

```text
50
```

---

# Applications of Heap

## 1. Priority Queue

Used in:

* CPU Scheduling
* Task Scheduling
* Event Handling

---

## 2. Heap Sort

Heap Sort works in:

```text
O(n log n)
```

---

## 3. Graph Algorithms

Used in:

* Dijkstra’s Algorithm
* Prim’s Algorithm

---

## 4. K Largest / Smallest Problems

Examples:

* Kth Largest Element
* Top K Frequent Elements

---

# Difference Between Max Heap and Min Heap

| Feature         | Max Heap           | Min Heap           |
| --------------- | ------------------ | ------------------ |
| Root Element    | Largest            | Smallest           |
| Parent Relation | Parent >= Children | Parent <= Children |
| Priority        | Higher Values      | Lower Values       |

---

# Key Intuition

## Max Heap

```text
Big elements rise upward.
```

## Min Heap

```text
Small elements rise upward.
```

This is the core idea behind heaps.
