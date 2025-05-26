# Sort Colors - Sort 3 numbers

## Description - 
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.  
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.  
You must solve this problem without using the library's sort function.  

eg.
```
 nums = [2,0,2,1,1,0]
```

## Steps - 
1. Three pointer low = mid = 0 and high = n - 1
2. code runs till mid <= high.
3. Three cases mid = 0 or 1 or 2
4. If nums[mid] == 1 simply move mid forward
5. if nums[mid] == 0 the low pointer always store the position where the next 0 must be inserted so swap(nums, low , mid) and low++ and mid++.
6. if nums[mid] == 2 then the high always store the position where the next 2 can be inserted so swap(nums , mid , high) and high--.
7. Please make sure we move mid when low moves but not with high because with high we are not sure whats coming to mid it can be 2 as well.
8. But with low its clear that every element below mid is 0 so if one comes its alright and if zero comes its still alright.



## Code 
```
class Solution {
    public void sortColors(int[] nums) {
        int low = 0 , mid = 0 , high = nums.length - 1;
        while(mid <= high){
            if(nums[mid] == 0){
                swap(nums , mid , low);
                low++;
                mid++;
            }else if(nums[mid] == 1) mid++;
            else{
                swap(nums , high , mid);
                high--;
            }
        }
    }

    private void swap(int[] nums , int i , int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
