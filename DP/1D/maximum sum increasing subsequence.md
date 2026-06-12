# Maximum Sum Increasing Subsequence 

Given an array arr[] of positive integers, find the maximum possible sum of a subsequence such that the elements of the subsequence are in strictly increasing order.

The subsequence does not need to be contiguous.
You must choose elements such that their order in the array is preserved and each chosen element is strictly greater than the previous one.

## Approach

If we know the answer to all previous index then we can get the answer of the current index in O(n) times hence we can get the the answer in total O(n^2)

```java

class Solution {
    public int maxSumIS(int arr[]) {
        int n = arr.length;

        int[] dp = new int[n];

        int ans = 0;

        for (int i = 0; i < n; i++) {
            dp[i] = arr[i];

            for (int j = 0; j < i; j++) {
                if (arr[j] < arr[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + arr[i]);
                }
            }

            ans = Math.max(ans, dp[i]);
        }

        return ans;
    }
}

```
