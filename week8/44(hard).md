### 44. Wildcard Matching

<img width="2868" height="1271" alt="image" src="https://github.com/user-attachments/assets/d8cefb4d-a323-4512-9708-30bbfbbe26a5" />

* 解題思路\
先初始化四個變數：\
i：指向字串 s 的位置\
j：指向 pattern p 的位置\
star：用來記錄「最後一次遇到 * 的位置」，一開始設為 -1 代表還沒遇到\
match：記錄當下 * 對應到 s 的位置，方便之後回溯使用\
當 s 還沒走完，就while持續比對\
情況1：正常 match\
如果：目前字元一樣 或是 p[j] 是 ?（可以 match 任一字元）\
那就代表這一格 match 成功，所以 i、j 都往前走\
情況2：遇到 *\
如果遇到 *：會先把這個位置記下來\
star = j：記錄 * 在 pattern 的位置\
match = i：記錄當下 s 的位置\
然後 j += 1，先假設 * 是「match 空字串」\
情況3：不 match，但之前有 *\
如果現在 mismatch，但之前出現過 *\
就「回去用那個 * 幫忙」\
具體做法是：\
j = star + 1 回到 * 的下一個位置\
match += 1 讓 * 多吃一個字元\
i = match 從新的位置重新開始比\
這裡是在做「貪心 + 回溯」\
情況4：完全不 match\
如果：現在不 match，而且也沒有 * 可以救\
那就直接回傳 False\
收尾（處理剩下的 *）\
因為 * 可以代表空字串，所以把剩下的 * 全部跳過\
最終判斷，如果 pattern 也剛好走完，才代表完全 match 成功

* 程式
```python
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        i = j = 0
        star = -1
        match = 0

        while i < len(s):
            # 情況1：字元相同 or ?
            if j < len(p) and (p[j] == s[i] or p[j] == '?'):
                i += 1
                j += 1

            # 情況2：遇到 *
            elif j < len(p) and p[j] == '*':
                star = j
                match = i
                j += 1

            # 情況3：不匹配，但之前有 *
            elif star != -1:
                j = star + 1
                match += 1
                i = match

            # 情況4：完全沒救
            else:
                return False

        # 把剩下的 * 消掉
        while j < len(p) and p[j] == '*':
            j += 1

        return j == len(p)        
