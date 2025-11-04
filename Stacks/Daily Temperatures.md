## Daily Temperatures
https://leetcode.com/problems/daily-temperatures/description/

Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature.   
If there is no future day for which this is possible, keep answer[i] == 0 instead.

Notice the pattern that using for look only it will take n^2 so we need a data structure that will work by computing the answer for multiple values when a new value comes in and that is stack.

```java

class Solution {
    public int[] dailyTemperatures(int[] t) {
        if(t.length == 1) return new int[1];
        int[] res = new int[t.length];
        Stack<int[]> s = new Stack<>();
        for(int i = 0 ; i < t.length ; i++){ 
            while(!s.isEmpty() && s.peek()[0] < t[i]){
                int idx = s.pop()[1];
                res[idx] = i - idx;
            }
            s.push(new int[]{t[i] , i});
        }
        return res;
    }
}

```

