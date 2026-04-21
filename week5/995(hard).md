### 995. Minimum Number of K Consecutive Bit Flips

<img width="2872" height="1273" alt="image" src="https://github.com/user-attachments/assets/dae18dd3-f14c-493b-bc0f-48566d5fe196" />

* 解題思路\
  這題我沒有真的去翻轉陣列，而是用一個 flip 變數來記錄目前位置被前面翻轉影響的次數（只看奇偶）。\
  因此當我在位置 i 時，實際的值可以用 nums[i] 和 flip 判斷；如果 nums[i] == flip，代表當前實際是 0，需要從這裡開始做一次翻轉。\
  每次翻轉我只記錄起點在 is_flipped[i]，並將 flip ^= 1 表示增加一個影響。\
  由於每個翻轉只影響長度 k 的區間，所以當 i >= k 時，我會用 flip ^= is_flipped[i-k] 移除已經過期的翻轉影響，讓 flip 始終代表當前有效的翻轉狀態。\
  這樣可以在 O(n) 時間內完成，而不需要真的修改陣列。
* 程式
```python
class Solution(object):
    def minKBitFlips(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        n = len(nums)
        is_flipped = [0] * n
        flip = 0
        res = 0

        for i in range(n):
            if i >= k:
                flip ^= is_flipped[i - k]

            # 當前實際的 bit
            if nums[i] == flip:
                if i + k > n:
                    return -1
                is_flipped[i] = 1
                flip ^= 1
                res += 1

        return res        
