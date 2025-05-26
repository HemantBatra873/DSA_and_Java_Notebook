# Subarray sums equals k

Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.

This problem would be much easier if we are promised only positive integers.

## Steps
1. ans = 0 , sum = 0

2. make a map of integer , integer and put (0,1) to specify that there is one Subarray with sum 0.

3. For every int in nums add num to sum and if we have the sum - k in the map those many Subarray we have found because if current sum is 10 and target is 15 then we need to find how many Subarray at the back we have with 5 as their sum. If we have 3 in map then we add 3 to our answer.

4. add the current sum to the map.

## Code

```
class Solution {
    public int subarraySum(int[] nums, int k) {
        int ans = 0;
        int sum = 0;
        Map<Integer , Integer> map = new HashMap<>();
        map.put(0,1);
        for(int num : nums){
            sum += num;
            if(map.containsKey(sum - k)) ans += map.get(sum - k);          
            map.put(sum , map.getOrDefault(sum , 0) + 1);
        }
        return ans;
    }
}

```
 