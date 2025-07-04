# Find the K-th Character in String Game I and II

## 1st part 

Alice and Bob are playing a game. Initially, Alice has a string word = "a".

You are given a positive integer k.

Now Bob will ask Alice to perform the following operation forever:

Generate a new string by changing each character in word to its next character in the English alphabet, and append it to the original word.
For example, performing the operation on "c" generates "cd" and performing the operation on "zb" generates "zbac".

Return the value of the kth character in word, after enough operations have been done for word to have at least k characters.

Note that the character 'z' can be changed to 'a' in the operation.

## Intiution and Learnings
Obviously there is the brute force approach where you can use a stringbuilder and keep appending to its length and then return k - 1th index when the length becomes more than equal to k.  

But the better approach will be to track down how the kth element would have been appended after every operation and then using this knowledge to directly form the kth element. 

For example if you want the k = 56th character then which character would have been used to form this character?

Lets see...

The string grows in the power of 2^n like 1, 2, 4, 8, 16, 32, 64, 128......

So for 56th character it was make from some character that was present in the string of length 32 because after that the string would have become of length 32 * 2 = 64 > 32 so the length of previous generation was 32.

Exactly it was the 56 - 32 character that was the 24th character so if we know the 24th character in the string of length 32 then 24th character's next character is the 56th character.

Now 24 character was made from some chracter from the string of length 16.

This sequence is 56 -> 24 -> 8 -> 4 -> 2 -> 1 and the first character is 'a' and the length of this sequence is 5 so the character is 'a' + 5 that is 'f'.

## Code (Beats 100%) Iterative

```java
class Solution {
    public char kthCharacter(int k) {
        int shifts = 0;
        
        while (k > 1) {
            int len = 1;
            while (2 * len < k) len *= 2;
            k -= len;
            shifts++;  
        }
        
        return (char) ('a' + shifts % 26);
    }
}
```

### Time complexity - O(logn)
This is because instead of brute force we just keep decreasing k in powers of 2

### Space complexity - O(1)
No extra space was used

## 2nd part 

Alice and Bob are playing a game. Initially, Alice has a string word = "a".

You are given a positive integer k. You are also given an integer array operations, where operations[i] represents the type of the ith operation.

Now Bob will ask Alice to perform all operations in sequence:

If operations[i] == 0, append a copy of word to itself.
If operations[i] == 1, generate a new string by changing each character in word to its next character in the English alphabet, and append it to the original word. For example, performing the operation on "c" generates "cd" and performing the operation on "zb" generates "zbac".
Return the value of the kth character in word after performing all the operations.

Note that the character 'z' can be changed to 'a' in the second type of operation.

### Learnings 

Just like 1st part but we need to keep in mind that the current k character came from which operation and based on that we determine how many characters ahead of 'a' have we came.

### Code (Beats 100%)

```java
class Solution {
    public char kthCharacter(long k, int[] o) {
        int swaps = 0;
        while(k > 1){
            long len = 1l;
            int idx = 0;
            while(len * 2 < k){
                idx++;
                len *= 2;
            }
            if(o[idx] == 1){
                swaps++;
            }
            k -= len;
        }
        swaps = swaps % 26;
        return (char)('a' + swaps);
    }
}
```

### Time complexity O(logn)
### Space complexity O(1)