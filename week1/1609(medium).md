<img width="2859" height="1272" alt="image" src="https://github.com/user-attachments/assets/fc969d7c-485e-47c5-bb61-4efd43b495d1" />
```python
from collections import deque

class Solution(object):
    def isEvenOddTree(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        queue = deque([root])  #BFS的解法
        level = 0

        while queue:

            size = len(queue)
            
            prev = None
            
            for _ in range(size):

                node = queue.popleft()
                
                val = node.val
                
                if level % 2 == 0:
                    # 必須奇數
                    if val % 2 == 0:
                        return False
                    # 必須遞增
                    if prev != None and val <= prev:
                        return False                    
                else:
                    # 必須偶數
                    if val % 2 == 1:
                        return False
                    # 必須遞減
                    if prev != None and val >= prev:
                        return False
                prev = val
                
                if node.left:
                    queue.append(node.left)
                
                if node.right:
                    queue.append(node.right)

            level += 1
        return True
        
```
