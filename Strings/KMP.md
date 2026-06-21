# KMP (Knuth-Morris-Pratt) Algorithm in Java

## What is KMP?

KMP (Knuth-Morris-Pratt) is a string matching algorithm that finds all occurrences of a pattern inside a text in **O(N + M)** time.

- `N` = length of text
- `M` = length of pattern

Unlike the brute-force approach, KMP does not recheck characters that have already been matched.

---

## Problem

Given:

```text
Text    = "ababcabcabababd"
Pattern = "ababd"
```

Find the starting index where the pattern occurs.

---

## Core Idea

Suppose we are matching:

```text
Text    : ababcabcabababd
Pattern : ababd
```

After matching some characters, if a mismatch occurs:

```text
ababc
ababd
    ^
mismatch
```

A brute-force solution starts again from the next character in the text.

KMP uses information about the pattern itself to determine:

> How much of the matched prefix can still be reused?

This information is stored in the **LPS array**.

---

# Step 1: Build the LPS Array

LPS stands for:

**Longest Proper Prefix which is also a Suffix**

For each position `i`:

```text
lps[i] =
length of the longest proper prefix
which is also a suffix
for pattern[0...i]
```

---

## Example

Pattern:

```text
a b a b a c a
0 1 2 3 4 5 6
```

Let's compute LPS.

### Index 0

Substring:

```text
a
```

No proper prefix exists.

```text
lps[0] = 0
```

---

### Index 1

Substring:

```text
ab
```

Prefixes:

```text
a
```

Suffixes:

```text
b
```

No match.

```text
lps[1] = 0
```

---

### Index 2

Substring:

```text
aba
```

Prefixes:

```text
a
ab
```

Suffixes:

```text
a
ba
```

Longest match:

```text
a
```

```text
lps[2] = 1
```

---

### Index 3

Substring:

```text
abab
```

Prefixes:

```text
a
ab
aba
```

Suffixes:

```text
b
ab
bab
```

Longest match:

```text
ab
```

```text
lps[3] = 2
```

---

### Index 4

Substring:

```text
ababa
```

Longest matching prefix and suffix:

```text
aba
```

```text
lps[4] = 3
```

---

### Index 5

Substring:

```text
ababac
```

No matching prefix and suffix.

```text
lps[5] = 0
```

---

### Index 6

Substring:

```text
ababaca
```

Longest matching prefix and suffix:

```text
a
```

```text
lps[6] = 1
```

---

## Final LPS Array

```text
Pattern : a b a b a c a
Index   : 0 1 2 3 4 5 6
LPS     : 0 0 1 2 3 0 1
```

---

# Efficient LPS Construction

Instead of checking all prefixes and suffixes repeatedly, KMP builds the LPS array in O(M).

### Key Observation

If:

```text
pattern[currentIndex] == pattern[matchedPrefixLength]
```

then we can extend the previous matching prefix.

Otherwise:

```java
matchedPrefixLength = lps[matchedPrefixLength - 1];
```

and try a smaller prefix.

---

## Java Implementation (LPS)

```java
private static int[] buildLpsArray(String pattern) {
    int patternLength = pattern.length();
    int[] lps = new int[patternLength];

    int matchedPrefixLength = 0;
    int currentIndex = 1;

    while (currentIndex < patternLength) {

        if (pattern.charAt(currentIndex)
                == pattern.charAt(matchedPrefixLength)) {

            matchedPrefixLength++;
            lps[currentIndex] = matchedPrefixLength;
            currentIndex++;

        } else {

            if (matchedPrefixLength != 0) {
                matchedPrefixLength =
                        lps[matchedPrefixLength - 1];
            } else {
                lps[currentIndex] = 0;
                currentIndex++;
            }
        }
    }

    return lps;
}
```

---

# Step 2: Pattern Matching

Maintain:

```java
int textIndex;
int patternIndex;
```

---

## If Characters Match

