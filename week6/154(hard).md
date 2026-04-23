### 154. Find Minimum in Rotated Sorted Array II

<img width="2876" height="1280" alt="image" src="https://github.com/user-attachments/assets/6a51daee-d714-4265-8e56-46df6ee208f5" />
* 解題思路 \
    使用binary search 因為每次砍一半可以節省時間複雜度，\
    透過比較mid和right來判斷最小值的位置：\
    if mid < right 表示最小值在左邊(包含mid) 於是砍掉右邊的元素們 right=mid\
    elif mid > right mid是屬於左邊序列大的數字，最小值應在右邊，於是砍掉左邊 left = mid+1\
    else 代表mid=right， 因為無法判斷 保守做right-1(線性掃描) 反正right不是唯一最小 最小至少還有mid扛\
    反覆while left< right 做到left==right就會停止(不可能做到>)\
    return left位置的nums數值

  
* 程式
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
