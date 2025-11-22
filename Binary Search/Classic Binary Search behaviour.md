# Binary Search Behavior (Classic Variant)

This document explains **exactly where `left` and `right` end** in classic binary search, including cases with **missing targets** and **multiple occurrences**.

---

## 1. Classic Binary Search Template

```java
while (left <= right) {
    int mid = left + (right - left) / 2;

    if (arr[mid] == target) return mid;     // returns ANY matching index
    else if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
}
```

---

# 2. If Target is **NOT Present**

When the loop ends:

```
right = last index whose value < target
left  = first index whose value > target
```

And always:

```
left = right + 1
```

### Example

Array:

```
[2, 4, 7, 9, 15]
```

Target: `8`

Result:

```
right = 2  (value 7)
left  = 3  (value 9)
```

---

# 3. If Target **Has Multiple Occurrences**

Classic binary search **does NOT guarantee first or last**.
It returns **any** index where the target appears.

Example:

```
[2, 4, 7, 7, 7, 9]
```

Target: `7`

Possible return values:

```
2 or 3 or 4
```

Depending on how mid splits.

---

# 4. If Target Is Present or Missing — Final Pointer Meaning

Regardless of duplicates:

### If found:

```
returns any matching mid
```

### If NOT found:

```
right → last element < target
left  → first element > target
left = right + 1
```

This property is guaranteed for every sorted array.

---

# 5. How To Find First or Last Occurrence

To force a specific direction:

### ✔️ First occurrence

```java
if (arr[mid] >= target) right = mid - 1;
else left = mid + 1;
```

### ✔️ Last occurrence

```java
if (arr[mid] <= target) left = mid + 1;
else right = mid - 1;
```

These modify the behavior so equality does NOT stop the search.

---

# 6. Summary (Easy to Memorize)

### Classic binary search:

* If **target exists** → return **any index**.
* If **target doesn't exist** →

  * `right` = last < target
  * `left` = first > target
  * `left = right + 1`

### Modified binary search

* Use it when you need **first** or **last** occurrence.

---

Let me know if you want a diagram version or Java code examples for each case.
