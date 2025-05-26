# Two Sum : Find two indices such that their values sum to a target. Pattern: Hashing
1. Make a map of Integer-Integer.
2. We iterate through the array.
3. For each number in the array we find **targer - number** , this is the complement of this number if this is present in the map then we can return both these indices.
4. Put the current number in the map with its indices.
5. O(n) solution with O(n) space.
```
public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{};
    }
```
