### 123. Best Time to Buy and Sell Stock III 
<img width="2864" height="1271" alt="image" src="https://github.com/user-attachments/assets/42ce50c6-2689-4cfb-aeda-35ea1f61ccd2" />


* 解題思路\
  這題限制最多只能完成兩次交易，因此我會把整個交易流程拆成四個階段來思考。第一次買進、第一次賣出、第二次買進、第二次賣出，所以我設計四個狀態：buy1、sell1、buy2、sell2。

  buy1 代表完成第一次買進後帳戶剩下的最大資產，sell1 代表完成第一次賣出後的最大獲利，buy2 代表完成第一次交易後再買進第二次股票時帳戶剩下的最大資產，sell2 代表完成第二次賣出後的最大獲利。

  初始化時我把 buy1 和 buy2 設成 float('-inf')，因為一開始還沒有買過股票，所以買入狀態不存在，必須用負無限大表示不合法狀態，避免出現還沒買股票卻直接賣出的情況。sell1 和 sell2 則初始化為 0，代表什麼都不做時獲利為 0。

  接著遍歷每一天的價格。更新 buy1 時，代表考慮要不要在今天進行第一次買進，所以寫成 buy1 = max(buy1, -price)。更新 sell1 時，代表考慮要不要在今天完成第一次賣出，因此寫成 sell1 = max(sell1, buy1 + price)。更新 buy2 時，表示已經完成第一次交易並獲得 sell1 的利潤後，再花今天的價格買進第二次股票，因此寫成 buy2 = max(buy2, sell1 - price)。最後更新 sell2，表示要不要在今天完成第二次賣出，因此寫成 sell2 = max(sell2, buy2 + price)。

  之所以這樣設計，是因為題目最多只允許兩次交易，而每一次交易一定會經過買進和賣出兩個動作，因此所有合法狀態其實只有第一次買、第一次賣、第二次買、第二次賣這四種。我們把每天的決策都映射到這四個狀態之間的轉移即可。

  為什麼只記錄四個變數就夠，而不用記錄所有買賣組合：因為未來的決策只會依賴目前狀態下的最佳結果，而不會依賴實際是透過哪一天買進或哪一天賣出得到的。例如對於 buy1 而言，我只需要知道截至目前為止第一次買進後最大的資產是多少，其餘比較差的買法未來永遠不可能變成最佳解，因此可以直接捨棄。同樣的道理也適用於 sell1、buy2 和 sell2。所以每個狀態只需要保留一個最佳值，不需要保留所有歷史路徑。

  從 DP 的角度來看，原本可以定義成每天都有四個狀態的 DP 表，也就是 dp[i][state]，但因為第 i 天只會依賴第 i-1 天的結果，所以不需要保留整張表，只需要保留前一天的四個最佳狀態即可，因此可以進一步壓縮成四個變數。

  時間複雜度方面，我只需要掃描一次價格陣列，每一天都只進行固定次數的狀態更新，因此時間複雜度是 O(n)。空間方面，我沒有額外建立 DP 陣列，只使用 buy1、sell1、buy2、sell2 四個變數來保存狀態，因此空間複雜度是 O(1)。
  
* 程式
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        buy1 = float('-inf')
        sell1 = 0

        buy2 = float('-inf')
        sell2 = 0

        for price in prices:
            buy1 = max(buy1, -price)
            sell1 = max(sell1, buy1 + price)

            buy2 = max(buy2, sell1 - price)
            sell2 = max(sell2, buy2 + price)

        return sell2        
