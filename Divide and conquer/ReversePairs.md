Yes. The main change is that for **reverse pairs**, the counting condition cannot be handled directly inside the normal merge comparison. We first count cross-half reverse pairs with a separate pointer, then perform the usual merge.

```java
class Solution {
    public int reversePairs(int[] nums) {
        return (int) mergeSort(nums, 0, nums.length - 1);
    }

    private long mergeSort(int[] nums, int left, int right) {
        if (left >= right) {
            return 0;
        }

        int middle = left + (right - left) / 2;

        long reversePairs = 0;

        reversePairs += mergeSort(nums, left, middle);
        reversePairs += mergeSort(nums, middle + 1, right);
        reversePairs += merge(nums, left, middle, right);

        return reversePairs;
    }

    private long merge(int[] nums, int left, int middle, int right) {
        long reversePairs = 0;

        // Count reverse pairs across the two sorted halves.
        int rightIndex = middle + 1;

        for (int leftIndex = left; leftIndex <= middle; leftIndex++) {
            while (rightIndex <= right
                    && (long) nums[leftIndex] > 2L * nums[rightIndex]) {
                rightIndex++;
            }

            // All elements before rightIndex form a reverse pair
            // with nums[leftIndex].
            reversePairs += rightIndex - (middle + 1);
        }

        // Normal merge.
        int[] temporary = new int[right - left + 1];

        int leftIndex = left;
        rightIndex = middle + 1;
        int temporaryIndex = 0;

        while (leftIndex <= middle && rightIndex <= right) {
            if (nums[leftIndex] <= nums[rightIndex]) {
                temporary[temporaryIndex++] = nums[leftIndex++];
            } else {
                temporary[temporaryIndex++] = nums[rightIndex++];
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

        return reversePairs;
    }
}
```

The important difference from your inversion solution is this section:

```java
int rightIndex = middle + 1;

for (int leftIndex = left; leftIndex <= middle; leftIndex++) {
    while (rightIndex <= right
            && (long) nums[leftIndex] > 2L * nums[rightIndex]) {
        rightIndex++;
    }

    reversePairs += rightIndex - (middle + 1);
}
```

Because both halves are already sorted, `rightIndex` **never needs to move backward**.

For example:

```text
Left:  [3, 5, 7]
Right: [1, 2, 4]
```

For `5`:

```text
5 > 2 * 1  → true
5 > 2 * 2  → true
5 > 2 * 4  → false
```

So there are `2` reverse pairs involving `5`.

This gives the same overall **merge-sort structure** as your `countInversions()` solution, with only the cross-half counting logic changed.

**Time:** `O(n log n)`
**Space:** `O(n)`

Also, `(long) nums[leftIndex] > 2L * nums[rightIndex]` is important to avoid integer overflow.
