### 932. Beautiful Array

<img width="2868" height="1273" alt="image" src="https://github.com/user-attachments/assets/e2f932bd-54e4-4e4d-9fc8-594078633025" />

* 解題思路 \
  題目理解：\
  給你 n，要產生一個排列 1 ~ n，滿足：\
  不存在 i < k < j，使得 2 * nums[k] == nums[i] + nums[j]，\
  所以，中間數 禁止等於 左右平均，關鍵：不能形成等差數列。
  
  核心方法：\
  用 divide and conquer，把陣列拆成奇數和偶數，透過 2x-1 和 2x 映射，確保不會產生等差數列，\
  實際步驟：\
  把數列拆成「奇數」和「偶數」，\
  假設已經有一個漂亮陣列 A，\
  構建奇數部分:  2x - 1 \
  構建偶數部分:  2x 

  定義一個函數： f(n) = 長度 n 的 beautiful array \
  遞迴\
  f(n) = 奇數部分 + 偶數部分 \
  奇數部分  = f((n+1)//2) 映射成 2*x - 1 \
  偶數部分  = f(n//2)     映射成 2*x 
* 程式
```python
class Solution(object):
    def beautifulArray(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        res = [1]
        
        while len(res) < n:
            temp = []
            
            # 奇數
            for x in res:
                if 2*x - 1 <= n:
                    temp.append(2*x - 1)
            
            # 偶數
            for x in res:
                if 2*x <= n:
                    temp.append(2*x)
            
            res = temp
        
        return res        
