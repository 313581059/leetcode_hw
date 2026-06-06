### 639. Decode Ways II 

<img width="2858" height="1268" alt="image" src="https://github.com/user-attachments/assets/836dd614-9821-490d-b08c-ad86e247b98f" />

* 解題思路\
* 程式
```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        MOD = 10**9 + 7
        n = len(s)

        # dp0 = dp[i-2]
        # dp1 = dp[i-1]
        dp0 = 1

        # 第一個字元自己能怎麼解
        if s[0] == '*':
            dp1 = 9
        elif s[0] == '0':
            dp1 = 0
        else:
            dp1 = 1

        for i in range(1, n):
            cur = 0

            # -------- 單獨解碼 --------
            if s[i] == '*':
                cur += 9 * dp1
            elif s[i] != '0':
                cur += dp1

            # -------- 兩位數一起解碼 --------
            prev = s[i - 1]
            curr = s[i]

            # **
            if prev == '*' and curr == '*':
                # 11~19 + 21~26
                cur += 15 * dp0

            # *數字
            elif prev == '*':
                if '0' <= curr <= '6':
                    # 1x 或 2x
                    cur += 2 * dp0
                else:
                    # 只能是1x
                    cur += dp0

            # 數字*
            elif curr == '*':
                if prev == '1':
                    # 11~19
                    cur += 9 * dp0
                elif prev == '2':
                    # 21~26
                    cur += 6 * dp0

            # 普通兩位數
            else:
                if 10 <= int(prev + curr) <= 26:
                    cur += dp0

            cur %= MOD

            dp0 = dp1
            dp1 = cur

        return dp1        
