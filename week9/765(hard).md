### 765. Couples Holding Hands

<img width="2866" height="1268" alt="image" src="https://github.com/user-attachments/assets/ace2c5e6-5aba-4858-bb86-52ab171a5824" />

* 解題思路\
  初始化一個hashmap 記錄每個人的位置，之後就可以只花O(1)找到伴侶\
  初始化swaps 代表交換次數\
  for 迴圈 每次檢查i 跟 i+1 是不是一對\
  是一對：不用swap；\
  if 不是一對：\
  swaps +1；把伴侶換到身邊並更新hashmap\
  greedy處理只會影響當前跟未處理區間，不會破壞已完成結果，保證全局最優；\
  每次swap 都是把一個錯誤pairing修正為正確pairing\
  return swaps
  
* 程式
```python
class Solution(object):
    def minSwapsCouples(self, row):
        """
        :type row: List[int]
        :rtype: int
        """
        pos = {person: i for i, person in enumerate(row)}  # 記錄每個人在哪個位置
        swaps = 0

        for i in range(0, len(row), 2):
            x = row[i]
            y = x ^ 1  # 找到x的伴侶

            if row[i + 1] != y:
                swaps += 1

                # 伴侶目前的位置
                partner_idx = pos[y]

                # 把 i+1 跟 partner_idx 的人交換
                row[i + 1], row[partner_idx] = row[partner_idx], row[i + 1]

                # 更新位置
                pos[row[partner_idx]] = partner_idx
                pos[row[i + 1]] = i + 1

        return swaps        
