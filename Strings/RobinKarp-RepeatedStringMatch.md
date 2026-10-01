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
        long highestPower = 1;

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
