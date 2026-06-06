### 458. Poor Pigs
<img width="2850" height="1268" alt="image" src="https://github.com/user-attachments/assets/97afc3e6-d9d4-4625-8a4c-97897f56ed08" />

* 解題思路\
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
