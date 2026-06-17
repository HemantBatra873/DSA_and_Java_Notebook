# Egg Dropping Puzzle

## Problem Statement

You are given:

- `n` identical eggs
- A building with `k` floors numbered from `1` to `k`

There exists an unknown floor `f` such that:

- Any egg dropped from a floor higher than `f` will break.
- Any egg dropped from floor `f` or below will survive.
- All eggs behave identically.
- A surviving egg can be reused.
- A broken egg is discarded.

The goal is to determine the value of `f` using the minimum number of egg drops in the **worst case**.

---

## Understanding the Problem

Suppose:

- `n = 2`
- `k = 36`
- Hidden floor `f = 20`

Then:

| Floor | Result |
|---------|---------|
| 1 - 20 | Survives |
| 21 - 36 | Breaks |

You do not know that `f = 20`.

Each drop gives information:

### Egg breaks

If you drop from floor `x` and the egg breaks:

```text
f < x
```

You only need to search below floor `x`.

### Egg survives

If you drop from floor `x` and the egg survives:

```text
f >= x
```

You only need to search above floor `x`.

The challenge is to minimize the number of drops required in the worst case.

---

# Solution 1: Classic Dynamic Programming

## State

Let:

```java
dp[e][f]
```

represent the minimum number of drops required with:

- `e` eggs
- `f` floors

---

## Transition

Suppose we drop an egg from floor `x`.

### Case 1: Egg breaks

We are left with:

```text
e - 1 eggs
x - 1 floors
```

Cost:

```java
dp[e - 1][x - 1]
```

### Case 2: Egg survives

We are left with:

```text
e eggs
f - x floors
```

Cost:

```java
dp[e][f - x]
```

Since we need the worst-case answer:

```java
1 + Math.max(
    dp[e - 1][x - 1],
    dp[e][f - x]
)
```

We try every possible floor `x` and choose the minimum.

---

## Recurrence

```java
dp[e][f] =
    min over all x (
        1 + max(
            dp[e - 1][x - 1],
            dp[e][f - x]
        )
    )
```

---

## Java Implementation

```java
class Solution {

    public int eggDrop(int eggs, int floors) {

        int[][] dp = new int[eggs + 1][floors + 1];

        for (int f = 1; f <= floors; f++) {
            dp[1][f] = f;
        }

        for (int e = 2; e <= eggs; e++) {

            for (int f = 1; f <= floors; f++) {

                dp[e][f] = Integer.MAX_VALUE;

                for (int x = 1; x <= f; x++) {

                    int worstCase =
                        1 + Math.max(
                            dp[e - 1][x - 1],
                            dp[e][f - x]
                        );

                    dp[e][f] =
                        Math.min(dp[e][f], worstCase);
                }
            }
        }

        return dp[eggs][floors];
    }
}
```

### Complexity

```text
Time  : O(n * kÂ²)
Space : O(n * k)
```

---

# Solution 2: Optimized Dynamic Programming

This is the more elegant interview solution.

Instead of asking:

> With `n` eggs and `k` floors, how many moves do we need?

Ask:

> With `n` eggs and `m` moves, how many floors can we test?

---

## State

Let:

```java
dp[e][m]
```

represent:

```text
Maximum number of floors that can be checked
using e eggs and m moves.
```

---

## Key Observation

Suppose we make one drop.

### Egg breaks

We can test:

```java
dp[e - 1][m - 1]
```

floors below.

### Egg survives

We can test:

```java
dp[e][m - 1]
```

floors above.

### Current floor

We also test the current floor itself.

Therefore:

```java
dp[e][m]
    = dp[e - 1][m - 1]
    + dp[e][m - 1]
    + 1;
```

---

## Example

For 2 eggs:

| Moves | Floors Testable |
|---------|---------|
| 1 | 1 |
| 2 | 3 |
| 3 | 6 |
| 4 | 10 |
| 5 | 15 |
| 6 | 21 |
| 7 | 28 |
| 8 | 36 |

Since 8 moves can test 36 floors:

```text
Answer = 8
```

---

## Java Implementation

```java
class Solution {

    public int eggDrop(int eggs, int floors) {

        long[][] dp = new long[eggs + 1][floors + 1];

        int moves = 0;

        while (dp[eggs][moves] < floors) {

            moves++;

            for (int e = 1; e <= eggs; e++) {

                dp[e][moves] =
                    dp[e - 1][moves - 1]
                    + dp[e][moves - 1]
                    + 1;
            }
        }

        return moves;
    }
}
```

### Complexity

```text
Time  : O(n * answer)
Space : O(n * answer)
```

---

# Key Interview Insight

The classic DP directly computes:

```text
Minimum moves needed for given eggs and floors.
```

The optimized DP computes:

```text
Maximum floors testable for given eggs and moves.
```

That change of perspective leads to the recurrence:

```java
dp[e][m]
    = dp[e - 1][m - 1]
    + dp[e][m - 1]
    + 1;
```

which is the standard optimized solution used in interviews and competitive programming.