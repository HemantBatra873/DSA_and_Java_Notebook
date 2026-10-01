# Find the repeating and missing number

Very similar approach to Single Number 2 problem on Leetcode.

```java
class Solution {
    public int[] findMissingAndRepeating(int[] nums) {
        int n = nums.length;

        // XOR of all numbers from 1 to n
        // and all numbers in the array.
        //
        // Every number that appears correctly will occur twice
        // and cancel out because:
        // x ^ x = 0
        //
        // What remains is:
        // repeating ^ missing
        int xor = 0;

        for (int index = 0; index < n; index++) {
            xor ^= nums[index];
            xor ^= (index + 1);
        }

        // Get the rightmost bit where the repeating
        // and missing numbers are different.
        int lowestBit = xor & (-xor);

        int firstNumber = 0;
        int secondNumber = 0;

        // Divide all numbers into two groups based on
        // the lowest set bit.
        //
        // Numbers with this bit set go into one group.
        // Numbers without it go into the other group.
        for (int index = 0; index < n; index++) {
            if ((nums[index] & lowestBit) != 0) {
                firstNumber ^= nums[index];
            } else {
                secondNumber ^= nums[index];
            }

            int number = index + 1;

            if ((number & lowestBit) != 0) {
                firstNumber ^= number;
            } else {
                secondNumber ^= number;
            }
        }

        // At this point, firstNumber and secondNumber
        // are the repeating and missing numbers,
        // but we don't know which is which.
        //
        // Check which one actually exists in the array.
        for (int num : nums) {
            if (num == firstNumber) {
                return new int[]{firstNumber, secondNumber};
            }
        }

        return new int[]{secondNumber, firstNumber};
    }
}
```
