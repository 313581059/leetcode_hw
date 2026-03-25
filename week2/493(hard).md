### 493. Reverse Pairs

<img width="2858" height="1266" alt="image" src="https://github.com/user-attachments/assets/1b225af2-89d1-4b64-b579-41e2240288e6" />
* 解題思路\
這題要計算有幾對i,j滿足i小於j 以及nums[i]大於兩倍nums[j] \
先舉一個例子2,4,3,5,1 會由merge_sort函數一直從中間切一刀 切成2,4,3、5,1再切2,4、3、5,1 

主要這題就是設計merge sort函數 \
如果index left大於等於index right就要return \
變數middle用來標記 左邊指到middle 右邊從middle+1開始指 \
遞迴merge sort 函數處理左半部分的nums array \
遞迴merge sort 函數處理右半部分的nums array

設計一個for loop 主要用來計算有幾對i,j符合題目要的定義 \
用一個while  loop \
對於每個左邊的元素nums[i]找到右邊的元素nums[j]是否滿足 大於兩倍 \
做一次 j+1 ，count儲存j-(mid+1) \
(這邊可以簡化成累加存到count變數就好嗎)

再用三個while loop處理merge_sort的動作 \
例如2,4跟3 \
第一個while會比較2,3跟4,3 得到[2,3]的排序 \
第二個while檢查整理左邊剩下的4 append到3後面 \
第三個while檢查整理右邊剩下的 沒有 就不用append \

整理好後更新nums

主程式呼叫這個寫好的mergesort \ 
從0到尾巴index 透過遞迴可以慢慢合併跟計算count return count

* 程式
```python
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
