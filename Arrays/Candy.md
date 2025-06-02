# Candy
There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
Return the minimum number of candies you need to have to distribute the candies to the children.

## Observation
1. One-dimensional dependency (array-based):
The decision at index i depends on neighbors like i - 1 and i + 1.

2. Relative constraints:
There are inequality-based relationships between adjacent elements (e.g., if rating[i] > rating[i-1], then candies[i] > candies[i-1]).

3. Minimum/optimal assignment:
You want to assign values optimally (e.g., minimum candies) under local constraints.

4. Two-directional correction:
The problem may need to be processed in both directions to ensure global correctness from local rules.

## Two pass greedy solution
1. First assign 1 candy to all.
2. Iterate from the left to give more candies when ever the element on the left has a lower rating.
3. Iterate from the right to give more candies whenever the element on the right has lower ratings and higher candies.

   
## Code
```
class Solution {
    public int candy(int[] ratings) {
        int ans = 0 , n = ratings.length;
        if(n == 1) return 1;
        int[] candies = new int[n];
        Arrays.fill(candies , 1);
        for(int i = 1 ; i < n ; i++){
            if(ratings[i] > ratings[i-1]) candies[i] = candies[i-1] + 1;
        }
        for(int i = n - 2 ; i >= 0 ; i--){
            if(ratings[i] > ratings[i+1] && candies[i+1]>=candies[i]) candies[i] = candies[i+1] + 1;
        }
        for(int i : candies) ans+= i;
        return ans;
    }
}
```
