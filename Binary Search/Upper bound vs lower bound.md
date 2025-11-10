# Binary Search: Lower Bound vs Upper Bound in Java

Both **lower bound** and **upper bound** are variations of **binary search** used to find specific positions in a **sorted array**.

---

## 🔍 Concept Overview

| Term            | Meaning                                 | Purpose                                                                    |
| --------------- | --------------------------------------- | -------------------------------------------------------------------------- |
| **Lower Bound** | Index of the **first element ≥ target** | Used to find where the target **could be inserted without breaking order** |
| **Upper Bound** | Index of the **first element > target** | Used to find where **the target ends** if there are duplicates             |

---

## ⚙️ 1. Lower Bound (`≥ target`)

**Goal:** Find the smallest index `i` such that
`arr[i] >= target`.

If all elements are smaller than `target`, it returns `arr.length`.

### ✅ Implementation in Java

```java
public static int lowerBound(int[] arr, int target) {
    int l = 0, r = arr.length; // notice r = n (exclusive)
    while (l < r) {
        int mid = l + (r - l) / 2;
        if (arr[mid] < target) {
            l = mid + 1;
        } else {
            r = mid;
        }
    }
    return l; // or r (both same)
}
```

### 🧠 Example

```java
int[] arr = {2, 4, 4, 4, 7, 9};
System.out.println(lowerBound(arr, 4));  // Output: 1 (first 4)
System.out.println(lowerBound(arr, 5));  // Output: 4 (first ≥5 → 7)
System.out.println(lowerBound(arr, 10)); // Output: 6 (no ≥10 → end)
```

---

## ⚙️ 2. Upper Bound (`> target`)

**Goal:** Find the smallest index `i` such that
`arr[i] > target`.

If all elements are ≤ target, it returns `arr.length`.

### ✅ Implementation in Java

```java
public static int upperBound(int[] arr, int target) {
    int l = 0, r = arr.length;
    while (l < r) {
        int mid = l + (r - l) / 2;
        if (arr[mid] <= target) {
            l = mid + 1;
        } else {
            r = mid;
        }
    }
    return l;
}
```

### 🧠 Example

```java
int[] arr = {2, 4, 4, 4, 7, 9};
System.out.println(upperBound(arr, 4)); // Output: 4 (first >4 → 7)
System.out.println(upperBound(arr, 5)); // Output: 4 (first >5 → 7)
System.out.println(upperBound(arr, 9)); // Output: 6 (no >9 → end)
```

---

## 📊 Visual Example

Consider array:
`[2, 4, 4, 4, 7, 9]`

| Target | lowerBound | upperBound | Explanation                        |
| ------ | ---------- | ---------- | ---------------------------------- |
| 4      | 1          | 4          | first ≥4 is at 1; first >4 is at 4 |
| 5      | 4          | 4          | both point to 7                    |
| 9      | 5          | 6          | last element is 9                  |
| 1      | 0          | 0          | all >1                             |

---

## 🧩 When to Use

| Use Case                                | Bound                     |
| --------------------------------------- | ------------------------- |
| Find first element not less than target | **Lower Bound**           |
| Find first element greater than target  | **Upper Bound**           |
| Count occurrences of a number           | `upperBound - lowerBound` |
| Insert position keeping sorted order    | **Lower Bound**           |

---

## 🧠 Quick Summary Table

| Property     | Lower Bound                       | Upper Bound          |
| ------------ | --------------------------------- | -------------------- |
| Condition    | `arr[mid] < target`               | `arr[mid] <= target` |
| Returns      | first index ≥ target              | first index > target |
| Used for     | insertion index, duplicates start | duplicates end       |
| Typical Loop | `while (l < r)`                   | `while (l < r)`      |
