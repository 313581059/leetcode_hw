### 493. Reverse Pairs

<img width="2858" height="1266" alt="image" src="https://github.com/user-attachments/assets/1b225af2-89d1-4b64-b579-41e2240288e6" />

程式```python

class Solution(object):
    def reversePairs(self, nums):

        self.count = 0
        
        def merge_sort(left, right):
            if left >= right:
                return
            
            mid = (left + right) // 2
            
            merge_sort(left, mid)    # 這兩行 都做完了才進到j
            merge_sort(mid+1, right) # 先從最小的merge慢慢越merge越大
            
            # 關鍵：先數 reverse pairs
            j = mid + 1
            for i in range(left, mid+1):
                while j <= right and nums[i] > 2 * nums[j]:
                    j += 1
                self.count += (j - (mid+1))
            
            # 跟 LeetCode 315 幾乎一樣的 merge
            temp = []
            i, j = left, mid+1
            
            while i <= mid and j <= right:
                if nums[i] <= nums[j]:
                    temp.append(nums[i])
                    i += 1
                else:
                    temp.append(nums[j])
                    j += 1
            
            while i <= mid:
                temp.append(nums[i])
                i += 1
            
            while j <= right:
                temp.append(nums[j])
                j += 1
            
            # 回填
            nums[left:right+1] = temp
        
        merge_sort(0, len(nums)-1)
        return self.count      
