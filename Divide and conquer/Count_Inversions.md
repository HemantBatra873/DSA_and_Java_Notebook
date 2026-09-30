Yes. The inversion count can be solved efficiently using both **Merge Sort** and a **Fenwick Tree (BIT)**.

## 1. Merge Sort

The key observation is during merging two sorted halves:

```text
Left  = [2, 5, 8]
Right = [1, 3, 7]
```

When `5 > 3`, then `5` and **every element after 5 in the left half** form an inversion with `3`.

So we can add:

```text
mid - leftIndex + 1
```

### Java

```java
class Solution {
    public long countInversions(int[] nums) {
        return mergeSort(nums, 0, nums.length - 1);
    }

    private long mergeSort(int[] nums, int left, int right) {
        if (left >= right) {
            return 0;
        }

        int middle = left + (right - left) / 2;

        long inversions = 0;

        inversions += mergeSort(nums, left, middle);
        inversions += mergeSort(nums, middle + 1, right);
        inversions += merge(nums, left, middle, right);

        return inversions;
    }

    private long merge(int[] nums, int left, int middle, int right) {
        int[] temporary = new int[right - left + 1];

        int leftIndex = left;
        int rightIndex = middle + 1;
        int temporaryIndex = 0;

        long inversions = 0;

        while (leftIndex <= middle && rightIndex <= right) {
            if (nums[leftIndex] <= nums[rightIndex]) {
                temporary[temporaryIndex++] = nums[leftIndex++];
            } else {
                temporary[temporaryIndex++] = nums[rightIndex++];

                // All remaining elements in the left half
                // form an inversion with nums[rightIndex - 1].
                inversions += middle - leftIndex + 1;
            }
        }

        while (leftIndex <= middle) {
            temporary[temporaryIndex++] = nums[leftIndex++];
        }

        while (rightIndex <= right) {
            temporary[temporaryIndex++] = nums[rightIndex++];
        }

        for (int index = 0; index < temporary.length; index++) {
            nums[left + index] = temporary[index];
        }

        return inversions;
    }
}
```

### Example

For:

```text
[5, 3, 2, 4, 1]
```

The algorithm eventually counts:

```text
5 > 3
5 > 2
5 > 4
5 > 1
3 > 2
3 > 1
2 > 1
4 > 1
```

Result:

```text
8
```

**Complexity:**

```text
Time:  O(n log n)
Space: O(n)
```

---

# 2. Fenwick Tree / Binary Indexed Tree

The Fenwick Tree approach is based on processing the array **from right to left**.

For every `nums[i]`, we need to know:

> How many elements already processed are smaller than `nums[i]`?

Since we're moving right → left, all previously processed elements are to the **right** of `i`.

For example:

```text
nums = [5, 3, 2, 4, 1]

Process:

1
4 → smaller elements = 1
2 → smaller elements = 1
3 → smaller elements = 2
5 → smaller elements = 4
```

Total:

```text
1 + 1 + 2 + 4 = 8
```

### Why coordinate compression?

A Fenwick Tree works naturally with indices such as:

```text
1, 2, 3, 4, 5...
```

But the array could contain:

```text
[-1000000000, 5, 999999999]
```

So we first **coordinate-compress** the values into their ranks.

For:

```text
[5, 3, 2, 4, 1]
```

Sorted:

```text
[1, 2, 3, 4, 5]
```

Ranks:

```text
1 → 1
2 → 2
3 → 3
4 → 4
5 → 5
```

### Java

```java
import java.util.Arrays;

class Solution {
    public long countInversions(int[] nums) {
        int[] sorted = nums.clone();
        Arrays.sort(sorted);

        FenwickTree fenwickTree = new FenwickTree(sorted.length);

        long inversions = 0;

        for (int index = nums.length - 1; index >= 0; index--) {
            int rank = lowerBound(sorted, nums[index]) + 1;

            // Number of elements smaller than nums[index]
            // that have already been processed.
            inversions += fenwickTree.query(rank - 1);

            fenwickTree.update(rank, 1);
        }

        return inversions;
    }

    private int lowerBound(int[] array, int target) {
        int left = 0;
        int right = array.length;

        while (left < right) {
            int middle = left + (right - left) / 2;

            if (array[middle] < target) {
                left = middle + 1;
            } else {
                right = middle;
            }
        }

        return left;
    }

    private static class FenwickTree {
        private final int[] tree;

        FenwickTree(int size) {
            tree = new int[size + 1];
        }

        void update(int index, int value) {
            while (index < tree.length) {
                tree[index] += value;
                index += index & -index;
            }
        }

        int query(int index) {
            int sum = 0;

            while (index > 0) {
                sum += tree[index];
                index -= index & -index;
            }

            return sum;
        }
    }
}
```

### Complexity

With binary search for coordinate compression:

```text
Sorting:       O(n log n)
Each query:    O(log n)
Each update:   O(log n)

Total:         O(n log n)
Space:         O(n)
```

---

## Merge Sort vs Fenwick Tree

|                          | Merge Sort          | Fenwick Tree                   |
| ------------------------ | ------------------- | ------------------------------ |
| Time                     | `O(n log n)`        | `O(n log n)`                   |
| Space                    | `O(n)`              | `O(n)`                         |
| Main idea                | Count while merging | Count frequencies              |
| Coordinate compression   | No                  | Usually required               |
| Handles duplicates       | Yes                 | Yes                            |
| Implementation           | Simpler             | More concepts                  |
| Useful beyond inversions | Sorting + counting  | Prefix/range frequency queries |

For **this specific problem**, I'd learn the **Merge Sort solution first** because the inversion-counting trick is particularly important in DSA. Then learn the Fenwick Tree version because the same `update()` + `query()` pattern appears in many other problems.
