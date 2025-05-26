# Rearrange Array Elements by Sign

You are given a 0-indexed integer array nums of even length consisting of an equal number of positive and negative integers.

You should return the array of nums such that the the array follows the given conditions:

Every consecutive pair of integers have opposite signs.
For all integers with the same sign, the order in which they were present in nums is preserved.
The rearranged array begins with a positive integer.
Return the modified array after rearranging the elements to satisfy the aforementioned conditions.


## Code 
```
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int ans[] = new int[nums.length];
        int i=0,j=1;
        int n=nums.length;
        for(int k=0;k<n;k++) {
            if(nums[k]<0) {
                ans[j] = nums[k];
                j+=2;
            }
            else{
                ans[i] = nums[k];
                i+=2;
            }
        }
        return ans;
    }
}
```
 