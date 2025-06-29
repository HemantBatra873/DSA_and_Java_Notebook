# Number of Subsequences That Satisfy the Given Sum Condition

You are given an array of integers nums and an integer target.

Return the number of non-empty subsequences of nums such that the sum of the minimum and maximum element on it is less or equal to target. Since the answer may be too large, return it modulo 109 + 7.

## Learnings
If there is a situation where you need to compute powers of a number like 2 in 1000 or 10000 don't do it recursively instead pre compute it iteratively.

Left - right is don't because left is a must in every subsequence but the numbers from left + 1 to right are optional so 2 ways for each of them.

## Approach 

First sort the array because without sorting we can't do the two Pointers approach.

Then pre compute powers of two upto the max length of array and mod it because it might not fit in integer range.

Then initialise and,left and right.

Then while loop runs until left <= right and if the nuns[left] + nuns[right] <= target then we can increment answer by 2 ^ (right - left) which means numbers from left + 1 to right. Then increment left as all values with left as smallest have been calculated.

If the sum is more than target decrement right because if it was not possible with current left it won't be possible for any value more than that as the array is sorted.


## Code (Beats 100%)

```java
class Solution {
    private int MOD = 1_000_000_007;

    public int numSubseq(int[] nums, int target) {
        int n = nums.length;
        Arrays.sort(nums);

        // Precompute powers of 2
        int[] pow = new int[n];
        pow[0] = 1;
        for (int i = 1; i < n; i++) {
            pow[i] = (pow[i - 1] * 2) % MOD;
        }

        int ans = 0;
        int left = 0, right = n - 1;

        while (left <= right) {
            if (nums[left] + nums[right] <= target) {
                ans = (ans + pow[right - left]) % MOD;
                left++;
            } else {
                right--;
            }
        }

        return ans;
    }
}
```