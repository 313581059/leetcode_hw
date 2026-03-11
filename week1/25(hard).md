### 25. Reverse Nodes in k-Group

<img width="2862" height="1265" alt="image" src="https://github.com/user-attachments/assets/659c79d6-0f55-41d1-9f5b-ebe37d39e6c2" />

程式

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
