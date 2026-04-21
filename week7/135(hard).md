### 135. Candy

<img width="2866" height="1277" alt="image" src="https://github.com/user-attachments/assets/9a1cde64-6ccf-49d8-98ea-3cc20e810bb4" />

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
