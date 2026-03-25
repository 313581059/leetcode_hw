### 3537. Fill a Special Grid

<img width="2857" height="1265" alt="image" src="https://github.com/user-attachments/assets/6d76e521-b8b0-4a62-83b0-f37af5a663b0" />

* 解題思路 \
  方塊版本的Divide and Conquer \
  base case [[0]] \
  遞迴設計：\
  已知n-1的方塊解（大小是 m × m）\
  構建n的方塊（大小是 2m × 2m）\
  把 n-1 的 grid 複製四份，放到四個象限\
  數值分配：\
  offset = m × m \
  右上：最小 → 不加 \
  右下：+1 × offset \
  左下：+2 × offset \
  左上：+3 × offset \
  每個象限的數值範圍會變成：\
  右上：[0, offset-1] \
  右下：[offset, 2offset-1] \
  左下：[2offset, 3offset-1] \
  左上：[3offset, 4offset-1]
  
  
  
* 程式
```python
class Solution(object):
    def specialGrid(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if n == 0:
            return [[0]]

        sub = self.specialGrid(n - 1)
        m = len(sub)
        size = m * 2
        offset = m * m

        grid = [[0] * size for _ in range(size)]

        for i in range(m):
            for j in range(m):
                val = sub[i][j]

                # 四個象限（照題目順序）
                grid[i][j + m] = val                  # 右上 (最小)
                grid[i + m][j + m] = val + offset     # 右下
                grid[i + m][j] = val + 2 * offset     # 左下
                grid[i][j] = val + 3 * offset         # 左上 (最大)

        return grid     
