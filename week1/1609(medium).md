### 1609. Even Odd Tree

<img width="2859" height="1272" alt="image" src="https://github.com/user-attachments/assets/fc969d7c-485e-47c5-bb61-4efd43b495d1" />

解題思維
這題要求對 binary tree 的每一層做條件檢查，因此我選擇使用 BFS 廣度優先搜尋來做 level order traversal(逐層遍歷)。\
BFS 可以一層一層處理節點，剛好符合題目需求。\
size = len(queue) 這行確保我一次只會處理完同一層的所有節點。\
prev 用來記錄「同一層前一個節點的值」，避免跨層比較。\
條件判斷：當偶數層的時候，數字必須都為奇數，且遞增；為奇數層的時候，數字必須都為偶數，且遞減。\
更新prev，也更新queue。\
一層處理完 換處理下一層(節點都被保存在更新的queue中)\
BFS遍歷這棵樹，每個 node 只會被訪問一次，時間複雜度為O(n)。

程式

```python
from collections import deque

class Solution(object):
    def isEvenOddTree(self, root):
        queue = deque([root])  # BFS的解法，BFS得到第一層的節點
        level = 0              # 奇數偶數層的判定

        while queue:  # 一層一層來
            size = len(queue)
            prev = None # 目前值每一層(輪)會更新，最左邊那顆還不用比所以暫定為None
            
            for _ in range(size):      # 一次只處理一層
                node = queue.popleft() # 取出 queue 最前面的 node，一顆一顆取出來檢查，檢查過了就檢查下一顆
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
                
                prev = val  # 把目前這顆node值記錄成下一顆node比較的基準
                # BFS 的核心，走到一個 node，把它的 children 加入 queue (queue會帶領走完整棵樹)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            level += 1

        return True
```
* 相似題 \
    ✅ 102 Binary Tree Level Order Traversal \
    少掉prev、level、奇偶數遞增遞減判定 \
    多了辦別什麼時候appendlist、遇到空list的處理
