# Maximum Subarray

## Description
Given an integer array nums, find the subarray with the largest sum, and return its sum.

## Steps
1. curr sum will represent our current sum which must never get 0.
2. maxSum os the overall maxSum which is set to Integer.MIN_VALUE.
3. At every iteration add the number to the current sum check if current sum is more than max and check if current sum is positive.
4. If current sum is not positive it adds nothing to the arrays that we will be forming with later numbers so we remove them by setting sum to 0.

## Code (Kadane Algorithm)
```java
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

```java
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

# MaxProduct Subarray Kadane's 

## Question

Given an integer array nums, find a subarray that has the largest product within the array and return it.

A subarray is a contiguous non-empty sequence of elements within an array.

You can assume the output will fit into a 32-bit integer.

## Key understanding

Initially I thought of kadane but as soon as I thought the sum could get -ve I left that approach but kadane was actually right we just need to modify the approach slightly and maintain the current minimum along with current maximum because in the next step current max can become current min and current min can become current max.

```java
public class Solution {
    public int maxProduct(int[] nums) {
        int res = nums[0];
        int curMin = 1, curMax = 1;

        for (int num : nums) {
            int tmp = curMax * num;
            curMax = Math.max(Math.max(num * curMax, num * curMin), num);
            curMin = Math.min(Math.min(tmp, num * curMin), num);
            res = Math.max(res, curMax);
        }
        return res;
    }
}
```