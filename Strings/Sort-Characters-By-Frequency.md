# Sort characters by frequency 

Given a string s, sort it in decreasing order based on the frequency of the characters.

 The frequency of a character is the number of times it appears in the string.

Return the sorted string. If there are multiple answers, return any of them.


Example 1:

Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.



```
class Solution {
    public String frequencySort(String s) {
        int n = s.length();
        if(n == 1) return s;
        PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> Integer.compare(b[1],a[1]));
        Map <Character , Integer > map = new HashMap<>();
        for(char c : s.toCharArray()){
            map.put(c , map.getOrDefault(c , 0) + 1);
        }
        for(Map.Entry<Character, Integer> entry : map.entrySet()){
            int[] arr = new int[]{entry.getKey() , entry.getValue()};
            pq.offer(arr);
        }
        StringBuilder sb = new StringBuilder();
        while(!pq.isEmpty()){
            int[] arr = pq.poll();
            for(int i = 0 ; i < arr[1] ; i++){
                sb.append((char)arr[0]);
            }
        }
        return sb.toString();
    }
}
```