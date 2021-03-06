## Best Time to Buy and Sell Stock

Say you have an array for which the \\(i^{th}\\) element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

**Code:**

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        low, max_p = float('inf'), 0
        for p in prices:
            max_p = max(max_p, p - low)
            low = min(low, p)
        return max_p
```
Idea: You want to find the biggest difference.

Keep updating two variables, the lowest value so far and the biggest difference between current price and the lowest value.
