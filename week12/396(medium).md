### 396. Rotate Function 

<img width="2867" height="1269" alt="image" src="https://github.com/user-attachments/assets/1fca6ddf-cc2a-4c18-8ca1-62414fe26799" />

* 解題思路\
  先計算整個 array 的總和，後面更新 rotate function 會用到\
  計算原本沒有 rotate 時的 F(0)\
  先把初始 rotate function 當作目前最大值\
  開始更新每次 rotation，從最後一個元素開始模擬 rotation\
  不用真的 rotate array，而是直接用上一個結果 O(1) 更新下一個結果
  
* 程式
```python
class Solution(object):
    def maxRotateFunction(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        
        total = sum(nums)
        f = sum(i * num for i, num in enumerate(nums))
        
        ans = f
        
        for i in range(n - 1, 0, -1):
            f = f + total - n * nums[i]
            ans = max(ans, f)
        
        return ans        
