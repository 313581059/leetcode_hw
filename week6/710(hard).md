### 710. Random Pick with Blacklist

<img width="2862" height="1271" alt="image" src="https://github.com/user-attachments/assets/d44994d6-e8ad-427c-b628-d998d492d101" />
*解題思路\
*程式
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
