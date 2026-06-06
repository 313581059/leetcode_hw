### 546. Remove Boxes 

<img width="2849" height="1268" alt="image" src="https://github.com/user-attachments/assets/2da2c09b-fdce-4e78-a0a6-5931932ed1c3" />

* 解題思路\
  定義一個dfs function，計算box l到r區間最大分數，\
  k代表右方相同盒子數量，\
  如果l>r：區間不存在，return 0。\
  如果r和r-1相同，先做合併：並且將r-1 k+1 (減少dp狀態)，

  設計兩種決策，\
  第一種：\
  決定現在就把boxes[r]同類盒子刪掉，\
  dfs(l,r-1,0)+(k+1)*(k+1)\
  前半部分：先把不包含r前面的區間處理完；後半部分：把目前這一整段同色包含k+boxes[r]一次刪掉\
  第二種：\
  決定先不刪boxes[r]想辦法留到合併後再刪，\
  dfs(l, i, k + 1) + dfs(i + 1, r - 1, 0)\
  前半部分：選擇讓i這個同色加入未來要一起刪的群組；後半部分：先把中間清掉讓合併可以成立

  避免重複計算，用三維陣列dp[l][r][k]紀錄每個狀態的答案
  return dfs(0, n-1, 0)
  
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
