# Best Time to Buy and Sell Stock I

eg. 7 , 1 , 5 , 3 , 6 , 4

## description -
You are given an array prices where prices[i] is the price of a given stock on the ith day.  
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.  
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.  

## Key observations - 
If you sell for more than you make a profit but if you sell for less you make a loss.  
In this question we can do **only one transaction** and therefore we pick the absolute best one to do. 


## Steps
1. At any time we need the previous minimum price.
2. If the current price is the min then we set it to min price.
3. else we calculate maxProfit by comparing maxProfit with prices[i] - minPrice.

```
public static int maxProfitSingleTransaction(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        
        int minPrice = prices[0];
        int maxProfit = 0;
        
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            } else {
                maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            }
        }
        return maxProfit;
    }
```

# Best Time to Buy and Sell Stock II

## Description -
You are given an integer array prices where prices[i] is the price of a given stock on the ith day.  
On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.  
Find and return the maximum profit you can achieve.  

## Observation -
In this question we can make **Multiple transactions** unlike its previous parts.
We can skip buying at any day by buying and selling on the same day.
At most one stock at a time is allowed.

## Steps
1. This is the perfect example of a **Greedy Problem** because we need to sell to profit as soon as possibe so that we can buy again at lower rates.
2. Also because its allowed to sell on one day and buy on the same if we have a case like 1 , 2 , 3 , 4 the profit from 1 to 4 is same as 1 to 2 to 3 to 4 because we are selling and buying on the same day.

## Code 
```
class Solution {
    public int maxProfit(int[] prices) {
         int p=0;
       for(int i=1;i<prices.length;i++){
           if(prices[i]>prices[i-1]){
               p+=prices[i]-prices[i-1];
           }
       }
       return p;
    }
```
}
