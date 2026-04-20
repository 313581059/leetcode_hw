### 45. Jump Game II 
<img width="2869" height="1258" alt="image" src="https://github.com/user-attachments/assets/1d6bedd8-e548-41ef-b0af-cf71f6805c39" />

* 解題思路
  用 greedy 維護每一步能到的範圍，當走到邊界就增加一步，並更新下一步的最遠距離，時間複雜度 O(n)\
  每一層（step）代表「一次跳躍能覆蓋的範圍」，在這範圍內，我們選擇讓「下一層能走最遠」\
  BFS 的層概念 + 貪心優化，因為最後一格不用再跳了，所以loop 到 n-1 就好。
* 程式
```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        steps = 0
        end = 0
        farthest = 0
        
        for i in range(len(nums) - 1):
            farthest = max(farthest, i + nums[i])
            
            if i == end:
                steps += 1
                end = farthest
        
        return steps        
