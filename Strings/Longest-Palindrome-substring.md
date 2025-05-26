# Longest Palindrome Substring

SOLUTION 1: Expand Around Centers (Most Popular Interview Solution)  
Time: O(n²), Space: O(1)  
Key Insight: Every palindrome has a center. For each possible center, expand outward and check the longest palindrome possible.


## Steps -
1. We go to each index and start expanding.
2. What does expanding means ? It means set two pointer left and right and keep expanding left-- and right++ until they are valid and equal.
3. This helps us get the longest palindromic substring.
4. Now when you get a maxLength. You have to first set the start that will be at (i - (maxLen - 1) / 2).


```


    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 2) return s;
        
        int start = 0, maxLen = 1;
        
        for (int i = 0; i < s.length(); i++) {
            // Check for odd-length palindromes (center at i)
            int len1 = expandAroundCenter(s, i, i);
            
            // Check for even-length palindromes (center between i and i+1)
            int len2 = expandAroundCenter(s, i, i + 1);
            
            int currentMaxLen = Math.max(len1, len2);
            
            // Update global maximum if current palindrome is longer
            if (currentMaxLen > maxLen) {
                maxLen = currentMaxLen;
                start = i - (currentMaxLen - 1) / 2; // Calculate start position
            }
        }
        
        return s.substring(start, start + maxLen);
    }
    
    /**
     * Helper method to expand around center and return palindrome length
     */
    private static int expandAroundCenter(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1; // Length of palindrome
    }
```
