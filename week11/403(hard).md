### 403. Frog Jump

<img width="2870" height="1266" alt="image" src="https://github.com/user-attachments/assets/551c0c11-da7d-47c6-9fa6-596097ef0b49" />

* 解題思路\
  這題我使用 DFS 搭配 Memoization 來解。我先把 stones 轉成 set，因為後面會一直檢查某個位置有沒有石頭，如果用 set 查詢時間是 O(1)。接著我記錄最後一顆石頭的位置，之後只要到達這個位置就代表成功。然後建立一個 memo dictionary，用來記錄已經計算過的狀態，避免重複搜尋。接著我定義 dfs(position, jump)，其中 position 表示目前站在哪顆石頭上，jump 表示上一跳的距離。這個狀態很重要，因為即使站在同一顆石頭，如果上一跳距離不同，下一步能跳的距離也會不同，所以必須把位置和上一跳一起當成狀態。如果目前的 (position, jump) 已經存在於 memo，就直接回傳之前計算好的結果。如果目前位置已經等於最後一顆石頭的位置，代表成功到達終點，直接回傳 True。接著根據題目規定，假設上一跳距離是 k，那下一跳只能是 k-1、k 或 k+1，所以我用 for 迴圈枚舉這三種可能的跳躍距離。如果下一跳距離小於等於 0 就直接跳過，因為青蛙不可能跳 0 步或負數步。然後利用 next_position = position + next_jump 算出跳完之後的位置，只有當這個位置真的有石頭時才繼續搜尋。如果有石頭，我就遞迴呼叫 dfs(next_position, next_jump)，看看從新的狀態出發能不能到達終點。只要其中有任何一種跳法成功到達終點，我就把目前狀態記錄成 True 存進 memo，並直接回傳 True。假如三種跳法全部試完都無法到達終點，就把目前狀態記錄成 False 存進 memo，然後回傳 False。最後因為題目規定第一步一定要跳 1，所以我先檢查位置 1 是否存在石頭，如果不存在就直接回傳 False；如果存在，就從 dfs(1,1) 開始搜尋。整體來說，這題的核心想法是把問題定義成「目前站在哪顆石頭以及上一跳距離是多少時，能不能到達終點」，再利用 DFS 搜尋所有合法跳法，並透過 memo 避免重複計算，因此每個狀態只會被計算一次，時間複雜度大約是 O(n²)，空間複雜度也是 O(n²)。
* 程式
```python
class Solution(object):
    def canCross(self, stones):
        """
        :type stones: List[int]
        :rtype: bool
        """

        stone_set = set(stones)
        last = stones[-1]

        memo = {}

        def dfs(position, jump):

            # 已經算過
            if (position, jump) in memo:
                return memo[(position, jump)]

            # 到終點
            if position == last:
                return True

            # 三種跳法
            for next_jump in [jump - 1, jump, jump + 1]:

                if next_jump <= 0:
                    continue

                next_position = position + next_jump

                # 有石頭才能跳
                if next_position in stone_set:

                    if dfs(next_position, next_jump):
                        memo[(position, jump)] = True
                        return True

            memo[(position, jump)] = False
            return False

        # 第一跳一定是1
        if 1 not in stone_set:
            return False

        return dfs(1, 1)         
