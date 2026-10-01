# Longest Palindromic Substring

## Problem

Given a string `s`, find the **longest palindromic substring**.

A palindrome reads the same forward and backward.

Example:

```text
s = "babad"

Answer = "bab"
```

`"aba"` is also a valid answer.

---

# SOLUTION 1: Expand Around Centers

**Time:** `O(n²)`
**Space:** `O(1)`

### Key Insight

Every palindrome has a **center**.

The center can be:

* A single character → odd-length palindrome
* The gap between two characters → even-length palindrome

For example:

```text
"racecar"

       c
       ↑
    center
```

Odd-length palindrome:

```text
racecar
   ↑
 center
```

Even-length palindrome:

```text
abba

  ↑↑
center
```

Therefore, for every index, we check **both types of centers**.

## Steps

1. Go to every index in the string.
2. Treat the current index as the center of an **odd-length** palindrome.
3. Treat the gap between the current index and the next index as the center of an **even-length** palindrome.
4. Expand two pointers:

   * `left--`
   * `right++`
5. Continue while:

   * `left` is valid
   * `right` is valid
   * `s[left] == s[right]`
6. Keep track of the longest palindrome found.
7. Calculate its starting position using:

```text
start = i - (maxLength - 1) / 2
```

## Code

```java
class Solution {

    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) {
            return s;
        }

        int start = 0;
        int maxLength = 1;

        for (int i = 0; i < s.length(); i++) {

            // Odd-length palindrome.
            // Example: "aba"
            int oddLength = expandAroundCenter(s, i, i);

            // Even-length palindrome.
            // Example: "abba"
            int evenLength = expandAroundCenter(s, i, i + 1);

            int currentLength = Math.max(oddLength, evenLength);

            if (currentLength > maxLength) {
                maxLength = currentLength;

                // Calculate where the palindrome starts.
                start = i - (currentLength - 1) / 2;
            }
        }

        return s.substring(start, start + maxLength);
    }

    /**
     * Expands outward from the given center
     * and returns the palindrome length.
     */
    private int expandAroundCenter(String s, int left, int right) {

        while (left >= 0
                && right < s.length()
                && s.charAt(left) == s.charAt(right)) {

            left--;
            right++;
        }

        // left and right have moved one position
        // outside the palindrome.
        return right - left - 1;
    }
}
```

### Why do we return `right - left - 1`?

Suppose:

```text
left = -1
right = 4
```

The valid palindrome was between:

```text
0 ... 3
```

So its length is:

```text
right - left - 1
= 4 - (-1) - 1
= 4
```

The `-1` is necessary because both pointers have moved **one position beyond** the palindrome.

---

# SOLUTION 2: Manacher's Algorithm

**Time:** `O(n)`
**Space:** `O(n)`

Manacher's Algorithm solves the same problem in **linear time**.

The main problem with Expand Around Centers is that we repeatedly compare characters that we may have already compared before.

Manacher's algorithm avoids much of this repeated work by **reusing information about previously discovered palindromes**.

---

## Key Idea

The biggest difficulty is handling both:

```text
Odd palindrome:   aba
Even palindrome:  abba
```

Manacher's algorithm solves this by transforming the string.

For example:

```text
Original:

abba
```

Add separators:

```text
#a#b#b#a#
```

Now every palindrome has a **single center**.

For example:

```text
#a#b#b#a#
      ↑
    center
```

We also add `#` at both ends so that we don't need separate handling for boundaries.

---

## Step 1: Transform the String

For:

```text
s = "abba"
```

Transform it into:

```text
# a # b # b # a #
```

Or:

```text
#a#b#b#a#
```

This converts:

```text
Odd palindrome:
aba
```

and:

```text
Even palindrome:
abba
```

into the same type of problem: **expand around one center**.

---

## Step 2: Create the `radius` Array

For every position, store how far the palindrome extends around that position.

We call this:

```java
radius[i]
```

Example:

```text
transformed = # a # b # b # a #

radius       0 1 0 1 4 1 0 1 0
                    ↑
                  center
```

The `4` means that the palindrome centered there extends `4` positions in both directions.

---

## Step 3: Maintain a Current Palindrome

We maintain two variables:

```java
int center = 0;
int right = 0;
```

