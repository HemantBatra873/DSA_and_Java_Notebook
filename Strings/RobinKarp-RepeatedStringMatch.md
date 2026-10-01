# Robin Karp / Repeated String Match

Given two strings a and b, return the minimum number of times you should repeat string a so that string b is a substring of it. If it is impossible for b​​​​​​ to be a substring of a after repeating it, return -1.

Notice: string "abc" repeated 0 times is "", repeated 1 time is "abc" and repeated 2 times is "abcabc".

```java
class Solution {

    public int repeatedStringMatch(String A, String B) {

        StringBuilder sb = new StringBuilder();
        int count = 0;

        // Make repeated string long enough
        while (sb.length() < B.length()) {
            sb.append(A);
            count++;
        }

        // Try current repetition
        if (rabinKarp(sb.toString(), B)) {
            return count;
        }

        // Try one more repetition for overlap cases
        sb.append(A);

        if (rabinKarp(sb.toString(), B)) {
            return count + 1;
        }

        return -1;
    }

    private boolean rabinKarp(String text, String pattern) {

        int n = text.length();
        int m = pattern.length();

        if (m > n) {
            return false;
        }

        int base = 256;
        int mod = 1_000_000_007;

        long patternHash = 0;
        long windowHash = 0;
        long highestPower = 1; // This is the highest power which gets multiplied to the number at the window's start when rolling the number

        // base^(m-1)
        // When we remove left char will have highest value of base
        for (int i = 0; i < m - 1; i++) {
            highestPower = (highestPower * base) % mod;
        }

        // Initial hashes
        for (int i = 0; i < m; i++) {
            patternHash =
                (patternHash * base + pattern.charAt(i)) % mod;

            windowHash =
                (windowHash * base + text.charAt(i)) % mod;
        }

        for (int i = 0; i <= n - m; i++) {

            // Hash matched
            if (patternHash == windowHash) {

                // Verify to avoid collisions
                if (text.substring(i, i + m).equals(pattern)) {
                    return true;
                }
            }

            // Slide window
            if (i < n - m) {

                // During subtraction the vale can become negative hence two mods
                windowHash =
                    (windowHash
                    - text.charAt(i) * highestPower % mod
                    + mod) % mod;

                windowHash =
                    (windowHash * base
                    + text.charAt(i + m)) % mod;
            }
        }

        return false;
    }
}
```

**Rabin–Karp** is a string-matching algorithm that uses a **hash value** to quickly find whether a pattern exists inside a larger string.

Think of it as:

> Instead of comparing the pattern with every substring character-by-character, compare their **hashes** first.

### Example

Suppose:

```text
Text:    "abcdef"
Pattern: "cde"
```

We want to find `"cde"` inside `"abcdef"`.

### Step 1: Hash the pattern

Calculate a hash for:

```text
"cde"
```

For example, conceptually:

```text
hash("cde") = X
```

### Step 2: Hash the first window

Take a substring of the same length as the pattern:

```text
"abc"
```

Calculate:

```text
hash("abc") = Y
```

Compare:

```text
Y == X ?
```

If not, move the window.

### Step 3: Slide the window

Instead of calculating the hash of `"bcd"` from scratch, **update the existing hash**.

```text
abc
 ↓
bcd
```

Remove:

```text
a
```

and add:

```text
d
```

This is called a **rolling hash**.

Then:

```text
hash("bcd")
```

can be calculated very quickly from:

```text
hash("abc")
```

### Step 4: Continue

```text
Text:    a b c d e f
         └───┘
          abc

          └───┘
           bcd

            └───┘
             cde  ← hash matches!
```

When:

```text
hash(window) == hash(pattern)
```

we **verify the actual strings**:

```java
text.substring(i, i + m).equals(pattern)
```

This verification is important because **two different strings can have the same hash** (a hash collision).

---

### How code does it

Code uses:

```java
int base = 256;
int mod = 1_000_000_007;
```

The hash is essentially built like:

```text
hash = hash × base + character
```

For example, conceptually:

```text
"abc"

((a × 256 + b) × 256 + c)
```

Then when the window moves:

```text
abc → bcd
```

your code does:

```java
windowHash =
    (windowHash
    - text.charAt(i) * highestPower % mod
    + mod) % mod;

windowHash =
    (windowHash * base
    + text.charAt(i + m)) % mod;
```

Meaning:

1. **Remove** the outgoing character.
2. **Shift** the remaining characters.
3. **Add** the incoming character.

### The whole algorithm

```text
1. Calculate pattern hash
          ↓
2. Calculate first window hash
          ↓
3. Compare hashes
          ↓
4. If equal → compare actual strings
          ↓
5. Slide window using rolling hash
          ↓
6. Repeat until text ends
```

### Why is it useful?

Naive search:

```text
Compare pattern with every window
→ potentially O(n × m)
```

Rabin–Karp:

```text
Calculate hash once
→ update hash in O(1) per window
→ potentially O(n + m)
```

So the **core idea to remember** is:

> **Hash the pattern → hash a window → compare → roll the window → verify when hashes match.**

And in your repeated-string problem, Rabin–Karp is simply being used as the **search engine** to check whether `B` occurs inside the repeated `A`.
