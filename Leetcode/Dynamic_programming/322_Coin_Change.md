## Link
https://leetcode.com/problems/coin-change/
```
You are given coins of different denominations and a total amount of money amount. 
Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
Example 2:

Input: coins = [2], amount = 3
Output: -1
Note:
You may assume that you have an infinite number of each kind of coin.
```
## Transfer function
dp[i] = min(dp[i], dp[i-coin[j]]+1), coin[j] is the amount of coin

set orignal dp[i] = amount + 1, and keep getting the min dp[i]

https://leetcode.com/articles/coin-change/
![Image of code](https://leetcode.com/media/original_images/322_coin_change_table.png)
1. i is the amount of money, coin[j] is the amount of coin
```python
class Solution:
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        dp = [amount+1] * (amount+1)
        dp[0] = 0
        
        for i in range(1, amount+1):
            for coin in coins:
                if coin <= i:
                    dp[i] = min(dp[i], dp[i-coin]+1)
        return -1 if dp[-1] == amount+1 else dp[-1]
```
