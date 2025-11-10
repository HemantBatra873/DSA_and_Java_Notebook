## Binary Search Variants: while (l < r) vs while (l <= r)

Binary search has two major loop variants depending on how we define the search interval:

1. Half-open interval: [l, r) → uses while (l < r)


2. Closed interval: [l, r] → uses while (l <= r)




---

⚙️ Type 1 — while (l < r) (Half-Open Interval)

Concept

The interval is half-open — l is inclusive and r is exclusive. The loop continues as long as l < r.

Stops when l == r, meaning the search range is empty.

Commonly used for boundary finding problems (e.g., lower bound, upper bound).


Typical Implementation (Java)

```java
int lowerBound(int[] arr, int target) {
    int l = 0, r = arr.length; // [l, r)
    while (l < r) {
        int mid = l + (r - l) / 2;
        if (arr[mid] >= target) {
            r = mid; // mid might be the answer
        } else {
            l = mid + 1; // exclude mid
        }
    }
    return l; // first index where arr[l] >= target
}
```

Example Usage

```java
int[] arr = {1, 3, 5, 7, 9};
int idx = lowerBound(arr, 6); // returns 3 (element 7)
```
Properties

Interval shrinks strictly each step → no infinite loop.

Best for finding boundaries.

Works like Arrays.binarySearch() for insertion points.



---

⚙️ Type 2 — while (l <= r) (Closed Interval)

Concept

The interval is fully closed — both ends l and r are inclusive. The loop continues as long as l <= r.

Stops when l > r (no elements left).

Commonly used for exact match searches.


Typical Implementation (Java)

```java
int binarySearch(int[] arr, int target) {
    int l = 0, r = arr.length - 1; // [l, r]
    while (l <= r) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == target) {
            return mid; // found exact match
        } else if (arr[mid] < target) {
            l = mid + 1; // search right half
        } else {
            r = mid - 1; // search left half
        }
    }
    return -1; // not found
}
```

Example Usage

```java
int[] arr = {2, 4, 6, 8, 10};
int idx = binarySearch(arr, 8); // returns 3
int idx2 = binarySearch(arr, 5); // returns -1 (not found)
```

Properties

Checks every element in range [l, r].

More intuitive for finding exact matches.

Must handle bounds carefully to avoid infinite loops.



---

🧩 Summary Table

Feature	while (l < r)	while (l <= r)

Interval type	Half-open [l, r)	Closed [l, r]
Common use	Boundary search (first/last true)	Exact match search
End condition	l == r	l > r
Updates	r = mid or l = mid + 1	r = mid - 1 or l = mid + 1
Infinite loop risk	Low	Medium (must update correctly)
Returns	Boundary index	Element index or -1



---

💡 Rule of Thumb

Task	Preferred Version

Search for exact match	while (l <= r)
Search for boundary (e.g., first/last true)	while (l < r)
Use case like lower bound / upper bound	while (l < r)
