# Z-Function (Z-Algorithm) in Java

## What is the Z-Function?

The Z-Function computes an array `zArray[]` where:

```
zArray[i] = Length of the longest substring starting at index i
            that matches the prefix of the string.
```

### Example

String:

```
aabxaabx
```

Index:

```
0 1 2 3 4 5 6 7
a a b x a a b x
```

Z-Array:

```
0 1 0 0 4 1 0 0
```

At index `4`, the substring `"aabx"` matches the prefix `"aabx"` for `4` characters.

Therefore:

```
zArray[4] = 4
```

---

# Core Idea

The algorithm maintains a matching window:

```java
[windowStart, windowEnd]
```

such that:

```java
input[windowStart...windowEnd]
```

matches:

```java
input[0...(windowEnd - windowStart)]
```

If the current index lies inside this window, previously computed information can be reused instead of comparing characters again.

This optimization reduces the complexity from:

```
O(N²) → O(N)
```

---

# Java Implementation

```java
public class ZFunction {

    public static int[] computeZArray(String input) {
        int stringLength = input.length();
        int[] zArray = new int[stringLength];

        int windowStart = 0;
        int windowEnd = 0;

        for (int currentIndex = 1; currentIndex < stringLength; currentIndex++) {

            if (currentIndex <= windowEnd) {
                int mirroredIndex = currentIndex - windowStart;

                zArray[currentIndex] = Math.min(
                        windowEnd - currentIndex + 1,
                        zArray[mirroredIndex]
                );
            }

            while (currentIndex + zArray[currentIndex] < stringLength
                    && input.charAt(zArray[currentIndex])
                    == input.charAt(currentIndex + zArray[currentIndex])) {

                zArray[currentIndex]++;
            }

            int currentMatchEnd =
                    currentIndex + zArray[currentIndex] - 1;

            if (currentMatchEnd > windowEnd) {
                windowStart = currentIndex;
                windowEnd = currentMatchEnd;
            }
        }

        return zArray;
    }

    public static void main(String[] args) {
        String input = "aabxaabx";

        int[] zArray = computeZArray(input);

        for (int value : zArray) {
            System.out.print(value + " ");
        }
    }
}
```

### Time Complexity

```
O(N)
```

### Space Complexity

```
O(N)
```

---

# Pattern Matching Using Z-Function

## Problem

Given:

```java
String text = "ababcababc";
String pattern = "abc";
```

Find all occurrences of the pattern inside the text.

---

## Trick

Create a combined string:

```java
pattern + "$" + text
```

Example:

```
abc$ababcababc
```

The delimiter (`$`) must be a character that does not appear in either string.

Compute the Z-array on this combined string.

Whenever:

```java
zArray[index] == pattern.length()
```

the pattern starts at:

```java
index - pattern.length() - 1
```

inside the original text.

---

# Java Implementation for Pattern Matching

```java
import java.util.ArrayList;
import java.util.List;

public class ZPatternMatching {

    private static int[] computeZArray(String input) {
        int stringLength = input.length();
        int[] zArray = new int[stringLength];

        int windowStart = 0;
        int windowEnd = 0;

        for (int currentIndex = 1; currentIndex < stringLength; currentIndex++) {

            if (currentIndex <= windowEnd) {
                int mirroredIndex = currentIndex - windowStart;

                zArray[currentIndex] = Math.min(
                        windowEnd - currentIndex + 1,
                        zArray[mirroredIndex]
                );
            }

            while (currentIndex + zArray[currentIndex] < stringLength
                    && input.charAt(zArray[currentIndex])
                    == input.charAt(currentIndex + zArray[currentIndex])) {

                zArray[currentIndex]++;
            }

            int currentMatchEnd =
                    currentIndex + zArray[currentIndex] - 1;

            if (currentMatchEnd > windowEnd) {
                windowStart = currentIndex;
                windowEnd = currentMatchEnd;
            }
        }

        return zArray;
    }

    public static List<Integer> findPatternOccurrences(
            String text,
            String pattern) {

        String combinedString =
                pattern + "$" + text;

        int[] zArray =
                computeZArray(combinedString);

        List<Integer> occurrences =
                new ArrayList<>();

        for (int currentIndex = 0;
             currentIndex < zArray.length;
             currentIndex++) {

            if (zArray[currentIndex] == pattern.length()) {

                occurrences.add(
                        currentIndex
                                - pattern.length()
                                - 1
                );
            }
        }

        return occurrences;
    }

    public static void main(String[] args) {

        String text = "ababcababc";
        String pattern = "abc";

        System.out.println(
                findPatternOccurrences(text, pattern)
        );
    }
}
```

Output:

```
[2, 7]
```

The pattern `"abc"` appears at:

```
Index 2
Index 7
```

---

# Why Mirrored Index Works

Suppose the current matching window is:

```java
[windowStart, windowEnd]
```

and the current index lies inside the window.

Then:

```java
int mirroredIndex = currentIndex - windowStart;
```

The substring inside the window is known to match the prefix.

Therefore the matching information already computed at `mirroredIndex` can be reused for `currentIndex`.

This avoids re-comparing characters and is the key reason the algorithm runs in O(N).

---

# Interview Notes

## Applications

1. Pattern Matching
2. Longest Prefix Matching
3. Repeated Substring Detection
4. String Compression
5. Competitive Programming String Problems

## Complexity

| Operation | Complexity |
|------------|------------|
| Build Z Array | O(N) |
| Pattern Search | O(N + M) |

Where:

- N = Length of text
- M = Length of pattern

---

# Z-Function vs KMP

| Feature | Z-Function | KMP |
|----------|------------|------|
| Time Complexity | O(N + M) | O(N + M) |
| Easier to Implement | Usually Yes | Usually No |
| Uses Prefix Information | Indirectly | Directly |
| Popular in Competitive Programming | Yes | Yes |

Both algorithms provide linear-time pattern matching.