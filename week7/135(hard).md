### 135. Candy

<img width="2866" height="1277" alt="image" src="https://github.com/user-attachments/assets/9a1cde64-6ccf-49d8-98ea-3cc20e810bb4" />

* 解題思路\
  這個函式輸入是一個 ratings 陣列，代表每個小孩的評分。\
  先取得總共有幾個小孩。\
  初始化每個人都有 1 顆糖，因為題目規定每人至少一顆。\
  接下來從左到右掃描，從第二個人開始\
  (處理右邊比左邊大)\
  如果當前這個人的評分比左邊的人高，那他的糖果數就要比左邊多一顆，這樣才能滿足題目的條件。\
  接著從右到左再掃一次，從倒數第二個人開始\
   (處理左邊比右邊大)\
  如果當前這個人的評分比右邊的人高，那他應該要比右邊多一顆糖，但要取 max，\
  因為他可能在前面的左到右掃描中已經拿到比較多糖了，不能把原本合法的結果覆蓋掉。\
  最後把所有糖果加總，就是最少需要的糖果數量。

* 程式碼
```python
class Solution(object):
    def candy(self, ratings):
        """
        :type ratings: List[int]
        :rtype: int
        """
        n = len(ratings)
        candies = [1] * n

        # 從左到右：確保右邊比左邊大就 +1
        for i in range(1, n):
            if ratings[i] > ratings[i - 1]:
                candies[i] = candies[i - 1] + 1

        # 從右到左：修正左邊比右邊大的情況
        for i in range(n - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candies[i] = max(candies[i], candies[i + 1] + 1)

        return sum(candies)        
