### 25. Reverse Nodes in k-Group

<img width="2862" height="1265" alt="image" src="https://github.com/user-attachments/assets/659c79d6-0f55-41d1-9f5b-ebe37d39e6c2" />

* 解題思路\
先設計一個反轉函數reverse \
輸入是head跟count 回傳是current跟previous \
反轉函數裡面有三個變數也代表現在要指到LinkList的哪一個點 \
如果count比0大 next先指向目前的下一個節點 \
現在的節點反轉箭頭 head變成尾巴能夠等等接著原先未反轉的linklist \
current會更新成next \
回傳的current是新的頭，告訴主程式接下來要從哪裡繼續往下做 \
previous是一串整理好的小group \
主程式先判斷夠不夠k個count \
比k小的時候直接return \
比k大的時候就套用reverse函數 \
遞迴呼叫主程式可以把每一個小group組回一條LinkList 

* 程式

```python
class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: Optional[ListNode]
        :type k: int
        :rtype: Optional[ListNode]
        """
        count, node = 0, head
        while node and count < k:
            node = node.next #數到沒有了就會跳出回圈
            count += 1
        if count < k:
            return head                           #舉例5
        new_head, prev = self.reverse(head,count)
        head.next = self.reverseKGroup(new_head,k) #舉例，將1.next=None化為1→下一段整理好的List；將2→1→4→3→None化為2→1→4→3→5
        return prev                                #舉例，2；4

    #關鍵設計    
    def reverse(self,head,count):
        prev, cur, nxt = None, head, head
        
        while count > 0 :
            nxt = cur.next  #先把下一個點標起來
            cur.next = prev #反轉箭頭
            prev = cur      #prev指向反轉箭頭後的head
            cur = nxt       #cur指向下一個點
            count-=1
        return(cur,prev)
```
* 相似題 
24. 算是k=2的25題 做法可以幾乎一樣
