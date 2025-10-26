# Sliding Window Maximum

https://leetcode.com/problems/sliding-window-maximum/

You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

## Important things 

- Brute force is easy.
- Even the approach with pq is intiutive but will still be considered O(nlogn).
- Best approach is to stimulate the window process.

## How do we stimulate the window

- First we use a deque of indexes. Simply because we are trying to remove the indexes that are not in the window or are not useful so we need two ends of a queue.
- Now for each index first we check if there are elements that are out of the window. If yes we remove them.
- Then we check if there are elements which are smaller than the current element because we are trying to maintain a monotonic queue where the biggest number stays in the front and th\
  smaller number is added to the back.
- Then we add the element to the back of the queue and if the index is bigger that the window size k then we add the first element to the result because thats the max element.

  ## Code in java

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> dq = new ArrayDeque<>(); 
        int ri = 0;

        for (int i = 0; i < n; i++) {
            while (!dq.isEmpty() && dq.peekFirst() <= i - k)
                dq.pollFirst();

            while (!dq.isEmpty() && nums[dq.peekLast()] < nums[i])
                dq.pollLast();

            dq.offerLast(i);

            if (i >= k - 1)
                result[ri++] = nums[dq.peekFirst()];
        }

        return result;
    }
}

  ```
