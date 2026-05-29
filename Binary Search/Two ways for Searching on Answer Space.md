# Binary Search Cheat Sheet

## The Root Cause of Confusion

Most binary search bugs happen because people mix two different templates.

Choose **one template** and stick to it.

---

# Template 1: Exact Search

Use when searching for a specific value.

Examples:

* Binary Search (LeetCode 704)
* Search Insert Position
* Find target in sorted array

```java
int low = 0;
int high = n - 1;

while (low <= high) {

    int mid = low + (high - low) / 2;

    if (arr[mid] == target)
        return mid;

    else if (arr[mid] < target)
        low = mid + 1;

    else
        high = mid - 1;
}

return -1;
```

### Rules

```text
while(low <= high)

low = mid + 1
high = mid - 1
```

Why?

Because `mid` has already been checked.

---

# Template 2: Binary Search on Answer

Use when solving optimization problems.

Examples:

* Allocate Books
* Painter's Partition
* Aggressive Cows
* Ship Packages Within D Days
* Split Array Largest Sum

---

## Mental Model

Imagine the search space looks like:

```text
F F F F F T T T T T
          ^
       Answer
```

We are searching for the **first True**.

---

## Generic Code

```java
int ans = -1;

while (low <= high) {

    int mid = low + (high - low) / 2;

    if (isPossible(mid)) {

        ans = mid;
        high = mid - 1;

    } else {

        low = mid + 1;
    }
}

return ans;
```

---

## Rules

If current answer is possible:

```java
high = mid - 1;
```

Try finding a smaller valid answer.

If current answer is not possible:

```java
low = mid + 1;
```

Need a larger answer.

---

# Why Not Use high = mid?

Example:

```text
low = 5
high = 6

mid = 5
```

If:

```java
high = mid;
```

Then:

```text
low = 5
high = 5
```

Next iteration:

```text
mid = 5
```

Again:

```java
high = mid;
```

Infinite loop.

With:

```java
while(low <= high)
```

Always use:

```java
low = mid + 1;
high = mid - 1;
```

---

# Alternative Binary Search Style

Some people use:

```java
while(low < high) {

    int mid = low + (high - low) / 2;

    if(isPossible(mid))
        high = mid;
    else
        low = mid + 1;
}

return low;
```

This is also correct.

---

# Valid Pairings

## Style A

```java
while(low <= high)
```

Updates:

```java
low = mid + 1;
high = mid - 1;
```

Return:

```java
ans
```

or target index.

---

## Style B

```java
while(low < high)
```

Updates:

```java
low = mid + 1;
high = mid;
```

Return:

```java
low
```

or

```java
high
```

because both become equal.

---

# Never Mix Templates

Wrong:

```java
while(low <= high)
high = mid;
```

Wrong:

```java
while(low < high)
high = mid - 1;
```

Mixing templates causes:

* Infinite loops
* Missing answers
* Off-by-one errors

---

# Interview Rule

For most DSA and interview problems:

Use:

```java
while(low <= high)
```

with:

```java
low = mid + 1;
high = mid - 1;
```

This handles:

* Exact Search
* First Valid Answer
* Last Valid Answer
* Binary Search on Answer

and is usually the easiest to reason about.

---

# Quick Decision Tree

### Searching for a target?

```java
while(low <= high)
```

Return index or -1.

---

### Minimizing something?

Examples:

* Allocate Books
* Painter Partition

Think:

```text
F F F F T T T T
```

Move:

```java
Possible -> Left
Not Possible -> Right
```

---

### Maximizing something?

Examples:

* Aggressive Cows

Think:

```text
T T T T F F F F
```

Move:

```java
Possible -> Right
Not Possible -> Left
```

---

# Golden Rule

Always draw:

```text
F F F F T T T T
```

or

```text
T T T T F F F F
```

Once you know where the answer lies, the binary search updates become obvious.
