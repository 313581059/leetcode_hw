### 2139. Minimum Moves to Reach Target Score

<img width="2842" height="1258" alt="image" src="https://github.com/user-attachments/assets/35c34ef9-9bf3-47c2-9cff-7940a3691921" />

* 解題思路\
  這題我採用「從 target 反推回 1」的 greedy 方法，因為正向不好決定何時乘 2\
  用 steps 來記錄目前用了幾步操作\
  當 target 還沒回到 1，而且我還有乘 2 的次數時，就繼續做貪心選擇\
  如果現在是偶數，代表有機會用除以 2 來快速縮小數字\
  做除以 2，並且把可用的 double 次數減 1\
  如果是奇數，就沒辦法直接除以 2，只能先減 1 讓它變成偶數\
  不管是哪種操作，我都把步數加 1\
  當 maxDoubles 用完後，我就不能再做除以 2\
  剩下只能一直減 1 才能回到 1\
  所以我直接加上 (target - 1) 步

  
* 程式
```python
class Solution(object):
    def minMoves(self, target, maxDoubles):
        steps = 0
        
        while target > 1 and maxDoubles > 0:
            if target % 2 == 0:
                target //= 2
                maxDoubles -= 1
            else:
                target -= 1
            steps += 1
        
        # 剩下只能 -1 沒加會TLE
        return steps + (target - 1)
