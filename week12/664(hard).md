### 664. Strange Printer 
<img width="2871" height="1276" alt="image" src="https://github.com/user-attachments/assets/6526855e-3949-4a2f-8218-98b98e73b26d" />

* 解題思路\
  這一題我會用區間動態規劃來解。我定義 dp[i][j] 代表印出字串 s 從 i 到 j 這一段所需要的最少次數。首先我會先建立一個 n 乘 n 的 DP 表，一開始全部初始化為 0，代表所有子問題都還沒有被計算，接著我會先處理最基本的情況，也就是當 i 等於 j 的時候，dp[i][i] 一定等於 1，因為單一字元不論如何都至少需要印一次，所以在初始化之後，對角線會全部被填成 1。

    接下來我會按照區間長度由小到大去填表，因為較長的區間會依賴較短區間的結果，所以必須先確保子問題已經算過。在轉移的時候，對於每一段區間 dp[i][j]，我一開始會先給一個基本解，也就是假設 s[i] 這個字元自己單獨印一次，因此剩下的部分交給 dp[i+1][j]，所以初始值會是 dp[i+1][j] 加一。這代表最直覺的做法，就是一個一個字元慢慢印。

    但這題的關鍵在於可以合併操作，如果在 i 到 j 的區間中找到某個位置 k，使得 s[i] 等於 s[k]，那代表這兩個相同字元可以在同一次印刷中完成，因此我就可以嘗試把這兩段拆開來看，也就是中間區間分成 dp[i][k-1] 和 dp[k+1][j]，然後把這兩個結果相加，並用來更新 dp[i][j] 的最小值。

    實際舉例來說，如果字串是 "aba"，當我算到 dp[0][2] 的時候，一開始會先得到 baseline，也就是先印 a，再處理 "ba"，所以會是 3 次。但我會發現 s[0] 和 s[2] 都是 a，因此這兩個 a 可以在同一次操作中完成，中間的 b 再單獨處理，所以整體可以從 3 次減少成 2 次。

    最後填完整個 DP 表之後，dp[0][n-1] 就是答案，也就是整個字串最少需要的印刷次數。這題的核心就是透過區間 DP 枚舉所有可能的切分點，並利用相同字元可以合併印刷的特性來做最佳化。
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
