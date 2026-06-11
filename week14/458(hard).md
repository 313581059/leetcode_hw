### 458. Poor Pigs
<img width="2850" height="1268" alt="image" src="https://github.com/user-attachments/assets/97afc3e6-d9d4-4625-8a4c-97897f56ed08" />

* 解題思路\
  rounds=Test/Die 得到時間內總共能做幾輪測試\
  pigs=0\
  while (round+1)^pigs < buckets:\
  pigs+1\
  用round+1代表一隻豬共有幾種狀態\
  pig次方是由於 例如一隻豬有5種 兩隻豬就會有25種\
  while迴圈check能不能涵蓋所有桶子

  時間複雜度是O(log  bucket除以log round+1)\
  空間複雜度是O(1)
* 程式
```python
class Solution(object):
    def poorPigs(self, buckets, minutesToDie, minutesToTest):
        """
        :type buckets: int
        :type minutesToDie: int
        :type minutesToTest: int
        :rtype: int
        """
        rounds = minutesToTest // minutesToDie

        pigs = 0
        while (rounds + 1) ** pigs < buckets:
            pigs += 1

        return pigs        
