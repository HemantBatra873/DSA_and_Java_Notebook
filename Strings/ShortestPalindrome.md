# Shortest Palindrome 

You are given a string s. You can convert s to a palindrome by adding characters in front of it.

Return the shortest palindrome you can find by performing this transformation.

This is the **Shortest Palindrome** problem. The key is to realize that we only need to find the **longest palindromic prefix** of `s`.

### Example

Suppose:

```text
s = "aacecaaa"
```

The longest prefix that is already a palindrome is:

```text
"aacecaa"
```

The remaining part is:

```text
"a"
```

So add the reverse of the remaining part to the front:

```text
"a" + "aacecaaa"
= "aaacecaaa"
```

The challenge is finding that longest palindromic prefix efficiently.

---

## Approach 1: Brute Force

We can check prefixes from longest to shortest.

For:

```text
"abcd"
```

Check:

```text
"abcd"  -> no
"abc"   -> no
"ab"    -> no
"a"     -> yes
```

Then the remaining string is `"bcd"`.

Reverse it:

```text
"dcb"
```

Add it in front:

```text
"dcb" + "abcd"
= "dcbabcd"
```

### Complexity

There can be `O(n)` prefixes, and checking each palindrome takes `O(n)`:

```text
Time:  O(n²)
Space: O(n)
```

But there is a much better approach using **KMP**.

---

# Approach 2: KMP

The trick is to find the **longest palindromic prefix** using the LPS array from KMP.

Construct:

```text
s + "#" + reverse(s)
```

For example:

```text
s = "aacecaaa"

reverse(s) = "aaacecaa"

combined:

"aacecaaa#aaacecaa"
```

Now calculate the KMP LPS array.

The final LPS value tells us:

> The length of the longest prefix of `s` that is also a suffix of `reverse(s)`.

And that is exactly the **longest palindromic prefix of `s`**.

For this example:

```text
longest palindromic prefix = "aacecaa"
length = 7
```

So:

```text
remaining = "a"
reverse(remaining) = "a"

answer = "a" + "aacecaaa"
       = "aaacecaaa"
```

### Java

```java
class Solution {
    public String shortestPalindrome(String s) {
        String reversed = new StringBuilder(s).reverse().toString();

        String combined = s + "#" + reversed;

        int[] lps = buildLps(combined);

        int palindromePrefixLength = lps[combined.length() - 1];

        String remaining = s.substring(palindromePrefixLength);
        String prefixToAdd = new StringBuilder(remaining)
                .reverse()
                .toString();

        return prefixToAdd + s;
    }

    private int[] buildLps(String s) {
        int[] lps = new int[s.length()];

        int prefixLength = 0;

        for (int index = 1; index < s.length(); index++) {
            while (prefixLength > 0
                    && s.charAt(index) != s.charAt(prefixLength)) {
                prefixLength = lps[prefixLength - 1];
            }

            if (s.charAt(index) == s.charAt(prefixLength)) {
                prefixLength++;
            }

            lps[index] = prefixLength;
        }

        return lps;
    }
}
```

### The important idea

Don't think of this primarily as a KMP problem. Think:

> **Find the longest prefix of `s` that is already a palindrome.**

Then:

```text
remaining part = s.substring(longestPalindromePrefix)

answer = reverse(remaining part) + s
```

KMP is simply the clever way of finding that prefix in **O(n)**.

### Complexity

```text
Time:  O(n)
Space: O(n)
```

This is a useful problem to learn because it combines a **palindrome observation** with the **LPS/KMP pattern-matching technique**.
