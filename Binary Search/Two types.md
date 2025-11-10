# Binary Search Variants: `while (l < r)` vs `while (l <= r)`

Binary search has two major loop variants depending on how we define the search interval:

1. **Half-open interval**: `[l, r)` → uses `while (l < r)`
2. **Closed interval**: `[l, r]` → uses `while (l <= r)`

---

## ⚙️ Type 1 — `while (l < r)` (Half-Open Interval)

### Concept
- The interval is **half-open** — `l` is inclusive, `r` is exclusive.
- Loop continues as long as `l < r`.
- Stops when `l == r`, meaning the search range is empty.
- Commonly used for **boundary finding** problems (e.g., lower bound, upper bound).

### Typical Implementation

```python
while l < r:
    mid = l + (r - l) // 2
    if condition(mid):
        r = mid        # mid might be the answer, so keep it
    else:
        l = mid + 1    # mid cannot be the answer, move right
```

### Example: Find First Index Where `arr[mid] >= target`

```python
l, r = 0, n
while l < r:
    mid = (l + r) // 2
    if arr[mid] >= target:
        r = mid
    else:
        l = mid + 1
return l  # first index where arr[l] >= target
```

### Properties
- Interval shrinks **strictly** each step → **no infinite loop**.
- Best for finding **boundaries**.
- Works exactly like Python's `bisect_left()`.

---

## ⚙️ Type 2 — `while (l <= r)` (Closed Interval)

### Concept
- The interval is **fully closed** — both `l` and `r` are inclusive.
- Loop continues as long as `l <= r`.
- Stops when `l > r` (no elements left).
- Commonly used for **exact match** searches.

### Typical Implementation

```python
while l <= r:
    mid = l + (r - l) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        l = mid + 1
    else:
        r = mid - 1
return -1  # not found
```

### Example: Search for a Target Element

```python
l, r = 0, n - 1
while l <= r:
    mid = (l + r) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        l = mid + 1
    else:
        r = mid - 1
return -1
```

### Properties
- Checks **every element** in range `[l, r]`.
- More intuitive for **exact matches**.
- Must handle bounds carefully to avoid infinite loops.

---

## 🧩 Summary Table

| Feature                | `while (l < r)`              | `while (l <= r)`             |
|------------------------|------------------------------|------------------------------|
| **Interval type**      | Half-open `[l, r)`           | Closed `[l, r]`              |
| **Common use**         | Boundary search (first/last true) | Exact match search         |
| **End condition**      | `l == r`                     | `l > r`                      |
| **Updates**            | `r = mid` or `l = mid + 1`   | `r = mid - 1` or `l = mid + 1` |
| **Infinite loop risk** | Low                          | Medium (must update correctly) |
| **Returns**            | Boundary index               | Element index or `-1`        |

---

## 💡 Rule of Thumb

| Task                                    | Preferred Version   |
|-----------------------------------------|---------------------|
| Search for **exact match**              | `while (l <= r)`    |
| Search for **boundary** (first/last true) | `while (l < r)`     |
| Use case like `bisect_left` / `bisect_right` | `while (l < r)`     |
