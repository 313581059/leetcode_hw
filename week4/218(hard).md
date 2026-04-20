### 218. The Skyline Problem 
<img width="2857" height="1266" alt="image" src="https://github.com/user-attachments/assets/3f9ca531-8972-44e0-b58e-b9abc29c63dd" />
* 解題思路\ 
建立建築物開始、建築物結束、heap\
按照x軸順序排列，觀察y軸如果有變化 就更新heap，\
並且有一個指標記錄前一個y 一個指標紀錄現在的y\
如果指標有變化 就記錄該x,y座標到答案的list裡面
  
* 程式
```python
import heapq
class Solution(object):
    def getSkyline(self, buildings):
        """
        :type buildings: List[List[int]]
        :rtype: List[List[int]]
        """
        events = []
        for l, r, h in buildings:
            events.append((l, -h, r))  # 左邊界（負高度）
            events.append((r, 0, 0))   # 右邊界

        events.sort()

        heap = [(0, float('inf'))]  # (height, end)
        res = []
        prev = 0

        for x, h, r in events:

            while heap[0][1] <= x:
                heapq.heappop(heap)

            if h != 0:
                heapq.heappush(heap, (h, r))

            curr = -heap[0][0]

            if curr != prev:
                res.append([x, curr])
                prev = curr

        return res      
