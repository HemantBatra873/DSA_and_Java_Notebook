# Java Priority Queue - Complete Guide

## Introduction

Priority Queue in Java is a data structure that serves elements based on their priority rather than their insertion order. It's implemented as a binary heap and is part of the Java Collections Framework.

## Key Characteristics

- **Natural Ordering**: By default, elements are ordered in ascending order (min-heap)
- **Generic**: Can store any type of objects
- **Not Thread-Safe**: Multiple threads should not access it concurrently without synchronization
- **No Null Elements**: Cannot contain null elements
- **Unbounded**: Can grow dynamically (though initial capacity can be specified)

## Import Statement

```java
import java.util.PriorityQueue;
import java.util.Comparator;
```

## Creating Priority Queues

### 1. Default Constructor (Min-Heap)
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
// Natural ordering: smallest element has highest priority
```

### 2. With Initial Capacity
```java
PriorityQueue<Integer> pq = new PriorityQueue<>(10);
// Initial capacity of 10 elements
```

### 3. With Custom Comparator
```java
PriorityQueue<Integer> pq = new PriorityQueue<>(Comparator.reverseOrder());
// For descending order (max-heap)
```

### 4. From Another Collection
```java
List<Integer> list = Arrays.asList(5, 2, 8, 1);
PriorityQueue<Integer> pq = new PriorityQueue<>(list);
```

## Essential Methods

### Adding Elements
- **`add(E e)`**: Inserts element into the queue
- **`offer(E e)`**: Inserts element (same as add for PriorityQueue)

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5);
pq.offer(3);
pq.add(8);
pq.add(1);
// Queue internally: [1, 3, 8, 5] (heap structure)
```

### Retrieving Elements
- **`peek()`**: Returns the head element without removing it (returns null if empty)
- **`element()`**: Returns the head element without removing it (throws exception if empty)

```java
Integer head = pq.peek(); // Returns 1 (smallest element)
Integer head2 = pq.element(); // Returns 1 (throws NoSuchElementException if empty)
```

### Removing Elements
- **`poll()`**: Retrieves and removes the head element (returns null if empty)
- **`remove()`**: Retrieves and removes the head element (throws exception if empty)
- **`remove(Object o)`**: Removes a specific element if present

```java
Integer removed = pq.poll(); // Removes and returns 1
Integer removed2 = pq.remove(); // Removes and returns next smallest
pq.remove(5); // Removes element 5 if present
```

### Other Useful Methods
- **`size()`**: Returns the number of elements
- **`isEmpty()`**: Checks if the queue is empty
- **`clear()`**: Removes all elements
- **`contains(Object o)`**: Checks if element exists
- **`toArray()`**: Converts to array

```java
int size = pq.size();
boolean empty = pq.isEmpty();
boolean contains = pq.contains(3);
pq.clear();
```

## Creating Descending Order Priority Queue (Max-Heap)

### Method 1: Using Comparator.reverseOrder()
```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
maxHeap.add(5);
maxHeap.add(2);
maxHeap.add(8);
maxHeap.add(1);
System.out.println(maxHeap.poll()); // Output: 8 (largest first)
```

### Method 2: Using Lambda Expression
```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
// or
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> Integer.compare(b, a));
```

### Method 3: Using Collections.reverseOrder()
```java
import java.util.Collections;
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
```

### Method 4: Custom Comparator Class
```java
class DescendingComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer a, Integer b) {
        return b.compareTo(a); // Reverse the natural order
    }
}

PriorityQueue<Integer> maxHeap = new PriorityQueue<>(new DescendingComparator());
```

## Custom Objects in Priority Queue

### Using Comparable Interface
```java
class Student implements Comparable<Student> {
    String name;
    int grade;
    
    public Student(String name, int grade) {
        this.name = name;
        this.grade = grade;
    }
    
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.grade, other.grade); // Ascending by grade
    }
}

PriorityQueue<Student> pq = new PriorityQueue<>();
```

### Using Custom Comparator
```java
// Priority by grade (descending), then by name (ascending)
PriorityQueue<Student> pq = new PriorityQueue<>((s1, s2) -> {
    if (s1.grade != s2.grade) {
        return Integer.compare(s2.grade, s1.grade); // Descending grade
    }
    return s1.name.compareTo(s2.name); // Ascending name
});
```

## Complete Example

```java
import java.util.*;

public class PriorityQueueExample {
    public static void main(String[] args) {
        // Min-Heap (default)
        System.out.println("=== Min-Heap (Ascending Order) ===");
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        minHeap.addAll(Arrays.asList(5, 2, 8, 1, 9, 3));
        
        System.out.print("Elements removed in order: ");
        while (!minHeap.isEmpty()) {
            System.out.print(minHeap.poll() + " ");
        }
        System.out.println(); // Output: 1 2 3 5 8 9
        
        // Max-Heap (descending order)
        System.out.println("\n=== Max-Heap (Descending Order) ===");
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
        maxHeap.addAll(Arrays.asList(5, 2, 8, 1, 9, 3));
        
        System.out.print("Elements removed in order: ");
        while (!maxHeap.isEmpty()) {
            System.out.print(maxHeap.poll() + " ");
        }
        System.out.println(); // Output: 9 8 5 3 2 1
        
        // String Priority Queue (lexicographical order)
        System.out.println("\n=== String Priority Queue ===");
        PriorityQueue<String> stringPQ = new PriorityQueue<>();
        stringPQ.addAll(Arrays.asList("banana", "apple", "cherry", "date"));
        
        System.out.print("Strings in order: ");
        while (!stringPQ.isEmpty()) {
            System.out.print(stringPQ.poll() + " ");
        }
        System.out.println(); // Output: apple banana cherry date
    }
}
```

## Time Complexity

| Operation | Time Complexity |
|-----------|----------------|
| `add()/offer()` | O(log n) |
| `peek()/element()` | O(1) |
| `poll()/remove()` | O(log n) |
| `remove(Object)` | O(n) |
| `contains()` | O(n) |

## Common Use Cases

1. **Dijkstra's Algorithm**: Finding shortest paths
2. **Huffman Coding**: Data compression
3. **Task Scheduling**: Priority-based task execution
4. **Merge K Sorted Lists**: Efficiently merging multiple sorted lists
5. **Top K Elements**: Finding K largest or smallest elements
6. **Median Finding**: Using two heaps (min and max)

## Important Notes

- Priority Queue is **not synchronized** - use `PriorityBlockingQueue` for thread-safe operations
- Elements are not guaranteed to be in sorted order when iterating (use `poll()` for sorted access)
- The iterator does **not** guarantee any particular order
- Comparison method must be consistent with `equals()` for proper behavior