# Lower Mid vs Upper Mid in Binary Search

Binary search behaves differently depending on how you calculate `mid`.
This document explains **when and why** to use:

* **Lower mid:** `(l + r) / 2`
* **Upper mid:** `(l + r + 1) / 2`

These two forms prevent infinite loops and control whether the search biases **left** or **right**.

---

# 1. Lower Mid `(l + r) / 2`

### ✔️ Used when you do:

```
r = mid;       // pushing search LEFT
```

### Why?

Because lower-mid always moves `mid` **toward the left**, preventing infinite loops when shrinking from the right.

### Example

```
l = 3, r = 4
mid = (3 + 4) / 2 = 3
```

This is correct because you intend to shrink **r**, not **l**.

### Used in:

* **Lower bound** (first index ≥ target)
* Searching for **first occurrence**

### Typical lower-bound loop

```
while (l < r) {
    mid = (l + r) / 2;
    if (arr[mid] < target) l = mid + 1;
    else r = mid;
}
```

This converges safely because `l` always increases and `r` always decreases.

---

# 2. Upper Mid `(l + r + 1) / 2`

### ✔️ Used when you do:

```
l = mid;        // pushing search RIGHT
```

### Why?

If you used lower-mid here, binary search can get stuck.

### Problem with lower-mid

Example:

```
l = 3, r = 4
mid = (3 + 4)/2 = 3
l = mid = 3   → infinite loop!
```

### Upper mid fixes this:

```
mid = (3 + 4 + 1)/2 = 4
l = mid = 4   → progresses
```

### Used in:

* **Upper bound − 1** (last index ≤ target)
* Searching for **last occurrence**

### Typical upper-bound loop

```
while (l < r) {
    mid = (l + r + 1) / 2;
    if (arr[mid] <= target) l = mid;
    else r = mid - 1;
}
```

This converges safely because `l` is forced to move right.

---

# 3. When to Use Which Mid?

### ✔️ If you do `r = mid` → use **lower mid**

Because:

* `mid` stays on the left side
* Works correctly with a decreasing `r`

### ✔️ If you do `l = mid` → use **upper mid**

Because:

* `mid` must be pushed right
* Prevents infinite loops when `l` moves upward

---

# 4. Easy Summary Table

| Goal                          | Condition            | Update                     | Mid Type      |
| ----------------------------- | -------------------- | -------------------------- | ------------- |
| First occurrence              | `arr[mid] >= target` | `r = mid - 1` or `r = mid` | **Lower mid** |
| Last occurrence               | `arr[mid] <= target` | `l = mid`                  | **Upper mid** |
| Lower bound (first ≥ target)  | `arr[mid] < target`  | `l = mid + 1`              | **Lower mid** |
| Upper-bound−1 (last ≤ target) | `arr[mid] <= target` | `l = mid`                  | **Upper mid** |

---

# 5. The Golden Rule

```
If your update is r = mid       → use lower mid
If your update is l = mid       → use upper mid
```

This is the entire secret.

