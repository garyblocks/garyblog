# Coin Change

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example:**

```
Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
```
```
Input: coins = [2], amount = 3
Output: -1
```
**Note:**
You may assume that you have an infinite number of each kind of coin.

**Code:**

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        backpack = [float('inf')] * (amount + 1)
        backpack[0] = 0
        for coin in coins:
            for x in range(coin, amount + 1):
                backpack[x] = min(backpack[x], backpack[x - coin] + 1)
        return backpack[amount] if backpack[amount] != float('inf') else -1
```
At each iteration, we try all coins and compute the result from all the amounts we have before.
