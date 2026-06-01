### 330. Patching Array 

<img width="2860" height="1270" alt="image" src="https://github.com/user-attachments/assets/cc5440d2-e412-403f-87f2-4a66b8ec373e" />

* 解題思路\
  維護一個 miss\
  代表目前「最小無法被組出的數字」。\
  接著看 nums[i]：\
  如果：nums[i] <= miss 代表它可以接在目前範圍後面。\
  例如：原本可組 1-7 加入 5 後可以變成 1-12 \
  所以：miss += nums[i]\
  但如果：nums[i] > miss\
  代表中間缺洞。最好的做法是直接補：miss： miss += miss\
  一直做到：miss > n 代表：1~n 全都能組出
  
* 程式
```python
class Solution(object):
    def minPatches(self, nums, n):
        """
        :type nums: List[int]
        :type n: int
        :rtype: int
        """
        miss = 1
        i = 0
        patches = 0

        while miss <= n:

            # nums[i] 可以接上目前覆蓋範圍
            if i < len(nums) and nums[i] <= miss:
                miss += nums[i]
                i += 1

            # nums[i] 太大，中間缺了 miss
            else:
                miss += miss
                patches += 1

        return patches        
