# Single Number 

Given an integer array nums where every element appears three times except for one, which appears exactly once. Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## Sorting and HashMap Approach

Out of scope due to requirements but these would be the most basic approaches.

## BITWISE Check

The idea is to look at **each bit position separately**.   
Since every number appears **3 times except one**, the number of `1`s at every bit position will be a multiple of 3, except for the bits belonging to the unique number.

```java
class Solution {
    public int singleNumber(int[] nums) {
        int answer = 0;

        // An integer has 32 bits.
        // We check each bit position independently.
        for (int bit = 0; bit < 32; bit++) {

            int count = 0;

            // Check this bit in every number.
            for (int index = 0; index < nums.length; index++) {

                // Shift the current number right by 'bit' positions.
                // Then & 1 checks whether that bit is 1.
                //
                // Example:
                // nums[index] = 5  -> 101
                // bit = 1
                // 5 >> 1 = 10
                // 10 & 1 = 0
                if (((nums[index] >> bit) & 1) == 1) {
                    count++;

                    // Every number except the unique one
                    // appears exactly 3 times.
                    //
                    // So groups of 3 cancel out.
                    count %= 3;
                }
            }

            // If count is 1, this bit belongs to the
            // number that appears only once.
            //
            // Set this bit in the answer.
            if (count != 0) {
                answer |= count << bit;
            }
        }

        return answer;
    }
}
```

### The core idea

Suppose:

```text
nums = [2, 2, 2, 5]
```

Binary:

```text
2 = 010
2 = 010
2 = 010
5 = 101
```

Look at each bit separately:

```text
Bit 0: 0 0 0 1 → count = 1
Bit 1: 1 1 1 0 → count = 3 → 0 after % 3
Bit 2: 0 0 0 1 → count = 1
```

So the remaining bits are:

```text
101 = 5
```

### These two lines are the most important

```java
((nums[index] >> bit) & 1)
```

**Gets the current bit.**

And:

```java
count %= 3;
```

**Removes the contribution of numbers appearing three times.**

Finally:

```java
answer |= count << bit;
```

**Puts the unique number's bit back into `answer`.**

So the overall pattern is:

```text
Check bit 0 → find unique bit
Check bit 1 → find unique bit
Check bit 2 → find unique bit
...
Check bit 31
        ↓
Reconstruct the unique number
```

This works in **O(32 × n) = O(n)** time and **O(1)** extra space.




## Second Approach (BITWISE State Machine)

Yes. This is the **bitwise state-machine version** of the same problem.

The previous solution explicitly counted each bit. This one does the same thing **without looping over 32 bits**.

```java
class Solution {
    public int singleNumber(int[] nums) {
        // 'ones' stores bits that have appeared exactly once.
        // 'twos' stores bits that have appeared exactly twice.
        int ones = 0;
        int twos = 0;

        for (int num : nums) {

            // Add the current number to 'ones'.
            // If a bit was already in twos, remove it from ones.
            ones = (ones ^ num) & ~twos;

            // Add the current number to 'twos'.
            // If a bit is now in ones, remove it from twos.
            twos = (twos ^ num) & ~ones;
        }

        // Numbers appearing three times have their bits
        // removed from both ones and twos.
        return ones;
    }
}
```

### The easiest way to understand it

For **each individual bit**, we need to track how many times it has appeared:

```text
0 → appeared 0 times
1 → appeared 1 time
2 → appeared 2 times
3 → appeared 3 times → back to 0
```

We only need two variables to represent these states:

```text
ones = bits that appeared 1 time
twos = bits that appeared 2 times
```

So for a particular bit:

```text
                 num has bit = 1
                         ↓
       ┌─────────────────────────────────┐
       │                                 │
       ↓                                 │
    0 times → 1 time → 2 times → 3 times
       ↑                         │
       └─────────────────────────┘
```

And after 3 occurrences, that bit disappears from both `ones` and `twos`.

---

### What does `ones = (ones ^ num) & ~twos` do?

Break it into two parts.

#### 1. `ones ^ num`

XOR toggles bits.

If a bit is:

```text
ones = 0
num  = 1
```

then:

```text
0 ^ 1 = 1
```

So the bit enters `ones`.

If it was already there:

```text
ones = 1
num  = 1

1 ^ 1 = 0
```

So it leaves `ones`.

But this alone isn't enough because we also need to track `twos`.

#### 2. `& ~twos`

This means:

> Don't allow a bit to remain in `ones` if that bit is currently in `twos`.

So:

```java
ones = (ones ^ num) & ~twos;
```

means:

> Toggle the bits using `num`, but remove anything that is already in `twos`.

---

### And `twos` does the same thing

```java
twos = (twos ^ num) & ~ones;
```

It toggles the bits in `twos`, but removes anything that is currently in `ones`.

Together, these two lines create the 3-state cycle.

---

### Let's trace one bit

Suppose one bit of `num` is `1` three times.

Initially:

```text
ones = 0
twos = 0
```

#### First occurrence

```text
ones = (0 ^ 1) & ~0
     = 1

twos = (0 ^ 1) & ~1
     = 0
```

State:

```text
ones = 1
twos = 0
```

The bit appeared **once**.

---

#### Second occurrence

```text
ones = (1 ^ 1) & ~0
     = 0

twos = (0 ^ 1) & ~0
     = 1
```

State:

```text
ones = 0
twos = 1
```

The bit appeared **twice**.

---

#### Third occurrence

```text
ones = (0 ^ 1) & ~1
     = 0

twos = (1 ^ 1) & ~0
     = 0
```

State:

```text
ones = 0
twos = 0
```

The bit appeared **three times**, so it has been cancelled.

---

### Why does the answer end up in `ones`?

The unique number appears only once.

Therefore, its bits go:

```text
0 → 1
```

and never reach the second or third state.

So at the end:

```java
return ones;
```

contains exactly the bits of the number that appeared once.

### A useful way to remember it

Think of:

```text
ones = "seen once"
twos = "seen twice"
```

and the algorithm maintains:

```text
First time  → ones
Second time → twos
Third time  → remove from both
```

The clever part is that **each bit position goes through this state machine independently**, even though we're operating on the entire 32-bit integer at once.

So compared with your previous solution:

| Approach     | Idea                               |
| ------------ | ---------------------------------- |
| Bit-counting | Explicitly process all 32 bits     |
| `ones/twos`  | Process all 32 bits simultaneously |

Both are **O(n)** time and **O(1)** space.
