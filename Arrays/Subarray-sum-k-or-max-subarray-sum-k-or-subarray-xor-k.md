# Subarray sums equals k

Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.

This problem would be much easier if we are promised only positive integers. As there wont be a possibility of subarrays with sum 0 due to negative numbers.

## Steps
1. ans = 0 , sum = 0

2. make a map of integer , integer and put (0,1) to specify that there is one Subarray with sum 0.

3. For every int in nums add num to sum and if we have the sum - k in the map those many Subarray we have found because if current sum is 10 and target is 15 then we need to find how many Subarray at the back we have with 5 as their sum. If we have 3 in map then we add 3 to our answer.

4. add the current sum to the map.

## Code

```java
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

 # Max subarray sum k

 Given an array nums of size n and an integer k, find the length of the longest sub-array that sums to k. If no such sub-array exists, return 0.

 # Mistakes
 Don't think about sliding window as if I get index 1 to 5 as a subarray I will move the left forward with out accounting for the possibility of finding some negatives that will lead to an array of sum 0 from index 6 to some index j and then the largest subarray would be 1 to j.

For **longest subarray with sum `k`**, the prefix-sum + HashMap idea is the same, but there are two important changes:

* Store the **first index** where a prefix sum occurs.
* When `sum - k` exists, calculate the length instead of counting occurrences.
* Do **not overwrite** an existing prefix-sum index, because the earliest index gives the longest subarray.

```java
class Solution {
    public int longestSubarray(int[] nums, int k) {
        int answer = 0;
        int sum = 0;

        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);

        for (int index = 0; index < nums.length; index++) {
            sum += nums[index];

            if (map.containsKey(sum - k)) {
                answer = Math.max(
                    answer,
                    index - map.get(sum - k)
                );
            }

            // Store only the first occurrence.
            if (!map.containsKey(sum)) {
                map.put(sum, index);
            }
        }

        return answer;
    }
}
```

### Why `map.put(0, -1)`?

Suppose:

```text
nums = [2, 3]
k = 5
```

At index `1`:

```text
sum = 5
sum - k = 0
```

The prefix sum `0` occurred at index `-1`, so:

```text
length = 1 - (-1) = 2
```

Therefore `[2, 3]` is correctly counted.

### Why don't we overwrite the index?

Consider:

```text
nums = [1, 2, 3, 1, 1]
k = 3
```

If a prefix sum occurs multiple times, we want its **earliest occurrence**:

```java
if (!map.containsKey(sum)) {
    map.put(sum, index);
}
```

Because:

```text
currentIndex - earliestIndex
```

will always produce the longest possible subarray.

So compared with your `subarraySum()` code:

```java
// Count all subarrays
map.put(sum, frequency);
```

becomes:

```java
// Remember earliest position
map.put(sum, firstIndex);
```

and:

```java
ans += map.get(sum - k);
```

becomes:

```java
ans = Math.max(ans, index - map.get(sum - k));
```

**Time:** `O(n)`
**Space:** `O(n)`



# Count subarrays with given xor K

Given an array of integers nums and an integer k, return the total number of subarrays whose XOR equals to k.

Yes. This is **almost exactly the same prefix-sum approach**, except you use **prefix XOR instead of prefix sum**.

The key identity is:

```text
prefixXor ^ previousPrefixXor = k
```

Therefore:

```text
previousPrefixXor = prefixXor ^ k
```

So your HashMap stores the **frequency** of each prefix XOR, just like your original `subarraySum()` solution stores prefix-sum frequencies.

```java
class Solution {
    public int subarraysWithXorK(int[] nums, int k) {
        int answer = 0;
        int xor = 0;

        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        for (int num : nums) {
            xor ^= num;

            if (map.containsKey(xor ^ k)) {
                answer += map.get(xor ^ k);
            }

            map.put(xor, map.getOrDefault(xor, 0) + 1);
        }

        return answer;
    }
}
```

### Compare it with your sum version

Your original:

```java
sum += num;

if (map.containsKey(sum - k)) {
    answer += map.get(sum - k);
}
```

XOR version:

```java
xor ^= num;

if (map.containsKey(xor ^ k)) {
    answer += map.get(xor ^ k);
}
```

That's basically the only conceptual change.

### Why `xor ^ k`?

Suppose:

```text
prefixXor = A
previousPrefixXor = B
```

The XOR of the subarray between them is:

```text
A ^ B
```

We want:

```text
A ^ B = k
```

XOR both sides with `k`:

```text
A ^ B ^ k = k ^ k
A ^ k = B
```

Therefore:

```text
B = A ^ k
```

So whenever we've already seen `xor ^ k`, every occurrence represents a subarray ending at the current index whose XOR is `k`.

And just like your original `subarraySum()` solution, we store **frequencies**, because multiple previous prefix XORs can produce multiple valid subarrays.

**Time:** `O(n)`
**Space:** `O(n)`