```java
textIndex++;
patternIndex++;
```

---

## If Entire Pattern Matches

```java
patternIndex == pattern.length()
```

Pattern found.

Store:

```java
textIndex - pattern.length()
```

Then continue searching:

```java
patternIndex = lps[patternIndex - 1];
```

to find additional matches.

---

## If Mismatch Occurs

### Case 1: Nothing Matched Yet

```java
patternIndex == 0
```

Move text forward.

```java
textIndex++;
```

---

### Case 2: Some Prefix Already Matched

Instead of restarting:

```java
patternIndex = lps[patternIndex - 1];
```

This is where KMP saves time.

---

# Complete Java Implementation

```java
import java.util.ArrayList;
import java.util.List;

public class KmpAlgorithm {

    public static List<Integer> search(
            String text,
            String pattern) {

        List<Integer> matchPositions = new ArrayList<>();

        if (pattern.isEmpty()) {
            return matchPositions;
        }

        int[] lps = buildLpsArray(pattern);

        int textIndex = 0;
        int patternIndex = 0;

        while (textIndex < text.length()) {

            if (text.charAt(textIndex)
                    == pattern.charAt(patternIndex)) {

                textIndex++;
                patternIndex++;
            }

            if (patternIndex == pattern.length()) {

                matchPositions.add(
                        textIndex - pattern.length());

                patternIndex =
                        lps[patternIndex - 1];
            }

            else if (textIndex < text.length()
                    && text.charAt(textIndex)
                    != pattern.charAt(patternIndex)) {

                if (patternIndex != 0) {

                    patternIndex =
                            lps[patternIndex - 1];

                } else {

                    textIndex++;
                }
            }
        }

        return matchPositions;
    }

    private static int[] buildLpsArray(String pattern) {

        int[] lps = new int[pattern.length()];

        int matchedPrefixLength = 0;
        int currentIndex = 1;

        while (currentIndex < pattern.length()) {

            if (pattern.charAt(currentIndex)
                    == pattern.charAt(matchedPrefixLength)) {

                matchedPrefixLength++;

                lps[currentIndex] =
                        matchedPrefixLength;

                currentIndex++;

            } else {

                if (matchedPrefixLength != 0) {

                    matchedPrefixLength =
                            lps[matchedPrefixLength - 1];

                } else {

                    lps[currentIndex] = 0;
                    currentIndex++;
                }
            }
        }

        return lps;
    }

    public static void main(String[] args) {

        String text = "ababcabcabababd";
        String pattern = "ababd";

        System.out.println(search(text, pattern));
    }
}
```

Output:

```text
[10]
```

---

# Why Does This Work?

Consider:

```text
Pattern = ababab
```

Suppose we matched:

```text
abab
```

and then got a mismatch.

The matched substring:

```text
abab
```

contains:

```text
Prefix = ab
Suffix = ab
```

Since we already know `"ab"` matches, there is no reason to compare it again.

Instead of restarting from index `0`, we jump directly to:

```text
lps[3] = 2
```

meaning:

```text
patternIndex = 2
```

and continue matching.

This is the key optimization that makes KMP run in linear time.

---

# Complexity Analysis

| Operation | Time Complexity |
|------------|----------------|
| Build LPS Array | O(M) |
| Search Pattern | O(N) |
| Total | O(N + M) |
| Space | O(M) |

Where:

- `N` = length of text
- `M` = length of pattern

---

# Common Applications

- Text editors (Find/Search functionality)
- Search engines
- DNA sequence matching
- Log analysis
- Plagiarism detection
- Pattern matching problems in competitive programming

---

# Key Interview Takeaway

KMP avoids rechecking characters by using the LPS array.

Whenever a mismatch occurs after some successful matches:

```java
patternIndex = lps[patternIndex - 1];
```

This allows the algorithm to reuse previous matching information and achieve an overall complexity of:

```text
O(N + M)
```

instead of the brute-force:

```text
O(N × M)
```