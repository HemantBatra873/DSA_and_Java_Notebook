# Maximum Subarray

## Description
Given an integer array nums, find the subarray with the largest sum, and return its sum.

## Steps
1. curr sum will represent our current sum which must never get 0.
2. maxSum os the overall maxSum which is set to Integer.MIN_VALUE.
3. At every iteration add the number to the current sum check if current sum is more than max and check if current sum is positive.
4. If current sum is not positive it adds nothing to the arrays that we will be forming with later numbers so we remove them by setting sum to 0.

## Code (Kadane Algorithm)
```
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = Integer.MIN_VALUE;
        int currentSum = 0;
        
        for (int i = 0; i < nums.length; i++) {
            currentSum += nums[i];
            if (currentSum > maxSum) {
                maxSum = currentSum;
            }
            if (currentSum < 0) {
                currentSum = 0;
            }
        }
        return maxSum;
    }
}
```

## Print max sum subarray(Kadane)

```
public class MaxSumSubarray {
    public static void main(String[] args) {
        int[] arr = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        findMaxSumSubarray(arr);
    }

    public static void findMaxSumSubarray(int[] arr) {
        int maxSum = arr[0];
        int currentSum = arr[0];
        int start = 0;
        int end = 0;
        int tempStart = 0;

        for (int i = 1; i < arr.length; i++) {
            if (currentSum < 0) {
                currentSum = arr[i];
                tempStart = i;
            } else {
                currentSum += arr[i];
            }

            if (currentSum > maxSum) {
                maxSum = currentSum;
                start = tempStart;
                end = i;
            }
        }

        System.out.println("Maximum Sum: " + maxSum);
        System.out.print("Subarray: [");
        for (int i = start; i <= end; i++) {
            System.out.print(arr[i]);
            if (i < end) System.out.print(", ");
        }
        System.out.println("]");
    }
}
```