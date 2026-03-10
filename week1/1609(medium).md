### 1609. Even Odd Tree

<img width="2859" height="1272" alt="image" src="https://github.com/user-attachments/assets/fc969d7c-485e-47c5-bb61-4efd43b495d1" />

程式

```python
from collections import deque

class Solution(object):
    def isEvenOddTree(self, root):
        queue = deque([root])  # BFS的解法
        level = 0

        while queue:
            size = len(queue)
            prev = None # 記錄上一個 node 的值
            
            for _ in range(size):
                node = queue.popleft() # 取出 queue 最前面的 node
                val = node.val         # 取得 node 的值
                
                if level % 2 == 0:
                    if val % 2 == 0: # 必須奇數
                        return False
                    if prev != None and val <= prev: # 必須遞增
                        return False
                else:
                    if val % 2 == 1: # 必須偶數
                        return False
                    if prev != None and val >= prev: # 必須遞減
                        return False
                
                prev = val  # 把目前值記錄成下一次比較的基準
                # BFS 的核心，走到一個 node，把它的 children 加入 queue
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            level += 1

        return True
