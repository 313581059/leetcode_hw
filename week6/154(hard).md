### 154. Find Minimum in Rotated Sorted Array II

<img width="2876" height="1280" alt="image" src="https://github.com/user-attachments/assets/6a51daee-d714-4265-8e56-46df6ee208f5" />
*解題思路\
*程式
```python
class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        left, right = 0, len(nums) - 1
        
        while left < right:
            mid = (left + right) // 2
            
            if nums[mid] < nums[right]:
                right = mid
            elif nums[mid] > nums[right]:
                left = mid + 1
            else:
                right -= 1
        
        return nums[left]        
