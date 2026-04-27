### 630. Course Schedule III

<img width="2869" height="1263" alt="image" src="https://github.com/user-attachments/assets/125102f9-c7a7-4791-bb4b-f1d9c5f18603" />

* 解題思路\
  這題核心想法是「貪心」，\
  我會優先選擇 deadline 早的課，並且用 heap 動態維護目前選的課。\
  把所有課程依照 截止時間 lastDay 由小到大sort\
  total_time 用來記錄目前修課的總時間\
  max_heap 用來存目前已經選的課的 duration\
  用「負數」來模擬 max heap，\
  因為 Python 的 heapq 是 min heap。\
  透過迴圈一門一門課去考慮，每一輪代表「我要不要修這門課」。\
  先「貪心地假設這門課可以修」\
  所以把 duration 加進總時間，並且把這門課放進 heap 裡。\
  如果目前總時間已經超過這門課的 deadline，代表「這樣選課是不合法的」\
  做出修正，從目前已選的課中移除一門，選擇移除「duration 最長的那門課」\
  移除最長的課，可以讓 total_time 減少最多，是最有效的調整方式。\
  最後 heap 裡剩下的課數量，就是最多可以修的課數。
  
* 程式
```python
import heapq

class Solution(object):
    def scheduleCourse(self, courses):
        """
        :type courses: List[List[int]]
        :rtype: int
        """
        # 先按照 deadline 排序
        courses.sort(key=lambda x: x[1])
        
        total_time = 0
        max_heap = []  # 用來存目前選的課（負數模擬 max heap）

        for duration, lastDay in courses:
            # 先假設這門課可以修
            total_time += duration
            heapq.heappush(max_heap, -duration)

            # 如果超過 deadline，就移除最花時間的課
            if total_time > lastDay:
                longest = -heapq.heappop(max_heap)
                total_time -= longest

        return len(max_heap)        
