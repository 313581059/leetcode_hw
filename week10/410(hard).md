### 410. Split Array Largest Sum 

<img width="2857" height="1272" alt="image" src="https://github.com/user-attachments/assets/f739c397-bdcd-4b71-ab4d-df7c4ccadb8c" />

* 解題思路\
  先把 binary search 的左界設成陣列最大值，因為不管怎麼切，每個數字一定要被放進某一段。所以答案不可能小於最大元素。\
  右界設成整個陣列總和。因為最極端情況是不切，全部放同一段。\
  答案一定介於max(nums) ~ sum(nums)之間\
  用def can_split(limit):這個 function 來檢查\
  如果規定：每段總和不能超過 limit\
  能不能在：k 段內完成切割

  一開始至少有一段。所以count = 1\
  cur_sum 用來記錄目前這一段的總和。\
  從左到右掃描整個陣列。\
  如果目前這段再加入 num，會超過 limit。\
  代表這段不能再放了。必須切新的一段。count += 1\
  cur_sum = num 目前這個 num 改成新的一段開頭。\
  else 如果還沒超過 limit，代表可以繼續塞進目前這段。cur_sum += num累加即可。
  最後檢查：\
  總段數是否小於等於 k。\
  如果是，代表這個 limit 合法。\
  否則代表 limit 太小。

  while left < right:\
  開始 binary search。\
  當左右界還沒重疊時持續搜尋。\
  mid = (left + right) // 2\
  mid 代表：\
  目前猜測的答案。\
  也就是：每段允許的最大總和\
  如果 mid 可以合法切割。\
  代表答案有可能更小。\
  因此往左半邊搜尋。right = mid\
  else:如果不能切成功。\
  代表mid 太小了。限制太嚴格。\
  所以答案一定比 mid 大。往右半邊搜尋。left = mid + 1\
  return left 最後 left 和 right 會停在：最小合法答案。
  
* 程式
```python
class Solution(object):
    def splitArray(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        
        # 最小可能答案：陣列最大值
        left = max(nums)
        
        # 最大可能答案：全部加總
        right = sum(nums)

        # 檢查：
        # 如果每段最大和不能超過 limit
        # 最少需要切成幾段
        def can_split(limit):
            count = 1
            cur_sum = 0

            for num in nums:

                # 如果再加會超過 limit
                # 就切新的一段
                if cur_sum + num > limit:
                    count += 1
                    cur_sum = num
                else:
                    cur_sum += num

            return count <= k

        while left < right:

            mid = (left + right) // 2

            # 可以切成功
            # 代表答案可以更小
            if can_split(mid):
                right = mid

            # 切不成功
            # 代表答案太小
            else:
                left = mid + 1

        return left        
        