They represent the palindrome that currently extends furthest to the right.

```text
center
   ↓
#a#b#b#a#
     └───────→ right
```

`right` is the **right boundary** of the palindrome.

---

## Step 4: Reuse the Mirror

This is the clever part of Manacher's algorithm.

Suppose we are currently inside a known palindrome:

```text
        center
          ↓
    a b c d c b a
    ↑             ↑
                  right
```

If we are checking position `i`, its mirrored position around `center` is:

```java
mirror = 2 * center - i;
```

Because the larger palindrome is symmetric, we already know something about the palindrome around `mirror`.

Therefore, we can initialize:

```java
radius[i] = Math.min(
    right - i,
    radius[mirror]
);
```

Instead of starting from zero.

This is what gives Manacher's algorithm its `O(n)` performance.

---

## Step 5: Expand Only When Necessary

After using the mirror information, we try to expand further:

```java
while (
    i + radius[i] + 1 < transformed.length
    && i - radius[i] - 1 >= 0
    && transformed.charAt(i + radius[i] + 1)
       == transformed.charAt(i - radius[i] - 1)
) {
    radius[i]++;
}
```

If this palindrome extends beyond the current `right`, update:

```java
center = i;
right = i + radius[i];
```

---

## Manacher's Algorithm Code

```java
class Solution {

    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) {
            return s;
        }

        // Add separators so that odd and even length
        // palindromes can be handled in the same way.
        StringBuilder transformed = new StringBuilder("^");

        for (char character : s.toCharArray()) {
            transformed.append('#');
            transformed.append(character);
        }

        transformed.append("#$");

        int length = transformed.length();
        int[] radius = new int[length];

        // Center and right boundary of the palindrome
        // that currently extends furthest to the right.
        int center = 0;
        int right = 0;

        // Store the center of the longest palindrome.
        int longestCenter = 0;

        for (int i = 1; i < length - 1; i++) {

            // Find the mirror position of i around center.
            int mirror = 2 * center - i;

            // If i is inside the current palindrome,
            // reuse information from its mirror.
            if (i < right) {
                radius[i] = Math.min(
                    right - i,
                    radius[mirror]
                );
            }

            // Try to expand the palindrome further.
            while (
                transformed.charAt(i + radius[i] + 1)
                    == transformed.charAt(i - radius[i] - 1)
            ) {
                radius[i]++;
            }

            // If this palindrome extends further right,
            // make it the new current palindrome.
            if (i + radius[i] > right) {
                center = i;
                right = i + radius[i];
            }

            // Keep track of the longest palindrome.
            if (radius[i] > radius[longestCenter]) {
                longestCenter = i;
            }
        }

        // Convert the center/radius in the transformed
        // string back to the original string.
        int start = (longestCenter - radius[longestCenter]) / 2;

        return s.substring(
            start,
            start + radius[longestCenter]
        );
    }
}
```

---

# Manacher's Algorithm — The Important Part

You do **not** need to memorize the entire implementation initially.

The important concepts are:

```text
1. Transform the string
        ↓
2. Store palindrome radius at every position
        ↓
3. Maintain the current rightmost palindrome
        ↓
4. Find the mirror position
        ↓
5. Reuse the mirror's radius
        ↓
6. Expand only if necessary
        ↓
7. Track the longest radius
```

The central formula is:

```java
int mirror = 2 * center - i;
```

And the key optimization is:

```java
radius[i] = Math.min(
    right - i,
    radius[mirror]
);
```

This lets us reuse work that was already done.

---

# Comparison

| Approach              |    Time |  Space | Main Idea                                   |
| --------------------- | ------: | -----: | ------------------------------------------- |
| Expand Around Centers | `O(n²)` | `O(1)` | Expand from every possible center           |
| Manacher's Algorithm  |  `O(n)` | `O(n)` | Reuse palindrome information using symmetry |

### Interview Recommendation

For most coding interviews, **Expand Around Centers** is usually easier to explain and implement correctly.

Know **Manacher's Algorithm** when the problem specifically requires `O(n)` time or when you want the optimized solution.

The most important thing to understand about Manacher's is not the code itself; it is the **mirror + right boundary optimization** that prevents repeatedly expanding over characters we already know about.
