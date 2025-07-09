# Reschedule Meetings for Maximum Free Time I

## Learnings and Observations 

If we have n meetings in eventTime it creates n + 1 gaps that we can merge to create one big freeTime.

If we can move k meetings we can merge k+1 continuous gaps in these meetings.

When you observe these main things it becomes quite obvious that we need to do a sliding window to find the max sum of k + 1 continuous gaps.

## Code

```java
class Solution {
    public int maxFreeTime(int eventTime, int k, int[] startTime, int[] endTime) {
        int n = startTime.length;
        int[] gaps = new int[n + 1];
        gaps[0] = startTime[0];
        for (int i = 1; i < n; ++i) {
            gaps[i] = startTime[i] - endTime[i - 1];
        }
        gaps[n] = eventTime - endTime[n - 1];
        int sz = Math.min(k + 1, gaps.length);
        int curr = 0, best = 0;
        for (int i = 0; i < sz; ++i) curr += gaps[i];
        best = curr;
        for (int i = sz; i < gaps.length; ++i) {
            curr += gaps[i] - gaps[i - sz];
            if (curr > best) best = curr;
        }
        return (int) best;
    }
}
```