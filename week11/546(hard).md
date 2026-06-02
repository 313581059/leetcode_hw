### 546. Remove Boxes 

<img width="2849" height="1268" alt="image" src="https://github.com/user-attachments/assets/2da2c09b-fdce-4e78-a0a6-5931932ed1c3" />

* 解題思路\
  
* 程式
```python
class Solution(object):
    def removeBoxes(self, boxes):
        """
        :type boxes: List[int]
        :rtype: int
        """
        n = len(boxes)

        # dp[l][r]
        dp = [[[0] * n for _ in range(n)] for _ in range(n)]

        def dfs(l, r, k):
            if l > r:
                return 0

            # 把尾巴同色全部吃掉
            while l < r and boxes[r] == boxes[r - 1]:
                r -= 1
                k += 1

            if dp[l][r][k]:
                return dp[l][r][k]

            # case1：直接消掉最後一段
            res = dfs(l, r - 1, 0) + (k + 1) * (k + 1)

            # case2：把同色拉過來合併
            for i in range(l, r):
                if boxes[i] == boxes[r]:
                    res = max(
                        res,
                        dfs(l, i, k + 1) + dfs(i + 1, r - 1, 0)
                    )

            dp[l][r][k] = res
            return res

        return dfs(0, n - 1, 0)
