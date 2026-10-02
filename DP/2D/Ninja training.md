This is the classic **Ninja Training / Vacation** DP problem. The key state is:

> `dp[day][lastActivity]` = maximum points up to `day` when `lastActivity` is the activity that cannot be chosen today.

I'll show all three approaches: **top-down → bottom-up → space optimized**.

---

## 1. Top-Down DP — Recursion + Memoization

We can define:

```text
recur(day, lastActivity)
```

where `lastActivity` tells us what we did on the previous day.

For example:

```text
lastActivity = 0 → running was done yesterday
lastActivity = 1 → stealth was done yesterday
lastActivity = 2 → fighting was done yesterday
lastActivity = 3 → nothing was done yesterday
```

For every day, try the two activities different from `lastActivity`.

```java
class Solution {
    public int maximumPoints(int[][] points) {
        int numberOfDays = points.length;
        int[][] dp = new int[numberOfDays][4];

        for (int[] row : dp) {
            Arrays.fill(row, -1);
        }

        return recur(numberOfDays - 1, 3, points, dp);
    }

    private int recur(int day, int lastActivity, int[][] points, int[][] dp) {
        if (dp[day][lastActivity] != -1) {
            return dp[day][lastActivity];
        }

        if (day == 0) {
            int maximumPoints = 0;

            for (int activity = 0; activity < 3; activity++) {
                if (activity != lastActivity) {
                    maximumPoints = Math.max(
                        maximumPoints,
                        points[0][activity]
                    );
                }
            }

            return dp[day][lastActivity] = maximumPoints;
        }

        int maximumPoints = 0;

        for (int activity = 0; activity < 3; activity++) {
            if (activity != lastActivity) {
                int currentPoints = points[day][activity]
                        + recur(day - 1, activity, points, dp);

                maximumPoints = Math.max(maximumPoints, currentPoints);
            }
        }

        return dp[day][lastActivity] = maximumPoints;
    }
}
```

### Complexity

There are:

```text
n × 4
```

states, and each state tries 3 activities.

**Time:** `O(n × 4 × 3)` → **O(n)**
**Space:** `O(n × 4)` for DP + `O(n)` recursion stack → **O(n)**

---

# 2. Bottom-Up DP

Now let's convert the same recurrence into tabulation.

The top-down recurrence was:

```text
dp[day][lastActivity]
    = max(
        points[day][activity] + dp[day - 1][activity]
      )
```

where:

```text
activity != lastActivity
```

### Base case

For day `0`:

```java
dp[0][0] = max(points[0][1], points[0][2]);
dp[0][1] = max(points[0][0], points[0][2]);
dp[0][2] = max(points[0][0], points[0][1]);
dp[0][3] = max(
    points[0][0],
    points[0][1],
    points[0][2]
);
```

`3` means there was no previous activity.

### Complete solution

```java
class Solution {
    public int maximumPoints(int[][] points) {
        int numberOfDays = points.length;
        int[][] dp = new int[numberOfDays][4];

        // Base case: day 0
        dp[0][0] = Math.max(points[0][1], points[0][2]);
        dp[0][1] = Math.max(points[0][0], points[0][2]);
        dp[0][2] = Math.max(points[0][0], points[0][1]);
        dp[0][3] = Math.max(
            points[0][0],
            Math.max(points[0][1], points[0][2])
        );

        // Build from day 1 onwards
        for (int day = 1; day < numberOfDays; day++) {
            for (int lastActivity = 0; lastActivity < 4; lastActivity++) {

                dp[day][lastActivity] = 0;

                for (int activity = 0; activity < 3; activity++) {
                    if (activity != lastActivity) {
                        int currentPoints =
                            points[day][activity]
                            + dp[day - 1][activity];

                        dp[day][lastActivity] = Math.max(
                            dp[day][lastActivity],
                            currentPoints
                        );
                    }
                }
            }
        }

        return dp[numberOfDays - 1][3];
    }
}
```

### Complexity

There are `n × 4` states, each checking 3 activities.

**Time:** `O(n × 4 × 3)` → **O(n)**
**Space:** `O(n × 4)` → **O(n)**

---

# 3. Space-Optimized Bottom-Up DP

Notice that:

```text
dp[day][lastActivity]
```

only depends on:

```text
dp[day - 1][activity]
```

We don't need the entire DP table. We only need the previous day's values.

So replace:

```java
int[][] dp
```

with:

```java
int[] previousDay
int[] currentDay
```

### Solution

```java
class Solution {
    public int maximumPoints(int[][] points) {
        int[] previousDay = new int[4];

        // Base case: day 0
        previousDay[0] = Math.max(points[0][1], points[0][2]);
        previousDay[1] = Math.max(points[0][0], points[0][2]);
        previousDay[2] = Math.max(points[0][0], points[0][1]);
        previousDay[3] = Math.max(
            points[0][0],
            Math.max(points[0][1], points[0][2])
        );

        for (int day = 1; day < points.length; day++) {
            int[] currentDay = new int[4];

            for (int lastActivity = 0; lastActivity < 4; lastActivity++) {
                for (int activity = 0; activity < 3; activity++) {
                    if (activity != lastActivity) {
                        int currentPoints =
                            points[day][activity]
                            + previousDay[activity];

                        currentDay[lastActivity] = Math.max(
                            currentDay[lastActivity],
                            currentPoints
                        );
                    }
                }
            }

            previousDay = currentDay;
        }

        return previousDay[3];
    }
}
```

### Complexity

**Time:** `O(n)`
**Space:** `O(4)` → **O(1)**

---

## Understanding the `lastActivity` trick

This is the most important part of this problem.

Suppose:

```text
points =

Day       Running   Stealth   Fighting
0            10        50        20
1            20        100       30
2            40        20        30
```

On day 0, we can choose anything.

Suppose we choose **Stealth (1)**.

Then on day 1:

```text
Stealth cannot be chosen.
```

So we can choose:

```text
Running
Fighting
```

That's why the state stores the **previous activity**.

The transition is always:

```java
if (activity != lastActivity)
```

and:

```java
points[day][activity] + dp[day - 1][activity]
```

The slightly confusing part is that `lastActivity` represents the activity that is **blocked today**, while `activity` represents what we **actually did today**.

### The three approaches at a glance

| Approach               |   Time |          Space |
| ---------------------- | -----: | -------------: |
| Recursion              | `O(n)` | `O(n)` + stack |
| Top-down + Memoization | `O(n)` |         `O(n)` |
| Bottom-up Tabulation   | `O(n)` |         `O(n)` |
| Space-optimized DP     | `O(n)` |         `O(1)` |

For interviews, I'd recommend being able to derive them in this order:

**Recursion → Memoization → Tabulation → Space Optimization**

That progression makes the conversion between DP approaches much easier.
