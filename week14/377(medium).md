### 377. Combination Sum IV

<img width="2858" height="1278" alt="image" src="https://github.com/user-attachments/assets/c4cc0f26-0b0b-4ee2-b482-8d79036cbe04" />

* 解題思路\
  初始化 DP\
  dp[i] 表示湊出總和 i 的方法數\
  dp[0] = 1 代表「什麼都不選」有一種方法\
  從小到大計算每個總和的方法數\
  嘗試每個 num\
  對每個數字，檢查能不能接到目前總和\
  如果目前 num 可以使用\
  那我就把湊出 i-num 的方法數加過來\
  等於把 num 接在最後面\
  最後回傳湊出 target 的總方法數
* 程式
```python
class Solution(object):
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        dp = [0] * (target + 1)
        dp[0] = 1
        
        for i in range(1, target + 1):
            for num in nums:
                if i >= num:
                    dp[i] += dp[i - num]
        
        return dp[target]        
        
