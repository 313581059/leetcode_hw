### 44. Wildcard Matching

<img width="2868" height="1271" alt="image" src="https://github.com/user-attachments/assets/d8cefb4d-a323-4512-9708-30bbfbbe26a5" />

* 解題思路\

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
