### 312. Burst Balloons
<img width="2851" height="1262" alt="image" src="https://github.com/user-attachments/assets/286dee8a-4c3b-4cf1-963c-7f7f41851f90" />

* 解題思路\
* 程式
```python
class Solution(object):
    def maxCoins(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums = [1] + nums + [1]
        n = len(nums)

        dp = [[0] * n for _ in range(n)]

        for length in range(2, n):
            for left in range(n - length):
                right = left + length

                for k in range(left + 1, right):
                    coins = (
                        dp[left][k]
                        + dp[k][right]
                        + nums[left] * nums[k] * nums[right]
                    )

                    dp[left][right] = max(dp[left][right], coins)

        return dp[0][n - 1]        
