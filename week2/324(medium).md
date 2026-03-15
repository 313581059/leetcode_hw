### 324. Wiggle Sort II

<img width="2849" height="1100" alt="image" src="https://github.com/user-attachments/assets/731f2892-c742-4120-a60b-ac7d90aa0e27" />

程式
```python
class Solution(object):
    def wiggleSort(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        nums.sort()
        mid = (len(nums) + 1) // 2
        left  = nums[:mid][::-1]
        right = nums[mid:][::-1]

        nums[::2] = left
        nums[1::2] = right
```
* Divide and Conquer \
  1. 排序 \
  2. 把數列分成兩半 \
  3. 大的放奇數位 \
     小的放偶數位
  

        
