### 240. Search a 2D Matrix II

<img width="2846" height="1273" alt="image" src="https://github.com/user-attachments/assets/5bf5ccd1-2223-4ccb-89ec-6212dadbb8f7" />

* 解題思路
  核心想法：從「右上角」開始找，如果目前數字 太大 → 往左（變小）；如果目前數字 太小 → 往下（變大），每一步都能排除一整列或一整行，。

  假設從 (row=0, col=n-1) 開始：
  while 還在矩陣範圍內:
    if 當前值 == target → 找到
    if 當前值 > target → col -= 1（往左）
    if 當前值 < target → row += 1（往下）
  時間複雜度：最多走 m + n 步 O(m+n)
  
* 程式
```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]:
            return False
        
        m, n = len(matrix), len(matrix[0])
        row, col = 0, n - 1  # 從右上角開始
        
        while row < m and col >= 0:
            if matrix[row][col] == target:
                return True
            elif matrix[row][col] > target:
                col -= 1
            else:
                row += 1
        
        return False        
