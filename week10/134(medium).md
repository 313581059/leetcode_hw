### 134. Gas Station 

<img width="2865" height="1262" alt="image" src="https://github.com/user-attachments/assets/6b1f5c59-330b-4793-ade6-4603e1c99061" />

* 解題思路\
  total 用來判斷整體油量夠不夠繞一圈\
  tank 表示目前車上的油\
  start 紀錄目前假設的起點\
  遍歷每個加油站：從左到右檢查每個加油站\
  計算這站的淨油量：diff 代表在這站加完油、開到下一站後剩多少\
  更新 total 與 tank：total 記錄整體總油量；tank 記錄目前路上的剩餘油量\
  如果 tank < 0：如果目前油量變負數，代表從 start 出發沒辦法走到這裡\
  直接把下一站設成新的起點，並把 tank 重置。
  
* 程式
```python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        total = 0
        tank = 0
        start = 0
        
        for i in range(len(gas)):
            diff = gas[i] - cost[i]
            
            total += diff
            tank += diff
            
            if tank < 0:
                start = i + 1
                tank = 0
        
        return start if total >= 0 else -1        
