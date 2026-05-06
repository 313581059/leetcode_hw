### 2405. Optimal Partition of String

<img width="2854" height="1273" alt="image" src="https://github.com/user-attachments/assets/54f78cf3-77de-467e-8c55-5c6caaa96ccd" />

* 解題思路\
  用一個 set 來記錄目前 substring 出現過的字元\
  並且至少會有一段，所以 count 初始化為 1\
  從左到右掃整個字串\
  如果這個字元已經出現過，代表不能再放在同一段\
  就切一段，段數加 1，並清空 set 重新開始\
  把目前字元加入新的 substring\
  最後回傳總段數
  
* 程式碼
```python
class Solution(object):
    def partitionString(self, s):
        """
        :type s: str
        :rtype: int
        """
        seen = set()
        count = 1  # 至少一段
        
        for ch in s:
            if ch in seen:
                count += 1
                seen.clear()
            seen.add(ch)
        
        return count        
