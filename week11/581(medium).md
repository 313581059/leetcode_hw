### 581. Shortest Unsorted Continuous Subarray 

<img width="2860" height="1277" alt="image" src="https://github.com/user-attachments/assets/c6825c7b-033d-4cc7-b971-800558cd7bc5" />

* 解題思路\
  初始化左右邊界，left 跟 right 用來記錄需要排序的區間\
  初始化目前最大最小值，max_seen 表示目前掃過最大的值，min_seen 表示目前掃過最小的值\
  從左往右檢查 array\
  持續更新目前看過最大的數\
  如果現在的數比前面最大值還小，代表排序被破壞了，所以更新 right\
  接著從右往左掃描\
  更新目前看過最小的值\
  如果現在的數比後面最小值還大，代表這裡也破壞排序，所以更新 left\
  如果 right 沒更新，代表本來就排序好，否則回傳區間長度
  
* 程式
```python
class Solution(object):
    def findUnsortedSubarray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        
        left = -1
        right = -1
        
        max_seen = nums[0]
        min_seen = nums[-1]
        
        # 從左往右找 right
        for i in range(n):
            max_seen = max(max_seen, nums[i])
            
            if nums[i] < max_seen:
                right = i
        
        # 從右往左找 left
        for i in range(n - 1, -1, -1):
            min_seen = min(min_seen, nums[i])
            
            if nums[i] > min_seen:
                left = i
        
        return 0 if right == -1 else right - left + 1        
