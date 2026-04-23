### 710. Random Pick with Blacklist

<img width="2862" height="1271" alt="image" src="https://github.com/user-attachments/assets/d44994d6-e8ad-427c-b628-d998d492d101" />


* 解題思路

1. init函式用來建立mapping\
首先設定bound 長度n-長度blacklist，只有[0,bound)內的不合法值要找替身\
再來寫一個for迴圈 由尾端向前掃，跳過blacklist的值\
製作不合法blacklist值 適合的替身對照表

2. pick函式\
x random抽取，遇到不合法值，查表後return；遇到合法的值，直接return。

為了避免重複使用同一個替代數字，我從尾端開始往下掃，確保每個替身只使用一次，同時維持 O(k) 的建構效率。

* 程式
```python
import random
class Solution(object):

    def __init__(self, n, blacklist):
        """
        :type n: int
        :type blacklist: List[int]
        """
        self.map = {}
        self.bound = n - len(blacklist)
        
        black = set(blacklist)
        
        # 可用來替換的數字（從尾巴找）
        last = n - 1
        
        for b in blacklist:
            if b < self.bound:
                # 找一個沒在 blacklist 裡的數字
                while last in black:
                    last -= 1
                self.map[b] = last
                last -= 1        

    def pick(self):
        """
        :rtype: int
        """
        x = random.randint(0, self.bound - 1)
        return self.map.get(x, x)        
