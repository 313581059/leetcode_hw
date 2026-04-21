### 761. Special Binary String

<img width="2873" height="1266" alt="image" src="https://github.com/user-attachments/assets/1848e66f-7b93-49ac-8063-9b12ee7364de" />

* 解題思路\
1. 透過for迴圈檢查字串的哪一個index 能夠代表一段符合的special binary string(抽出來一定本身就是1開頭0結尾)
2. 遞迴讓這個小段的substring 在變得1能夠多在前面的位置滿足special binary string
3. 透過一個暫時的陣列儲存1+整理好的substring+0
4. 將陣列裡多個小substring 排序成大的在前小的在後
5. return 陣列裡合併起來的數字
* 程式
```python
class Solution(object):
    def makeLargestSpecial(self, s):
        """
        :type s: str
        :rtype: str
        """
        res = []
        count = 0
        start = 0
        
        for i, c in enumerate(s):
            if c == '1':
                count += 1
            else:
                count -= 1
            
            # 找到一個完整 special substring
            if count == 0:
                # 遞迴處理中間
                inner = self.makeLargestSpecial(s[start+1:i])
                res.append('1' + inner + '0')
                start = i + 1
        
        # 排序讓字典序最大
        res.sort(reverse=True)
        
        return ''.join(res)        
