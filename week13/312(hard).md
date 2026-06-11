### 312. Burst Balloons
<img width="2851" height="1262" alt="image" src="https://github.com/user-attachments/assets/286dee8a-4c3b-4cf1-963c-7f7f41851f90" />

* 解題思路\
  這題我用dp區間，先在陣列左右各補上一個1處理邊界問題，\
  取得新陣列長度n 建立n* n的dp表\
  其中dp[left][right]代表left跟right這個開區間裡面的氣球全部都被戳完能獲得的最大分數\
  for迴圈長度由小到大計算+for迴圈枚舉每一個左端點+\
  for k in range left+1到right 代表在left跟right中間每一個氣球最後戳掉第k顆時\
  被清空的dp[left][k]+dp[k][right]+left* k*right分數 這個最佳分數有各種可能 找max保存下來\
  填完所有區間後return dp[0][n-1]

  時間複雜度O(n^3)因為有三個迴圈\
  空間複雜度：DP表 O(n^2)
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
