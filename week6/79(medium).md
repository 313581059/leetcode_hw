### 79. Word Search

<img width="2855" height="1266" alt="image" src="https://github.com/user-attachments/assets/b8bd25e6-924c-463f-a534-d2129e939c93" />

* 解題思路 \
  DFS + Backtracking \
  從每個點當起點做 DFS，如果當前字母符合，就往四個方向繼續找下一個字母，\
  定義 dfs(i, j, k)，(i, j)：目前位置，k：目前匹配到 word[k] 

  遞迴邏輯:\
  1. 如果 matrix[i][j] != word[k] → return False
  2. 如果 k == len(word)-1 → return True（全部匹配）
  3. 標記這格為已訪問
  4. 往四個方向 DFS
  5. 還原（backtracking）# 做這步是因為這條路不行，要讓別條路可以再用這個格子！
* 程式
```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        m, n = len(board), len(board[0])
        
        def dfs(i, j, k):
            if board[i][j] != word[k]:
                return False
            
            if k == len(word) - 1:
                return True
            
            temp = board[i][j]
            board[i][j] = "#"  # 標記已訪問
            
            for dx, dy in [(1,0), (-1,0), (0,1), (0,-1)]:
                x, y = i + dx, j + dy
                if 0 <= x < m and 0 <= y < n:
                    if dfs(x, y, k + 1):
                        return True
            
            board[i][j] = temp  # 回溯
            return False
        
        for i in range(m):
            for j in range(n):
                if dfs(i, j, 0):
                    return True
        
        return False        
