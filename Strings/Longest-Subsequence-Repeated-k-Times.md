# Longest Subsequence Repeated k Times

You are given a string s of length n, and an integer k. You are tasked to find the longest subsequence repeated k times in string s.

A subsequence is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.

A subsequence seq is repeated k times in the string s if seq * k is a subsequence of s, where seq * k represents a string constructed by concatenating seq k times.

For example, "bba" is repeated 2 times in the string "bababcba", because the string "bbabba", constructed by concatenating "bba" 2 times, is a subsequence of the string "bababcba".
Return the longest subsequence repeated k times in string s. If multiple such subsequences are found, return the lexicographically largest one. If there is no such subsequence, return an empty string.

## BFS + Greedy approach

### Algorithm
1. Start with an empty string.
2. Put the empty string in a queue.
3. while the queue is not empty poll a string and try to insert every character from 'a' to 'z' in it and check if it appears in the string atleast k times.
4. If it does then we update result to this new string and add it to the queue.
5. For checking if the string is a k subsequence of another string we take two pointers i and c where i is the index of the currenct character that we are finding and c is the total count of the subsequence. 


```java
class Solution {
    public String longestSubsequenceRepeatedK(String s, int k) {
        String r="";
        Queue<String> q=new LinkedList<>();
        for(q.add("");!q.isEmpty();) {
            String c=q.poll();
            for(char ch='a';ch<='z';ch++) {
                String n=c+ch;
                if(isK(n,s,k)) {
                    r=n;
                    q.add(n);
                }
            }
        }
        return r;
    }
    boolean isK(String s,String t,int k) {
        int c=0,i=0;
        for(char ch:t.toCharArray()) {
            if(ch==s.charAt(i)) {
                if(++i==s.length()) {
                    i=0;
                    if(++c==k) return true;
                }
            }
        }
        return false;
    }
}
```
