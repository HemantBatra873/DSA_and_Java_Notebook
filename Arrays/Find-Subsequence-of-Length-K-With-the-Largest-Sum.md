#  Find Subsequence of Length K With the Largest Sum

You are given an integer array nums and an integer k. You want to find a subsequence of nums of length k that has the largest sum.

Return any such subsequence as an integer array of length k.

A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

## My original code (6ms)

Make a map of values and indexes and then sort the map based on values.  
Then pick the k top values and set flags for those indexes.  
Iterate over the flags and where true that values is added from the nums array.

```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        int n = nums.length;
        boolean[] flag = new boolean[n];
        int[][] map = new int[n][2];
        int[] res = new int[k];
        int idx = 0;
        for(int i = 0 ; i < n ; i++){
            map[i][0] = nums[i];
            map[i][1] = i;
        }
        Arrays.sort(map , (a,b) -> Integer.compare(b[0], a[0]));
        for(int i = 0 ; i < k ; i++){
            flag[map[i][1]] = true;
        }
        for(int i = 0 ; i < n ; i++){
            if(flag[i]){
                res[idx] = nums[i];
                idx++;
            }
        }
        return res;
    }
}
```

## More cleaner Priority Queue Code (9ms)

Keep only top k elements in the pq and then make a list out of them and sort the list based on indexes and make a result out of the list.

```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));

        for (int i = 0; i < nums.length; i++) {
            pq.offer(new int[]{nums[i], i}); 
            if (pq.size() > k) {
                pq.poll(); 
            }
        }

        List<int[]> list = new ArrayList<>(pq);
        list.sort(Comparator.comparingInt(a -> a[1])); 

        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = list.get(i)[0];
        }

        return res;
    }
}
```

## The best code (2ms) - threshold counting method

Make a sorted copy of the original array.  
Now get the n - k th element of the sorted array, this is the threshold value. All the values in the final array will be larger than this.  
The problem is we dont have idea about the values equal to threshold. What if we the threshold value is 5 and in the array it appears 4 times and in top k elements it appears only 2 times.  
For that purpose we must know the frequency of threshold in top k elements.  
After this we can simply iterate over the original array and add every value more than threshhold and also threshold until the frequency is equal to the frequency in top k elements.

```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        int n = nums.length;
        int[] sorted = Arrays.copyOf(nums, n);

        Arrays.sort(sorted);

        int threshold = sorted[n - k];
        int thresholdCnt = 0;
        for (int i = n - k; i < n; i++) {
            if (sorted[i] == threshold) {
                thresholdCnt++;
            }
        }

        int[] ans = new int[k];

        int p = 0;
        for (int num : nums) {
            if (num > threshold) {
                ans[p++] = num;
            } else if (num == threshold && thresholdCnt > 0) {
                ans[p++] = num;
                thresholdCnt--;
            }
            if (p== k) {
                break;
            }
        }

        return ans;
    }
}
```
