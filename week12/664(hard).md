### 664. Strange Printer 
<img width="2871" height="1276" alt="image" src="https://github.com/user-attachments/assets/6526855e-3949-4a2f-8218-98b98e73b26d" />

* 解題思路\
* 程式
```python
class Solution(object):
    def strangePrinter(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)

        dp = [[0] * n for _ in range(n)]

        # 長度1
        for i in range(n):
            dp[i][i] = 1

        # 區間長度
        for length in range(2, n + 1):

            for i in range(n - length + 1):

                j = i + length - 1

                # 最笨情況：s[i]自己印一次
                dp[i][j] = dp[i + 1][j] + 1

                # 找能跟 s[i] 合併印的
                for k in range(i + 1, j + 1):

                    if s[i] == s[k]:

                        left = dp[i][k - 1]
                        right = dp[k + 1][j] if k + 1 <= j else 0

                        dp[i][j] = min(dp[i][j], left + right)

        return dp[0][n - 1]      
