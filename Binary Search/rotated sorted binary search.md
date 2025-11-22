# Rotated sorted binary search 

so if you had an array which was sorted and then go trotted left or right by some index you can still apply binary search to it. 

in order to apply binary search first start by taking left 0 right to the last index of the array and then we will keep going till the left is less than equal to right just like in the normal binary search. 


the main thing that will change by the rotation is that first will have to find out which part left or right is still sorted including the mid element if the left half is sorted then we will check if the target belongs to the left half if it does belong to the left half then we will move the right to mid minus one as you will move the left to mid + 1 

and vice versa if the right half including May Day sorted then first level check if the target belongs to the right half and if it does then we will move the left to mid + 1 as we will move the right to mid minus one 

```java

class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] >= nums[left]) {
                if (nums[left] <= target && target <= nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {
                if (nums[mid] <= target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }

        return -1;        
    }
}

```